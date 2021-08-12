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