
+ [x] 10. **Sessions in database**
  + Since the beginning, all Session IDs are stored in memory. It means, if your application stops, all Session IDs are lost.
  + To avoid that, you will create a new authentication system, based on Session ID stored in database (for us, it will be in a file, like `User`).
  + Create a new model `UserSession` in [models/user_session.py](models/user_session.py) that inherits from `Base`:
    + Implement the `def __init__(self, *args: list, **kwargs: dict):` like in `User` but for these 2 attributes:
      + `user_id`: string.
      + `session_id`: string.
  + Create a new authentication class `SessionDBAuth` in [api/v1/auth/session_db_auth.py](api/v1/auth/session_db_auth.py) that inherits from `SessionExpAuth`:
    + Overload `def create_session(self, user_id=None):` that creates and stores new instance of `UserSession` and returns the Session ID.
    + Overload `def user_id_for_session_id(self, session_id=None):` that returns the User ID by requesting `UserSession` in the database based on `session_id`.
    + Overload `def destroy_session(self, request=None):` that destroys the `UserSession` based on the Session ID from the request cookie.
  + Update [api/v1/app.py](api/v1/app.py) to instantiate `auth` with `SessionDBAuth` if the environment variable `AUTH_TYPE` is equal to `session_db_auth`.
