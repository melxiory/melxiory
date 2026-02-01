<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com/?font=Fira+Code&size=28&duration=2800&pause=2000&color=43B02A&center=true&vCenter=true&width=600&height=70&lines=Selenium+Learning;Test+Automation" alt="Typing SVG" />
</p>

<div align="center">

![Python](https://img.shields.io/badge/Python-3.11+-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Selenium](https://img.shields.io/badge/Selenium-4+-43B02A?style=for-the-badge&logo=selenium&logoColor=white)
![pytest](https://img.shields.io/badge/pytest-Latest-0A9EDC?style=for-the-badge&logo=pytest&logoColor=white)
![POM](https://img.shields.io/badge/Page_Object_Pattern-FF6B6B?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)

</div>

---

## 📋 Overview

A comprehensive **Selenium learning project** demonstrating **test automation best practices** using **pytest** and the **Page Object Model (POM)** design pattern. Perfect for learning browser automation and testing fundamentals.

### What You'll Learn

- 🎯 **Page Object Model** implementation
- 🔧 **pytest** fixtures and parametrization
- ⏱️ **Explicit & Implicit Waits**
- 📸 **Screenshot** capture on failure
- 🏗️ **Clean Architecture** for test automation
- 🔄 **Cross-browser testing**
- 📊 **HTML Reports** generation
- 🎪 **Mocking** external dependencies

---

## 🚀 Tech Stack

| Component | Technology |
|-----------|------------|
| **Language** | Python 3.11+ |
| **Test Framework** | pytest 7+ |
| **Browser Automation** | Selenium 4 |
| **Pattern** | Page Object Model |
| **Reporting** | pytest-html |
| **Linting** | ruff, black |

---

## 📦 Installation

### Prerequisites

- Python 3.11 or higher
- Chrome/Firefox/Edge browsers
- ChromeDriver/GeckoDriver (auto-managed by webdriver-manager)

### Step 1: Clone the Repository

```bash
git clone https://github.com/melxiory/selenium_learning_project.git
cd selenium_learning_project
```

### Step 2: Create Virtual Environment

```bash
# Windows
python -m venv venv
venv\Scripts\activate

# Linux/Mac
python3 -m venv venv
source venv/bin/activate
```

### Step 3: Install Dependencies

```bash
pip install -r requirements.txt
```

### Step 4: Run Tests

```bash
# Run all tests
pytest

# Run with HTML report
pytest --html=report.html --self-contained-html

# Run specific test file
pytest tests/test_login.py

# Run with verbose output
pytest -v
```

---

## 📁 Project Structure

```
selenium_learning_project/
├── pages/                   # Page Object classes
│   ├── base_page.py        # Base page with common methods
│   ├── login_page.py       # Login page object
│   ├── home_page.py        # Home page object
│   └── __init__.py
├── tests/                   # Test cases
│   ├── test_login.py       # Login tests
│   ├── test_search.py      # Search tests
│   └── conftest.py         # pytest fixtures
├── utils/                   # Helper utilities
│   ├── driver_manager.py   # WebDriver setup
│   ├── screenshot.py       # Screenshot utilities
│   └── config.py           # Configuration
├── reports/                 # Test reports
├── .env.example             # Environment variables template
├── pytest.ini              # pytest configuration
└── requirements.txt
```

---

## 🎯 Page Object Pattern

### Base Page

```python
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC

class BasePage:
    def __init__(self, driver):
        self.driver = driver
        self.timeout = 10

    def find_element(self, locator):
        return WebDriverWait(self.driver, self.timeout).until(
            EC.presence_of_element_located(locator)
        )

    def click(self, locator):
        element = self.find_element(locator)
        element.click()

    def enter_text(self, locator, text):
        element = self.find_element(locator)
        element.clear()
        element.send_keys(text)
```

### Login Page Object

```python
from selenium.webdriver.common.by import By
from pages.base_page import BasePage

class LoginPage(BasePage):
    # Locators
    USERNAME_INPUT = (By.ID, "username")
    PASSWORD_INPUT = (By.ID, "password")
    LOGIN_BUTTON = (By.CSS_SELECTOR, "button[type='submit']")
    ERROR_MESSAGE = (By.CSS_SELECTOR, ".error")

    def __init__(self, driver):
        super().__init__(driver)
        self.url = "https://example.com/login"

    def load(self):
        self.driver.get(self.url)

    def login(self, username, password):
        self.enter_text(self.USERNAME_INPUT, username)
        self.enter_text(self.PASSWORD_INPUT, password)
        self.click(self.LOGIN_BUTTON)

    def get_error_message(self):
        return self.find_element(self.ERROR_MESSAGE).text
```

---

## 🧪 Test Examples

### Basic Login Test

```python
import pytest
from pages.login_page import LoginPage

class TestLogin:
    def test_valid_login(self, driver):
        login_page = LoginPage(driver)
        login_page.load()
        login_page.login("user@example.com", "password123")
        assert driver.current_url == "https://example.com/dashboard"

    def test_invalid_login(self, driver):
        login_page = LoginPage(driver)
        login_page.load()
        login_page.login("invalid@example.com", "wrongpass")
        error = login_page.get_error_message()
        assert "Invalid credentials" in error
```

### Parametrized Test

```python
@pytest.mark.parametrize("username, password, expected", [
    ("user@example.com", "validpass", "success"),
    ("", "password", "username_required"),
    ("user@example.com", "", "password_required"),
])
def test_login_scenarios(driver, username, password, expected):
    login_page = LoginPage(driver)
    login_page.load()
    login_page.login(username, password)
    # Assert based on expected result
```

---

## 🔧 Fixtures (conftest.py)

```python
import pytest
from selenium import webdriver
from utils.driver_manager import DriverManager

@pytest.fixture(scope="function")
def driver():
    driver = DriverManager.get_driver(browser="chrome")
    driver.maximize_window()
    yield driver
    driver.quit()

@pytest.fixture(scope="function")
def login_page(driver):
    from pages.login_page import LoginPage
    page = LoginPage(driver)
    page.load()
    return page
```

---

## 📸 Screenshot on Failure

```python
@pytest.mark.hookwrapper
def pytest_runtest_makereport(item):
    outcome = yield
    report = outcome.get_result()
    if report.when == "call" and report.failed:
        driver = item.funcargs.get("driver")
        if driver:
            screenshot_path = f"screenshots/{item.name}.png"
            driver.save_screenshot(screenshot_path)
```

---

## 🧪 Running Different Test Scenarios

### Run tests by marker

```bash
# Run only smoke tests
pytest -m smoke

# Run only regression tests
pytest -m regression
```

### Run tests on different browsers

```bash
# Chrome
pytest --browser=chrome

# Firefox
pytest --browser=firefox

# Headless mode
pytest --headless=true
```

### Parallel execution

```bash
# Install pytest-xdist
pip install pytest-xdist

# Run with 4 parallel workers
pytest -n 4
```

---

## 📊 HTML Reports

Generate beautiful HTML reports:

```bash
pytest --html=reports/report.html --self-contained-html
```

Report features:
- ✅ Test results summary
- ⏱️ Execution time per test
- 📸 Screenshots on failure
- 📊 Test statistics

---

## 🔧 Configuration

### pytest.ini

```ini
[pytest]
testpaths = tests
python_files = test_*.py
python_classes = Test*
python_functions = test_*
addopts =
    -v
    --strict-markers
    --tb=short
markers =
    smoke: Smoke tests
    regression: Regression tests
    slow: Slow running tests
```

---

## 🎓 Learning Path

1. **Week 1**: Basic Selenium operations
   - Finding elements
   - Clicking and typing
   - Waiting strategies

2. **Week 2**: Page Object Pattern
   - Creating page classes
   - Separating locators
   - Reusable methods

3. **Week 3**: pytest Framework
   - Fixtures
   - Parametrization
   - Markers

4. **Week 4**: Advanced Topics
   - Cross-browser testing
   - Parallel execution
   - CI/CD integration

---

## 🤝 Contributing

Contributions are welcome! This is a learning project, so feel free to:

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 👨‍💻 Author

**melxiory**

- GitHub: [@melxiory](https://github.com/melxiory)

---

## 🙏 Acknowledgments

- [Selenium](https://www.selenium.dev/) - Browser automation tools
- [pytest](https://docs.pytest.org/) - The pytest framework
- [Martin Fowler](https://martinfowler.com/bliki/PageObject.html) - Page Object Pattern concept

---

## 📚 Additional Resources

- [Selenium Python Documentation](https://www.selenium.dev/documentation/)
- [pytest Documentation](https://docs.pytest.org/)
- [Page Object Model Guide](https://www.selenium.dev/documentation/test_practices/encouraged/page_object_models/)

---

<div align="center">

### 🌟 Star this repo if it helped you!

[![GitHub stars](https://img.shields.io/github/stars/melxiory/selenium_learning_project?style=social)](https://github.com/melxiory/selenium_learning_project/stargazers)
[![GitHub forks](https://img.shields.io/github/forks/melxiory/selenium_learning_project?style=social)](https://github.com/melxiory/selenium_learning_project/network/members)

### 🎓 Learning Test Automation? Start here!

</div>
