# OAuth2.0 Grant Reference
This is an overview of the various OAuth2.0 authorization flows and their respective request and response parameters, as defined in [RFC6749](https://tools.ietf.org/html/rfc6749). Please refer to that for more detailed information. This reference aims to provide a quick and easy reference for developers working with OAuth clients.

## 📖 Contents
1. [Authorization Code Grant](#authorization-code-grant)
    1. [Authorization Request](#authorization-code-authorization-request)
    2. [Authorization Response](#authorization-code-authorization-response)
    3. [Token Request](#authorization-code-token-request)
    4. [Token Response](#common-token-response)
2. [Password Credentials Grant](#2-password-credentials-grant)
    1. [Token Request](#password-credentials--token-request)
    2. [Token Response](#common-token-response)
3. [Client Credentials Grant](#3-client-credentials-grant)
    1. [Token Request](#client-credentials-token-request)
    2. [Token Response](#common-token-response)
4. [Token Refresh](#token-refresh)
    1. [Token Refresh Request](#token-refresh-request)
    2. [Token Refresh Response](#token-refresh-response)
5. [Common Token Response](#common-token-response)
6. [Error Responses](#error-responses)

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
| Parameter | Value | Required |
|---|---|---|
| `response_type` | `code` | Required |
| `client_id` | _string_ | Required | 
| `redirect_uri` | _string_ | Optional |
| `scope` | _string_ | Optional |
| `state` | _string_ | Recommended |

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
| Parameter | Value | Required |
|---|---|---|
| `grant_type` | `authorization_code` | Required |
| `code` | _string_ | Required | 
| `redirect_uri` | _string_ | Required |
| `client_id` | _string_ | Required |

[🔝](#-contents)

## [Common Token Response](#common-token-response)


[🔝](#-contents)

---

# 2. Password Credentials Grant
## Password Grant: Token Request

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

---

# 3. Client Credentials Grant

---

# 4. Common Token Response
###### Token Response Headers:

| Parameter | Value |
|---|---|
| `cache-control` | `nostore` |
| `pragma` | `no-cache` |

###### Token Response Parameters:
| Parameter | Value | Required |
|---|---|---|
| `access_token` | _string_ | Required |
| `token_type` | `bearer` \| `mac` | Required |
| `expires_in` | _integer_ | Recommended |
| `refresh_token` | _string_ | Optional |
| `scope` | _string_ | Optional |

[🔝](#-contents)

---

# 4. Token Refresh

---

# 5. Error Responses
###### Response Parameters:
| Value | Description |
|---|---|
| `invalid_request` | The request is missing a required parameter, includes an invalid parameter value, includes a parameter more than once, or is otherwise malformed. |
| `unauthorized_client` | The resource owner or authorization server denied the request. |
| `access_denied` | The authorization server does not support obtaining an authorization code using this method. |
| `unsupported_response_type` | The requested scope is invalid, unknown, or malformed. |
| `invalid_scope` | The authorization server encountered an unexpected condition that prevented it from fulfilling the request. (This error code is needed because a 500 Internal Server Error HTTP status code cannot be returned to the client via an HTTP redirect.) |
| `temporarily_unavailable` | The authorization server is currently unable to handle the request due to a temporary overloading or maintenance of the server. (This error code is needed because a 503 Service Unavailable HTTP status code cannot be returned to the client via an HTTP redirect.) |

[🔝](#-contents)

