# Keycloack OAuth2 - Flow Examples

The purpose of this project is to give URI samples how to deal with Keycloack OAuth2.

It dependes on having Wildfly running in localhost:8080

## Authorization code
http://127.0.0.1:8080/auth/realms/oauth-demo/protocol/openid-connect/auth?response_type=code&client_id=odata4-oauth&redirect_uri=http://localhost

## Implicit
http://127.0.0.1:8080/auth/realms/oauth-demo/protocol/openid-connect/auth?response_type=token&client_id=odata4-oauth&redirect_uri=http://localhost&nonce=11111&state=FFFFF

## Password
POST /auth/realms/oauth-demo/protocol/openid-connect/token HTTP/1.1
Host: 127.0.0.1:8080
Cache-Control: no-cache
Postman-Token: 121c3628-2da3-e3be-c566-6bdeb963932e
Content-Type: application/x-www-form-urlencoded

grant_type=password&username=user&password=user&client_id=odata4-oauth
