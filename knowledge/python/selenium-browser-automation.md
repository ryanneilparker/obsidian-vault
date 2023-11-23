# How to automate your browser using python with selenium
## Setup

### Install Chrome WebDriver
- [Download Chrome v19 WebDriver](https://edgedl.me.gvt1.com/edgedl/chrome/chrome-for-testing/119.0.6045.105/win64/chromedriver-win64.zip)
- Place the driver in a directory called `drivers` in the root of the project.

### Create Python Virtual Environment and Install Selenium Package

```bash
python -m venv venv
venv/scripts/activate
pip install selenium
pip freeze > requirements.txt
```

### Configure Startup Script

```python
# setup/startup.py

from selenium import webdriver

webdriver_path = os.join.path('drivers', 'chromedriver-win64')
driver = webdriver.Chrome(executable_path=webdriver_path)
```



- Install a Selenium supported WebDriver for your favourite browser.
	- 
```
- Install selenium python package.
```python
from selenium.webdriver.import Chrome
from selenium.webdriver.chrome.options import Options
opts = Options()
assert opts.headless
browser = Chrome(options=opts)
browser.get('https://duckduckgo.com')
```

## Interactions
- Inspect page to find element ids.
```python
search_form = browser.find_element_by_id('search_form_input_homepage')
search_form.send_keys('real python')
search_form.submit()
results = broser.find_elements_by_class_name('result')
print(results[0].text)
```
- Always close the browser session before exiting your python session
```python
browser.close()
quit()
```