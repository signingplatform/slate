# Exceptions

Signing uses conventional HTTP response codes to indicate the success or failure of an API request. In general: Codes in the 2xx range indicate success. Codes in the 4xx range indicate an error that failed given the information provided (e.g., a required parameter was omitted, signing limit exceeded, etc.). Codes in the 5xx range indicate an error with Signing's servers.

**Attributes**

Params | Meaning
------ | -------
type | The type of error returned.
content | string - A message providing more details about the error. For limit exceeding errors, these messages can be shown to your users.
code | Int - indicating the error code reported

**Error Types**

Exception | Meaning
--------- | -------
SigningClientUnAuthorizedException | Unauthorized -- Your API key is wrong.
SigningClientException | Internal Server Error -- We had a problem with our server. Try again later.
SigningClientLimitExceededException | You have exceeded your signing limit

## Handling Error

```python
try:
    # use signing library to make request
except SigningClientUnAuthorizedException as e :
    # invalid client id or secret key
    print(f"Message is {e.content} ")
    print(e.code)

except SigningClientLimitExceededException as e :
    # client exceeded the signing limit

except SigningClientException as e :
    # Exception raised when the SDK is used incorrectly.

except Exception as e:
    # Something else happened, completely unrelated to signing
    
```
Our Client libraries raise exceptions for many reasons, such as a limit exceeded, invalid parameters, authentication errors, and network unavailability. We recommend writing code that gracefully handles all possible API exceptions.