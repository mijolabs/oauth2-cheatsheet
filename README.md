# mijolabs/oauth2-reference
An overview of the various OAuth2.0 authorization flows and their respective request and response parameters, as defined in [RFC6749](https://tools.ietf.org/html/rfc6749). It aims to provide a quick and easy reference for developers building clients. Please refer to the official RFC specification for more detailed information.

## 📖 Table of Contents
- [Authorization Code](#authorization-code-flow)
  - [HTTP Request](#http-request)
- [Password](#password-flow)
- [Client Credentials](#client-credentials-flow)
---

# Authorization Code Flow

## 1a. Authorization Request
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

[📖🆙](#table-of-contents)

## 1b. Authorization Response
###### Response Parameters:
| Parameter | Value | Required |
|---|---|---|
| `code` | _string_ | Required |
| `state` | _string_ | Recommended |

## 1c. Error Response
###### Response Parameters:

| Parameter | Value | Description |
|---|---|---|
| `error` | `invalid_request` | The request is missing a required parameter, includes an invalid parameter value, includes a parameter more than once, or is otherwise malformed. |
| `error` | `unauthorized_client` | The resource owner or authorization server denied the request. |
| `error` | `access_denied` | The authorization server does not support obtaining an authorization code using this method. |
| `error` | `unsupported_response_type` | The requested scope is invalid, unknown, or malformed. |
| `error` | `invalid_scope` | The authorization server encountered an unexpected condition that prevented it from fulfilling the request. (This error code is needed because a 500 Internal Server Error HTTP status code cannot be returned to the client via an HTTP redirect.) |
| `error` | `temporarily_unavailable` | The authorization server is currently unable to handle the request due to a temporary overloading or maintenance of the server. (This error code is needed because a 503 Service Unavailable HTTP status code cannot be returned to the client via an HTTP redirect.) |

## 2a. Access Token Request
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

## 2b. Server Token Response
###### Response Headers:
| Parameter | Value |
|---|---|
| `cache-control` | `nostore` |
| `pragma` | `no-cache` |

###### Response Parameters:
| Parameter | Value | Required |
|---|---|---|
| `access_token` | _string_ | Required |
| `token_type` | `bearer` \| `mac` | Required |
| `expires_in` | _integer_ | Recommended |
| `refresh_token` | _integer_ | Optional |
| `scope` | _integer_ | Optional |

# Password
Request
| http method | get |
| header | content-type: application/x-www-form-urlencoded |
| parameter | value | required |
|---|---|---|
| response_type | code | true |
| client_id | str | true | |
| redirect_uri | str |
Authorization Code Response

# Client Credentials
Request
| http method | get |
| header | content-type: application/x-www-form-urlencoded |

| parameter | value | required |
|---|---|---|
| response_type | code | true |
| client_id | | true | |
| redirect_uri |  |

Authorization Code Response

