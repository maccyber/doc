---
description: Automatic authentication, token validation, and login/logout for ID-Porten
---

# ID-porten sidecar

!!! warning "Status: Alpha"
    This feature is only available in [team namespaces](../../../clusters/team-namespaces.md)

    **Experimental**: subject to API change, instability, or removal.

## Description

A reverse proxy that automatically handles of ID-porten login, logout, and front-channel logout.

!!! info "Prerequisite"
    **Ensure that you first [enable ID-porten for your application](README.md).**

All HTTP requests to the application will be intercepted by a sidecar ("_wonderwall_").

If the user does _not_ have a valid local session with the sidecar, the request will be proxied as-is without 
modifications to the application container.

In order to obtain a local session, the user must be redirected to the `/oauth2/login` endpoint, which performs the
[OpenID Connect Authorization Code Flow as specified by ID-porten](https://docs.digdir.no/oidc_guide_idporten.html).
Tokens acquired from this flow are validated and verified according to the specifications. 

If the user successfully completed the login flow, a session is established with the sidecar. All requests that are 
forwarded to the application container will now contain an `Authentication` header with the user's access token from ID-porten:

```
Authentication: Bearer JWT_ACCESS_TOKEN
X-Pwned-By: wonderwall
```

## Spec

=== "nais.yaml"
    ```yaml
    spec:
      idporten:
        sidecar:
          enabled: true
    ```

See the [NAIS manifest](../../../nais-application/application.md#idportensidecar).

## Endpoints

The sidecar provides these endpoints under `https://app.ingress`:

* `/oauth2/login` redirects the user to ID-porten to perform the OpenID Connect Authorization Code Flow.
* `/oauth2/callback` handles callbacks from ID-porten as part of the OpenID Connect Authorization Code Flow.
* `/oauth2/logout` implements [self-initiated logout](README.md#self-initiated-logout).
* `/oauth2/logout/frontchannel` implements [front-channel logout](README.md#front-channel-logout).

## Usage

- When you must authenticate a user, redirect to `https://app.ingress/oauth2/login`.
- Redirects after successful authentication follow these rules in ascending priority:
    1. `/` (default).
    2. The URL set in the `Referer` header.
    3. The URL or relative path set in the query parameter `redirect`, e.g. `https://app.ingress/oauth2/login?redirect=/some/path`.
- The ID-porten access token can be exchanged for a [TokenX](../tokenx.md) token.

## Responsibilities and Guarantees

The following describes the contract for usage of the sidecar.

**The sidecar guarantees the following:**

* The `Authentication` header is added to the original request if the user has a valid session.
* The `Authentication` header is removed from the original request if the user _does not_ have a valid session.
* All HTTP requests to the `/oauth2` endpoints [defined above](#endpoints) are owned by the sidecar and will never be forwarded to the application.
* The sidecar is safe to enable and use with multiple replicas of your application.

**The sidecar does _not_ guarantee the following:**

* Automatic refresh of the user's tokens. 
* Highly available session store.
    * It currently connects and persists session data to an automatically provisioned Redis instance that runs with a single replica.
* Secure your application's endpoints.
* Validity of the user's access token. The token may be expired by the time your application receives it.

**Your application should:**

* Secure its own endpoints.
* Validate the claims and signature for the ID-porten `access_token` attached by the sidecar.
    * That is, validate the standard claims such as `iss`, `iat`, `exp`.
    * Note that the `aud` claim is _not_ set for ID-porten access tokens.
      You should instead validate that the `client_id` claim has a value equal to your ID-porten client ID.