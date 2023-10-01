THE WEATHER DATA SCRAPER(🌥️🌞🌦️⚡🌤️)




Here we are going to see how to scrape weather data using Python.

We will scrape the weather information from Google using bs4 and requests libraries in python. 

OVERVIEW

The weather data scapper downloads high resolution weather data from the weather stations around the world for the user.



MODULES REQUIRED


Requests- It is a Python HTTP library. It makes HTTP requests simpler. 
we just need to add the URL as an argument and the get() gets all the information from it.
!pip install requests


Pandas- Pandas is a library that may be used to manipulate and analyse data. 
It is customary to extract data and save it in the desired format.
!pip install pandas

BeautifulSoup- is another powerful Python library for pulling out data from HTML/XML files. 
It creates a parse tree for parsed pages that can be used to extract data from HTML, which is useful for web scraping.
!pip install bs4


URL = f'https://www.google.com/search?q=weather+{query}'


CODE

from requests_html import HTMLSession
import csv

s = HTMLSession()

query = 'India'

url = f'https://www.google.com/search?q=weather+{query}'

r = s.get(url, headers={'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/117.0.0.0 Safari/537.36 Edg/117.0.2045.47'})

temp = r.html.find('span#wob_tm', first=True).text
unit = r.html.find('div.vk_bk.wob-unit span.wob_t', first=True).text
description = r.html.find('div.VQF4g', first=True).find('span#wob_dc', first=True).text


data = [query, temp, unit, description]


csv_file = 'weather_data.csv'


with open(csv_file, mode='w', newline='') as file:
    writer = csv.writer(file)
    writer.writerow(['Query', 'Temperature', 'Unit', 'Description']) 
    writer.writerow(data)  

print(query, temp, unit, description)

print(f"Data has been saved in '{csv_file}' file.")



This is just a basic code which scrapes the weather data found on website into a CSV file which can be used to visualize the data in a meaningful way. I would appreciate feedback or suggestions. :)

