---
title: Refreshing an Access Token
is_documentation: true
side_menu:
  - title: Authorization overview
    url: /authorization/authorization-overview/
  - title: Registering an application
    url: /authorization/registering-an-application/
  - title: Multi language support
    url: /authorization/multi-language-support/
  - title: Authorization Code Grant (external users)
    url: /authorization/authorization-code-grant/
  - title: Refreshing an Access Token
    url: /authorization/refreshing-an-access-token/
    active: true
  - title: Resource Owner Password Credentials Grant (internal users)
    url: /authorization/resource-owner-password-credentials-grant/
---

>**Important note**: To utilize this authentication flow your application must have `refresh_token` grant type admitted.

For more general information please refer to [authorization overview](/api-rest-documentation/authorization/authorization-overview/).

## Access token request

### Example

```http
POST /oauth2/token
Host: auth.system.trans.eu
Content-Type: application/x-www-form-urlencoded

grant_type=refresh_token
&refresh_token=tGzv3JOkF0XG5Qx2TlKWIA
```

### Request parameters

| Name | Required | Type |  Description |
|---|---|---|---|
| grant_type | yes | string | Must be set to `refresh_token`. |
| refresh_token | yes | string | The refresh token issued during authorization. |
| client_id | no| string | Application client_id obtained during registration. Only required if `Authorization` header is not sent. |
| client_secret | no | string | Application client_secret obtained during registration. Only required if `Authorization` header is not sent. |

### Header parameters

| Name | Required | Value |
|---|---|---|
| Authorization | yes | Base 64 encoded string that contains the client_id and client_secret keys. The field must have the format: `Authorization: Basic <base64 encoded client_id:client_secret>`.  |
| Content-Type | yes |  application/x-www-form-urlencoded

## Access token response

### Example

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "access_token": "59d9aa9b15cd59a61fc52014792efb6caa82373b",
  "expires_in": 3600,
  "token_type": "Bearer",
  "scope": "offers.loads.manage",
  "refresh_token": "d52d1d998d6533a3be8e7f26f904be513287938b"
}
```

### Response parameters

| Name | Description |
|---|---|
| access_token | Access token to use by application for authorization. |
| expires_in | Time in seconds until token expires. |
| token_type | Type `Bearer` is returned as defined in [rfc6749](http://tools.ietf.org/html/rfc6750). |
| scope | Space separated list of scopes that access token has access to. |
| refresh_token | Single serving token that can be used to extend lifetime of access token. |
