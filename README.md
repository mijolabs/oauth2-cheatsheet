# OAuth 2.0 Cheatsheet
This is an overview of the various OAuth2.0 authorization flows and their respective request and response parameters, as defined in [RFC6749](https://tools.ietf.org/html/rfc6749). This reference aims to provide a quick and easy reference for developers. Please refer to the specification for more detailed information.

## 📖 Contents
- [Authorization Code Grant](#authorization-code-grant)
    1. [Authorization Request](#authorization-code-authorization-request)
    2. [Authorization Response](#authorization-code-authorization-response)
    3. [Token Request](#authorization-code-token-request)
    4. [Token Response](#common-token-response)
- [Password Credentials Grant](password-credentials-grant)
    1. [Token Request](#password-credentials-token-request)
    2. [Token Response](#common-token-response)
- [Client Credentials Grant](#client-credentials-grant)
    1. [Token Request](#client-credentials-token-request)
    2. [Token Response](#common-token-response)
- [Token Refresh](#token-refresh)
    1. [Token Refresh Request](#token-refresh-request)
    2. [Token Response](#common-token-response)
- [Common Token Response](#common-token-response)
- [Error Responses](#error-responses)
    - [Authorization Endpoint: Error Responses](#authorization-endpoint-error-responses)
    - [Token Endpoint: Error Responses](#token-endpoint-error-responses)

---

# Authorization Code Grant

## Authorization Code: Authorization Request

###### HTTP Request:

| Method | URI |
| --- | --- |
| `GET` | authorization_endpoint |

###### Request Headers:

| Parameter | Value |
|---|---|
| `content-type` | `application/x-www-form-urlencoded` |

###### Request Parameters:

| Parameter | Value | Required | Comment |
|---|---|---|---|
| `response_type` | `code` | Required | |
| `client_id` | _string_ | Required | |
| `redirect_uri` | _string_ | Optional | |
| `scope` | _string_ | Optional | |
| `state` | _string_ | Recommended | |
| `code_challenge` | _string_ | Optional | Required for [PKCE](https://tools.ietf.org/html/rfc7636). |
| `code_challenge_method` | `plain` \| `S256` | Optional | Defaults to `plain` if not present in the request. |

[🔝](#-contents)

## Authorization Code: Authorization Response

###### Response Parameters:

| Parameter | Value | Mandatory |
|---|---|---|
| `code` | _string_ | Required |
| `state` | _string_ | Recommended |

[🔝](#-contents)

## Authorization Code: Token Request

###### HTTP Request:

| Method | URI |
| --- | --- |
| `POST` | token_endpoint |

###### Request Headers:

| Parameter | Value |
|---|---|
| `content-type` | `application/x-www-form-urlencoded` |

###### Request Parameters:

| Parameter | Value | Required | Comment |
|---|---|---|---|
| `grant_type` | `authorization_code` | Required | |
| `code` | _string_ | Required | |
| `redirect_uri` | _string_ | Required | |
| `client_id` | _string_ | Required | |
| `code_verifier` | _string_ | Optional | Required for [PKCE](https://tools.ietf.org/html/rfc7636). |

[🔝](#-contents)

## Authorization Code: Token Response

[Common Token Responses](#common-token-response)

[🔝](#-contents)

## Token Endpoint: Error Responses

[Token Endpoint: Error Responses](#token-endpoint-error-responses)

[🔝](#-contents)

---

# 2. Password Credentials Grant

## Password Credentials: Token Request

###### HTTP Request:

| Method | URI |
| --- | --- |
| `POST` | token_endpoint |

###### Request Headers:

| Parameter | Value |
|---|---|
| `content-type` | `application/x-www-form-urlencoded` |

###### Request Parameters:

| Parameter | Value | Required |
|---|---|---|
| `grant_type` | `password` | Required |
| `username` | _string_ | Required |
| `password` | _string_ | Required |
| `scope` | _string_ | Optional |

[🔝](#-contents)

## Password Credentials: Token Response

[Common Token Response](#common-token-response)

[🔝](#-contents)

## Token Endpoint: Error Responses

[Token Endpoint: Error Responses](#token-endpoint-error-responses)

[🔝](#-contents)

---

# Client Credentials Grant

## Client Credentials: Token Request

###### HTTP Request:

| Method | URI |
| --- | --- |
| `POST` | token_endpoint |

###### Request Headers:

| Parameter | Value |
|---|---|
| `content-type` | `application/x-www-form-urlencoded` |

###### Request Parameters:

| Parameter | Value | Required |
|---|---|---|
| `grant_type` | `client_credentials` | Required |
| `scope` | _string_ | Optional |

[🔝](#-contents)

## Client Credentials: Token Response

[Common Token Response](#common-token-response)

[🔝](#-contents)

## Token Endpoint: Error Responses

[Token Endpoint: Error Responses](#token-endpoint-error-responses)

[🔝](#-contents)

---

# Token Refresh

## Token Refresh Request

###### HTTP Request:

| Method | URI |
| --- | --- |
| `POST` | token_endpoint |

###### Request Headers:

| Parameter | Value |
|---|---|
| `content-type` | `application/x-www-form-urlencoded` |

###### Request Parameters:

| Parameter | Value | Required |
|---|---|---|
| `grant_type` | `refresh_token` | Required |
| `refresh_token` | _string_ | Required |
| `scope` | _string_ | Optional |

[🔝](#-contents)

## Token Response

[Common Token Response](#common-token-response)

[🔝](#-contents)

## Token Endpoint: Error Responses

[Token Endpoint: Error Responses](#token-endpoint-error-responses)

[🔝](#-contents)

---

# Common Token Response

###### Token Response Headers:

| Parameter | Value |
|---|---|
| `cache-control` | `nostore` |
| `pragma` | `no-cache` |

###### Token Response Parameters:

| Parameter | Value | Required | Comment |
|---|---|---|---|
| `access_token` | _string_ | Required | |
| `token_type` | `bearer` \| `mac` | Required | |
| `expires_in` | _integer_ | Recommended | The lifetime in seconds of the access token. |
| `refresh_token` | _string_ | Optional | Not included in response to a [Client Credentials Grant token request](#client-credentials-token-request). |
| `scope` | _string_ | Optional | |

[🔝](#-contents)

## Token Request: Error Responses

[Token Request Error Responses](#token-request-error-responses)

[🔝](#-contents)

---

# Error Responses

###### Authorization Endpoint: Error Responses

| Value | Description |
|---|---|
| `unauthorized_client` | The client is not authorized to request an authorization code using this method. |
| `access_denied` | The resource owner or authorization server denied the request. |
| `unsupported_response_type` | The authorization server does not support obtaining an authorization code using this method. |
| `invalid_scope` | The requested scope is invalid, unknown, or malformed. |
| `server_error` | The authorization server encountered an unexpected condition that prevented it from fulfilling the request. (This error code is needed because a 500 Internal Server Error HTTP status code cannot be returned to the client via an HTTP redirect.) |
| `temporarily_unavailable` | The authorization server is currently unable to handle the request due to a temporary overloading or maintenance of the server.  (This error code is needed because a 503 Service Unavailable HTTP status code cannot be returned to the client via an HTTP redirect.) |

[🔝](#-contents)

###### Token Endpoint: Error Responses

| Value | Description |
|---|---|
| `invalid_request` | The request is missing a required parameter, includes an unsupported parameter value (other than grant type), repeats a parameter, includes multiple credentials, utilizes more than one mechanism for authenticating the client, or is otherwise malformed. |
| `invalid_client` | Client authentication failed (e.g., unknown client, no client authentication included, or unsupported authentication method). The authorization server MAY return an HTTP 401 (Unauthorized) status code to indicate which HTTP authentication schemes are supported. If the client attempted to authenticate via the "Authorization" request header field, the authorization server MUST respond with an HTTP 401 (Unauthorized) status code and include the "WWW-Authenticate" response header field matching the authentication scheme used by the client. |
| `invalid_grant` | The provided authorization grant (e.g., authorization code, resource owner credentials) or refresh token is invalid, expired, revoked, does not match the redirection URI used in the authorization request, or was issued to another client. |
| `unauthorized_client` | The authenticated client is not authorized to use this authorization grant type. |
| `unsupported_grant_type` | The authorization grant type is not supported by the authorization server. |
| `invalid_scope` | The requested scope is invalid, unknown, malformed, or exceeds the scope granted by the resource owner. |

[🔝](#-contents)
