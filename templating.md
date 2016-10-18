## 引入了 jinja2 的一些包
## 引入了 .globals 的上下文
## 引入了 .signals 的信号机制
---
## 类
#### class Environment(BaseEnvironment):
- """Works like a regular Jinja2 environment but has some additional
    knowledge of how Flask's blueprint works so that it can prepend the
    name of the blueprint to referenced templates if necessary.
    """
- options['loader'] = app.create_global_jinja_loader()
,   然后调用下面的DispatchingJinjaLoader

#### DispatchingJinjaLoader(BaseLoader):
- 改写了 jinja2 的一些方法
- init 传参时有app名
-  result = set()      
- -    result.update(loader.list_templates())
