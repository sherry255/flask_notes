#### 简介上说主要借鉴的 Django
## 引入了 .globals.request 和 ._compat.with_metaclass

`http_method_funcs = frozenset(['get', 'post', 'head', 'options','delete', 'put', 'trace', 'patch'])`

- frozenset是冻结的集合，它是不可变的，存在哈希值，好处是它可以作为字典的key，也可以作为其它集合的元素。缺点是一旦创建便不能更改，没有add，remove方法。

---
## 类
#### View


```
class classmethod(object):

    """
    classmethod(function) -> method

    Convert a function to be a class method.

    A class method receives the class as implicit first argument,
    just like an instance method receives the instance.
    To declare a class method, use this idiom:

      class C:
          def f(cls, arg1, arg2, ...): ...
          f = classmethod(f)

    It can be called either on the class (e.g. C.f()) or on an instance
    (e.g. C().f()).  The instance is ignored except for its class.
    If a class method is called for a derived class, the derived class
    object is passed as the implied first argument.

    Class methods are different than C++ or Java static methods.
    If you want those, see the staticmethod builtin.
    """
    def __getattribute__(self, name): # real signature unknown; restored from __doc__
        """ x.__getattribute__('name') <==> x.name """
        pass

    def __get__(self, obj, type=None): # real signature unknown; restored from __doc__
        """ descr.__get__(obj[, type]) -> value """
        pass

    def __init__(self, function): # real signature unknown; restored from __doc__
        pass

    @staticmethod # known case of __new__
    def __new__(S, *more): # real signature unknown; restored from __doc__
        """ T.__new__(S, ...) -> a new object with type S, a subtype of T """
        pass

    __func__ = property(lambda self: object(), lambda self, v: None, lambda self: None)
    ```

---
```
class staticmethod(object):
    """
    staticmethod(function) -> method

    Convert a function to be a static method.

    A static method does not receive an implicit first argument.
    To declare a static method, use this idiom:

         class C:
         def f(arg1, arg2, ...): ...
         f = staticmethod(f)

    It can be called either on the class (e.g. C.f()) or on an instance
    (e.g. C().f()).  The instance is ignored except for its class.

    Static methods in Python are similar to those found in Java or C++.
    For a more advanced concept, see the classmethod builtin.
    """
    def __getattribute__(self, name): # real signature unknown; restored from __doc__
        """ x.__getattribute__('name') <==> x.name """
        pass

    def __get__(self, obj, type=None): # real signature unknown; restored from __doc__
        """ descr.__get__(obj[, type]) -> value """
        pass

    def __init__(self, function): # real signature unknown; restored from __doc__
        pass

    @staticmethod # known case of __new__
    def __new__(S, *more): # real signature unknown; restored from __doc__
        """ T.__new__(S, ...) -> a new object with type S, a subtype of T """
        pass

    __func__ = property(lambda self: object(), lambda self, v: None, lambda self: None)
    ```

### 一个重要的方法:        ._compat.with_metaclass

__new__() 方法的特性：

__new__() 方法是在类准备将自身实例化时调用。
__new__() 方法始终都是类的静态方法，即使没有被加上静态方法装饰器。

而如果新式类中重写了__new__()方法，那么你可以自由选择任意一个的其他的新式类（必定要是新式类，只有新式类必定都有__new__()，因为所有新式类都是object的后代，而经典类则没有__new__()方法）的__new__()方法来制造实例，包括这个新式类的所有前代类和后代类，只要它们不会造成递归死循环。具体看以下代码解释：

http://stackoverflow.com/questions/2608708/what-is-the-difference-between-type-and-type-new-in-python

http://stackoverflow.com/questions/395982/metaclass-new-cls-and-super-what-is-the-mechanism-exactly?rq=1
