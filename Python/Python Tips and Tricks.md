## Python Tips and Tricks
```python
#Ternary Conditionals
condition = True
x = 1 if condition else 0

#Underscore Placeholders
num1 = 1_000_000_000
num2 = 10_000_000
total = num1 + num2
print(f'{total:,}') #Uses f-string to format output w/ commas

#Context Managers- manage resources for you by opening and closing resources automatically 
with open('test.txt','r') as f:
  file_contents = f.read()
  #Works w/ other resources like threads, DB connections, etc
  
#Enumerate Function
names = ['Bob','Steve','Jim']
for index,name in enumerate(names):
  print(index,name)

for index,name in enumerate(names, start=1): #Can specify starting index value
  print(index,name)
  
#Zip Function- loops over n lists at once
#when lists are different lengths, it stops at the end of the shortest list
names = []
heroes = []
universes = []
for name,hero,universe in zip(names,heroes,universes):
  print(name,hero)
  
for value in zip(names,heroes,universes):
  print(value) #Value is a tuple of the results of the 3 lists

#Unpacking
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
`python3 -m module_name` Searches Sys.path for named module and excecutes its contents as the main module
Runs the specified module even if it isnt in the cwd 



