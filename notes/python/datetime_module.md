## Datetime Module
- Contains a date, datetime, & time class
- Default format is yyyy-mm-dd
```python
import datetime

#Date Class
birthday = datetime.date(2002,4,5)
print(birthday) #2002-04-05
print(birthday.year) #2002
print(birthday.month) #4
print(birthday.day) #5 

#Timedelta Class (difference btw 2 dates)
start_date = datetime.date(2000,1,1)
time_added = datetime.timedelta(100) #increases date by 100 days
print(start_date + time_added) #2000-04-10

#Day-name, Month-name Day #, Year
print(birthday.strftime("%A, %B %d, %Y")) #ex: Tuesday, January 31, 1956
message = "Vikram was born on {:%A,%B %d, %Y}."
print(message.format(birthday)) #Vikram was born on Tuesday, Jannuary 31, 1956.

#Datetime Class
launch_date = datetime.date(2017,3,30)
launch_time = datetime.time(22,27,0) #hr,min,sec
launch_datetime = datetime.datetime(2017,3,30,22,27,0)#yyyy,mm,dd,hr,min,sec

print(launch_date) #2017-03-30
print(launch_time) #22:27:00
print(launch_datetime) #2017-03-30 22:27:00

print(launch_time.hour) #22 
print(launch_time.minute) #27

print(launch_datetime.year) #2017
print(launch_datetime.hour) #22

#Access Current Datetime (UTC format)
now = datetime.datetime.today()
print(now) #2019-05-05 11:21:42.298504
print(now.microsecond) #298504

#Convert Strings to Datetime Object
moon_landing = "7/20/1969"
moon_landing_dt = datetime.datetime.strptime(moon_landing, "%m/%d/%Y")
print(moon_landing_dt) #1969-07-20 00:00:00
print(type(moon_landing_dt)) #<class 'datetime.datetime'>
```