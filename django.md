# 创建django项目

```python
#创建项目
django-admin startproject    #项目名
mysite
-  __ init__.py
- settings.py   配置文件
- urls  路由文件
- wsgi.py   服务器文件
manage.py   django指令文件
```

# 创建django应用

```python
python manage.py startapp polls
```

## polls

- migrations  迁移文件包

- __ init__.py
- admin.py   自定义后台界面
- apps.py      应用的配置，主要设置应用名称
- models.py  数据模型
- tests.py   测试文件
- views.py   视图（MVT中的V）

# 配置项目

## setting.py

- 配置语言

```python
LANGUAGE_CODE = 'zh-hans'
```

- 配置时区

```python
TIME_ZONE = 'Asia/Shanghai'
```

- 添加应用

```python
INSTALLED_APPS = [
    ...
    'polls',
]
```

- 数据库

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': os.path.join(BASE_DIR, 'db.sqlite3'),
    }
}
```

# 创建第一个视图

- 在应用视图文件中创建视图函数  views.py

  ```python
  from django.shortcuts import render
  from django.http import HttpResponse
  # Create your views here.
  
  def index(request):
      return HttpResponse("123")
  ```

- 在应用中创建路由文件<polls/urls.py>

  ```python
  from django.urls import path
  from . import views
  
  urlpatterns = [
      path('',views.index)   #views.index-----视图函数
  ]
  ```

- 在项目文件包导入应用路由（mysite/urls）

  ```python
  from django.contrib import admin
  from django.urls import path,include
  
  urlpatterns = [
      path('admin/', admin.site.urls),
      path('polls/', include("polls.urls")),
  ]
  ```

# 配置数据库

> 数据库版本  5.5以上

1. mysql

   ```python
   DATABASES = {
       'default': {
           'ENGINE': 'django.db.backends.mysql',
           'NAME':"polls",
           'HOST':'localhost',
           'PORT':3306,
           'USER':"root",
           'PASSWORD':'123123'
       }
   }
   ```

2. pymysql配置

   ```python
   import pymysql
   pymysql.install_as_MySQLdb()
   ```

3. 创建模型（polls/models.py）

   ```python
   class Question(models.Model):
       question_text = models.CharField(max_length=200)
       pub_date = models.DateTimeField('date published')
   
   
   class Choice(models.Model):
       question = models.ForeignKey(Question, on_delete=models.CASCADE)
       choice_text = models.CharField(max_length=200)
       votes = models.IntegerField(default=0)
   ```

# 创建迁移文件

```python
python manage.py makemigrations polls
```

执行迁移

```python
python manage.py migrate
```

# 创建站点

```python
python manage.py createsuperuser
```



Student.objects.create(name=name,tel=tel,c=c)



```python
Course.objects.filter(id=id).delete()
```



csrf_token   jinjia的标签  (jinjia函数  必须有返回值，)   跨域[令牌,解决跨域问题   



## ModelForm

```python
class Meta:
    model=User  #验证的模型
    fields="__all__"  #验证的字段，是一个集合
    widgets={
        'name':forms.TextInput(attrs={'class':'aaa'})
    }
    lables={
        'name':"姓名"
    }
    error_messages={
        'name':{'required':"必填"}
    }
```





save可以直接保存一对一，一对多，多对多

注意：在多对多中如果使用了save(commit=False)  还需执行一下   form.save_m2m()







collectstatic



from django.utils.deprecation import MiddlewareMixin





process_request    不能有return

process_response     必需有return

process_view()   不能有return

process_exscption  可以有return  也可以没有























































