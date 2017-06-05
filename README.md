# Keycloack OAuth2 and OpenID Connect

The purpose of this project is to give flow samples how to deal with Keycloack OAuth2 and OpenID Connect.

As premise the developer must have a Wildfly running in 127.0.0.1:8080.

Steps to set up:

1) Create a realm called "oauth-demo"
2) Create a client called "odata4-oauth"
3) Create a user, set roles to user, etc...

![Clients section](https://github.com/cbelleza/keycloack/blob/master/img/ClientsSection.png)

## OAuth2 flow types

Keycloack support the following OAuth2 flows:

### Authorization code

##### *Step 1: User grants access*

http://127.0.0.1:8080/auth/realms/oauth-demo/protocol/openid-connect/auth?response_type=code&client_id=odata4-oauth&redirect_uri=http://localhost&state=FFFFF

##### *Step 2: Application requests access token*
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

OR using "Authorization" header "Basic BASE64(client_id:client_secret)"

```
POST /auth/realms/oauth-demo/protocol/openid-connect/token HTTP/1.1
Host: 127.0.0.1:8080
Authorization: Basic b2RhdGE0LW9hdXRoOjljYmEyMzhkLTc0ZjItNDJmZC1hMmIwLTVlNzc3Yjk1ODhiYw==
Content-Type: application/x-www-form-urlencoded

grant_type=authorization_code
code=gRmtfV5LSUrlzdcnNX_tzLw7vk_RCc4k2o1kAXJS_aU.de981c0e-14bf-4258-8d4c-99e26063eeba
redirect_uri=http%3A%2F%2Flocalhost
```

### Implicit
http://127.0.0.1:8080/auth/realms/oauth-demo/protocol/openid-connect/auth?response_type=token&client_id=odata4-oauth&redirect_uri=http://localhost&nonce=11111&state=FFFFF

### Password
```
POST /auth/realms/oauth-demo/protocol/openid-connect/token HTTP/1.1
Host: 127.0.0.1:8080
Content-Type: application/x-www-form-urlencoded

grant_type=password
client_id=odata4-oauth
client_secret=8fb0027b-980b-48d6-af0b-a15f74fb465d
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

## OpenID Connect endpoints

### Userinfo

```
GET /auth/realms/oauth-demo/protocol/openid-connect/userinfo HTTP/1.1
Host: 127.0.0.1:8080
Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6ICJGTzZXamFRTHBNakJVWFRUMEl4Zmd2Vi1SSFZqb0dqQkRFMEFEYTJydVp3In0.eyJqdGkiOiIyN2U0NjNlZi02YWRjLTQ0OGQtODc2Yi1mNTE2OTRkYWM1MjkiLCJleHAiOjE0OTY1NDEwOTcsIm5iZiI6MCwiaWF0IjoxNDk2NTQwMTk3LCJpc3MiOiJodHRwOi8vMTI3LjAuMC4xOjgwODAvYXV0aC9yZWFsbXMvb2F1dGgtZGVtbyIsImF1ZCI6Im9kYXRhNC1vYXV0aCIsInN1YiI6IjM0NmIyYTM5LWVlMTktNDYwYS04OWJjLTgxODM5MDUxMDE3OCIsInR5cCI6IkJlYXJlciIsImF6cCI6Im9kYXRhNC1vYXV0aCIsIm5vbmNlIjoiMTExMTEiLCJhdXRoX3RpbWUiOjE0OTY1NDAxOTcsInNlc3Npb25fc3RhdGUiOiI0NGM3ODdkNy0zNjkyLTQxMzAtYmIyMy02MGViNGY4NjQzN2UiLCJhY3IiOiIxIiwiY2xpZW50X3Nlc3Npb24iOiJmNTYwNzE3ZC1jODJhLTRmMDEtOWE0Yi1kOTdkOTU2MjcyMmMiLCJhbGxvd2VkLW9yaWdpbnMiOltdLCJyZWFsbV9hY2Nlc3MiOnsicm9sZXMiOlsidW1hX2F1dGhvcml6YXRpb24iXX0sInJlc291cmNlX2FjY2VzcyI6eyJhY2NvdW50Ijp7InJvbGVzIjpbIm1hbmFnZS1hY2NvdW50IiwibWFuYWdlLWFjY291bnQtbGlua3MiLCJ2aWV3LXByb2ZpbGUiXX19LCJuYW1lIjoiIiwicHJlZmVycmVkX3VzZXJuYW1lIjoidXNlciJ9.N9mz4z_-fOjgcy7IJj2PcZewegirL5c-xC6irwg5aQ1cHOBR1fO1dGYq1dBR9V3bPSAaRjCxh5PxL-xfnMEyL8w0f2_zZ0NnCJ9mbnyh730Ba7tEDyH7zKjbu7UtaUNy3cVHqmUyNVvDncugiqtw4an8vK6z1hAK8O1_IAtGz5C7Rh89INRV5IhyjGRm6ZaxCeR4PBEMgtmv07ZlcX9mDbV-CtIKW8FR9fd1oHWrV2yEuu9asnS5erkydGbq8sw_LUGkS5CEnPU2EJn8SIRcE-S1DLrzyOYYWDa2DP2zOYQtY5kGOHXH_4CXpKniX2NNM3LYyhIBw2_jO9OHU5TXVA
Cache-Control: no-cache
```

### Logout

```
POST /auth/realms/oauth-demo/protocol/openid-connect/logout HTTP/1.1
Host: 127.0.0.1:8080
Cache-Control: no-cache
Content-Type: application/x-www-form-urlencoded

client_id=odata4-oauth
client_secret=9cba238d-74f2-42fd-a2b0-5e777b9588bc
refresh_token=eyJhbGciOiJSUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6ICJGTzZXamFRTHBNakJVWFRUMEl4Zmd2Vi1SSFZqb0dqQkRFMEFEYTJydVp3In0.eyJqdGkiOiI3OWFmZWNmNC0wOGFmLTQ1ZGMtOGJhNC1kODNhOGE1ZmFkZDMiLCJleHAiOjE0OTY1NDI5MDQsIm5iZiI6MCwiaWF0IjoxNDk2NTQxMTA0LCJpc3MiOiJodHRwOi8vMTI3LjAuMC4xOjgwODAvYXV0aC9yZWFsbXMvb2F1dGgtZGVtbyIsImF1ZCI6Im9kYXRhNC1vYXV0aCIsInN1YiI6IjM0NmIyYTM5LWVlMTktNDYwYS04OWJjLTgxODM5MDUxMDE3OCIsInR5cCI6IlJlZnJlc2giLCJhenAiOiJvZGF0YTQtb2F1dGgiLCJhdXRoX3RpbWUiOjAsInNlc3Npb25fc3RhdGUiOiI0NGM3ODdkNy0zNjkyLTQxMzAtYmIyMy02MGViNGY4NjQzN2UiLCJjbGllbnRfc2Vzc2lvbiI6IjhlMTE1ZTUyLWIwYTktNDFlMC1hZDIxLTNiOTE1ZWQyNmVkNSIsInJlYWxtX2FjY2VzcyI6eyJyb2xlcyI6WyJ1bWFfYXV0aG9yaXphdGlvbiJdfSwicmVzb3VyY2VfYWNjZXNzIjp7ImFjY291bnQiOnsicm9sZXMiOlsibWFuYWdlLWFjY291bnQiLCJtYW5hZ2UtYWNjb3VudC1saW5rcyIsInZpZXctcHJvZmlsZSJdfX19.UYbfTJ5w7zZm2wz2cDj1NQjb3tBV29pJ9IWGRvMtOsks8gFc5aJHAZMg8iAnxe-3MbYcyNF5HSQmdjKTFx2T1pm4N8vGXNOIzE-HCNqyZfjsCvX5pqefUYzheVFhFiBNvBu3621k9xAkJEvPecUqlXThkZjSjDV1-Djx67Qr7xqPjdkM2kYLNaDrCZ7Z45ZmKfUNEjEOUtf15kz01Zyua9jO9vtySXBp2RzkJF_0_LOXv-VHu94I7u8rgjAQ72ME2ZlCRXwOv0wG3wJoTvscu8pehL6um86Kekhayu7P_zdq68gBBec4tLF_7bdOu3WhIyTxhInHdbmBBXmsQt946Q
```
