# Python
---
## Ternary Conditionals
```python
condition = True
x = 1 if condition else 0
```

## Number Formatting
``` python
num1 = 1_000_000_000
num2 = 10_000_000
total = num1 + num2
print(f'{total:,}') #Uses f-string to format output w/ commas
```

## Context Managers
Manage resources such as IO connections, threads, db connections, etc. by opening & closing resources automatically
```python
with open('test.txt','r') as f:
  file_contents = f.read()
```
  
## Enumerate Functions
```python
names = ['Bob','Steve','Jim']
for index,name in enumerate(names):
  print(index,name)

for index,name in enumerate(names, start=1): #Can specify starting index value
  print(index,name)
```

## Zip Function 
Loops over `n` lists at once. When lists are different lengths, it stops at the end of the shortest list
```python
for name, hero, universe in zip(names, heroes, universes):
  print(name,hero)
  
for value in zip(names, heroes, universes):
  print(value) #Value is a tuple of the results of the 3 lists
```

## Unpacking
```python
a,b = (1,2)
print(a) #1
print(b) #2
c,_ = (4,5) #use underscore when you don't want to use a variable
print(c) #4

x,y,*z = (1,2,3,5,6,7)
print(x) #1
print(y) #2
print(z) #[3,5,6,7]

x,y,*_, z = (1,2,3,4,6,7,) #ignores all values after 1 & 2 but until 7, which is stored in z
```

## Requests Library
``` python
import requests

url_params = {'page' : 2, 'count' : 25}
r = requests.get("https://httpbin.org/get", params=url_params)

body = {'username' : 'corey', 'password' : 'testing'}
r = requests.post("https://httpbin.org/post", data=body, timeout=3) 

#include the timeout argument to Raise a ReadTimeout Error if the website does not respond in time
r_dict = r.json() 
```

## Environment Variables
MacOS terminal: 
- `export <var-name>=<var-value>` (add new env var)
- `export <existing-var-name>=<var-value>:$<existing-var-name>` (prepend values to an existing env var)
- `unset <var-name>` (remove env var)

`os.environ` acts like a python dictionary 

If you have other scripts updating the environment while your python script is running, calling os.environ again will not reflect the latest values since the mapping is only read when the python script is initially run.

```python
import os

os.environ['DB_USER'] = str(123) # env vars must always be strings

db_user = os.environ['DB_USER'] 
db_user = os.environ.get('DB_USER') # safe way of accessing potentially undefined env vars
```

## Memoization/Caching
Examples calculate the nth term of the fibonacci sequence
Basic implementation with dictionary
```python
fibonacci_cache = {}

def fibonacci(n):
    if n in fibonacci_cache:
        return fibonacci_cache[n]
    elif n == 1 or n == 2:
        value = 1
    else:
        value = fibonacci(n-1) + fibonacci(n-2)
    
    fibonacci_cache[n] = value 
    return value 
```

Optimized implementation with function tools
``` python
from functools import lru_cache

@lru_cache(maxsize=1000)
def fibonacci(n):
    if n == 1 or n ==2:
        return 1
    else:
        return fibonacci(n-1)+fibonacci(n-2)
```
## Config Parser
[Documentation](https://docs.python.org/3/library/configparser.html). Configuration file format:
``` ini
[section]
option1 = value1
option2 = value2
```
Reading the configuration file:
```python
from configparser import ConfigParser

parser = ConfigParser()
parser.read('file.ini')

if parser.has_section('database'):
    items = parser.items('database')
```
Its good to store things that could change in the configuration file (e.g. endpoints, db logins/tables/sprocs)

## CSV Files
```python
import csv

with open(file1, 'r'), open(file2, 'w') as f1, f2:
  csv_read = csv.reader(f1)
  csv_writer = csv.writer(f2)
  next(csv_read) # Skip header row

  for line in csv_reader:
      csv_writer.writerow([line[0],"extra col"])
```

## Matplotlib
- `figure` acts as a contianer for all plot elements
- `axes` contains most of the figures elements and sets the coordinate system
    - will usually contain 2 `axis` elements that control the ticks
  
``` python
import matplotlib.pyplot as plt

fig, ax = plt.subplots()

ax.axis('equal')    # makes it so patches are not stretched
ax.set_xlim(0,100)  # sets the x limits on the graph

# Add a line
from matplotlib.lines import Line2D
line = Line2D([x0,x1], [y0,y1])
ax.add_line(line)

# Add Shapes/Patches
from matplotlib.patches import Rectangle, Circle
r = Rectangle(top_left, width, height, fill=False)
ax.add_patch(r)

c = Circle((x_center,y_center), radius, fill=False)
ax.add_patch(c)

ax.scatter(x,y,facecolors='none',edgecolors='purple') # empty circles with an edge color

plt.show()
```


## Python Executable
- MacOS installs python 2.7 by default and should not be deleted 
    - `/usr/bin/python` and `/usr/bin/python2` are symlinks to default install: `System/Library/Frameworks/Python.framework/Versions/2.7/bin/python2.7`
- Python 3+ versions are installed in 
    - `/usr/local/bin/python3` is a symlink to version 3.5 installed in `/Library/Frameworks/Python.framework/Versions/3.5` by downloading python from internet
    - `/usr/local/bin/python3.9` is a symlink to version 3.9 installed in `/usr/local/Cellar` by homebrew (same goes for `pip3.9`) 
    - `/usr/bin/python3` is the actual install of version 3.8. Note sure how it got there but it is currently looked at on the path after the other version of python3 in the local/bin so it is not found unless the version is being explicitly looked for
    - All 3 versions of python3 are needed for ROS stuff so thats fun
- `python3 -m module_name` Searches the path for the module and excecutes its contents as the main module (Runs the specified module even if it isnt in the cwd)
- Note: find symlinks using `ls -l`