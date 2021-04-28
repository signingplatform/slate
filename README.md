<p align="center">
  <img src="https://raw.githubusercontent.com/slatedocs/img/main/logo-slate.png" alt="Signing: API Documentation" width="226">
  <br>
</p>

<p align="center">Slate helps you create beautiful, intelligent, responsive API documentation.</p>

<p align="center"><em>Signing documentation was created with Slate. Check it out at <a href="https://slatedocs.github.io/slate">slatedocs.github.io/slate</a>.</em></p>

Features
------------

* **Clean, intuitive design** — With Slate, the description of your API is on the left side of your documentation, and all the code examples are on the right side. Inspired by [Stripe's](https://stripe.com/docs/api) and [PayPal's](https://developer.paypal.com/webapps/developer/docs/api/) API docs. Slate is responsive, so it looks great on tablets, phones, and even in print.

* **Everything on a single page** — Gone are the days when your users had to search through a million pages to find what they wanted. Slate puts the entire documentation on a single page. We haven't sacrificed linkability, though. As you scroll, your browser's hash will update to the nearest header, so linking to a particular point in the documentation is still natural and easy.

* **Slate is just Markdown** — When you write docs with Slate, you're just writing Markdown, which makes it simple to edit and understand. Everything is written in Markdown — even the code samples are just Markdown code blocks.

* **Write code samples in multiple languages** — If your API has bindings in multiple programming languages, you can easily put in tabs to switch between them. In your document, you'll distinguish different languages by specifying the language name at the top of each code block, just like with GitHub Flavored Markdown.

* **Out-of-the-box syntax highlighting** for [over 100 languages](https://github.com/rouge-ruby/rouge/wiki/List-of-supported-languages-and-lexers), no configuration required.

* **Automatic, smoothly scrolling table of contents** on the far left of the page. As you scroll, it displays your current position in the document. It's fast, too. We're using Slate at TripIt to build documentation for our new API, where our table of contents has over 180 entries. We've made sure that the performance remains excellent, even for larger documents.

* **Let your users update your documentation for you** — By default, your Slate-generated documentation is hosted in a public GitHub repository. Not only does this mean you get free hosting for your docs with GitHub Pages, but it also makes it simple for other developers to make pull requests to your docs if they find typos or other problems. Of course, if you don't want to use GitHub, you're also welcome to host your docs elsewhere.

* **RTL Support** Full right-to-left layout for RTL languages such as Arabic, Persian (Farsi), Hebrew etc.

Getting started with Slate is super easy! Simply press the green "use this template" button above and follow the instructions below. Or, if you'd like to check out what Slate is capable of, take a look at the [sample docs](https://slatedocs.github.io/slate/).

Getting Started with Slate
------------------------------

To get started with Slate, please check out the [Getting Started](https://github.com/slatedocs/slate/wiki#getting-started)
section in our [wiki](https://github.com/slatedocs/slate/wiki).

We support running Slate in three different ways:
* [Natively](https://github.com/slatedocs/slate/wiki/Using-Slate-Natively)
* [Using Vagrant](https://github.com/slatedocs/slate/wiki/Using-Slate-in-Vagrant)
* [Using Docker](https://github.com/slatedocs/slate/wiki/Using-Slate-in-Docker)


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