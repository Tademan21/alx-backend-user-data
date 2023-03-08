

  + Create a new authentication class `SessionDBAuth` in [api/v1/auth/session_db_auth.py](api/v1/auth/session_db_auth.py) that inherits from `SessionExpAuth`:
    + Overload `def create_session(self, user_id=None):` that creates and stores new instance of `UserSession` and returns the Session ID.
    + Overload `def user_id_for_session_id(self, session_id=None):` that returns the User ID by requesting `UserSession` in the database based on `session_id`.
    + Overload `def destroy_session(self, request=None):` that destroys the `UserSession` based on the Session ID from the request cookie.
  + Update [api/v1/app.py](api/v1/app.py) to instantiate `auth` with `SessionDBAuth` if the environment variable `AUTH_TYPE` is equal to `session_db_auth`.
