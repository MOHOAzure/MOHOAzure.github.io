## Python 

Commonly Seen Questions, including Python [knowledge](#knowledge) & [programming](#programming), mainly Python 3

### Knowledge
- List some standard libraries in python
  - [os](https://docs.python.org/3/library/os.html) : operating system dependent functionalities, such as OS name, file system representation of the path, and shell cmd
  - [sys](https://docs.python.org/3/library/sys.html) : access to variables used or maintained by the interpreter, like argv and command line flags.
  - [cmd](https://docs.python.org/3/library/cmd.html) : writing line-oriented command interpreters
  - [html.parser](https://docs.python.org/3/library/html.parser.html) : HTML file parser
  - [re](https://docs.python.org/3/library/re.html) : regular expression matching operations
  - [math](https://docs.python.org/3/library/math.html) : mathematical  calculation
  - [datetime](https://docs.python.org/3/library/datetime.html) : manipulate date & time
  - [threading](https://docs.python.org/3/library/threading.html) : thread-based parallelism
  - [multiprocessing](https://docs.python.org/3/library/multiprocessing.html) : process-based parallelism
  - [venv](https://docs.python.org/3/library/venv.html) : creating lightweight “virtual environments” with developer own site directories

- List some built-in data types in python
  - int, float
  - str
  - bool
  - list, tuple, range
  - dict
  - bytes
  - Details: <https://docs.python.org/3/library/stdtypes.htm>

- Mutable v.s. Immutable
  * Immutable
      * int, float, str, bool, tuple, range, bytes, frozenset
      * Change to the value involves creation of a new object with the value, refer the original variable to the new created object. If the original object is no longer refered (reference counting=0), then it is garbage collected.
  * Mutable
      * list, dict, set, custom class (general case)
  
- Python GIL
  - GIL (Global Interpreter Lock) is a mutex lock, which allows only one **thread** to control of the python interpreter.
  Since python uses reference counting for memory management, race conditions will occur when two threads increase or decrease a memory value simultaneously.
  The reference count counting could be kept safe by adding **locks** to all data structures that are shared across threads so that they are not modified inconsistently.
  Multiple locks can cause deadlock problem and decreased performance (repeated acquisition and release of locks).
  The GIL is a **single lock** to the interpreter which limits execution of any python code requires acqiring the interpreter lock.
  This prevents deadlock problem and doesn't introduce much performance overhead.
  GIL has drawbacks.
  The most obvious drawback is that GIL makes CPU-bound program single-threaded.
  In a multi-threaded context, only one thread could be in a state of execution at any point of time. 
  Other threads would be executed when the current thread is finished or is terminated because of time consuming operation.
  Therefore, even in a multi-threaded context with more than one CPU, threads are not executed concurrently.
  - Details: <https://realpython.com/python-gil/>
  
- Thread v.s. Process
  - Process
    * Basic unit for OS to allocate resource and execute
    * Processes are independent
    * Processes run in separate memory spaces
    * Multiprocess is good at CPU-bound since each process has its own GIL and they can be executed concurrently
  - Thread
    * Basic unit for CPU operation
    * Threads are independent
    * Threads (of the same process) run in a shared memory space
    * Multithread is good at IO-bound. When a thread is sleeping or waiting for input, another thread can be executed

- Session v.s. Cookie
  - Cookies and Sessions are used to store information. Cookies are only stored on the client-side machine, while sessions get stored on the client as well as a server.
  - Session
    - A session creates a file in a temporary directory on the server where registered session variables and their values are stored. This data will be available to all pages on the site during that visit.
    - A session ends when the user closes the browser or after leaving the site, the server will terminate the session after a predetermined period of time, commonly 30 minutes duration.
  - Cookies
    - Cookies are text files stored on the client computer and they are kept of use tracking purpose. Server script sends a set of cookies to the browser. For example name, age, or identification number etc. The browser stores this information on a local machine for future use.
    - When next time browser sends any request to web server then it sends those cookies information to the server and server uses that information to identify the user.

- List and explain some common `Errors`
  - IOError: Raised when Input/Output
  - AttributeError: Raised when an attribute reference or assignment fails. E.g., refer to a non-existing attribute of a object
  - ImportError: Raised when the import statement has troubles trying to load a module
  - SyntaxError: Raised when the parser encounters a syntax error
  - IndentationError: Base class for syntax errors related to incorrect indentation. This is a subclass of SyntaxError
  - IndexError: Raised when a sequence subscript is out of range
  - KeyError: Raised when a mapping (dictionary) key is not found in the set of existing keys
  - NameError: Raised when a local or global name is not found

- What are \*args and \*\*kwargs in fun(\*args and \*\*kwargs)?
  - \*args:  used to pass a variable number of Non-Keyword arguments to a function.
  - \*\*kwargs: used to pass a keyworded, variable-length argument list to a function.
  ```python
  def fun(*args, **kwargs):
    for arg in args:
      print("Next argument through *argv:", arg)
    for key, value in kwargs.items():
      print("Next Key:Value = %s:%s" %(key, value))
  
  fun("Hi", "Great", first="Cool",mid="Nice",last="Bye")
  ```
  ![](https://i.imgur.com/bJ5Cmro.png)
  
- Difference in `range(100)` between python2 and python3
  - In python2, `range(100)` returns a list
  - In python3, it returns a iterator in order to reduce memory consumption.

- Difference between \_\_new\_\_ and \_\_init\_\_
  - \_\_new\_\_ : the first step of instance creation. 
    \_\_new\_\_ is called first with a parameter `cls` (class), and is responsible for **returning** a new instance of a class.
    In general, you shouldn't need to override \_\_new\_\_ unless you're subclassing an immutable type like str, int, unicode or tuple. 
  - \_\_init\_\_ : initialization of a new instance after it's been created.
    \_\_init\_\_ is called with a parameter `self`, which is and instance return by \_\_new\_\_.
    \_\_init\_\_ dosen't return value, it initiate fileds of an instance.
  ```python
  class Car(object):
      def __init__(self):
        print("This is __init__", self)

      def __new__(cls):
        print("This is __new__", object.__new__(cls))
        print("cls ID:", id(cls))
        return object.__new__(cls)

  Car()
  print("class ID of Car:", id(Car))
  ```
    ![](https://i.imgur.com/Flcw5gi.png)

- 2 ways of file handling, using with and not using it
  - Use `with`, which deals with exception & file close internally
  ```python
    with open('file_path', 'w') as file:
      file.write('using with')
  ```
  
  - Not use `with`
  ```python
    file = open('file_path', 'w')
    try:
      file.wirte('not using with')
    except:
      pass
    finally:
      file.close()
  ```

- Explain python `assert`
  - Test a condition in program returns `True`, otherwise the program raises an `AssertionError` 
  ```python
  val=0
  assert val==0, "OK, Value is 0"
  assert val!=0, "Value should be 0"
  ```
  ![](https://i.imgur.com/HvxpcCe.png)
  
- In regular expression, explain difference between (.\*) and (.\*?)
  - (.\*) : it's greedy, matching as **much** as it can.
  - (.\*?) : it's non-greedy, matching as **little** as it can.
  ```python  
  import re
  str="<a> foo </a><a> bar </a>"
  greedy=re.findall(r'<a>(.*)</a>',str)
  nongreedy=re.findall(r'<a>(.*?)</a>',str)
  print("(.*) is greedy",greedy)
  print("(.*?) is non-greedy",nongreedy)
  ```
  ![](https://i.imgur.com/WM42jxa.png)
  
- Give examples to explain ```try except else finally```
  - ```finally``` is executed regardless of whether the statements in the try block fail or succeed
  - ```else``` is executed only if the statements in the try block don't raise an exception.
  ```python  
  try:
      print("HI")
  except IOError as errorMsg:
      print('Err', errorMsg)
  else:
      print("No error, come to else statement")
  finally:
      print("Next example")

  try:
      print("try to open a non-existing file")
      foo = open("foo.txt")
  except IOError:
      print("error")
  else:
      print(foo.read())
  finally:
      print("finished")
  ```
  ![](https://i.imgur.com/LJqZEra.png)

- copy v.s. deepcopy
  - If the "copied" variable is **immutable**, `copy` and `deepcopy` both act lilke `=`
    ```python  
    import copy
    var="HA"
    print(id(var))
    var_copy = copy.copy(var)
    print(id(var_copy))
    var_deepcopy = copy.deepcopy(var)
    print(id(var_deepcopy))
    ```
    ![](https://i.imgur.com/MUPAntU.png)
  - If the "copied" variable is **mutable**
    - `deepcopy`: create a place and assign it with the copied value
    - `copy`: only copy the 'shallow', and create a place point to the 'deep' part of the copied varaible
    ```python
    import copy
    list=[1,[2,3]]
    list_copy=copy.copy(list)
    list_deepcopy=copy.deepcopy(list)
    print("Print the value and its id. They look like 3 independent varibles.")
    print(list, id(list))
    print(list_copy, id(list_copy))
    print(list_deepcopy, id(list_deepcopy))

    list[0]=9
    print("Change 'shallow' part of the variable. They still look like 3 independent varibles.")
    print(list)
    print(list_copy)
    print(list_deepcopy)

    list[1][1]=999
    print("Change 'deep' part of the variable. Now, the difference between copy and deepcopy comes out.")
    print(list)
    print(list_copy)
    print(list_deepcopy)
    ```
    ![](https://i.imgur.com/G2Mpozw.png)
  
- Interchange between python dict and json
  ```python  
  import json
  dic={"name":"HA"}
  res=json.dumps(dic)
  print(res, type(res))
  res=json.loads(res)
  print(res, type(res))
  ```
  ![](https://i.imgur.com/7bnhVct.png)
  
- SQL injection
  * If the input contains `;+SQL`, and SQL following the `;` will be executed.
  ```python
  input_name='person_name'
  sql="SELECT * FROM tbl WHERE name=%s" % input_name
  print("A normal sql:", sql)

  input_name='person_name; DROP DATABASE XXX'
  sql="SELECT * FROM tbl WHERE name=%s" % input_name
  print("A malicious sql:", sql)
  ```
  ![](https://i.imgur.com/zRobcIj.png)
  
  * Solution: use `params`  
  ```python
  params=[input_name]
  count = table.execute("SELECT * FROM tbl WHERE name=%s",params)
  ```

- Elaspse time measurement
  ```python
  from timeit import default_timer as timer
  start = timer()

  print("Hi! Good day!")

  end = timer()
  print("elaspse time", end - start)
  ```
  ![](https://i.imgur.com/Is2TGL3.png)

### Programming
  
- Remove repeated values in a list
  ```python
  list=[11,11,12,13,15,13]
  dic=set(list)
  new_list=[x for x in dic]
  ```
  ![](https://i.imgur.com/5Eokj2w.png)
  
- Delete a key in a dictionary
  ```python
  dic={"key1":"v1", "key2":"v2"}
  del dic["key1"]  
  ```
  ![](https://i.imgur.com/5Mpw94x.png)
  
- Merge two dictionaries
  ```python
  dic1={"k1":"v1"}
  dic2={"k2":"v2"}
  dic1.update(dic2)
  ```
  ![](https://i.imgur.com/KrmA3UW.png)
  
- Sum up 1 to 100
  ```python
  sum(range(1,101))
  ```
  ![](https://i.imgur.com/myZWIz1.png)
  
- Modify a global variable in a function
  ```python
  a=5

  def fn():
      global a
      a=0

  print("Before", a)
  fn()
  print("After", a)
  ```
  ![](https://i.imgur.com/OMfIK0J.png)


- Given a list of numbers, return their square numbers which are larger than a threshold (specified value).
  ```python
  def fn_sqr(x):
    return x**2

  def fn_ans(list, threshold):
    return [i for i in list if i>threshold]

  list=[1,2,3,4,5]
  threshold=10
  res=map(fn_sqr, list)
  res=fn_ans(res, threshold)
  ```
  ![](https://i.imgur.com/KyD9X17.png)
  

- Generate random numbers: one integer and 3 decimal numbers
  ```python
  import random

  res_int=random.randint(0,10)
  res_decimal=random.random()

  print("Random int", res_int)
  print("Random decimal", res_decimal)
  ```
  ![](https://i.imgur.com/GBBWUN0.png)

- Find *Person Name* in `<div class="person_nam">Person Name</div>` where class name is uncertain
  ```python
  import re

  str='<div class="person_nam">Person Name</div>'
  res=re.findall(r'<div class=".*">(.*?)</div>',str)
  # ".*" : deal wit verious class name
  # (.*?): select text

  print(res)
  ```
  ![](https://i.imgur.com/HGGIPNM.png)

- Give examples of `sort` and `sorted` using a list=[0,-1,3,-10,5,9]
  * `sort` is a function belongs to list class, and it modify the list passed as a parameter.
  * `sorted` is a function which creates a new list containing a sorted version of the list it is given.
  ```python
  list=[0,-1,3,-10,5,9]
  list.sort()
  print('with sort:', list)

  list=[0,-1,3,-10,5,9]
  res=sorted(list)
  print('original:',list)
  print('with sorted:', res)
  ```
  ![](https://i.imgur.com/clzqbjs.png)
  
- Given a string, remvoe duplicated character and sort the string ascendingly.
  ```python
  s="ajldjlajfdljfddd"
  s=set(s)
  s=list(s)
  s.sort(reverse=False)
  res="".join(s)
  print(res)
  ```
  ![](https://i.imgur.com/kXGliav.png)
  
- Multiply two numbers with `lambda`
  ```python
  sum=lambda a,b:a*b
  print(sum(9,6))
  ```
  ![](https://i.imgur.com/mkYFcmK.png)
  
- Sort a dictionary by key names
  ```python
  dic={"Name":"Ange","Age":27, "Country":"JP"}
  list=sorted(dic.items(), key=lambda i:i[0])
  dic=dict(list)
  print(dic)
  ```
  ![](https://i.imgur.com/vmNRg00.png)
  
- Count the number of each character in a given string, `s='fjljgpmupwer|ksdf#$kl*@'`
  ```python
  from collections import Counter
  s='fjljgpmupwer|ksdf#$kl*@'
  res=Counter(s)
  # Access context of Count
  for i in res.keys():
      print("%s:%s" % (i, res[i]))
  ```
  ![](https://i.imgur.com/mM6BN96.png)
  
- Given a str='not 404 found 成果 666 大好', try to remove the english & number parts and then output '成果' & '大好'
  ```python
  import re
  str='not 404 found 成果 666 大好'
  # preprocss str
  list=str.split(' ')

  res=re.findall(r'\d+|[a-zA-Z]+',str)
  # \d+ : find numbers (as same as [0-9]+)
  # [a-zA-Z]+: find alphabets

  # remove numbers & alphabets
  for i in res:
      if i in list:
          list.remove(i)

  print(list)
  ```
  ![](https://i.imgur.com/3UYfEDY.png)
  
- Given a list=[1, 2, 3, 4, 5, 6, 7, 8, 9, 10], try to find odd numbers with `filter` and group them in a list
  ```python
  list=[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
  newlist=filter(lambda i:i%2==1, list)
  newlist=[i for i in newlist]
  print(newlist)
  ```
  ![](https://i.imgur.com/q7qnJry.png)
  
- Retrieve current timestamp
  ```python
  import datetime
  log_time=str(datetime.datetime.now().strftime('%Y-%m-%d %H:%M:%S'))
  print(log_time)
  ```
- Parse [[1,2],[3,4],[5,6]] to [1,2,3,4,5,6]
  ```python
  list=[[1,2],[3,4],[5,6]]
  new_list = [j for i in list for j in i]
  print(new_list)
  ```
  ![](https://i.imgur.com/M85qR6u.png)
  
- Swap two values
  ```python  
  a, b = 1,0
  a, b = b,a
  ```
  
- Given a string, replace its numerical numbers with a white space 
  ```python
  import re
  str="Wow 999 Nice"
  res=re.sub(r'\d+',' ', str)
  print(res)
  ```
  ![](https://i.imgur.com/OR34t4d.png)
  
- Split a string by `:` or space
  ```python  
  str="target str:this a string"
  res=re.split(r':| ',str)
  print(res)
  ```
  ![](https://i.imgur.com/Fqaw7iO.png)
  
- Find Gmail accounts
  ```python
  emails=["Mail_A@gmail.com", "Mail_A@gmail.com.fake", "Mail_B@yahoo.com", "Mail_C@domain.mail"]

  for mail in emails:
      res=re.match("\S+@gmail.com$",mail)
      if res:
          print("Find a Gmail:", mail)
      else:
          print("Not a Gmail:", mail)

  ```
  ![](https://i.imgur.com/M9WAFJ6.png)
  
- Demo ```zip```
  ```python  
  list_a=[1,2]
  list_b=[3,4]
  res=[tuple for tuple in zip(list_a, list_b)]
  print(res)

  tuple_a=(1,2)
  tuple_b=(3,4)
  res=[tuple for tuple in zip(tuple_a, tuple_b)]
  print(res)

  str_a="HI"
  str_b="GOOD"
  res=[tuple for tuple in zip(str_a, str_b)]
  ```
  ![](https://i.imgur.com/n2tp75u.png)
  
- Sort a list ascendingly but without `sort` function
  - find out the min number, and reverse it in a new space
  ```python  
  list=[2,3,-5,14,9,0]
  new_list=[]

  def my_sort(list):
      n=min(list)
      new_list.append(n)
      list.remove(n)
      if len(list)>0:
          my_sort(list)

  my_sort(list)
  print(new_list)
  ```
  ![](https://i.imgur.com/oF63miO.png)
  
- Sort a string list by string length
  ```python
  list=["a","xyz","bc"]
  res=sorted(list, key=lambda x:len(x))
  list.sort(key=len)
  print('res:', res)
  print('sorted list:',list)
  ```
  ![](https://i.imgur.com/ZTFqz2A.png)
  
- Implement a singleton pattern
  ```python
  class Singleton(object):
      __instance=None

      def __new__(cls,name,age):
          if not cls.__instance:
              cls.__instance=object.__new__(cls)
          return cls.__instance

  ins_dog=Singleton("doge",1)
  ins_cat=Singleton("kitty",2)

  print(id(ins_dog))
  print(id(ins_cat))

  ins_dog.name='wang wang'
  print("cat name", ins_cat.name)
  ```
  ![](https://i.imgur.com/2cqABBz.png)

- Remove the space at the begining and the end of a string
  ```python
  str=" YEAH "
  str.strip()
  ```  
  
- Remove the space in a string
  ```python
  str="HA HA YEAH "
  # Method 1
  res=str.replace(" ","")
  print(res)

  # Method 2
  list=str.split(" ")
  res="".join(list)
  print(res)
  ```
  ![](https://i.imgur.com/LGhNwsW.png)
  
  
- Update `[i for i in range(3)]` to a generator
  ```python
  gen = (i for i in range(3))
  ```
  
- Count frequency of a substring inside a string
  ```python
  str="This a very very cool demo"
  count=str.count('very')
  print(str+'\nCount very:', count)
  ```
  ![](https://i.imgur.com/qR5oT24.png)
  
- Read from a excel file
  ```python
  import pandas as pd
  df=pd.read_excel('file.xlsx')
  print(df)
  ```
  
- Demo `search`, `findall`, and `match` in regular expression
  ```python  
  import re
  s="This year is 2000. 100%!"
  res=re.search(r'\d+',s).group()
  print(res)
  res=re.findall(r'\d+',s)
  print(res)
  res=re.match("This",s)
  print(res)
  print("The following raise err since the string isn't start with '100'")
  res=re.match("100",s).group()
  print(res)
  ```
  ![](https://i.imgur.com/gIWxDMU.png)
  
<!-- Template
- 
  ```python
  ```
  ![]()
  
  - Question
  ```python
  ```
  ![ResultPic]()
-->
