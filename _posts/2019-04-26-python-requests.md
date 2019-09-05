# request

* 基本请求

  ```python
  req = requests.get("http://www.baidu.com")
  req = requests.post("http://www.baidu.com")
  req = requests.put("http://www.baidu.com")
  req = requests.delete("http://www.baidu.com")
  req = requests.head("http://www.baidu.com")
  req = requests.options("http://www.baidu.com")
  ```

* get请求

  ```python
  import requests
  
  url = "http://www.baidu.com/s"
  params = {'wd': '尚学堂'}
  response = requests.get(url, params=params)
  print(response.url)
  response.encoding = 'utf-8'
  html = response.text
  # print(html)
  ```

* post请求

  ```python
  import requests
  url = "http://www.sxt.cn/index/login/login.html"
  formdata = {
      "user" : "18234778600",
      "password" : "123456"
  }
  response = request.post(url,data=formdata)
  response.encoding = 'utf-8'
  html = response.text
  print(html)
  ```

* 自定义请求头

  ```python
  headers = {'User-Agent':'python'}
  r = requests.get('http://www.zhidaow.com', headers = headers)
  print(r.request.headers['User-Agent'])
  ```

* 设置超时时间

  ```python
  requests.get('http://github.com',timeout=0.01)
  ```

* 代理访问

  ```python
  import requests
  proxies = {
    "http": "http://10.10.1.10:3128",
    "https": "https://10.10.1.10:1080",
  }
  requests.get("http://www.zhidaow.com", proxies=proxies)
  ```

* session自动保存cookies

  ```python
  # 创建一个session对象 
  s = requests.Session() 
  # 用session对象发出get请求，设置cookies 
  s.get('http://httpbin.org/cookies/set/sessioncookie/123456789') 
  ```

* ssl验证

  ```python
  # 禁用安全请求警告
  requests.packages.urllib3.disable_warnings()
  
  resp = requests.get(url, verify=False, headers=headers)
  ```

* | 代码                 | 含义                         |
  | -------------------- | ---------------------------- |
  | resp.json()          | 获取响应内容（以json字符串） |
  | resp.text            | 获取响应内容 (以字符串)      |
  | resp.content         | 获取响应内容（以字节的方式） |
  | resp.headers         | 获取响应头内容               |
  | resp.url             | 获取访问地址                 |
  | resp.encoding        | 获取网页编码                 |
  | resp.request.headers | 请求头内容                   |
  | resp.cookie          | 获取cookie                   |

