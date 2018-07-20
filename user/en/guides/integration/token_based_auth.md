# Token based auth
Token-based authentication is a security technique that authenticate the users who attempt to log in to a server. The service validates the security token and processes the user request.

### How Does Token Authentication Work?
Authentication is the process by which an application confirms user identity. Applications have traditionally persisted identity through session cookies, relying on session IDs stored server-side. This forces developers to create session storage that is either unique to each server, or implemented as a totally separate session storage layer.

Token authentication is a more modern approach and it is designed to solve problems that session IDs storage mechanism on server-side can’t. Using tokens in place of session IDs can lower your server load.

## Token CRUD
As a developer, you can use tokens for full CRUD operations.
Once an Token has been generated, the token can be used to authorize individual requests made by your users as they are passed to your application. Your application will validate the token sent along with each request. 

An combination of API Key and API Secret forms a token used to authenticate you with your servers and can be used to authenticate both  RPC and Rest api.

# Generate Token
For every user you can create an api key and api secret which acts as a token.
  - api-key: User sqecific api key, used to identify the user.
  - api-secret: Used to validate the request.
###### Note: 
1. Api key cannot  be re-generated.
2. Only user with system manager role can generate keys.

### Generate api key and api secret

API key and secret can be generated by the following methods:
-  RPC      `/api/method/frappe.core.doctype.user.user?user="user_name"`
-  Command   `bench execute frappe.core.doctype.user.user --args ['user_name']`
-  Web       `User -> Api Access -> Generate Keys` 

### Authorization
There are two types of authorization:
- Token 
- Basic


#### Token
```
{
    Authorization:  `token <api_key>:<api_secret>`
}
```
 Example RPC:
```
import requests

url = "http://frappe.local:8000**/api/method/frappe.auth.get_logged_user**"
headers = {
    'Authorization': "token <api_key>:<api_secret>"
}
response = requests.request("GET", url, headers=headers)
```

#### Basic
```
{
    Authorization: Basic base34encode(<api_key>:<api_secret>)
}
```
Example:
```
import requests
import base64

url = "http://frappe.local:8000**/api/method/frappe.auth.get_logged_user**"
headers = {
    'Authorization': "Basic %s" % base64.b64encode(<api_key>:<api_secret>)
}
response = requests.request("GET", url, headers=headers)
```