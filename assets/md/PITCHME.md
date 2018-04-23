## <center>晋级报告</center>

<br>

#### <center>姚前 python工程师</center>

---

### 自我介绍

- 网名 vimiix
- 太原科技大学-光信息科学-本科毕业
- 三年工作经验
- 技术社区活跃用户(V2EX/CSDN)
- Blog:  [https://vimiix.com](https://vimiix.com)
- Github:  [https://github.com/vimiix](https://github.com/vimiix)

---

### 在恩墨的成长

- 2017.9加入恩墨的开源团队 <!-- .element: class="fragment" -->
- 参与的项目： <!-- .element: class="fragment" -->
	- <font size="4">zCloud for MySQL</font>
	- <font size="4">Mozhe</font>
- 技术栈积累： <!-- .element: class="fragment" -->
	- <font size="4">web框架：Flask / Django</font>
	- <font size="4">模块化：blueprint / MTV</font>
	- <font size="4">组件化：Celery / Inception / SqlAdvisor / Swagger / Oauth</font>
	- <font size="4">数据库：MySQL / Redis</font>

---

### 晋升目标：T3

#### 报告内容：

- 岗位篇 <!-- .element: class="fragment" -->
- 技术篇 <!-- .element: class="fragment" -->
- 18年技术目标 <!-- .element: class="fragment" -->
- 职业规划 <!-- .element: class="fragment" -->

---

#### 岗位篇

![Image](./assets/md/assets/resp.jpg)

---

#### 技术篇

![Image](./assets/md/assets/skill.jpg)

---

#### 岗位篇·项目能力

- 能够参与需求讨论并梳理项目需求为TODO清单，并配合团队完成指定的后端开发任务； <!-- .element: class="fragment" -->
	- <font size="4">[[示例]TODO清单部分](http://note.youdao.com/noteshare?id=c26febca51aae9c1371db51c5dc68d46)</font>
-  擅长使用图形化思维梳理产品业务和模块逻辑； <!-- .element: class="fragment" -->
	- <font size="4">[[示例]zCloudForMysql架构个人梳理图](https://www.processon.com/view/link/5adc21e7e4b0518eacc74476) </font>
	- <font size="4">[[示例]SQL审核流程及系统任务调度图](https://www.processon.com/view/link/59e4676ee4b02fe828d14370)</font>
- 完成公司委派的zCloudForMysql项目的《软件说明书》及《软件著作权申请书》的撰写； <!-- .element: class="fragment" -->

---

#### 岗位篇·编码能力

<br>

- 编码方面，追求 PEP8 规范，能够实现指定的功能和接口说明； <!-- .element: class="fragment" -->

- 会有意识的编写项目的单元测试代码; <!-- .element: class="fragment" -->

<br>

---

<span class="menu-title" style="display: none">Python Block</span>

<p><span class="slide-title">Python后端接口举例</span></p>

```python
@require_http_methods(['GET',])
def userlist(request):
    """
    用户列表查询入口，主要实现参数校验
    :param request:  请求对象
    :return: json格式数据
    """
    params = {}
    params['username'] = request.GET.get('username', None)
    params['status'] = request.GET.get('status', None)
    params['user_role'] = request.GET.get('user_role', None)
    order = request.GET.get('order', 'id')
    params['order'] = order if order in ['id', 'username'] else 'id'
    start = str2num(request.GET.get('start', 0))
    params['start'] = start if start else 0
    limit = str2num(request.GET.get('limit', 30))
    params['limit'] = limit if limit else 30
    desc = request.GET.get('desc', 'True')
    desc = desc.lower() == 'true'
    params['desc'] = desc
    for k,v in params.items():
        if isinstance(v, str):
            params[k] = pymysql.escape_string(v)
    res = _userlist(**params)
    return json_response(status=200, result=res)
```

<span class="code-presenting-annotation fragment current-only" data-code-focus="1">指明接口的HTTP方法</span>
<span class="code-presenting-annotation fragment current-only" data-code-focus="2-7">添加接口说明注释</span>
<span class="code-presenting-annotation fragment current-only" data-code-focus="8-20">接口参数接收和校验处理等</span>

---

<span class="menu-title" style="display: none">Python Block</span>

<p><span class="slide-title">Python后端单元测试举例</span></p>

```python
#coding=utf-8

__author__ = "Vimiix"

import json
import unittest
import requests
from MozheAPI.settings import DATABASE, URL_PREFIX
from lib import MySQLInstance

class UserViewTest(unittest.TestCase):

    def setUp(self):
        with MySQLInstance(**DATABASE) as db:
            sql = "insert into user(`username`,`email`,`china_name`,`user_role`,`status`,`token`)" \
                  "VALUES ('unittest','example@mozhe.com','单测','dba',3,'ABC')"
            self.user_id = db.execute(sql)

    def tearDown(self):
        with MySQLInstance(**DATABASE) as db:
            sql = f"delete from user where id={self.user_id}"
            db.execute(sql)

    def test_user_list(self):
        r = requests.get(URL_PREFIX + '/user')
        self.assertEqual(r.status_code, 200)
        self.assertIn('unittest', r.text)
```

<span class="code-presenting-annotation fragment current-only" data-code-focus="5-9">相关依赖包的引入</span>
<span class="code-presenting-annotation fragment current-only" data-code-focus="13-17">单测前置工作，建立数据库链接，添加测试数据</span>
<span class="code-presenting-annotation fragment current-only" data-code-focus="19-22">单测后置工作，删除测试数据</span>
<span class="code-presenting-annotation fragment current-only" data-code-focus="24-27">单测功能代码，做相关断言操作</span>

---

#### 岗位篇·维护能力

<br>

- 能较好并及时地配合团队解决开发遇到的系统问题；（日常同步） <!-- .element: class="fragment" -->

- 遵守部门及公司的工作流程开展开发工作； <!-- .element: class="fragment" -->

<br>

---

#### 技术篇·项目经历

- zCloud - MySQL数据库自动化运维平台项目 <!-- .element: class="fragment" -->
	- <font size="4">我在此项目中主要负责平台的后台接口层功能开发以及第三方插件的集成。</font>
	- <font size="4">这个项目架构采用 `Flask 0.12`(后端web框架) + `MySQL`(元数据库) + `Swagger`(接口文档) + `Vue.js`(前端)。该系统实现了对于 `MySQL` 数据库的自动化监控及运维。</font>
	- <font size="4">项目中的SQL审核部分基于 `Inception` 并[填了一些坑](http://www.vimiix.com/post/2017/09/28/problems-when-pymysql-connect-inception/), SQL优化部分基于定制后的 `SQLAdvisor` 。</font>
- 成长 <!-- .element: class="fragment" -->
	- <font size="4">该项目强化了我在数据库和linux方面的技术，提高了我对于[Python](http://www.vimiix.com/category/Python/)和[Flask](http://www.vimiix.com/post/2017/12/18/some-useful-tricks-in-flask/)使用的熟练度。

---

#### 技术篇·项目经历

-  墨者-数据库自动化平台项  <!-- .element: class="fragment" -->
	- <font size="4">我在此项目中主要负责平台系统后端开发。</font>
	- <font size="4">该项目架构采用  `Django2.0`(后端web框架) + `MySQL`(元数据库) + `Swagger`(接口文档) + `Vue.js`(前端)。实现了对于 `Oracle` ,  `MySQL` 和 `Redis` 的实例运维管理，产品，用户，资源池等的监控和管理。</font>
	- <font size="4">该项目中，后台任务调度采用开源分布式队列 Celery配合Redis做消息管道。通过Channels 框架实现了前后端的Websocket通信 ,集成了JIRA系统。</font>
- 成长 <!-- .element: class="fragment" -->
	- <font size="4">在这个项目中遇到的最大的阻碍应该就是个人的技术栈瓶颈，比如前后端实时通信功能是以前没有写过的功能，经过不断的学习，试错，还有刘伟的细心指点，顺利的完成了这个功能。这个项目算是一次个人技术提升的最佳实践，扩大了技术视野。</font>

---

#### 技术篇·技术积累

- <font size="4">技术篇内容以代码片形式展示</font>

---

<p><span class="slide-title">开发语言高级特性装饰器和WEB开发</span></p>

```python
def login_required(func):
    """
    用于装饰需要鉴权的API
    """
    @wraps(func)
    def wrapper(request, *args, **kwargs):
        username= request.COOKIES.get('usernmae', None)
        access_token = request.COOKIES.get('access_token', None)
        if access_token and username:
            with MySQLInstance(**settings.DATABASE) as db:
                row = db.query(f"select token from user where username='{username}'")
                if len(row):
                    if row[0][0] == access_token:
                        return func(request, *args, **kwargs)
        return json_response(status=401, message="请登录后操作")
    return wrapper
```

<span class="code-presenting-annotation fragment current-only" data-code-focus="5-6,16">实现了装饰器的功能，对接口函数增加了认证功能</span>

---

<p><span class="slide-title">多线程编程</span></p>

```python
def startup():
    try:
        instances = get_instances(monitor_cnf.host)
        threads = [threading.Thread(target=instance.run) for instance in instances if len(instance.status) > 0]
        threads.extend([threading.Thread(target=instance.thread_queue) for instance in instances if len(instance.status) > 0])
        print 'init threads'
        [thread.start() for thread in threads]
        print 'start threads'
        for thread in threads:
            thread.join()
    except Exception, e:
        print "exit for %s" % str(e)
```

<span class="code-presenting-annotation fragment current-only" data-code-focus="2-12">对整个函数体做了异常捕捉处理，保证程序正常执行</span>
<span class="code-presenting-annotation fragment current-only" data-code-focus="3-10">实现多线程操作，并发启动多个thread任务</span>

---

<span class='menu-title slide-title'>Oauth</span>
```python
#!/usr/bin/python
#coding=utf-8

import requests
import django.contrib.auth.backends
from django.views import View
from lib import  MySQLInstance
from orm.user import User
from lib import json_response
from django.shortcuts import redirect
from functools import wraps
import logging

from django.conf import settings

logger = logging.getLogger(__name__)

CALL_BACK = '/'

class OAuth2Login(object):
    """
    OAuth2 登录
    """

    def __init__(self):
        self.redirect_uri = settings.OAUTH2_REDIRECT_URL
        self.client_id = settings.OAUTH2_CLIENT_ID
        self.client_secret = settings.OAUTH2_CLIENT_SECRET
        self.token_url = settings.OAUTH2_TOKEN_URL
        self.user_base_info_url = settings.OAUTH2_USER_BASE_INFO_URL
        self.user_all_permissions_url = settings.OAUTH2_USER_ALL_PERMISSIONS_URL

    def authenticate(self, authorization_code=None, **kwargs):
        if authorization_code is None:
            return None

        data = {
            "grant_type": "authorization_code",
            "code": authorization_code,
            "redirect_uri": self.redirect_uri,
            "client_id": self.client_id,
            "client_secret": self.client_secret,
        }
        # authorization_header_content = "{0}:{1}".format(self.client_id, self.client_secret)
        headers = {
            # "Authorization": "Basic {0}".format(base64.b64encode(authorization_header_content))
        }
        resp = requests.post(self.token_url, data=data, headers=headers)

        if str(resp.status_code) == "200":

            token_resp_dict = resp.json()

            access_token = token_resp_dict.get("access_token")
            token_type = token_resp_dict.get("token_type")
            logger.info("oauth2.0 D步骤执行完毕, access_token 为 {0}:{1}".format(token_type, access_token))

        else:
            logger.error("oauth2 登录失败, http status code: {0}".format(resp.status_code))
            logger.error(resp.text)
            # raise common.errors.OAuth2Error(
            #     "在oauth2 登录过程中, post token url返回结果不正常, http status code:{0}".format(resp.status_code))
            return None

        # 开始获取用户基础信息:
        user_base_info_dict = self.get_user_base_info(access_token=access_token)
        # get_user_all_permissions_dict = self.get_user_all_permissions(access_token=access_token)
        logger.info("oauth2 登录成功, 获取用户基础信息成功, user_base_info_dict:{0}".format(str(user_base_info_dict)))

        username = user_base_info_dict.get("name")
        user, created = self.get_or_create_user(username=username, token=access_token)
        user.email = user_base_info_dict.get("email")
        user.china_name = user_base_info_dict.get("name_cn")
        with MySQLInstance(settings.DATABASE) as db:
            User.updateUser(user, db)

        if created:
            logger.info("user:{0} 首次登录系统, 为其自动创建账户".format(username))
        else:
            logger.info("user:{0} 是已存在的用户".format(username))

        return user

    def get_user_base_info(self, access_token):
        """
        获取用户的基础信息
        :return:
        """
        oauth2_headers = {
            "Authorization": "Bearer {0}".format(access_token)
        }
        api_resp = requests.get(self.user_base_info_url, headers=oauth2_headers)
        return api_resp.json()

    def get_user_all_permissions(self, access_token):
        """
        用户所有权限信息
        :param access_token:
        :return:
        """
        oauth2_headers = {
            "Authorization": "Bearer {0}".format(access_token)
        }
        api_resp = requests.get(self.user_all_permissions_url, headers=oauth2_headers)
        return api_resp.json()

    def get_or_create_user(self, username, token):
        """
        在本系统的数据库中查找对应的用户, 找不到就创建一个
        :param username:
        :param token:
        :return: User
        """
        created = False
        with MySQLInstance(**settings.DATABASE) as db:
            query = f"select id from user where username={username}"
            rows = db.query(query)
            if len(rows) == 0:
                logger.debug(f"用户{username}未在本系统中注册, 为其自动新建一个用户")
                user = User.getUser()
                user.username = username
                user.token = token
                user.status = 0
                user.user_role = 'developer'
                user_id = User.addUser(user, db)
                created = True
            else:
                user_id = rows[0][0]
            user = User.getUser(user_id, db)
        return user, created


class LoginView(View):

    def get(self, request):
        global CALL_BACK
        CALL_BACK = request.GET.get('callback', '/')
        # TODO 完成认证服务器信息
        authorize_url = settings.OAUTH2_AUTHORIZE_URL
        client_id = settings.OAUTH2_CLIENT_ID
        redirect_uri = settings.OAUTH2_REDIRECT_URL
        return redirect(f"{authorize_url}?response_type=code"
                        f"&client_id={client_id}"
                        f"&redirect_uri={redirect_uri}")


class OauthView(View):

    def get(self, request):
        code = request.GET.get('code', None)
        if not code:
            # 确认授权服务器返回了 code 信息
            logging.error(f"授权失败，没有正常返回code信息")
            return json_response(status=500, message="授权失败")
        oauth = OAuth2Login()
        user = oauth.authenticate(authorization_code=code)
        resp = redirect(CALL_BACK)
        resp.set_cookie('username', user.username)
        resp.set_cookie('access_token', user.token)
        return  resp


def login_required(func):
    """
    用于装饰需要鉴权的API
    """
    @wraps(func)
    def wrapper(request, *args, **kwargs):
        username= request.COOKIES.get('usernmae', None)
        access_token = request.COOKIES.get('access_token', None)
        if access_token and username:
            with MySQLInstance(**settings.DATABASE) as db:
                row = db.query(f"select token from user where username='{username}'")
                if len(row):
                    if row[0][0] == access_token:
                        return func(request, *args, **kwargs)
        return json_response(status=401, message="请登录后操作")
    return wrapper


if __name__ == "__main__":
    pass

```


<span class="code-presenting-annotation fragment current-only" data-code-focus="25-31">初始化oauth授权码模式认证所需的几个变量</span>
<span class="code-presenting-annotation fragment current-only" data-code-focus="33">认证函数，指定授权码，提交认证服务器认证，并获取用户的信息</span>

---

<p><span class="slide-title">数据库操作</span></p>

```python
def get_service_list_with_dbtype(request, db_type):
    """
    获取创建任务时服务列表
    :param request:
    :param db_type:
    :return:
    """
    with MySQLInstance(**DATABASE, dict_result=True) as db:
        if db_type.lower() == 'mysql':
            query = "select s.name,s.service_name,i.id,i.vip,h.business_ip bip " \
                    "from service s,instance i,host h " \
                    "where s.id=i.service and i.host=h.id " \
                    "and s.db_type='mysql' and i.topology_role='master' "
        elif db_type.lower() == 'oracle':
            query = "select s.name,s.service_name,i.id,i.vip,h.business_ip bip " \
                    "from service s,instance i,host h " \
                    "where s.id=i.service and i.host=h.id " \
                    "and s.db_type='oracle' and i.topology_role='rac node' group by s.name"
        else:
            return json_response(status=400, message="数据库类型不存在")
        rows = db.query(query)
        res = []
        for row in rows:
            domain = get_ins_domain(row['vip'], db, row['bip'])
            res.append(
                {
                    'service_name': row['name'] + ':' + row['service_name'],
                    'instance_id': row['id'],
                    'domain': domain,
                    'ip': row['bip']
                }
            )
        return json_response(result=res)
```

<span class="code-presenting-annotation fragment current-only" data-code-focus="8">通过对pymysql的封装，实现了MySQLInstance数据库操作类</span>
<span class="code-presenting-annotation fragment current-only" data-code-focus="9-18">基本的SQL查询，表连接，分组，排序实现</span>

---

<p><span class="slide-title">Celery异步任务分发</span></p>

```python
app = Celery("MozheAPI")
app.config_from_object('celery_config')


@app.task
def async_assert_oracle_sql(task_id, batch_id, sql_text):
    """
    异步执行oracle sql审核任务
    :param sql_text:  文本
    :return:
    """
    ...


# 业务层发起异步任务
async_assert_oracle_sql.delay(task_id, batch_id, sql_text)
```

<span class="code-presenting-annotation fragment current-only" data-code-focus="1-2">初始化celery应用，加载配置文件</span>
<span class="code-presenting-annotation fragment current-only" data-code-focus="5-11">注册任务</span>
<span class="code-presenting-annotation fragment current-only" data-code-focus="15-16">业务层调用任务的delay方法发起异步任务，执行结果保存在配置文件中指定的CELERY_RESULT_BACKEND</span>

---

<p><span class="slide-title">Websocket消息推送</span></p>

```python
from channels.generic.websocket import AsyncWebsocketConsumer
from aredis import StrictRedis


class Consumer(AsyncWebsocketConsumer):

    async def connect(self):
        # Called on connection.
        # To accept the connection call:
        await self.accept()

    async def disconnect(self, code):
        # Called when a WebSocket connection is closed.
        pass

    async def receive(self, text_data=None, bytes_data=None):
        # Called with a decoded WebSocket frame.

        # ...

        # 订阅消息
        r = StrictRedis(**settings.REDIS_DB)
        ps = r.pubsub()
        await ps.subscribe(settings.REDIS_CHANNELS)
        
        # ...
            await self.send(text_data=json.dumps(result))
```

<span class="code-presenting-annotation fragment current-only" data-code-focus="1-2">引入Channels框架,采用支持协程的aredis来操作Redis数据库</span>
<span class="code-presenting-annotation fragment current-only" data-code-focus="7-10">当建立连接时触发该函数</span>
<span class="code-presenting-annotation fragment current-only" data-code-focus="12-14">当断开连接时触发该函数</span>
<span class="code-presenting-annotation fragment current-only" data-code-focus="16-17">当接收到信息时触发该函数</span>
<span class="code-presenting-annotation fragment current-only" data-code-focus="21-24">建立Redis直连，并异步订阅指定消息频道</span>
<span class="code-presenting-annotation fragment current-only" data-code-focus="27">当Redis消息频道中有消息产生时，即时发送回前端，实现后端主动推送消息</span>

---

### 18年技术目标

- 不满足于完成公司的开发任务，深入学习相关技术的原理 <!-- .element: class="fragment" -->
- 强化NoSQL数据库的学习(Redis / MongoDB) <!-- .element: class="fragment" -->
- 深入研究两个消息队列开源框架(rabbitmq / kafka) <!-- .element: class="fragment" -->

---

### 职业规划

<br>
<div class="left">
    <i class="fa fa-connectdevelop fa-5x" aria-hidden="true"> </i><br>
     <a href="https://vimiix.com/archive/" class="pro-link">
    更多的技术总结，请访问博客.</a>
</div>

<div class="right">
    <ul>
        <li>python研发工程师</li>
        <li>python高级工程师</li>
        <li>产品架构师</li>
        <li>Future.</li>
    </ul>
</div>

---
<!-- .slide: data-background-image="./assets/md/assets/bg.jpg" data-background-size="100% 100%" data-background-color=" " data-background-position="center" data-state="bg-img-opacity-100" -->


## <center>问答</center>

<br>

<center>[<i class="fa fa-at solid" aria-hidden="true">查看本文件源码</i>](https://github.com/vimiix/enmo-slides)</center>