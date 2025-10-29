# E-commerce-web-UPI-and-API-Automation-Framework

import pytest
from selenium import webdriver
from pages.login_page import LoginPage

@pytest.fixture
def setup():
    driver = webdriver.Chrome()
    driver.get("https://www.saucedemo.com/")
    yield driver
    driver.quit()

def test_login_valid_user(setup):
    login = LoginPage(setup)
    login.enter_username("standard_user")
    login.enter_password("secret_sauce")
    login.click_login()
    assert "inventory" in setup.current_url
