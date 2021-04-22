# Exceptions


The Signing API throws the following exceptions:


Exception | Error Code | Meaning
--------- | ---------- | -------
SigningClientUnAuthorizedException | 401 | Unauthorized -- Your API key is wrong.
SigningClientException | 500 | Internal Server Error -- We had a problem with our server. Try again later.
SigningClientLimitExceededException | 429 | You have exceeded your signing limit
