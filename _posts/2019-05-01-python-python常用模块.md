# python常用模块

### os模块

```python
os.remove()#删除文件
os.unlink()#删除文件
os.raname()#重命名文件
os.listdir()#列出指定目录下所有文件
os.chdir()#改变当前工作目录
os.getcwd()#获取当前工作目录
os.mkdir()#新建目录
os.rmdir() #删除空目录(删除非空目录, 使用shutil.rmtree())
os.makedirs() #创建多级目录
os.removedirs() #删除多级目录
os.stat(file)#获取文件属性
os.chmod(file) #修改文件权限
os.utime(file) #修改文件时间戳
os.name(file) #获取操作系统标识
os.system() #执行操作系统命令
os.execvp() #启动一个新进程
os.fork() #获取父进程ID，在子进程返回中返回0
os.execvp() #执行外部程序脚本（Uinx）
os.spawn() #执行外部程序脚本（Windows）
os.access(path, mode) #判断文件权限(详细参考cnblogs)
os.wait() #暂时未知
os.path#模块：
os.path.split(filename) #将文件路径和文件名分割(会将最后一个目录作为文件名而分离)
os.path.splitext(filename) #将文件路径和文件扩展名分割成一个元组
os.path.dirname(filename) #返回文件路径的目录部分
os.path.basename(filename) #返回文件路径的文件名部分
os.path.join(dirname,basename) #将文件路径和文件名凑成完整文件路径
os.path.abspath(name) #获得绝对路径
os.path.splitunc(path) #把路径分割为挂载点和文件名
os.path.normpath(path) #规范path字符串形式
os.path.exists() #判断文件或目录是否存在
os.path.isabs() #如果path是绝对路径，返回True
os.path.realpath(path) #返回path的真实路径
os.path.relpath(path[, start]) #从start开始计算相对路径 
os.path.normcase(path) #转换path的大小写和斜杠
os.path.isdir() #判断name是不是一个目录，name不是目录就返回false
os.path.isfile() #判断name是不是一个文件，不存在返回false
os.path.islink() #判断文件是否连接文件,返回boolean
os.path.ismount() #指定路径是否存在且为一个挂载点，返回boolean
os.path.samefile() #是否相同路径的文件，返回boolean
os.path.getatime() #返回最近访问时间 浮点型
os.path.getmtime() #返回上一次修改时间 浮点型
os.path.getctime() #返回文件创建时间 浮点型
os.path.getsize() #返回文件大小 字节单位
os.path.commonprefix(list) #返回list(多个路径)中，所有path共有的最长的路径
os.path.lexists #路径存在则返回True,路径损坏也返回True
os.path.expanduser(path) #把path中包含的”~”和”~user”转换成用户目录
os.path.expandvars(path) #根据环境变量的值替换path中包含的”$name”和”${name}”
os.path.sameopenfile(fp1, fp2) #判断fp1和fp2是否指向同一文件
os.path.samestat(stat1, stat2) #判断stat tuple stat1和stat2是否指向同一个文件
os.path.splitdrive(path) #一般用在windows下，返回驱动器名和路径组成的元组
os.path.walk(path, visit, arg) #遍历path，给每个path执行一个函数详细见手册
os.path.supports_unicode_filenames() #设置是否支持unicode路径名

```



### simplejson

```python
simplejson.dump(obj,fp,**kwargs)  #将python对象写到文件中以json格式
simplejson.dumps(obj, **kwargs)：#将python对象表示成字符串(JSON的格式)
simplejson.load(fp, **kwargs)：#从文件中(包含JSON结构)读取为python对象
simplejson.loads(s, **kwargs)：#从字符串中(包含JSON结构)读取为python对象
simplejson.JSONDecoder：#load/loads的时候调用，将JSON格式序列解码为python对象
simplejson.JSONEncoder：#dump/dumps的时候调用，将python对象编码为JSON格式序列
```



### importlib

```python
#importlib模块支持传入字符串来引入一个模块。
def main():
    print(__name__)

import importlib 
def dynamic_import(module):
 	return importlib.import_module(module)
 
 module_two = dynamic_import('bar')
 module_two()

```



### datatime  time转换

```python
import datetime
import time

# 日期时间字符串
st = "2017-11-23 16:10:10"
# 当前日期时间
dt = datetime.datetime.now()
# 当前时间戳
sp = time.time()

# 1.把datetime转成字符串
def datetime_toString(dt):
    print("1.把datetime转成字符串: ", dt.strftime("%Y-%m-%d %H:%M:%S"))


# 2.把字符串转成datetime
def string_toDatetime(st):
    print("2.把字符串转成datetime: ", datetime.datetime.strptime(st, "%Y-%m-%d %H:%M:%S"))


# 3.把字符串转成时间戳形式
def string_toTimestamp(st):
    print("3.把字符串转成时间戳形式:", time.mktime(time.strptime(st, "%Y-%m-%d %H:%M:%S")))


# 4.把时间戳转成字符串形式
def timestamp_toString(sp):
    print("4.把时间戳转成字符串形式: ", time.strftime("%Y-%m-%d %H:%M:%S", time.localtime(sp)))


# 5.把datetime类型转外时间戳形式
def datetime_toTimestamp(dt):
    print("5.把datetime类型转外时间戳形式:", time.mktime(dt.timetuple()))

```



# Elasticsearch_dsl

```python
#相关导入
import time
from elasticsearch import Elasticearch
from elasticsearch_dsl import Search
```

```python
#创建相关实例
es = Elasticsearch()

# using参数是指定Elasticsearch实例对象，index指定索引，可以缩小范围，index接受一个列表作为多个索引，且也可以用正则表示符合某种规则的索引都可以被索引，如index=["bank", "banner", "country"]又如index=["b*"]后者可以同时索引所有以b开头的索引，search中同样可以指定具体doc-type

s = Search(using=es, index="time_appid_placementid_country")
```

```python
# 添加索引，其中index和doc_type自己指定一个值即可，id可以指定，如果没有指定elasticsearch会随机分配，body即为索引的内容
dict_1 = {"any": "test", "timepstamp": "ddd"}
es.index(index="bank", doc_type="account", id="qwe", body=dict_1)
```

```python
# 通过id获取特定文档，各参数的意义同上
res = es.get(index="bank", doc_type="account", id=1)
```

```python
# 根据字段查询，可以多个查询条件叠加,hightlight可以指定高亮，但是我的没有出现高亮，对数据处理没啥用不去深究
# res_2 = s.query("match", gender="F").query("match", age="32").highlight("age").execute()
```

```python
# 用Q()对象查询多个对象，在多个字段中，fields是一个列表，可以存放多个field，query为所要查询的值，如果要查询多个值可以用空格隔开（似乎查询的时候Q对象只接受同种类型的数据，如果文本和数字混杂在一块就会报错，建立查询语句出错，有待考察，如query="Amber 11"就会失败，fields也是一样，另外query可以接受单个数字的查询，如果是多个同样会报相同的错误）
# Q()第一个参数是查询方法，具体用法及其他方法可以参考elasticsearch的官方文档
q = Q("multi_match", query="Amber Hattie", fields=["firstname"])
res_3 = s.query(q).execute()
```

