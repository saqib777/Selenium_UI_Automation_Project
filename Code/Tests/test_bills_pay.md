```
from pages.login_page import LoginPage
from pages.bill_pay_page import BillPayPage

class TestBillPay:

    def test_bill_pay_page_loads(self, setup):
        login = LoginPage(setup)
        login.login_as("john", "demo")

        bill_pay = BillPayPage(setup)
        bill_pay.open_bill_pay()
        assert bill_pay.is_bill_pay_page_loaded()

```
