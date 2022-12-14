# Image Scraper
A library to scrape images from websites like Google, Getty and many more in the future.

## Pre-requisites:
1. conda create --name imagescraper python==3.8.8
2. pip install -r requirements.txt
3. Download Google Chrome 
4. Download Google Webdriver based on your Chrome version (See Setup below for more info)

## Setup:
1. Open cmd
2. Clone the repository (or [download](https://github.com/daisyyu2121/GoogleImageScraper/archive/refs/heads/main.zip))
    ```
    git clone https://github.com/daisyyu2121/GoogleImageScraper
    ```
3. Install Dependencies
    ```
    pip install -r requirements.txt
    ```  
4. Download the Chrome Webdriver
    - Download from [here](https://chromedriver.chromium.org/downloads)  
5. Change certain configs 
- in main.py
    - **line 22** website_list[index] for the website you want to scrape from
    - **line 26** the name of result file 
    - **line 29** for the number of images you want to scrape
- in GoogleImageScrapper.py
    - **line 64** change the url that you want to start
6. Run the code
    ```
    python main.py
    ```

## Usage:
```python
#Import libraries (Import in other website scrapers in the future)
from GoogleImageScrapper import GoogleImageScraper
from GettyImagesScrapper import GettyImageScraper
import os
from patch import webdriver_executable

#Define file path (Don't change)
webdriver_path = os.path.normpath(os.path.join(os.getcwd(), 'webdriver', webdriver_executable()))
image_path = os.path.normpath(os.path.join(os.getcwd(), 'photos'))

#Website used for scraping: 
website_list = ['google', 'getty', 'shutterstock', 'bing']
search_site = website_list[1] #change index number here to select the website you are using

#Add new search key into array ["cat","t-shirt","apple","orange","pear","fish"]
search_keys= ["cat","t-shirt"]

#Parameters
number_of_images = 10
headless = True
min_resolution=(0,0)
max_resolution=(1920,1080)

#Main program
#Choose if using Google or Getty Images Scrapper (or add in other options next time)
for search_key in search_keys:
    if search_site == 'google':
        image_scrapper = GoogleImageScraper(webdriver_path,image_path,search_key,number_of_images,headless,min_resolution,max_resolution)
    if search_site == 'getty':
        image_scrapper = GettyImageScraper(webdriver_path,image_path,search_key,number_of_images,headless,min_resolution,max_resolution)
    if search_site == 'shutterstock':
        image_scrapper = ShutterstockImageScraper(webdriver_path,image_path,search_key,number_of_images,headless,min_resolution,max_resolution)
    if search_site == 'bing':
        image_scrapper = BingImageScraper(webdriver_path,image_path,search_key,number_of_images,headless,min_resolution,max_resolution)
    image_urls = image_scrapper.find_image_urls()
    image_scrapper.save_images(image_urls)

#Release resources    
del image_scrapper

