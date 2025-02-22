# Web Scraping with Beautiful Soup

## Project Objective
To scrape the Times of India homepage and extract the routing options, their hyperlinks, descriptions, and image URLs, and save the extracted information into an Excel sheet.

## Prerequisites
- Basic understanding of Python.
- Installation of necessary libraries: Beautiful Soup, Requests, and Pandas.

## Setup
1. **Install Required Libraries:**
   ```bash
   pip install beautifulsoup4 requests pandas
Import Libraries:
import requests
from bs4 import BeautifulSoup
import pandas as pd

## Steps to Develop the Project
**Step 1: Fetch the HTML Content**
Send an HTTP request to the Times of India homepage using the requests library:
```bash
response = requests.get("https://timesofindia.indiatimes.com")
Data_from_website = BeautifulSoup(response.content, "lxml")
```

**Step 2: Parse the HTML Content**

Identify and extract the routing options, hyperlinks, descriptions, and image URLs using Beautiful Soup:
```bash
label_name = []
api_link = []
img_url = []
descriptions = []

for i in Data_from_website.find_all("a"):
    label_name.append(i.get_text())
    api_link.append(i.get("href"))
    img_tag = i.find('img')
    img_scr = img_tag.get('src') if img_tag else None
    img_url.append(img_scr)

dis_1 = Data_from_website.find_all("p")
dis_2 = Data_from_website.find_all("figcaption")
dis_3 = Data_from_website.find_all("span")

for tag in dis_1 + dis_2 + dis_3:
    descriptions.append(tag.text)
```
**Step 3: Store Data in an Excel Sheet**

Create a Pandas DataFrame and save it to an Excel file:
```bash
min_length = min(len(label_name), len(api_link), len(img_url), len(descriptions))

label_name = label_name[:min_length]
api_link = api_link[:min_length]
img_url = img_url[:min_length]
descriptions = descriptions[:min_length]

df = pd.DataFrame({'Names': label_name, "Links": api_link, "Image": img_url, "Description": descriptions})
df.to_csv("times_of_india.csv", index=False)
```
## Conclusion

This project involved web scraping the Times of India homepage to extract routing options, their hyperlinks, descriptions, and image URLs. Using Python libraries such as Beautiful Soup, Requests, and Pandas, I successfully fetched, parsed, and stored the relevant data into an Excel sheet.
