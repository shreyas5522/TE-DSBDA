## Commands
```
import bs4
import pandas as pd
import requests
```
```
request1= requests.get("https://books.toscrape.com/catalogue/page-2.html")
```
```
print(request1)
```
```
soup = bs4.BeautifulSoup(request1.text)
```
```
print(soup)
```
```
arti=soup.select('article h3 a' )
print(len(arti))
```
```
soup.select('article h3 a')
```
```
soup.select('article p i')
```
```
soup.select('article h3 a')[0]['title']
```
```
title_list=[]
```
```
rating_list=[]
```
```
print(title_list)
```
```
for num_pages in range(0,51):
 reqnew= requests.get('https://books.toscrape.com/catalogue/page-2.html')
 page_req_text= bs4.BeautifulSoup(reqnew.text)

for item in page_req_text.select('article h3 a'):
    title_list.append(item['title'])

for n in range(0,60,3):
    rating_list.append(page_req_text.select( 'article p')[n]['class'][1])
```
```
sl=dict(zip(title_list,rating_list))
```
```
new=pd.DataFrame.from_dict(sl,orient='index')
```
```
new.to_csv('index.csv')
```
```
new
```



