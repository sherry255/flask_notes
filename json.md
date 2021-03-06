##1. 关于json:
* flask.jsonify()
```
	try:
    from itsdangerous import simplejson as _json
except ImportError:
    from itsdangerous import json as _json
```

#### `jsonify` would be useful when you are building an API someone would query and expect json in return. E.g: The REST github API could use this method to answer your request.
#### `dumps`, is more about formating data/python object into json and work on it inside your application. For instance, I need to pass an object to my representation layer where some javascript will display graph. You'll feed javascript with the Json generated by dumps.


```
def jsonify(*args, **kwargs):
"""..."""
    return current_app.response_class(dumps(dict(*args, **kwargs),
        indent=indent),
        mimetype='application/json')
```

## 2. 如果你想修改一个已经打开的文本模式的文件的编码方式，可以先使用 detach() 方法移除掉已存在的文本编码层，并使用新的编码方式代替。下面是一个在 sys.stdout 上修改编码方式的例子

* TextIOWrapper
```
>>>sys.stdout.encoding
'UTF-8'
>>> sys.stdout = io.TextIOWrapper(sys.stdout.detach(), encoding='latin-1')
>>> sys.stdout.encoding 'latin-1'
```

* BufferedReader
```
>>>f = io.open(".bashrc", "rb")
>>> type(f)
<type '_io.BufferedReader'>
```


## 3. JSON 处理str or file
```
   json.loads(str)
   json.load(file)

   json.dumps(str)
   json.dump(file)
```

##  4. setdefault的用法

* 在字典中一个key映射多个值
```
>>> d = {} # A regular dictionary
>>> d.setdefault('a', []).append(2)
>>> d.setdefault('b', []).append(4)
>>> d
{'a': [1,2,4]}
```


## 5. Python 中的短路求值:
* "or"
```
s = s.decode(kwargs.pop('encoding', None) or 'utf-8')
```

## 6. check if request is ajax:
`request.is_xhr`

## 7. json.dumps(indent, sort_key)
* sort_keys是告诉编码器按照字典排序(a到z)输出。
```
>>> print json.dumps(parsed, indent=4, sort_keys=True)
[
    "foo",
    {
        "bar": [
            "baz",
            null,
            1.0,
            2
        ]
    }
]


>>> print json.dumps(parsed, indent=2, sort_keys=True)
[
  "foo",
  {
    "bar": [
      "baz",
      null,
      1.0,
      2
    ]
  }
]


>>> print json.dumps(parsed, indent=1, sort_keys=True)
>>>[
 "foo",
 {
  "bar": [
   "baz",
   null,
   1.0,
   2
  ]
 }
]
```


```
>>> print json.dumps(parsed, indent=None, sort_keys=True)
["foo", {"bar": ["baz", null, 1.0, 2]}]
```

```
>>> print json.dumps(parsed, indent=None)
["foo", {"bar": ["baz", null, 1.0, 2]}]
```

```
>>> print json.dumps(parsed, indent=None, sort_keys=False)
["foo", {"bar": ["baz", null, 1.0, 2]}]
```


## 8. jsonify
* config设置了json格式的, 而且不是ajax请求的,indent = 2.
* 默认indent=None

```
if current_app.config['JSONIFY_PRETTYPRINT_REGULAR'] \
        and not request.is_xhr:
        indent = 2

```
