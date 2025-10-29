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

from selenium.webdriver.common.by import By

class LoginPage:
    def __init__(self, driver):
        self.driver = driver
        self.username = (By.ID, "user-name")
        self.password = (By.ID, "password")
        self.login_button = (By.ID, "login-button")

    def enter_username(self, name):
        self.driver.find_element(*self.username).send_keys(name)

    def enter_password(self, pwd):
        self.driver.find_element(*self.password).send_keys(pwd)

    def click_login(self):
        self.driver.find_element(*self.login_button).click()
