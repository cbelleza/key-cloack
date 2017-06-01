# Keycloack OAuth2 - Flow Samples

The purpose of this project is to give flow samples how to deal with Keycloack OAuth2.

As premise the developer must have a Wildfly running in 127.0.0.1:8080.

Steps to set up:

1) Create a realm called "oauth-demo"
2) Create a client called "odata4-oauth"
3) Create a user, set roles to user, etc...

![Clients section](https://github.com/cbelleza/keycloack/blob/master/ClientsSection.png)


## Authorization code
http://127.0.0.1:8080/auth/realms/oauth-demo/protocol/openid-connect/auth?response_type=code&client_id=odata4-oauth&redirect_uri=http://localhost

## Implicit
http://127.0.0.1:8080/auth/realms/oauth-demo/protocol/openid-connect/auth?response_type=token&client_id=odata4-oauth&redirect_uri=http://localhost&nonce=11111&state=FFFFF

## Password
```
POST /auth/realms/oauth-demo/protocol/openid-connect/token HTTP/1.1
Host: 127.0.0.1:8080
Cache-Control: no-cache
Content-Type: application/x-www-form-urlencoded

grant_type=password&username=user&password=user&client_id=odata4-oauth
```

## Client credentials
```
POST /auth/realms/oauth-demo/protocol/openid-connect/token HTTP/1.1
Host: 127.0.0.1:8080
Cache-Control: no-cache
Content-Type: application/x-www-form-urlencoded

grant_type=client_credentials&client_id=odata4-oauth&client_secret=8fb0027b-980b-48d6-af0b-a15f74fb465d
```
