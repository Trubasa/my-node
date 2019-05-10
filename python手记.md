- filter

- sorted

  - sorted([1,2,3],key=abs)
  - sorted(['a','Af'],key=str.lower)
  - sorted([1,2,3],reverse=True)

- enumerate 枚举

  ```python
  for index,element in enumerate(['a',"b","c"]):
  	print(index,element)
    
  """
  0 a
  1 b
  2 c
  """
  
  ```

- lambda

- 获取函数的名称

  ```
  f.__name__
  ```

- decorator （装饰器不太会）

- functools.partial()

- module模块

  ```python
  # 目录下的__init__.py 代表该文件夹模块
  # 多个文件的引入可以用元素的方式
  from myModules.talk import (hello,ok)
  ```

- 定义类

  ```
  __str__   # 让输入格式好看
  __repr__  # 同理
  
  # 枚举相关
  __iter__
  __next__
  
  __getitem__ # 切片
  
  __getattr__  # 获取不到属性时会访问这个
  
  __call__ # 实例调用自身的默认方法
  ```

- type 可以用于创建类
