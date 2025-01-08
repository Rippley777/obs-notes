from selenium import webdriver
from selenium.webdriver.common.keys import Keys
import time

# Replace these with your actual login credentials and URLs
sites = [
    {'url': 'https://example.com/login', 'username': 'your_username1', 'password': 'your_password1', 'username_field': 'username', 'password_field': 'password'},
    {'url': 'https://another-example.com/login', 'username': 'your_username2', 'password': 'your_password2', 'username_field': 'username', 'password_field': 'password'},
    {'url': 'https://third-example.com/login', 'username': 'your_username3', 'password': 'your_password3', 'username_field': 'username', 'password_field': 'password'}
]

# Initialize the WebDriver (make sure to specify the correct path to your WebDriver)
driver = webdriver.Chrome('/path/to/chromedriver')

for site in sites:
    driver.get(site['url'])

    # Find the username and password fields and enter the login credentials
    username_field = driver.find_element_by_name(site['username_field'])
    password_field = driver.find_element_by_name(site['password_field'])

    username_field.send_keys(site['username'])
    password_field.send_keys(site['password'])

    # Find the login button and click it (you may need to adjust this based on the site's HTML)
    login_button = driver.find_element_by_xpath('//button[@type="submit"]')
    login_button.click()

    # Wait for the login process to complete (you may need to adjust the sleep time)
    time.sleep(5)

# Close the browser when done
driver.quit()
