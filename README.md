# scraping_project

###### USE  FILE V3_Linkedin_Scraper_Selenium_keyword_Recruiter.ipynb

## WHAT THIS WEB-SCRAPER CAN DO
* Login to Linkedin and scrape Recruiter's **Name, Title, # of connections ** 
* Customize this scraper by changing search_term variable in box[6] to keyphrase you're seeking
* 
## WALKTHROUGH OF HOW TO USE THIS SCRAPER
1. Import all libraries from box [1]
2. Head over to (Selenium)["https://chromedriver.chromium.org/downloads"] and download webdriver for your computer.

###### How to Find your Chrome version number:
1. Open Chrome browser
2. Click Chrome(upper left), then click "about", and you should see your version #

###### How to Configure Chrome Driver:
1. First, navigate to (Selenium)["https://chromedriver.chromium.org/downloads"] and download webdriver.
2. Go to find, and type in chromedriver. 
3. Click on Chromedriver and it should open up in terminal and say successfully Started.(Stay in terminal)
###### How to find executable_path on your computer
5. In terminal, copy your **executable_path** path to your Chrome driver on your computer which is located 
on the 2nd line of your terminal window under last login.

```
# your secret credentials:
import getpass
email = "youremail@gmail.com" 
password = getpass.getpass() #safely store your password here. 
#Note: you will manually have to type your password each time you run this program
```

###### Go to linkedin and login
**You don't have to change anything on this step
```
time.sleep(3)
browser.find_element_by_id('username').send_keys(email)
browser.find_element_by_id('password').send_keys(password)
time.sleep(3)
browser.find_element_by_id('password').send_keys(Keys.RETURN)
#Set Sleep time of 20
time.sleep(3)
```

###### Type Recruiter("or another search term") into text box and hit enter.
1. Change ```search_term``` variable to a different search term ( such as developer )
2. Change ```input.send_keys('**Recruiter**')``` to your new search term

```
search_term = "Recruiter"

input = browser.find_element_by_class_name('search-global-typeahead__input')
input.send_keys('Recruiter')
time.sleep(3)
input.send_keys(Keys.RETURN)
```
