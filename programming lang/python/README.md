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
  
- 

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
