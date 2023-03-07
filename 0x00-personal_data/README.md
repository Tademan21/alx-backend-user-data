
       
    + name
    + email
    + phone
    + ssn
    + password
  + Only your `main` function should run when the module is executed.

+ [x] 5. **Encrypting passwords**<br/>[encrypt_password.py](encrypt_password.py) contains a script that meets the following requirements:
  + **INFO**: User *passwords* should **NEVER** be stored in *plain text* in a database.
  + Implement a `hash_password` function that expects one string argument name password and returns a salted, hashed password, which is a byte string.
  + Use the `bcrypt` package to perform the hashing (with `hashpw`).

+ [x] 6. **Check valid password**<br/>[app.py](app.py) contains an `is_valid` function that expects 2 arguments and returns a boolean:
  + Arguments:
    + `hashed_password`: `bytes` type.
    + `password`: `str` type.
  + Use bcrypt to validate that the provided password matches the hashed password.
