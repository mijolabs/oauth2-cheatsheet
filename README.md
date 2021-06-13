# OAuth 2.0 Cheatsheet
This is an overview of the various OAuth2.0 authorization flows and their respective request and response parameters, as defined in [RFC6749](https://tools.ietf.org/html/rfc6749). This reference aims to provide a quick and easy reference for developers. Please refer to the specification for more detailed information.

This [repository](https://github.com/mijolabs/oauth2-cheatsheet) automatically generates a static webpage at https://mijolabs.github.io/oauth2-cheatsheet.

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
- [Extensions](#extensions)
    - [PKCE](#pkce)
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
| `code_challenge` | _string_ | Optional | Required for [PKCE](#pkce). |
| `code_challenge_method` | `plain`\|`S256` | Optional | Optional when using PKCE. Defaults to `plain` if not present in the request but `S256` strongly recommended. |

[🔝](#oauth-20-cheatsheet)

## Authorization Code: Authorization Response

###### Response Parameters:

| Parameter | Value | Mandatory |
|---|---|---|
| `code` | _string_ | Required |
| `state` | _string_ | Recommended |

[🔝](#oauth-20-cheatsheet)

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
| `code_verifier` | _string_ | Optional | Required for [PKCE](#pkce). |

[🔝](#oauth-20-cheatsheet)

## Authorization Code: Token Response

[Common Token Responses](#common-token-response)

[🔝](#oauth-20-cheatsheet)

## Token Endpoint: Error Responses

[Token Endpoint: Error Responses](#token-endpoint-error-responses)

[🔝](#oauth-20-cheatsheet)

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

[🔝](#oauth-20-cheatsheet)

## Password Credentials: Token Response

[Common Token Response](#common-token-response)

[🔝](#oauth-20-cheatsheet)

## Token Endpoint: Error Responses

[Token Endpoint: Error Responses](#token-endpoint-error-responses)

[🔝](#oauth-20-cheatsheet)

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

[🔝](#oauth-20-cheatsheet)

## Client Credentials: Token Response

[Common Token Response](#common-token-response)

[🔝](#oauth-20-cheatsheet)

## Token Endpoint: Error Responses

[Token Endpoint: Error Responses](#token-endpoint-error-responses)

[🔝](#oauth-20-cheatsheet)

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

[🔝](#oauth-20-cheatsheet)

## Token Response

[Common Token Response](#common-token-response)

[🔝](#oauth-20-cheatsheet)

## Token Endpoint: Error Responses

[Token Endpoint: Error Responses](#token-endpoint-error-responses)

[🔝](#oauth-20-cheatsheet)

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

[🔝](#oauth-20-cheatsheet)

## Token Request: Error Responses

[Token Request Error Responses](#token-request-error-responses)

[🔝](#oauth-20-cheatsheet)

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

[🔝](#oauth-20-cheatsheet)

###### Token Endpoint: Error Responses

| Value | Description |
|---|---|
| `invalid_request` | The request is missing a required parameter, includes an unsupported parameter value (other than grant type), repeats a parameter, includes multiple credentials, utilizes more than one mechanism for authenticating the client, or is otherwise malformed. |
| `invalid_client` | Client authentication failed (e.g., unknown client, no client authentication included, or unsupported authentication method). The authorization server MAY return an HTTP 401 (Unauthorized) status code to indicate which HTTP authentication schemes are supported. If the client attempted to authenticate via the "Authorization" request header field, the authorization server MUST respond with an HTTP 401 (Unauthorized) status code and include the "WWW-Authenticate" response header field matching the authentication scheme used by the client. |
| `invalid_grant` | The provided authorization grant (e.g., authorization code, resource owner credentials) or refresh token is invalid, expired, revoked, does not match the redirection URI used in the authorization request, or was issued to another client. |
| `unauthorized_client` | The authenticated client is not authorized to use this authorization grant type. |
| `unsupported_grant_type` | The authorization grant type is not supported by the authorization server. |
| `invalid_scope` | The requested scope is invalid, unknown, malformed, or exceeds the scope granted by the resource owner. |

[🔝](#oauth-20-cheatsheet)

## Extensions

###### PKCE

[RFC7636](https://tools.ietf.org/html/rfc7636):
    >OAuth 2.0 public clients utilizing the Authorization Code Grant are susceptible to the authorization code interception attack. This specification describes the attack as well as a technique to mitigate against the threat through the use of Proof Key for Code Exchange(PKCE, pronounced "pixy").

The following parameters are added in the client's [Authorization Code Grant](#authorization-code-grant) requests:

###### Authorization Code Grant: Authorization Request Parameters:

| Parameter | Value | Required | Comment |
|---|---|---|---|
| `code_challenge` | _string_ | Optional | Required for [PKCE](#pkce). |
| `code_challenge_method` | `plain`\|`S256` | Optional | Optional when using PKCE. Defaults to `plain` if not present in the request but `S256` strongly recommended. |

###### Authorization Code Grant: Token Request Parameters:

| Parameter | Value | Required | Comment |
|---|---|---|---|
| `code_verifier` | _string_ | Optional | Required for [PKCE](https://tools.ietf.org/html/rfc7636). |


###### Client Creates a Code Verifier
`code_verifier` = high-entropy cryptographic random STRING using the unreserved characters `A-Z` / `a-z` / `0-9` / `-` / `.` / `_` / `~`, with a minimum length of 43 characters and a maximum length of 128 characters.

It is RECOMMENDED that the output of a suitable random number generator be used to create a 32-octet sequence. The octet sequence is then base64url-encoded to produce a 43-octet URL safe string to use as the code verifier.

###### Client Creates the Code Challenge
The client then creates a code challenge derived from the code verifier by using one of the following transformations on the code verifier:
   `plain`
      `code_challenge` = `code_verifier`

   `S256`
      `code_challenge` = `BASE64URL-ENCODE(SHA256(ASCII(code_verifier)))`

    >If the client is capable of using `S256`, it MUST use `S256`, as `S256` is Mandatory To Implement (MTI) on the server. Clients are permitted to use `plain` only if they cannot support `S256` for some technical reason and know via out-of-band configuration that the server supports "plain". The `plain` transformation is for compatibility with existing deployments and for constrained environments that can't use the `S256` transformation.

###### Generating code_verifier and code_challenge in Python
```python
import secrets
import hashlib
import base64

def generate_code_verifier(self, length: int = 128) -> str:
    if not 43 <= length <= 128:
        raise ValueError("Parameter 'length' must verify '43 <= length <= 128'")
    code_verifier = secrets.token_urlsafe(96)[:length]
    return code_verifier

def generate_code_challenge(self, code_verifier: str, code_challenge_method: str = 'S256') -> str:
    if code_challenge_method == 'S256':
        code_challenge = hashlib.sha256(code_verifier.encode('utf-8')).digest()
        code_challenge = base64.urlsafe_b64decode(code_challenge)
        code_challenge = code_challenge.decode('utf-8').rstrip('=')
    elif code_challenge_method == 'plain':
        code_challenge = code_verifier
    return code_challenge

code_verifier = generate_code_verifier()
code_challenge = generate_code_challenge(code_verifier))
```

[🔝](#oauth-20-cheatsheet)

---
