# pymonitor
This tool will monitor the general info(process, core, os etc) and performance info(memory, load,disk space etc).
Also it will poll performance data in to the db for every two minutes.It will send a report for every day.


1.Create a virtual env and install all packages in requirements.txt
2.do migrations
3.create a super user through terminal 
4.fill server details in server_details.py in connection
5.follow celery run steps to start in celery run steps.txt

Usage:


import requests
import json
import pdb

#### to get token
r = requests.post("http://127.0.0.1:8000/login/", data={'username': 'vinod', 'password': 'admin123'})
token = json.loads(r.text)['token']

#### to register user
r = requests.post("http://127.0.0.1:8000/users_info/", 
    data={'username': 'vinod', 
        'password': 'admin123', 
        'email':'test@gmail.com',
        'fname':'Vinod',
        'lname':'Kopperla',
        'mobile':'8142832767',
        'hometown':'Anantapur'},headers={'Authorization': 'Token {}'.format(token)})

#### to register user to get all users data
result = requests.get("http://127.0.0.1:8000/users_info/", 
    headers={'Authorization': 'Token {}'.format(token)})
print(result.text) 

#### to register use  to get user data

result = requests.get("http://127.0.0.1:8000/users_info/siva", 
    headers={'Authorization': 'Token {}'.format(token)})
print(json.loads(result.text))

####  to update the user data
r = requests.put("http://127.0.0.1:8000/users_info/vinod/", 
    data={'username': 'vinod', 
        'password': 'admin123', 
        'email':'vinod@gmail.com',
        'fname':'Vinod Kumar',
        'lname':'K',
        'mobile':'1234567',
        'hometown':'Anantapur'},headers={'Authorization': 'Token {}'.format(token)})
print(r.text)

#### to delete user data
r = requests.delete("http://127.0.0.1:8000/users_info/vinod", 
    headers={'Authorization': 'Token {}'.format(token)})
print(r.text)

####  to get all  general_info
result = requests.get("http://127.0.0.1:8000/general_info/", 
    headers={'Authorization': 'Token {}'.format(token)})
print(result.text) 
####  to get specific server info
result = requests.get("http://127.0.0.1:8000/general_info/192_168_64_132", 
    headers={'Authorization': 'Token {}'.format(token)})
print(result.text)

####  to get all servers performance
result = requests.get("http://127.0.0.1:8000/performance_info/", 
    headers={'Authorization': 'Token {}'.format(token)})
print(result.text)

####  to get specific server performance 
result = requests.get("http://127.0.0.1:8000/performance_info/192_168_64_132", 
    headers={'Authorization': 'Token {}'.format(token)})
print(result.text)
