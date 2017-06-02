# Keycloack OAuth2

The purpose of this project is to give flow samples how to deal with Keycloack OAuth2.

As premise the developer must have a Wildfly running in 127.0.0.1:8080.

Steps to set up:

1) Create a realm called "oauth-demo"
2) Create a client called "odata4-oauth"
3) Create a user, set roles to user, etc...

![Clients section](https://github.com/cbelleza/keycloack/blob/master/img/ClientsSection.png)

## OAuth2 flow types

Keycloack support the following OAuth2 flows:

### Authorization code

#### *Step 1: User grants access*

http://127.0.0.1:8080/auth/realms/oauth-demo/protocol/openid-connect/auth?response_type=code&client_id=odata4-oauth&redirect_uri=http://localhost&state=FFFFF

#### *Step 2: Application requests access token*
```
POST /auth/realms/oauth-demo/protocol/openid-connect/token HTTP/1.1
Host: 127.0.0.1:8080
Cache-Control: no-cache
Content-Type: application/x-www-form-urlencoded

grant_type=authorization_code
client_id=odata4-oauth
client_secret=8fb0027b-980b-48d6-af0b-a15f74fb465d
code=DxdTjfianxXyPnYbzvbAMpi2y01vE_xCqne-3f3I51o.1af86eb3-705d-46cd-850f-ea4639b08849
redirect_uri=http://localhost
```

### Implicit
http://127.0.0.1:8080/auth/realms/oauth-demo/protocol/openid-connect/auth?response_type=token&client_id=odata4-oauth&redirect_uri=http://localhost&nonce=11111&state=FFFFF

### Password
```
POST /auth/realms/oauth-demo/protocol/openid-connect/token HTTP/1.1
Host: 127.0.0.1:8080
Cache-Control: no-cache
Content-Type: application/x-www-form-urlencoded

grant_type=password
client_id=odata4-oauth
username=user
password=user
```

### Client credentials
```
POST /auth/realms/oauth-demo/protocol/openid-connect/token HTTP/1.1
Host: 127.0.0.1:8080
Cache-Control: no-cache
Content-Type: application/x-www-form-urlencoded

grant_type=client_credentials
client_id=odata4-oauth
client_secret=8fb0027b-980b-48d6-af0b-a15f74fb465d
```
