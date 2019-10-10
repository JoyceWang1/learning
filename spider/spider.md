# 基础知识
## 工作原理
0.获取数据 -\> 1.解析数据 -\> 2.提取数据 -\> 3.存储数据

## 基本示例
> 操作对象的变化：
> - URL -\> Response 对象 -\> 字符串(html) -\> BeautifulSoup 对象
> - BeautifulSoup 对象 -\> list -\> Tag 对象
> - BeautifulSoup 对象 -\> Tag 对象


![ spiderimg]()([https://raw.githubusercontent.com/JoyceWang1/learning/master/img/spiderimg.png][1])

### 0. 获取数据`Requests`
Python 实现的话，基础库：requests
```python
import requests

# 0.获取数据 requests
res = requests.get('https://www.baidu.com')
print(type(res))	# <class 'requests.models.Response'>

# 二进制
if res.status_code == 200:
	with open('xyz.jpg','wb') as photo:	# 图片需要以二进制 wb 读写
		photo.write(res.content)
# 文本
if res.status_code == 200:
	with open('./三国演义第一章.md','w') as f:
		f.write(res.text)

# Response 4个基本属性：
# response.status_code	# http 返回码
# response.content	# 返回数据转化为二进制，用于图片、视频等
# response.text	# 返回数据转化为字符串
# response.encoding	# res 对象的编码
```
[HTTP 返回码][2]
### 1. 解析数据`BeautifulSoup`
> 解析数据：读懂 html
bs 不是标准库，需要安装：`pip3 install BeautifulSoup4` ，查看`pip list |grep -i Beau`

```python
# bs 对象
# 解析数据
# 『要解析的文本』 必须必须是字符串
# 『解析器』 简单的是内置 htmp.parser
# bs_obj = BeautifulSoup(要解析的文本,'解析器')
bs = BeautifulSoup(res.text,'html.parser')
```

### 2. 提取数据`BeautifulSoup`
关键知识点：

1. `find/find_all`

| 方法 | 作用 | 用法 |示例 | 返回值对象 |
|:----|:----|:----|:----|:----|
| `find()`| 提取满足要求的**首个**数据 | `bs_obj.find(标签,属性)` | `soup.find('div',class_='books')` | Tag |
| `find_all()`| 提取满足要求的** 所有**数据 | `bs_obj.find_all(标签,属性)` | `soup.find_all('div',class_='books')` | ResultSet |

注：
- `class_`是为了区分 Python 的 class
- 标签和属性可以任选其一，也可以一起使用

```python
# 提取数据
# 2大知识点： find() 与 find_all() 、Tag 对象
item = bs.find('div')
```

2. `Tag`

| 属性/方法 | 作用 |
|:----|:----|
| `Tag.find()` 和 `Tag.find_all()` | 提取 Tag 中的 Tag |
| `Tag.text` | 提取 Tag 中的文字 |
| `Tag['属性名']` | 输入参数：属性名，可以提取 Tag 中这个属性的值 |

## 爬虫伦理
`Robots`协议：互联网爬虫工人的道德规范，全程为『网络爬虫排除标准』Rotots exclusion protocol ，网站会告诉爬虫哪些可以抓取，哪些不可以。
Robots 详情：`域名 + /robots.txt` ，比如：
- [https://baidu.com/robots.txt][3]
- [https://www.taobao.com/robots.txt][4]
Robots 参数：
- `Allow`  允许被访问
- `Disallow` 不允许被访问
```html
User-agent:  Baiduspider  #百度爬虫
Allow:  /article # 允许访问 /article.htm
Allow:  /oshtml # 允许访问 /oshtml.htm
Allow:  /ershou # 允许访问 /ershou.htm
Allow: /$ # 允许访问根目录，即淘宝主页
Disallow:  /product/ # 禁止访问/product/
Disallow:  / # 禁止访问除 Allow 规定页面之外的其他所有页面
​
User-Agent:  Googlebot # 谷歌爬虫
Allow:  /article
Allow:  /oshtml
Allow:  /product # 允许访问/product/
Allow:  /spu
Allow:  /dianpu
Allow:  /oversea
Allow:  /list
Allow:  /ershou
Allow: /$
Disallow:  / # 禁止访问除 Allow 规定页面之外的其他所有页面
```

[1]:	https://raw.githubusercontent.com/JoyceWang1/learning/master/img/spiderimg.png
[2]:	https://localprod.pandateacher.com/python-manuscript/crawler-html/exercise/HTTP%E5%93%8D%E5%BA%94%E7%8A%B6%E6%80%81%E7%A0%81.md
[3]:	http://baidu.com/robots.txt
[4]:	https://www.taobao.com/robots.txt

