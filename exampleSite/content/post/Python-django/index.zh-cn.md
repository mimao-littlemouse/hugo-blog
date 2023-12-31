---
# 帖子的发布作者
author: mimao
# 帖子的标题
title: 初识 Python Django
# 帖子的日期
date: 2023-07-07
# 帖子的描述
description: 初识Python Django并快速对其进行了解
# 帖子的标签
tags:
  - python-django
# 帖子分类
categories:
  - Python
---

# 初始django框架

## django简介

相比flask轻量级web框架，django内置了许多的模块 所以体型较大，称之为重量级web框架

### 目录结构
#### python安装后的安装目录结构介绍
```
Python39:
	--python.exe
	Scripts:
		--pip.exe
	Lib:
		--内置模块
		site-pakeages:
			--第三方模块

	
			安装完  django之后的目录结构介绍
				Python39:
	--python.exe
	Scripts:
		--pip.exe
		--django-admin.exe  (这个是一个工具，帮助咱们在创建项目的时候，自动创建项目结构)
	Lib:
		--内置模块
		site-pakeages:
			--第三方模块
			--django         (框架的源码存放处)

```

#### 安装方法：

使用 pip install django  安装即可

##### 项目创建的方法
	在存放django项目的文件夹中，打开cmd(cmd指终端)，
	输入  django-admin startproject 项目名称     即可创建成功

##### 项目结构介绍

```
存放项目的文件夹：
	项目名称命名的文件夹：
		--manage.py   ( 项目的管理 )

		项目名称命名的文件夹：
			-- __init__.py  
			-- asgi.py   		（接收网络请求  异步） 
			-- settings.py		（项目配置文件）
			-- urls.py		（书写 url与函数的关系）
			-- wsgi.py   		（接收网络请求  同步）

				django_demo：
	mysite：
		--manage.py  
 
		mysite：
			-- __init__.py
			-- asgi.py
			-- settings.py
			-- urls.py
			-- wsgi.py

			manage.py比较常用，但很少修改   asgi.py wsgi.py 这几个文件很少用   settings.py  urls.py常常用 和 修改
		项目中生成app
			(即 这里的app 可以理解为一个功能模块)
			创建app
				在项目文件夹中，打开cmd,运行manage.py文件 并带上相应的参数
				即：  输入    py manage.py startapp app的名称    即可
			app的文档结构
				app名称：
	migrations:					（固定的 不用管   （可称之为数据库变更记录））
		-- __init__.py
	-- __init__.py					
	-- admin.py					（django默认提供的admin后台管理  一般调试数据的时候用用）
	-- apps.py					（可 理解为 app的入口类）
	-- models.py					（对数据库进行操作的 django中有模块进行了内部封装 称为orm ）
	-- tests.py					（单元测试用的）
	--views.py					（视图  ）
		
```


##### 运行 django项目

```
1.首先 确保 app已经注册
在  settings.py中的 installed_apps中写上 ， 
'app名称.apps.app名称Config'    这样完成即可
			
2.其次，编写好  url 与 视图函数之间的关系
在 urls.py 中编写,按照 原有的样式 编写自己的 url   即可

即：先导入 from django_demo import views   
然后  urlpatterns的列表中书写  path('index/',views.index)

3.然后，在 views.py 中编写 视图函数
虽然在urls.py中编写好了 对应的url与视图函数的关系，
但该视图函数还未在 views.py中进行实现，
所以，需要根据原有的 例子，进行编写即可

即：然后

from django.shortcuts import render,HttpResponse   #HttpResponse是要加上去的

# Create your views here.
#然后，在下面书写视图函数，该视图函数 必须带一个request的参数
def index(request):
    return HttpResponse('hello world!')

			4.然后，在 项目目录文件夹路径中，打开cmd,输入  python manage.py runserver  即可
	django项目
		templates目录介绍
			在views中书写视图函数时，如需返回一个页面，一般处理是，直接返回一个 render(request,'html文件名.html')   
			而这个 html文件 的寻找方式 有两种：
			第一种，是直接在app中创建一个 templates文件夹，render在寻找模板的方式上，如果没有在settings中配置的templates配置项添加 os.path.join(BASE_DIR,templates)  则寻找模板方式是，在 app注册中一个一个的去寻找对应app文件夹中的templates中，是否存在这样一个html模板文件    第二种，如果添加了那个配置项，则会先去 根目录的templates中寻找，如果根目录没有，才会去 对应的app中去寻找


第一种，是项目默认寻找templates模板的方式，第二种是手动配置之后的寻找方式
			注意：我觉得，用第二种在一个项目多套系统中，可以起到 公共模块封装到根目录  私有模块封装到私有的templates中的 减少项目体积的作用
		url介绍
			"""django_demo URL Configuration

The `urlpatterns` list routes URLs to views. For more information please see:
    https://docs.djangoproject.com/en/4.1/topics/http/urls/
Examples:
Function views
    1. Add an import:  from my_app import views
    2. Add a URL to urlpatterns:  path('', views.home, name='home')
Class-based views
    1. Add an import:  from other_app.views import Home
    2. Add a URL to urlpatterns:  path('', Home.as_view(), name='home')
Including another URLconf
    1. Import the include() function: from django.urls import include, path
    2. Add a URL to urlpatterns:  path('blog/', include('blog.urls'))
"""
		在模板中引入静态文件
			配置静态文件夹
				STATIC_URL = 'static/'
STATICFILES_DIRS = [
    os.path.join(BASE_DIR, "static")
]
				并且 static文件夹需放置在 项目根目录
			第一种：  之前在html中如何引入，就如何引入
			第二种：动态引入静态文件
				在html的顶部，添加 {% load static %}    然后，在引入的路径中，将路径替换为 {% static 'static后的路径，不用再写static，写static之后的路径即可' %}
				例如：  <link src="{% static '路径' %}"/>
		模板语法
			在html中使用
				插值模板语法
					通过 render的第三个参数，传一个字典数据 到html模板中，在html模板中使用 {{字典中的key变量}}  接收就行
						例如：

render(request,'index.html',{'name':'名字'})

index.html中：

{{name}}

会显示为：

名字
				其他模板语法
					{% for    in  %}
html内容
{% endfor %}
						{% if 条件 %}
html内容
{% endif %}
							{% if 条件 %}
html内容
{% else %}
html内容
{% endif %}
								{% if 条件 %}
html内容
{% elif 条件 %}
html内容
{% else %}
html内容
{% endif %}
					列表 和  字典都可循环
						注意：字典的.keys不需要加括号  .values也不需要
					获取 列表中的元素 获取字典中的元素都是用.的方式获取
						例如： list=[1,2]

print(list.0)   --> 1

dict={'nhao':'你好'}

print(dict.nhao)  --> 你好
				在 模板语法中，
					注意：不能使用 () 和 %
						内部会自动读  如果你需要加 (),他会自己加

但 ()有参数，这是，这样的使用，在模板语法中，是不允许的

					在django模板语法中，只能使用 . 进行取值
					或使用 过滤器
						|过滤器:参数 参数 ...
		请求和响应
			接收 用户请求
				request.method
					获取请求的方式
				request.GET
					获取用户提交的url数据
				request.POST
					获取用户提交的表单数据
				.get()方法获取 数据
					例如：request.GET.get('nid')

也可以设置默认值:
request.GET.get('nid','')
			响应用户
				返回 字符串
					HttpResponse('')
				返回 页面
					render(request,'')
				返回 重定向
					redirect('地址')
						重定向是 直接将重定向返回给浏览器，让浏览器自己去找
			像别的服务器发起请求
				安装好第三方模块  requests
					requests.get()


requests.post()
			用正则表达式匹配的功能，来对url进行处理
				在 urls中的url地址中书写  <int:nid>
例如： path('/depart/<int:nid>/list/',views.depart_list)

在 views中：

可以： def depart_list(request,nid):   #可以用 nid进行接收
		print(nid)
		在django项目中自带了一个 csrf_token权限验证机制
			解决因多了这个机制而报 403错误的方法是：
				在 html中的form表单中，添加 {% csrf_token %}即可 
例如：html中, 
<form method="post" action="/index/">
{% csrf_token %}
<input type="text"/>
<input type="submit" value="提交"/>
<form>
		数据库模块
			常见的数据库第三方模块
				pymysql
				mysql
				mysqlclient
					这个是python3之后的，前两个版本中，最新的，也是最好用的
				注意：一般 用mysqlclient
					安装：  pip install mysqlclient
				cmd中如何使用mysql
					输入
						mysql -u root -p 打开mysql登录界面，输入密码进入mysql
						查看数据库
							show databases;
						使用数据库
							use testdb;
						查看数据库中的所有的表
							show tables;
						查看表中的数据，或者操作表
							和sql一样
						注意：在mysql中，所有命令以 ; 结束

如果不打 ;  号 代表你还未输入完，mysql就不会执行，只有 打了 ; 号，敲一下回车，才会执行你输入的命令
			django中有内置的ORM框架
				ORM框架介绍
					可以创建、修改、删除 表
还可以对表中的数据进行操作
但无法创建数据库
					用 cmd查看mmysql数据库中的数据库
						mysql -u root -p

然后输入密码

然后输入 show databases;

即可查看
					配置数据库 配置项
						在 django中的settings.py的配置文件中，配置databases配置项，在 配置项中添加：(例如  如下：)

DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',				#数据库引擎
        'NAME': '',    							#数据库名字
        'USER':'root',							#数据库用户名
        'PASSWORD':'admin123',						#数据库用户密码
        'HOST':'127.0.0.1',						#数据库所在服务器的ip，在本地就可以 直接写 127.0.0.1  或 localhost
        'PORT':'3306'							#数据库端口号
    }
}
					使用ORM框架
						操作表结构
							创建表
								在 app目录下，创建 models.py文件，在文件中书写 数据库表的一个类

然后，在项目根目录下，打开cmd 或 在控制台中：
 
输入  python manage.py makemigrations   #创建迁移

然后，再输入 python manage.py migrate    #迁移

即可 完成该数据库的表的创建
									在models.py中书写 表类的例子：

from django.db import models

class UserInfo(models.Model):
	name=models.CharField(verbose_name='用户名',max_length=32)
	password=models.CharField(verbose_name='密码',max_length=64)
	age=models.IntegerField(verbose_name='年龄')


#verbose_name 可以看作是备注
	
									创建字段的类型的方法有：
										.CharField()

.SmallIntegerField()
.IntegerField()
.BigIntegerField()

.DecimalField()    max_digits 最大长度   decimal_places 小数点占位个数

.DateTimeField()   #含有 年月日 时分秒
.DateField()       #只含有  年月日
										对该字段创建外键约束：
											UserInfo  与  DepartmentInfo    UserInfo表中 含有DepartmentInfo中的Id，此时 UserInfo表中的部门ID要参照DepartmentInfo中的ID
此时，在UserInfo表中 对depart_id字段建立外键约束
所以：

depart=models.ForeignKey(to='DepartmentInfo',to_field='id',on_delete=models.CASCADE)   设置参照DepartmentInfo表中的id字段对该字段进行外键约束

其中：
on_delete=models.CASCADE  是对其外键设置级联（即：当DepartmentInfo中对应的id值所在一整行数据要被删除时，UserInfo表中有着对应关系的depart字段的值的这一行数据，将会一同被删除）


on_delete=models.SET_NULL,null=True,blank=True  是对其外键设置为  置空（即：当DepartmentInfo中对应的id值所在一整行数据要被删除时，UserInfo表中有着对应关系的depart字段的值的这一行数据，将会一同设置为空(null)）
											在使用 ForeignKey()方法绑定的字段，该字段， 会有两种调用方法：

注意：该字段不要加_id  因为在创建该表字段的时候，会自己加上一个 id

使用该字段的时候， 字段_id  可以获取到存储到数据库中的对应的id值

字段  可以获取到一个 对象，该对象就是 约束该字段的那张表的对象，对此 你可以获取到对应的id相等的那行数据
										对字段创建 值约束（可以理解为 选择约束（由 django自带的约束））
											比如：

gender_choices=(
	(1,'男'),
	(2,'女')
)

gender=models.SmallIntegerField(verbose_name='性别',choices=gender_choices)

代码中 choices=gender_choices 便是值约束
							删除表
								如果 想删除其中一个表
									只需在 models.py文件中，将 对应的class进行注释即可
										然后执行迁移命令即可
							修改表
								删除列
									将models.py中对应的类中的字段进行注释即可
										然后执行迁移命令即可
								新增列
									两个选择
										第一种：
											直接在 models.py中对应的类中，新增字段，并对其字段进行默认值声明（即：  age=models.Integer(default=默认值)）  然后，再执行迁移命令

除了使用 default设置默认值，还可以设置为空（ null=True,blank=True ）
										第二种：
											直接 执行迁移命令，再输入迁移命令之后，控制台会有提示 让你对新增字段输入一个默认值
									之所以 有两个选择，并相较于删除列比较复杂，是因为此时修改表并进行新增列，会导致之前有数据的列对应的新增列没有默认值或设置值的时候而出现问题
						操作表数据
							首先，导入 app中的models.py文件 中的表类
from app.models from UserInfo


							新增数据
								UserInfo.objects.create(name='',password='')

							刷选数据
								UserInfo.objects.filter(id=1)

UserInfo.objects.all()
									.filter(条件)
.all()
										获取到的数据是一个 QuerySet类型的数据，可以看作一个列表，列表中每个数据都是一个对象，对象中封装了对应的字段，可以通过这些字段来获取对应的数据
									.first()   获取满足条件的第一行数据
										得到的数据是一个对象
								.filter(条件)

filter中的条件，有两种书写方式：

第一种，直接写  .filter(id=1)

第二种，用字典   filter_dict={'id':1,'name':'小王'}
.filter(**filter_dict)

filter_dict={'id__gte':1,'name__contains':'小王'}
.filter(**filter_dict)
									而且，对于条件中的等于 大于 啥的，有以下 实例：

对于 数字类型数据：
id=1		等于1
id__gt=1    	大于1
id__gte=1	大于等于1
id__lt=1    	小于1
id__lte=1	小于等于1

对于字符串类型数据：
name__startswith=‘小’		以什么开头
name__endswith='王'        	以什么结尾
name__contains='小'		包含
							删除数据
								根据刷选出来的数据，进行删除
									UserInfo.objects.filter(id=1).delete()

UserInfo.objects.all().delete()
							更新数据
								根据刷选出来的数据，进行更新
									UserInfo.objects.filter(id=1).update(name='',age=0)

UserInfo.objects.all().update(name='',age=0)
							对数据进行排序
								order_by('id')  对id进行正序排列 
								order_by('-id')  对id进行倒序排列 
							判断数据是否存在，返回 true或false
								.exists()

在 刷选数据的方法后面.一下
							判断刷选 排除所写条件之外的数据  .exclude()
							对返回数据的选择
								单独使用 all filter  方法，返回的是 一个queryset类型的列表数据 并且每一个元素是对象
								1. 结合 first()  返回的可以是 对象
								2. 结合 values('name','password',....) 可以选择返回的字段，并返回的数据类型是 字典类型

3. 如果 结合的是 values_list('name','password',....) 也可以选择返回的字段，并且返回的数据类型虽然是列表类型，但是元素是字典类型
		模板的继承
			模板
				{% block 模板名字 %}{% endblock %}
				母版
					只需在母版中书写   {% block content %} {% endblock %}
				继承母版
					该html文件，只需写上 {% extends '路径 + 母版文件.扩展名（如果在同一目录下，则不需要路径）' %}

和  

{% block content %}
自身对应的内容即可
{% endblock %}
		python中数据类型的转换
			str  -->    datetime
				str_text.strptime('%Y-%m-%d')
			datetime -->  str
				dt.strftime('%Y-%m-%d-%H-%M')
			choices
				django中，对于 choices存储的数据：比如

gender_choices = (
	(1,'男'),
	(2,'女')
)

UserInfo.objects.create(gender=choices(gender_choices))

UserInfo.objects.filter(id=1).first().gender   -->   1

UserInfo.objects.filter(id=1).first().get_gender_display()   -->   男
		表单
			简介
				django中表单实现校验和布局的书写，原始的方法进行书写，或使用Form 或 ModelForm
			表单组件
				减少 原始代码的书写，原始代码的书写会导致代码急速上升，而使用ModelForm书写，则可以减少代码书写，主要用户对表数据的增加
				Form
					这个用的也比较少
						可以用于登录
				ModelForm
					简化 input的书写
						直接 声明一个类继承 forms.Form
例如：
from django import forms
from django.core.validators import RegexValidator   #引入正则表达式
class StarfInfoFormModel(forms.ModelForm):
	id = froms.CharField(disabled=True)      #加一个disabled=True是为了，它能显示，但不可编辑
	mobile = forms.CharField(label='手机号',validators=[RegexValidator(r'^1[3-9]\d{9}$')])	   #自定义验证规则

	class Meta:
		model = models.StarfInfo
		#fields='__all__'    					这个是代表取类中所有字段
		fields=['name','gender','age']				这个是代表取 fields列表中列出的字段
		#exclude=['level']					这个是指 exclude中列出的字段，进行排除，该字段不进行自动添加input的处理
	def __init__(self,*args,**kwargs):
		super().__init__(*args,kwargs)
		for name,field in self.fields.items():
			field.widget.attrs = { 'placeholder':field.label }   #为所有输入框添加placeholder属性

					表单校验
						在上面的基础上
						先取消 form表单原有的校验
							<form novalidate><form>   在form标签中，加入 novalidate即可
						按上面那样书写
							会进行 非空校验，如果需要其他校验，则 需自己在 Meta类上面添加对应表单字段的验证规则：例如：

class StarfInfoModel(forms.ModelForm):
	name = forms.CharField(min_length=2,.....)     #像这样，加入自己想再次校验的字段，并添加对应的校验规则
	class Meta:
		.......
						如果，不习惯英文的错误提示
							在 settings.py 中的 LANGUAGE_CODE配置项中，将 en-us  改为：  zh-hans
这样 就把英文 改为了 中文的错误提示
						判断是否校验成功，则只需
							form = StarfInfoFormModel(request.POST)
if form.is_vaild():
	form.save()
form.errors
						第一个，里面的代码介绍了 使用正则表达式进行校验的方式
						下面，介绍 使用钩子函数对其字段进行单独校验
							在 StarfInfoFormModel类中，

书写 :

def clean_mobile(self):
	mobile_id = self.instance.pk               可以通过self.instance.pk来获取字段所在的这张表的id
	txt_mobile = self.cleaned_data['mobile']
	if len(txt_mobile)!=11:
		raise ValidationError('格式错误')
	return txt_mobile
					初始化表单中组件的值
						只需：
							form = StarfInfoModelForm(instance=form_obj_data)

只需 添加instance ，然后 将数据库中获取的对象数据的形式的数据传给instance即可
					保存用户提交的数据
						用于 增加
							form = StarfInfoModelForm(data=request.POST)
if form.is_vaild():
	form.save()
						用于编辑
							form = StarfInfoModelForm(data=request.POST,instance=starf_obj_data)
if form.is_vaild():
	form.save()

在原有data的情况下 添加一个 instance        则是指 ，在 instance的数据下，保存data中改动的数据
					保存到数据库中的数据，想不仅仅是用户输入的
						直接：
							form.instance.字段名= 值
		django中 巧妙的用法
			切片
				可以使用列表的切片功能 实现分页的功能
			将views视图函数中返回给html的字符串  输出显示为 html 
				将 该字符串标记为  安全字符串进行输出即可
					例如：

from django.utils.safestring import make_safe

make_safe('字符串')    这就将字符串转化为了 安全字符串
			复制一份get请求，再为get请求的参数 添加其他新的参数
				在原有的get方式的url请求参数后，添加 其他参数    即：http://localhost:8080/list/?id=1&btn=2   
变成 http://localhost:8080/list/?id=1&btn=2&page=12

则可以通过 ：

import copy

query_dict=copy.deepcopy(request.GET)          #request.GET 是返回的get请求中所带的参数 		是QueryDict类型的值
query_dict._mutable=Ture  			#通过设置 _mutable=Ture 进而来设置QueryDict类型数据可用setlist()更改即可
query_dict.setlist('page',[12])		#设置为 可改之后，通过设置 setlist('page',[12])  即可实现
			将QueryDict转换为 url形式	使用.urlencode()
			分页的一些思维
				使用面向对象的思维，创建一个 自定义的组件
				然后，为了确保 在搜索的时候，保留之前的分页数据
		ajax 的使用
			简介
				ajax的使用，依赖jquery
				ajax请求
					例如：

$.ajax({
	url:'/admin/login',
	type:'post',
	data:{
		username:'admin123',
		password:'3eikeidkeee44e74e74e7'
	},
	datatype:'json',
	success:function(res)=>{
		console.log(res)
	}
})
				在 django中使用 ajax进行post请求时，因添加csrf验证比较麻烦
					因此，可以使用@csrf_exempt标注在视图方法中即可，表示该视图函数不进行csrf校验

导入： from django.views.decorators.csrf import csrf_exempt
			ajax中经常使用的方法
				$.each()
					data= { 'name':'小iu','age':12}

$.each(data,(key,value)=>{
	console.log(f'key:{key};value:{value}')
})

遍历字典类型数据
				$.ajax
				$(function()=>{
	
})
				$('')
					.attr()
						value = $('#nid').attr('id_text')
					.click(()=>{

})
		echarts的使用方法
		文件上传
			使用form表单提交文件
				例如：
html中：
<form method='post' enctype="multipart/form-data">
	{% csrf_token %}
    <input type="file" name='avator'/>
</form>

视图函数中，使用 request.files.get('avator')进行接收即可

如果需要保存该内容，可以这样：
avator_file = request.files.get('avator')
with open(avator_file.name,mode='wb') as f:
	for chunk in avator_file.chunks():
		f.write(chunk)

		读取excel
			安装依赖
				pip install openpyxl
			使用 load_workbook模块读取
				导入
					导入load_workbook 即：  from openpyxl import load_workbook
				使用load_workbook()方法
load_workbook(文件路径或文件对象) 可以获取一个工作簿对象
					然后，可以通过工作簿对象获取 工作表，然后通过cell方法获取数据
					即：

wb = load_workbook(文件对象)

sheet = wb.worksheets[0]   获取工作簿中的第一个工作表
cell = sheet.cell(1,1)     获取工作表中第一行第一列的数据
				方法
					sheet方法
						.rows()    从第一行开始获取，获取所有数据
						.iter_rows()    也是获取所有行的数据，但可以使用min_row来设置起始行，即设置最小行数是从第几行开始

.iter_rows(min_row=2) 这个设置代表最小从第二行开始获取所有行的数据
						row[列索引].value
							获取每行中对应列数的值
								无论是.rows 还是 .iter_rows  都可以用for 遍历

例如：

for row in sheet.iter_rows(min_row=2):
	row_col_value = row[0].value   			这样就获取到了 每行第一列的值了
		django中较为特殊的两个文件夹
			static文件夹
				配置静态文件夹
					STATIC_URL = 'static/'
STATICFILES_DIRS = [
    os.path.join(BASE_DIR, "static")
]
					并且 static文件夹需放置在 项目根目录
			media文件夹
				使用之前还需配置
					配置
						urls.py中：
from django.urls import re_path
from django.views.static import serve
from django.conf import settings

urlpatterns=[
	re_path(r'^media/(?P<path>.*)$',serve,{'document_root':settings.MEDIA_ROOT,name='media'})
]


settings中：

添加两行：
先导入os

import os
MEDIA_ROOT = os.path.join(BASE_DIR,'media')     指media的根路径
MEDIA_URL = '/media/'
					使用
						配合 modelform使用
							在model中，

将文件字段
avator = FileField(verbose_name='',,upload_to='地址或目录（指media目录下面的目录名称或（例如：/vedio））')  

然后，在 forms(data=request.POST,files=request.Files) 
						也可以使用form 进行
							手动保存（）这就是与 modelform的区别，一个有model 一个没有model


***

## 初创 django 项目


创建django项目：
1.首先，决定好项目名称
在存放项目的文件夹中，打开cmd,输入：django-admin startproject 项目名称
2.创建好基本目录之后，该目录只是用作url以及项目配置的，真正用于开发的，是创建app进行页面和路由的开发
3.创建app,将目录切入到含有manage.py的文件夹中，打开cmd输入: python manage.py startapp 项目名称_web也行(自己定义)
4.对 app进行注册，在settings.py中的install_app配置项中，添加：app名称.apps.app名称所有单词大写Config  即可
5.并在settings.py中配置好static文件夹，找到static_url选项，在其下面书写：STATICFILES_DIRS=[os.path.join(BASE_DIR,'static')] 
注意：os模块需自己在文件内容顶部(导入path的下面)导入
6.在项目根目录(即：含有manage.py文件的文件夹中)，创建static文件夹，并搭建好： css js img plugins的目录结构
7.然后，在app目录下，创建templates文件夹，并创建 app名称 app名称_layout 两个文件夹
（注意：在views中render templates中的html文件的时候，带上app名称 app名称_layout 或其他app中的app名称 app名称_layout 
（这样可以避免 render的时候使用同一个html文件）） 这是一个重点
8.之后，便可以在根目录下，打开cmd，输入 python manage.py migrate 实现迁移去使用sqlite数据
（默认使用sqlite数据库，如需使用其他数据库，可以在settings.py中配置(例如：mysql数据库，配置项有：engine name user password host port)）
9.之后，就是修改urls.py views.py 增加html文件，书写views中的逻辑代码，并在根目录中，打开cmd,输入 python manage.py runserver [port] 运行项目了（[port可填，可不填，不填默认端口号 8000]）

使用bootstrap中的 字体图标库
1.下载图标库中的源码，将源码中的svg图标拷贝一份，在html中，使用img进行引入即可（在django中有用）
或者
2.将其源码中的font拷贝一份，在html中，使用 <i class="bi bi-svg图标名称"></i>（在django中没用）

组件的灵活使用，以及模板的灵活使用，将大大提高开发效率，减少代码冗余
注意：html模板名称：可以写成 (  templates目录下文件夹名称或不写 )/模板名称.html 例如：项目名称_layout/模板名称.html 或 模板名称.html
1.导入( include )
{% include "html模板名称" %}
2.继承(extends)与占位(block)
在母模板中：{% block 占位名称 %}{% endblock %}
在子模版中：{% extends 'html模板名称' %}  {% block 占位名称 %}占位内容{% endblock %}
（其实可以一致套下去，但不建议这样做，套两三个就可以了，以免出现辨别困难，增加开发难度）

***

## django 中各个模块介绍
### request 请求模块 请求示例

获取django中获取url有如下三种方法：

获取带参数URL：request.get_all_path()

获取不带参数URL：request.path

获取主机地址：request.get_host()

### template 模板模块

模板语法如下：
```
{{变量名}}
{% %}
```

### models 数据模块

#### django中的models.py介绍

1.使用 
python manage.py makemigrations
python manage.py migrate
将写好的models.py中的表结构，在配置好的数据库中生成对应的表结构

2.生成models.py文件，利用已经存在的数据库生成
配置好数据库的配置项，然后，输入：
#(1). 如果已经执行过 python manage.py startapp app名称 命令生成应用,直接写
python manage.py  inspectdb > app名称/models.py 
#(2). 如果没有执行过 python manage.py startapp app名称 命令生成应用，可以直接将生成的models内容输出为 models.py文件
python manage.py  inspectdb > models.py 

3.models.py中，书写规范：
from django.db import models

class UserInfo(models.Model):
	name=models.CharField(verbose_name='用户名',max_length=32)
	password=models.CharField(verbose_name='密码',max_length=64)
	age=models.IntegerField(verbose_name='年龄')

4.讲解
(1).verbose_name 可以看作是备注
(2).创建字段的类型的方法有：
字符字段（可以用：max_length来明确字符长度，其实，这可以当作 string字符串类型）
.CharField()
短整形字段
.SmallIntegerField()
整形字段
.IntegerField()
长整形字段
.BigIntegerField()
小数字段
.DecimalField()    max_digits 最大长度   decimal_places 小数点占位个数
时间字段
.DateTimeField()   #含有 年月日 时分秒
日期字段
.DateField()       #只含有  年月日
(3).对该字段创建外键约束：
UserInfo  与  DepartmentInfo    UserInfo表中 含有DepartmentInfo中的Id，此时 UserInfo表中的部门ID要参照DepartmentInfo中的ID
此时，在UserInfo表中 对depart_id字段建立外键约束
所以：
depart=models.ForeignKey(to='DepartmentInfo',to_field='id',on_delete=models.CASCADE)   设置参照DepartmentInfo表中的id字段对该字段进行外键约束
其中：
on_delete=models.CASCADE  是对其外键设置级联（即：当DepartmentInfo中对应的id值所在一整行数据要被删除时，UserInfo表中有着对应关系的depart字段的值的这一行数据，将会一同被删除）
on_delete=models.SET_NULL,null=True,blank=True  是对其外键设置为  置空（即：当DepartmentInfo中对应的id值所在一整行数据要被删除时，UserInfo表中有着对应关系的depart字段的值的这一行数据，将会一同设置为空(null)）
在使用 ForeignKey()方法绑定的字段，该字段， 
会有两种调用方法：
注意：该字段不要加_id  因为在创建该表字段的时候，会自己加上一个 id
使用该字段的时候:
第一种，调用方法：字段_id  可以获取到存储到数据库中的对应的id值
第二种，调用方法：字段  可以获取到一个 对象，该对象就是 约束该字段的那张表的对象，对此 你可以获取到对应的id相等的那行数据

(4).对字段创建 值约束（可以理解为 选择约束（由 django自带的约束））
比如：
gender_choices=(
	(1,'男'),
	(2,'女')
)

gender=models.SmallIntegerField(verbose_name='性别',choices=gender_choices)
代码中 choices=gender_choices 便是值约束
注意：在使用models.py模块访问到数据之后，
第一种，可以通过 get_gender_display() 方法 获取该字段gender的值 1对应的"男"  
第二种，通过字段gender可以获取 1


### admin 模块
#### admin.py文件介绍
```
from django.contrib import admin

# Register your models here.
# 1.从django的contrib版本中调用admin包,该包 包含admin等自动化站点管理工具
# 需要在admin后台中显示哪些数据, 则相应从models中导入对应模型类用以调用数据
# from app名称.models import model中表的类名

# 2.
# class 表类名Admin(admin.ModelAdmin):
    # '''表对应的类模型admin管理类'''
    # 3.
    # 指定每页显示多少条信息
    # list_per_page = 10  
    # 4.
    # list_display中不仅可以写模型类的属性(即 表的列名), 也可以写模型类的方法
    # list_display = ['','',...]
    # 5.
    # 指定下拉列表框的位置以及存在与否
    # actions_on_top = False  # 上面的下拉列表开关设置
    # actions_on_bottom = True  # 下面的下拉列表开关设置
    # 6.
    # list_filter = ['属性名']  # 列表过滤栏设置指定过滤的['属性']
    # search_fields = True      # 搜索框的开关设置
    # search_fields = ['属性名']  # 搜索栏设置指定搜索属性['属性']
    # 7.
    # fields = ['属性名','属性名',...]  # fields 修改每个objects在admin中属性的排列顺序

    # fieldsets 设置组, 在组内放入属性分类
    # fieldsets = (  
    #     ('基本或其他名称',{'fields':['属性名']}),
    #     ('高级或其他名称',{'fields':['属性名']})
    # )

    # 注意： fields 和 fieldsets 两个通常情况下只选择一个使用

    # 8.
    # 嵌套或者叫关联子对象和父对象
    # (1). 创建嵌套对象, 声明嵌套类型(块嵌套或表格嵌套)以及额外编辑数量:(以块嵌套为例)
    # class 自定义关联类名StackedInline(admin.StackedInline):
    #       model = 类名  # 关联的子对象
    #       extra = 2  # 额外编辑2个子对象

    # (2).使用方法 
    # 在需要进行关联的'表类名Admin'类后加上 inline = [上方定义的关联类] :
    # inline = [自定义关联类名StackedInline]


# 自定义admin自动化管理工具, 要改写admin中的ModelAdmin(模型_管理)的参数
# 9.修改列表显示, 则更改list_display中的列表内容
# class 类名Admin(admin.ModelAdmin):
#     list_display = ['列名', '列名',...]

# 用admin包内的site站点模块, 使用register注册方法, 注册从模型中导入的模型类(单个)
# admin.site.register(类名,类名Admin)
```


### tests 模块

#### tests.py文件介绍

测试的格式，大致是：
```
# # Create your tests here.
# 1.导入相关模块
# from django.test import TestCase, Client
# from .models import Student
# 2.创建一个 类名TestCase的类，继承TestCase 并在类中书写setup 和 以test开头的方法的需要测试的方法 在最好虽然可以写tearDown方法，但不需要这样，因为django会帮咱们做
# class StudentTestCase(TestCase):
#     """
#     3.在student类中，首先书写 setup进行初始化 进行测试的准备工作
#     def setUp(self)：用来初始化环境，包括创建初始数据，或做一些其他准备工作
#     setUp的功能，可以对 模型student表进行添加数据，添加的数据会放到一个临时的数据库中，前提是 settings中的数据库已配置好
#     4.书写 需要进行测试的方法 可以通过 self.assertEqual(变量, 值, 提示内容) 或 self.assertTrue(bool值,需要print打印出来的信息)  进行断言
#     如果需要测试请求是否有问题，则可以通过client = Client() response = client.get('/') 或 response = client.post('/',data)
#     def test_xxx(self)：xxx可以是任何东西，以test_开头的方法，都会被django认为是需要测试的方法，跑测试时会被执行
#     注：每个需要被测试的方法都是相互独立的
#     def tearDown(self)：跟setUp相对，用来清理测试环境和测试数据（在django中可以不关心这个）
#     """
#     5.例如：
#     def setUp(self):
#         print('setUp')

#     # 需要进行测试的方法
#     def test_xxx(self):
#         print('test_xxx')
#         self.assertEqual(变量, 值, 需要print打印出来的信息)
```

```
案例：
from django.test import TestCase, Client
from .models import Student


class StudentTestCase(TestCase):
    """
    def setUp(self)：用来初始化环境，包括创建初始数据，或做一些其他准备工作
    def test_xxx(self)：xxx可以是任何东西，以test_开头的方法，都会被django认为是需要测试的方法，跑测试时会被执行。
        注：每个需要被测试的方法都是相互独立的
    def tearDown(self)：跟setUp相对，用来清理测试环境和测试数据（在django中可以不关心这个）
    """
    def setUp(self):
        print('setUp')
        Student.objects.create(
            name='stu1',
            sex=1,
            email='test1@qq.com',
            qq='333',
            phone='111',
        )

    # 测试数据创建以及sex字段的正确展示
    def test_create_and_sex_show(self):
        print('test_create_and_sex_show')
        student = Student.objects.create(
            name='huyang',
            sex=1,
            email='test2@qq.com',
            profession='t1',
            qq='123',
            phone='test2123',
        )
        # django提供了get_xxx_display方法，可以替换sex_show
        self.assertEqual(student.sex_show, '男', '性别字段内容跟展示不一样')
        # self.assertEqual(student.get_sex_display, '男', '性别字段内容跟展示不一样')

    # 测试查询是否可用
    def test_filter(self):
        print('test_filter')
        Student.objects.create(
            name='huyang',
            sex=1,
            email='testfilter@qq.com',
            profession='t2',
            qq='222',
            phone='22322',
        )
        name = 'stu1'
        students = Student.objects.filter(name=name)
        self.assertEqual(students.count(), 1, '应该只存在一个名称为{}的记录'.format(name))

    # 测试首页的可用性
    def test_get_index(self):
        print('test_get_index')
        client = Client()
        response = client.get('/')
        self.assertEqual(response.status_code, 200, 'status code must be 200!')

    # 测试post请求
    def test_post_student(self):
        print('test_post_student')
        client = Client()
        data = dict(
            name='test_for_post',
            sex=1,
            email='333@dd.com',
            profession='t2',
            qq='2323',
            phone='3222'
        )
        response = client.post('/', data)
        self.assertEqual(response.status_code, 302, 'status code must be 302!')

        response = client.get('/')
        with open('temp.html', 'wb') as f:
            f.write(response.content)
        self.assertTrue(b'test_for_post' in response.content,
                        'response content must contain `test_for_post`')

```