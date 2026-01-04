```
from pages.register_page import RegisterPage

class TestRegister:

    def test_register_page_loads(self, setup):
        register = RegisterPage(setup)
        register.open_register_page()
        assert register.is_register_page_loaded()
```
