# Project Documentation :

## Quotes-Web-Scrapper
This project demonstrates web scraping of famous quotes using Python and BeautifulSoup. The script extracts quotes, authors, and tags from Quotes to Scrape and stores the data in a structured format.

## Features:

**•** Scrapes quotes, authors, and tags from multiple pages.

**•** Saves data in CSV.

**•** Includes error handling and rate-limiting to prevent server overload.

## 🛠 Tech Stack:

**•** Python

**•** BeautifulSoup (for parsing HTML)

**•** Requests (for handling HTTP requests)

**•** Pandas (for data storage & processing)



**Import Libraries**
import pandas as pd
import requests
from bs4 import BeautifulSoup
from tqdm import tqdm

To Load BeautifulSoup
res = requests.get('https://quotes.toscrape.com/')
soup = BeautifulSoup(res.text, 'html.parser')
print(soup.find('span', class_ = 'text').text[1:-1])
The world as we have created it is a process of our thinking. It cannot be changed without changing our thinking.
Quotes Scraping In First Page
quotes = []
for i in soup.find_all('span', class_ = 'text'):
    quotes.append(i.text[1:-1])
quotes
['The world as we have created it is a process of our thinking. It cannot be changed without changing our thinking.',
 'It is our choices, Harry, that show what we truly are, far more than our abilities.',
 'There are only two ways to live your life. One is as though nothing is a miracle. The other is as though everything is a miracle.',
 'The person, be it gentleman or lady, who has not pleasure in a good novel, must be intolerably stupid.',
 "Imperfection is beauty, madness is genius and it's better to be absolutely ridiculous than absolutely boring.",
 'Try not to become a man of success. Rather become a man of value.',
 'It is better to be hated for what you are than to be loved for what you are not.',
 "I have not failed. I've just found 10,000 ways that won't work.",
 "A woman is like a tea bag; you never know how strong it is until it's in hot water.",
 'A day without sunshine is like, you know, night.']
Scraping All The Details Of Quotes In First Page
data = []

for sp in soup.find_all('div', class_ = 'quote'):
    
    quote       = sp.find('span', class_ = 'text').text[1:-1]
    author_name = sp.find('small').text
    author_id   = sp.find('a').get('href')
    
    tags        = []
    for tag in sp.find_all('a', class_ = 'tag'):
        tags.append(tag.text)
    tags = ','.join(tags)
    data.append([quote, author_name, author_id, tags])   
Created a DataFrame
pd.DataFrame(data, columns = ['quote', 'author_name', 'author_id', 'tags'])
quote	author_name	author_id	tags
0	The world as we have created it is a process o...	Albert Einstein	/author/Albert-Einstein	change,deep-thoughts,thinking,world
1	It is our choices, Harry, that show what we tr...	J.K. Rowling	/author/J-K-Rowling	abilities,choices
2	There are only two ways to live your life. One...	Albert Einstein	/author/Albert-Einstein	inspirational,life,live,miracle,miracles
3	The person, be it gentleman or lady, who has n...	Jane Austen	/author/Jane-Austen	aliteracy,books,classic,humor
4	Imperfection is beauty, madness is genius and ...	Marilyn Monroe	/author/Marilyn-Monroe	be-yourself,inspirational
5	Try not to become a man of success. Rather bec...	Albert Einstein	/author/Albert-Einstein	adulthood,success,value
6	It is better to be hated for what you are than...	André Gide	/author/Andre-Gide	life,love
7	I have not failed. I've just found 10,000 ways...	Thomas A. Edison	/author/Thomas-A-Edison	edison,failure,inspirational,paraphrased
8	A woman is like a tea bag; you never know how ...	Eleanor Roosevelt	/author/Eleanor-Roosevelt	misattributed-eleanor-roosevelt
9	A day without sunshine is like, you know, night.	Steve Martin	/author/Steve-Martin	humor,obvious,simile
Scraping Quotes For All Pages
data = []
for page in tqdm(range(1,11)):
    
    link = 'https://quotes.toscrape.com/page/' + str(page)
    res = requests.get(link)
    soup = BeautifulSoup(res.text, 'html.parser')
    
    for sp in soup.find_all('div', class_ = 'quote'):

        author_id = sp.find('a').get('href')
        author_name = sp.find('small', class_ = 'author').text
        quote = sp.find('span', class_ = 'text').text[1:-1]
        
        tags = []
        for tag in sp.find_all('a', class_ = 'tag'):
            tags.append(tag.text)
        tags = ','.join(tags)
        data.append([author_id, author_name, tags, quote])
Created a DataFrame For All Pages Of Quotes Websites
df = pd.DataFrame(data, columns = ['author_id', 'author_name', 'tags', 'quote'])
df
author_id	author_name	tags	quote
0	/author/Albert-Einstein	Albert Einstein	change,deep-thoughts,thinking,world	The world as we have created it is a process o...
1	/author/J-K-Rowling	J.K. Rowling	abilities,choices	It is our choices, Harry, that show what we tr...
2	/author/Albert-Einstein	Albert Einstein	inspirational,life,live,miracle,miracles	There are only two ways to live your life. One...
3	/author/Jane-Austen	Jane Austen	aliteracy,books,classic,humor	The person, be it gentleman or lady, who has n...
4	/author/Marilyn-Monroe	Marilyn Monroe	be-yourself,inspirational	Imperfection is beauty, madness is genius and ...
...	...	...	...	...
95	/author/Harper-Lee	Harper Lee	better-life-empathy	You never really understand a person until you...
96	/author/Madeleine-LEngle	Madeleine L'Engle	books,children,difficult,grown-ups,write,write...	You have to write the book that wants to be wr...
97	/author/Mark-Twain	Mark Twain	truth	Never tell the truth to people who are not wor...
98	/author/Dr-Seuss	Dr. Seuss	inspirational	A person's a person, no matter how small.
99	/author/George-R-R-Martin	George R.R. Martin	books,mind	... a mind needs books as a sword needs a whet...
100 rows × 4 columns

Save The Quotes Dataset
df.to_csv('Quotes.csv', index = False)
 
df['author_link'] = 'https://quotes.toscrape.com' + df['author_id']
quote = sp.find('span', class_ = 'text').text[1:-1]
quote
'... a mind needs books as a sword needs a whetstone, if it is to keep its edge.'
author_name = sp.find('small', class_ = 'author').text
author_name
'George R.R. Martin'
author_id = sp.find('a').get('href')
author_id
'/author/George-R-R-Martin'
tags = []
for tag in sp.find_all('a', class_ = 'tag'):
    tags.append(tag.text)
tags = ','.join(tags)
quote = sp.find('span', class_ = 'text')
quote.text
'“A day without sunshine is like, you know, night.”'
author_name = sp.find('small', class_ = 'author')
author_name.text
'Steve Martin'
author_id = sp.find('a').get('href')
author_id
'/author/Steve-Martin'
tags = []
for tag in sp.find_all('a', class_ = 'tag'):
    tags.append(tag.text)
tags = ','.join(tags)
for i in soup.find_all('small', class_ = 'author'):
    print(i.text)
Albert Einstein
J.K. Rowling
Albert Einstein
Jane Austen
Marilyn Monroe
Albert Einstein
André Gide
Thomas A. Edison
Eleanor Roosevelt
Steve Martin
