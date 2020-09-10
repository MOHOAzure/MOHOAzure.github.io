## Python 

Commonly Seen Questions, including [algorithms](#algorithm) & Python [knowledge](#knowledge), mainly Python 3

### Algorithm
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


- 
  ```python
  ```
  ![]()
  

- 
  ```python
  ```
  ![]()


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
  
- Python GIL
  * GIL (Global Interpreter Lock) is a mutex lock, which allows only one **thread** to control of the python interpreter.
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
  Details: <https://realpython.com/python-gil/>

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
