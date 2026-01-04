```
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC


class AccountsPage:
    def __init__(self, driver):
        self.driver = driver
        self.wait = WebDriverWait(driver, 10)

    # Locator
    ACCOUNTS_OVERVIEW_HEADER = (By.XPATH, "//h1[contains(text(),'Accounts Overview')]")
    ACCOUNT_ROWS = (By.CSS_SELECTOR, "table tbody tr")

    def is_accounts_page_loaded(self):
        self.wait.until(
            EC.presence_of_element_located(self.ACCOUNTS_OVERVIEW_HEADER)
        )
        return True

    def has_accounts(self):
        rows = self.driver.find_elements(*self.ACCOUNT_ROWS)
        return len(rows) > 0
```
