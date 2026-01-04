```
import pytest
from pages.login_page import LoginPage

class TestLogin:

    def test_valid_login(self, setup):
        login = LoginPage(setup)
        login.login_as("john", "demo")
        assert login.is_login_successful()

    def test_invalid_login(self, setup):
        login = LoginPage(setup)
        login.login_as("Saaq_7", "wrongpassword")
        assert "could not be verified" in login.get_login_error_message()
```
