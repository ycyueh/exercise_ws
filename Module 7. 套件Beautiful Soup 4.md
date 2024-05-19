##  Module 7. 套件Beautiful Soup 4

套件介紹及常用功能
Beautiful Soup是一個 HTML parser，將 Document 轉換成一個樹狀結構，提供簡單的函式來走訪、搜尋、修改分析此樹狀結構，支援CSS選擇器。

常用功能
我們主要用 BeautifulSoup 套件來作為網站解析的工具。
	find() 方法 (取得單一元素)
	find_all() 方法 (取得元素集合)
  CSS選擇器
	select_one() 方法 (取得單一元素)
	select() 方法 (取得元素集合)

### BeautifulSoup 基本用法

soup.select()：
回傳的結果是元素集合（list 型態，BeautifulSoup ResultSet）

soup.select_one()：
回傳的結果是單一元素（BeautifulSoup Result）

### Beautifulsoup 套件

'''
參考網頁
[1] Python 使用 Beautiful Soup 抓取與解析網頁資料，開發網路爬蟲教學
https://blog.gtwang.org/programming/python-beautiful-soup-module-scrape-web-pages-tutorial/2/

```python
mport requests as req
from bs4 import BeautifulSoup as bs
from pprint import pprint

 # PTT NBA 板

url = "https://www.ptt.cc/bbs/NBA/index.html"

# 用 requests 的 get 方法把網頁抓下來

res = req.get(url) 

# 指定 lxml 作為解析器

soup = bs(res.text, "lxml") 

# 第一個 <a></a>

print(soup.find("a")) 

# 全部 <a></a>，此時回傳 list

print(soup.find_all("a")) 

# 指定 list 某個元素的 html

print(soup.find_all("a")[2]) 

# 取得 id 為 logo 的元素

logo = soup.find(id = "logo")
print(logo)

# 取得所有 div，類別名稱為 r-ent，回傳為 list

posts = soup.find_all("div", class_ = "r-ent")
print(posts)
'''
以下透過 CSS selector 取得元素，
回傳格式為 list
'''

# 輸出 title

print(soup.select_one('title'))

# 輸出 a

print(soup.select('a'))

# 透過 class 名稱取得元素

print(soup.select("a.board"))

# 透過 id 名稱取得元素

print(soup.select_one("#logo"))

# 透過 attribute 取得元素

print(soup.select('a[class="board"]'))

# 取得單一節點的文字內容 (select_one 會回傳單一 bs element 物件，select 會回傳 list)

print(soup.select_one('title').get_text())
print(soup.select('a')[0].get_text())

# 透過迭代取得所有 a 的文字內容

for a in soup.select('a'):
    print(a.get_text())

# 透過迭代取得所有 a 的屬性 href

for a in soup.select('a'):
    if a.has_attr('href'):
        print(a['href']) # a.get("href")
    else:
        print("=" * 50)
        print(f"連結[{a.get_text()}] 沒有 href 屬性")
        print("=" * 50)
```



i