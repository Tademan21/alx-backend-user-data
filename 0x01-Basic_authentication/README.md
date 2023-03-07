# Basic authentication

This project contains tasks for learning to authenticate a user using the Basic authentication scheme.

## Tasks To Complete

+ [x] 0. **Simple-basic-API**
  + Setup and start server:
    ```powershell
    bob@dylan:~$ pip3 install -r requirements.txt
    ...
    bob@dylan:~$
    bob@dylan:~$ API_HOST=0.0.0.0 API_PORT=5000 python3 -m api.v1.app
    
  + Now you will validate all requests to secure the API.
  + Update the method `def authorization_header(self, request=None) -> str:` in [api/v1/auth/auth.py](api/v1/auth/auth.py):
    + If request is `None`, returns `None`.
    + If `request` doesn't contain the header key `Authorization`, returns `None`.
    + Otherwise, return the value of the header request Authorization.
  + Update the file [api/v1/app.py](api/v1/app.py):
    + Create a variable `auth` initialized to None after the `CORS` definition.
    + Based on the environment variable `AUTH_TYPE`, load and assign the right instance of authentication to `auth`:
      + If `auth`:
        + Import `Auth` from `api.v1.auth.auth`.
        + Create an instance of `Auth` and assign it to the variable `auth`.
  + Now the biggest piece is the filtering of each request. For that you will use the Flask method `before_request`:
    + Add a method in [api/v1/app.py](api/v1/app.py) to handler `before_request`
      + If `auth` is `None`, do nothing.
      + If `request.path` is not part of this list `['/api/v1/status/', '/api/v1/unauthorized/', '/api/v1/forbidden/']`, do nothing - you must use the method `require_auth` from the auth instance.
      + If `auth.authorization_header(request)` returns `None`, raise the error `401` - you must use `abort`.
      + If `auth.current_user(request)` returns `None`, raise the error `403` - you must use `abort`.

+ [x] 6. **Basic auth**
  + Create a class `BasicAuth` in [api/v1/auth/basic_auth.py](api/v1/auth/basic_auth.py) that inherits from `Auth`. For the moment this class will be empty.
  + Update [api/v1/app.py](api/v1/app.py) for using `BasicAuth` class instead of `Auth` depending on the value of the environment variable `AUTH_TYPE`, If `AUTH_TYPE` is equal to `basic_auth`:
    + Import `BasicAuth` from `api.v1.auth.basic_auth`.
    + Create an instance of `BasicAuth` and assign it to the variable `auth`.
  + Otherwise, keep the previous mechanism with `auth` an instance of `Auth`.

+ [x] 7. **Basic - Base64 part**
  + Add the method `def extract_base64_authorization_header(self, authorization_header: str) -> str:` in the class `BasicAuth` in [api/v1/auth/basic_auth.py](api/v1/auth/basic_auth.py) that returns the Base64 part of the `Authorization` header for a Basic Authentication:
    + Return None if `authorization_header` is `None`.
    + Return None if `authorization_header` is not a string.
    + Return None if `authorization_header` doesn't start by `Basic` (with a space at the end).
    + Otherwise, return the value after `Basic` (after the space).
    + You can assume `authorization_header` contains only one `Basic`.

+ [x] 8. **Basic - Base64 decode**
  + Add the method `def decode_base64_authorization_header(self, base64_authorization_header: str) -> str:` in the class `BasicAuth` in [api/v1/auth/basic_auth.py](api/v1/auth/basic_auth.py) that returns the decoded value of a Base64 string `base64_authorization_header`:
    + Return `None` if `base64_authorization_header` is `None`.
    + Retu
