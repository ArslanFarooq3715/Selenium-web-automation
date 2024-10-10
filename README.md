# Web Forum Scraper

## Overview
This project is a web scraping tool designed to automate data extraction from web forums. It uses Django as the backend framework, Selenium for browser automation, and Tor for accessing dark web content. This guide will take you through the process of setting up your own web scraping application from scratch.

## Table of Contents
1. [Technologies Used](#technologies-used)
2. [Requirements](#requirements)
   - [Libraries](#libraries)
   - [Additional Software](#additional-software)
3. [Setup Instructions](#setup-instructions)
   - [Django Application Setup](#django-application-setup)
   - [Connecting pgAdmin to Django](#connecting-pgadmin-to-django)
4. [Web Automation Code Snippets](#web-automation-code-snippets)
   - [Chrome Browser Automation](#chrome-browser-automation)
   - [Tor Browser Automation](#tor-browser-automation)
5. [Common Functions for Element Access](#common-functions-for-element-access)
6. [Database Insertion](#database-insertion)
7. [Conclusion](#conclusion)

## Technologies Used
- **Visual Studio Code**: A powerful code editor for development.
- **Google Chrome**: The web browser used for standard web automation.
- **Tor Browser**: Used to access dark web content.
- **Django**: A high-level Python web framework for backend development.
- **PL/SQL**: For database interaction.
- **JavaScript, CSS, HTML**: Technologies for frontend development.

## Requirements

### Libraries
To install the necessary Python libraries, create a `requirements.txt` file with the following content:

To install these libraries, run:

```bash
pip install -r requirements.txt
```

### Additional Software
- **[pgAdmin](https://www.pgadmin.org/download/)**: Download and install pgAdmin to manage your PostgreSQL database.

## Setup Instructions

### Django Application Setup
Follow these steps to set up your Django application:

1. **Install Django**:
   If you haven’t already installed Django, you can do so via pip:

   ```bash
   pip install django
   ```

2. **Create a Django Project**:
   Create a new Django project using the following command:

   ```bash
   django-admin startproject myproject
   cd myproject
   ```

3. **Run Migrations**:
   Prepare your database by running migrations:

   ```bash
   python manage.py migrate
   ```

4. **Start the Development Server**:
   To see your project in action, run:

   ```bash
   python manage.py runserver
   ```

   You can access your application at `http://127.0.0.1:8000/`.

### Connecting pgAdmin to Django
1. **Open pgAdmin** and connect to your PostgreSQL server.
2. **Create a New Database**:
   - Right-click on the "Databases" node and select "Create" > "Database".
   - Enter your database name and click "Save".

3. **Update `settings.py`**:
   Configure your database settings in `myproject/settings.py`:

   ```python
   DATABASES = {
       'default': {
           'ENGINE': 'django.db.backends.postgresql',
           'NAME': 'your_database_name',
           'USER': 'your_username',
           'PASSWORD': 'your_password',
           'HOST': 'localhost',
           'PORT': '5432',
       }
   }
   ```

4. **Install psycopg2**: 
   This is required for Django to communicate with PostgreSQL:

   ```bash
   pip install psycopg2
   ```

## Web Automation Code Snippets

### Chrome Browser Automation
To automate actions in Chrome, use the following code:

```python
from selenium import webdriver
from selenium.webdriver.support.ui import WebDriverWait

options = webdriver.ChromeOptions()
options.add_argument("--disable-blink-features=AutomationControlled")
options.add_argument("--no-sandbox")
options.add_argument("--disable-dev-shm-usage")
options.add_argument("--disable-gpu")
options.add_argument("--disable-cache")
options.add_argument("--start-maximized")
options.add_experimental_option("excludeSwitches", ["enable-automation"])
options.add_experimental_option('useAutomationExtension', False)

driver = webdriver.Chrome(options=options)
wait = WebDriverWait(driver, 10)
driver.get('<address of target website>')
```

### Tor Browser Automation
To automate actions in the Tor browser, use the following code:

```python
from selenium import webdriver
from selenium.webdriver.firefox.service import Service
from selenium.webdriver.firefox.options import Options
from selenium.webdriver.support.ui import WebDriverWait

tor_path = r"C:/Users/abc/Desktop/Tor Browser/Browser/firefox.exe"
gecko_path = "E:/Osint/darkweb/geckodriver32/geckodriver.exe"

profile = webdriver.FirefoxProfile()
profile.set_preference('network.proxy.socks_port', 9150)

options = Options()
options.binary_location = tor_path
options.profile = profile

service = Service(executable_path=gecko_path)
driver = webdriver.Firefox(service=service, options=options)
driver.delete_all_cookies()

wait = WebDriverWait(driver, 10)
conn_btn = wait.until(EC.element_to_be_clickable((By.XPATH, '//*[@id="connectButton"]')))
conn_btn.click()
t.sleep(20)

driver.get('<address of target website>')
```

## Common Functions for Element Access
Here are some common Selenium functions for element interaction:

- **Presence of All Elements**: 
  ```python
  EC.presence_of_all_elements_located
  ```
- **Element Clickable**: 
  ```python
  EC.element_to_be_clickable
  ```
- **Element Visibility**: 
  ```python
  EC.visibility_of_element_located
  ```
- **Visibility of All Elements**: 
  ```python
  EC.visibility_of_all_elements_located
  ```
- **Text Present in Element**: 
  ```python
  EC.text_to_be_present_in_element
  ```
- **Element Selected**: 
  ```python
  EC.element_to_be_selected
  ```
- **Invisibility of Element**: 
  ```python
  EC.invisibility_of_element_located
  ```
- **Element Selection State**: 
  ```python
  EC.element_selection_state_to_be
  ```
- **Element Visibility**: 
  ```python
  EC.visibility_of
  ```
- **Presence of Element**: 
  ```python
  EC.presence_of_element_located
  ```
- **Frame Available and Switch**: 
  ```python
  EC.frame_to_be_available_and_switch_to_it
  ```
- **Staleness of Element**: 
  ```python
  EC.staleness_of
  ```
- **Alert Present**: 
  ```python
  EC.alert_is_present
  ``` 

## Database Insertion
To insert records into your database using Django's ORM:

1. **Define Your Model**: In `models.py` of your app, define your data model:

   ```python
   from django.db import models

   class MyModel(models.Model):
       field1 = models.CharField(max_length=100)
       field2 = models.TextField()
   ```

2. **Run Migrations**:
   ```bash
   python manage.py makemigrations
   python manage.py migrate
   ```

3. **Insert a Record**:

   ```python
   from myapp.models import MyModel

   record = MyModel(field1='value1', field2='value2')
   record.save()
   ```

## Conclusion
This README provides a comprehensive guide to setting up a web scraping application. Follow each section carefully to create your own tool. Adjust the code snippets and configurations based on your specific requirements.

📬 **Contact Me: If you're interested in building an application that monitors dark web platforms, feel free to reach out:**

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Connect on LinkedIn</title>
    <style>
        .linkedin-button {
            display: inline-block;
            padding: 10px 20px;
            background-color: #0077b5; /* LinkedIn Blue */
            color: white;
            text-decoration: none;
            border-radius: 5px;
            font-size: 16px;
            margin: 10px 0;
            border: 1px solid #0077b5; /* LinkedIn Blue Border */
            transition: background-color 0.3s, border-color 0.3s;
        }
        .linkedin-button:hover {
            background-color: #005582; /* Darker LinkedIn Blue */
            border-color: #005582; /* Darker LinkedIn Blue Border */
        }
    </style>
</head>
<body>

    <h1>Let's Connect!</h1>
    <p>If you're interested in building an application that monitors dark web platforms, feel free to reach out:</p>
    
    <a href="https://www.linkedin.com/in/your-username" target="_blank" class="linkedin-button">
        Connect on LinkedIn
    </a>

</body>
</html>

