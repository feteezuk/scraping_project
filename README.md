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
2. Change ```input.send_keys('Recruiter')``` to your new search term 

```
search_term = "Recruiter"

input = browser.find_element_by_class_name('search-global-typeahead__input')
input.send_keys('Recruiter')
time.sleep(3)
input.send_keys(Keys.RETURN)
```

###### CLICK ON PEOPLE to get list of people #
1. This will specifically click on the first ```li button``` in the upper nav under the search bar. Normally, it's "People" pill that gets clicked.

```
browser.find_element_by_xpath("/html/body/div[5]/div[3]/div/div[2]/section/div/nav/div/ul/li[1]/button").click()
```

###### Add This code to Get a Dataframe of your search term.
1. The ```iter``` counter is used by the while loop to iterate through the different pages based on the search term
***Important Note: You must change the "recruiter" to your search term in variable "the_link"
```the_link="https://www.linkedin.com/search/results/people/?keywords=recruiter&origin=SWITCH_SEARCH_VERTICAL&page="```
2. the_link variable concatenates with the string version of the iter counter, and stripped of any spaces which will naviagte to your specific search terms link. Leave a comment below if you're having trouble with the link.
3. The iter variable is an outer loop which waits for the x variable **2 inner loops** 1.```#Get Name and NUMBER of connections``` and the 2. ```# Get JOB Title of reCruiter``` . Once the inner loops are complete, the ```iter=iter+1``` gets updated to the next number up which brings the next page of the search term, such as:

```https://www.linkedin.com/search/results/people/?keywords=recruiter&origin=SWITCH_SEARCH_VERTICAL&page=1```
```https://www.linkedin.com/search/results/people/?keywords=recruiter&origin=SWITCH_SEARCH_VERTICAL&page=2```
```https://www.linkedin.com/search/results/people/?keywords=recruiter&origin=SWITCH_SEARCH_VERTICAL&page=3```
```https://www.linkedin.com/search/results/people/?keywords=recruiter&origin=SWITCH_SEARCH_VERTICAL&page=4```





```
title=[]
name = []
number_of_connections=[]
link = []
iter=1
while iter<5:
    the_link="https://www.linkedin.com/search/results/people/?keywords=recruiter&origin=SWITCH_SEARCH_VERTICAL&page="
    the_link = the_link+str(iter).strip()
    browser.get(the_link)

    desc = browser.find_elements_by_class_name("entity-result__title-text")

    x=0
    #Get Name and NUMBER of connections
    while x < len(desc):
        name_and_deg_aray = desc[x].text.split("\n")
        name.append(name_and_deg_aray[0]) #Don't change 0, it grabs name and puts into array
        number_of_connections.append(name_and_deg_aray[3])
        link.append(browser.find_element_by_partial_link_text(name_and_deg_aray[0]).get_attribute("href"))
        x=x+1
    

    # Get JOB Title of reCruiter
    x=0
    title_aray = browser.find_elements_by_class_name('entity-result__primary-subtitle')
    while x < len(title_aray):
        title.append(title_aray[x].text)
        x=x+1
    
   
    iter=iter+1
    
#create DataFrame 
df=pd.DataFrame({'name': name,'title':title, 'number_of_connections':number_of_connections, 'link':link})




df

```
