---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - python
  - shell


toc_footers:
  - <a href='#'>Signing Platform</a>

includes:
  - errors

search: true

code_clipboard: true
---

# Introduction

Welcome to the Signing API! You can use our API to access Signing endpoints, which can get your documents signed.

We have language bindings in Shell, Python! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

The Signing API is organized around REST. Our API has predictable resource-oriented URLs, accepts form-encoded request bodies, returns JSON-encoded responses, and uses standard HTTP response codes, authentication, and verbs.

# Installation
Signing is compatible with python versions >= 3.8, and is available through PyPI:

<code>pip install signing</code>

All prerequisite packages will be automatically added to your environment.

If you downloaded the source code, navigate to the cloned directory in a terminal, switch to your preferred python3 environment, then run

<code>pip install .</code>


Dependencies that are automatically installed include:

  - pydantic
  - python-dotenv
  - requests
  - urllib3



# Authentication

## Intialize

> To authorize, use this code:

```python
from signing_client import APIClient

api_client = APIClient(clientid = {{clientid}}, 
                      client_secret = {{secretkey}}, 
                      url = {{url}}
                      )
```

```shell
# With shell, you can just pass the correct header with each request
curl --request POST 'http://127.0.0.1:8000/sign/' \
  --header 'X-API-Key: {{secretkey}}' \
  --header 'X-API-Client: {{clientid}}' \
```

> Make sure to replace `clientid` with your client id.
> Make sure to replace `secretkey` with your client secret key.

The Signing API uses clientid and secret key to authenticate requests.

Your API keys carry many privileges, so be sure to keep them secure! Do not share your secret API keys in publicly accessible areas such as GitHub, client-side code, and so forth.

Use your API key by setting it in the initial configuration of APIClient(). The Python library will then automatically send this key in each request.

All API requests must be made over HTTPS. Calls made over plain HTTP will fail. API requests without "X-API-Key" and "X-API-Client" in headers will also fail.

### Python
### Args
Parameter | Default | Description
--------- | ------- | -----------
clientid | - | Your personal client id
client_secret | - | your secret key
url | - | Server URL (optional)


### HTTP
### Headers
Parameter | Default | Description
--------- | ------- | -----------
X-API-Key | - | Your secret key
X-API-Client | - | Your client id

<aside class="notice">
You must replace <code>clientid</code> and <code>secretkey</code> with your personal client id and secret key.
</aside>


# Signing

## Sign

```python
from signing_client import SignResource

sign_resource = SignResource(api_client = api_client, 
                pdf_hash=hashlib.sha256(b'some').hexdigest(), 
                signer_information={'name': 'fake_name'})
sign_resource.sign()
```

```shell
curl --request POST 'http://127.0.0.1:8000/sign/' \
  --header 'X-API-Key: {{secretkey}}' \
  --header 'X-API-Client: {{clientid}}' \
```

> The above command returns JSON structured like this:

```json
  {
    "id": 1,
    "document": "hashed document"
  }
```

This endpoint sign your document.

### Python

### Args

Parameter | Default | Description
--------- | ------- | -----------
api_client | - | Your intialized client object.
pdf_hash | - | Content to sign
signer_information | - | Information to sing the content

### HTTP

`POST http://127.0.0.1:8000/sign/`

### Headers
Parameter | Default | Description
--------- | ------- | -----------
X-API-Key | - | Your secret key
X-API-Client | - | Your client id

### Query Parameters
Parameter | Default | Description
--------- | ------- | -----------
pdf_hash | - | Content to sign
signer_information | - | Information to sing the content

### Returns
With valid authorization, api will return a signed document