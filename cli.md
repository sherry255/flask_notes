# 一些命令行的脚本

## 用到的库

### click

- Flask 的作者Armin Ronacher 创造的一个库, <http://click.pocoo.org/5/> 美观的命令行接口

## 类

### NoAppException(click.UsageError):

- (app找不到时抛出异常)

### DispatchingApp(object):

- """Special application that dispatches to a flask application which is imported by name in a background thread. If an error happens it is is recorded and shows as part of the WSGI handling which in case of the Werkzeug debugger means that it shows up in the browser. """ app 任务调度 ???

### ScriptInfo(object):

- 创造app类的实例,
- 最后调用 def locate_app(app_id):

### AppGroup(click.Group):

### FlaskGroup(AppGroup):
