# Problem Statement: 

As there were lot of QE / developers, the application may have lot of micro-services and they may notice a bug in application or while testing an application then they will create an issue in the GitHub. Not every issue should not be considered as an issue, There will be an development team in an organisation, one of the developer should be there as an reviewer that person should review the issues which are raised in GitHub daily or weekly and that person will understand if there an genuine issue or not. 

If that issue is not valid then they will close it. 
If the issue is valid then they have to track and work on that issue to show amount of work or no.of issue they fixed. Then they need to create a jira ticket in jira board.

# Root cause: 

DevOps engineer can automate this issue using python modules and API’s on windows/ linux server.

When an developer writes the comment called “/jira” in GitHub issue then GitHub will know that there is an python application and it is hosted on ec2 instance then it will send an web-hook and it will automatically trigger it and create an jira ticket. In that ticket all the information will be send by using that web-hook. 

The web-hook will have the following details:
description of the issue
who has created this issue 
When did they created this issue

These all details will be converted into a json format automatically. It will send the json info to the python application we have created and we will make an API call to jira.


Part1: As a DevOps Engineer, we will configure a web-hook in the GitHub. This web hook will tells the GitHub to keep track the comment called “/jira”. In the web hook configuration DevOps engineer will provides an url for the python application. Provide an Json for the python application.

Part2: we will send the json to jira which we have received from the GitHub where we are making an API call with jira and we are creating an jira ticket 


Jira Setup

Jira Api call

Python script

Execution of the script

https://vysyarajujyothsna3.atlassian.net?continue=https%3A%2F%2Fvysyarajujyothsna3.atlassian.net%2Fwelcome%2Fsoftware&atlOrigin=eyJpIjoiZjA1YTA2NjA3MzMxNGQwNWE2NmEwNjY0ODU3ZGQ1YzYiLCJwIjoiaiJ9

When we want to interact with an application, there are 2 ways either CLI or API. Here we are using python hence API is best way to interact with python. So here we need to create an API token 

In Jira board, go to profile and account setting. In security tab, we can create and manage API token

<img width="1887" height="1112" alt="image" src="https://github.com/user-attachments/assets/b595101c-b6f4-4482-8511-d4dfc60b0806" />

Now we have to know how to talk to jira API’s, like which modules in python we have to use and on which url we have to access this jira. 

We can refer jira API documentation: https://developer.atlassian.com/cloud/jira/platform/rest/v3/intro/

Create a project/space in jira 

<img width="2106" height="794" alt="image" src="https://github.com/user-attachments/assets/9ebcf050-2bf9-4903-9c1e-0009bbc255ef" />

<img width="2511" height="733" alt="image" src="https://github.com/user-attachments/assets/af13f632-dbc5-4ba4-adfa-b3266ad8300d" />

Explanation about the code:

-> import requests:  Request module, which is used to make api calls as jira models are not as stable as aws ( boto3 module like creating ec2 ), that’s why we use a standard module which is request module. 


->from requests.auth import HTTPBasicAuth: From the request package we have imported, we will import a module called HTTPBasicAuth because we want to authenticate with jira. If you don’t authenticate with jira. If anyone is tries to make api calls with the application, jira will not gives the output. Only the valid user with valid api token can access it.

-> import json: we have used json module to get the output from the json file

-> Now coming to python code for Jira setup and API call:

We can refer it from Jira documentation: 
https://developer.atlassian.com/cloud/jira/platform/rest/v3/intro/#about

In jira we will create an ticket or issue, so we will use issue code here

<img width="2470" height="1470" alt="image" src="https://github.com/user-attachments/assets/484c8c00-45c5-4141-8955-944419f48f75" />

Here we will prefer only code which is related to mandatory fields to create an issue 

The mandatory fields to create an issue are:

<img width="1427" height="1037" alt="image" src="https://github.com/user-attachments/assets/62554a59-780c-475f-ae3e-903f374ae8e9" />

<img width="1454" height="1037" alt="image" src="https://github.com/user-attachments/assets/2919af82-d084-4a9d-a502-7a40422b7054" />

Here work type is the issue type, it has id. Here we want to create the work type is a story for that it will an id. Go to configure board 

<img width="2497" height="975" alt="image" src="https://github.com/user-attachments/assets/e2898682-a285-42a3-8452-f69ef3e2ea33" />

<img width="1694" height="1191" alt="image" src="https://github.com/user-attachments/assets/b0712368-466a-4551-8524-c97c705ddd8a" />

The story work type has id 10004

In the project/space which has mandatory field, we will provide key as SCRUM.

<img width="1455" height="1148" alt="image" src="https://github.com/user-attachments/assets/6a7d34a4-eb1e-4183-ae04-c53c0046474a" />

<img width="1544" height="1188" alt="image" src="https://github.com/user-attachments/assets/914d4cad-6db2-4905-a07a-cfd5b9e9ac91" />

We don’t need to mention reporter because we are using api token

refer request-module.py file to create an jira ticket

After executing this we will get an output that will create an backlog

<img width="1191" height="186" alt="image" src="https://github.com/user-attachments/assets/2263aeff-8940-4c9b-af97-6b0c0996104a" />

<img width="2491" height="1117" alt="image" src="https://github.com/user-attachments/assets/fd828b7a-052c-42c2-b927-d1f2ecf4827a" />

# Jira and GitHub integration using python:

Github has an entity should talk to python using web hooks, the python application can be stored in a Ec2 instance of an server. GitHub has to talk to the python. The python script has to interact with Jira using Jira API’s.

Now we have to convert python script to an API

In the GitHub web hook we have to provide the the Url/API of the python application we have Written. We will use the flask to write this python application. For that we have to convert the python code that we have used earlier to Flask framework so that an API is exposed.

Once we provided that Url to the GitHub, it will send the entire json Payload information.

-> API (Flask Framework): Application Interface

API’s are works on HTTP protocol/ request types 

Post,Get,Put,Delete are 4 API request types

# Install Flask application: 

python3 -m venv .venv 

source .venv/bin/activate

pip3 install flask (flask is a package)

# Example:

*We just need a flask module, which is a part of flask package (if we take a entire flask package, it will take lot of time to execute entire program)

from flask import Flask

app = Flask(__name__)  —> creating an flask app instance because we will perform all the actions using it.

@app.route(‘/‘)  —> this line is a decorator,  this line will execute before function trigger
In real time before a person interacting with a micro service, this decorator will helps to authenticate for person verification.

If any person wants to access this hello api are they trying to access on the path / . If they are trying to access on that path / then they can access the hello_world function 


def hello_world():

    return 'Hello, World!'
if __name__ == '__main__':

    app.run("0.0.0.0")

Decorator: if someone wants to access the api, will use a decorator before the function definition then it will give access to only the authenticated users to access the function.


# Create an Ec2 Instance 
ssh into that server and create an python file to write the flask application code

Refer flask-app.py file for python code using flask module

now use the below public DNS url to link github and jira api through webhook

<img width="2547" height="574" alt="image" src="https://github.com/user-attachments/assets/1ef5bf12-61c4-4442-924c-62c02bd76280" />

<img width="2291" height="1022" alt="image" src="https://github.com/user-attachments/assets/84a580c3-988d-4cfb-b89a-b7d3e69c9f5d" />

<img width="1401" height="436" alt="image" src="https://github.com/user-attachments/assets/8d4b4027-fee9-4ac1-bd3f-1f1198fb39f5" />

now execute the python flask application

<img width="1722" height="317" alt="image" src="https://github.com/user-attachments/assets/dac42e1e-d235-45b6-a420-ad6fbe08280c" />

go to jira issues and create and comment '/jira' 

<img width="1812" height="783" alt="image" src="https://github.com/user-attachments/assets/0caaebfe-3a92-4f60-93e6-129931bc6020" />

<img width="2239" height="1042" alt="image" src="https://github.com/user-attachments/assets/79bb1de5-f92c-4533-9ed8-b627958b9a5c" />

once we have commented in the issue the Jira API will trigger and it will create the backlog 

<img width="1800" height="530" alt="image" src="https://github.com/user-attachments/assets/11b963de-869f-4f1f-a7c9-ce7897e9690b" />







