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

<img width="2551" height="842" alt="image" src="https://github.com/user-attachments/assets/310593b3-b30a-4bce-8f57-f604b5bf5479" />

<img width="2321" height="724" alt="image" src="https://github.com/user-attachments/assets/367466cf-64a0-4ac8-b3f4-6358969d44ac" />

Now we have to know how to talk to jira API’s, like which modules in python we have to use and on which url we have to access this jira. 

We can refer jira API documentation: https://developer.atlassian.com/cloud/jira/platform/rest/v3/intro/

Create a project in jira 

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

# This code sample uses the 'requests' library:
# http://docs.python-requests.org

import requests
from requests.auth import HTTPBasicAuth
import json

url = "https://vysyarajujyothsna3.atlassian.net/rest/api/3/issue"
EMAIL = "vysyarajujyothsna3@gmail.com"

API_TOKEN=" "

auth = HTTPBasicAuth(EMAIL, API_TOKEN)

headers = {
  "Accept": "application/json",
  "Content-Type": "application/json"
}

payload = json.dumps( {
  "fields": {
    "description": {
      "content": [
        {
          "content": [
            {
              "text": "My first jira ticket",
              "type": "text"
            }
          ],
          "type": "paragraph"
        }
      ],
      "type": "doc",
      "version": 1
    },
    "project": {
      "key": "SCRUM"
    },
    "issuetype": {
      "id": "10004"
    },
    "summary": "First JIRA Ticket",
  },
  "update": {}
} )

response = requests.request(
   "POST",
   url,
   data=payload,
   headers=headers,
   auth=auth
)

print(json.dumps(json.loads(response.text), sort_keys=True, indent=4, separators=(",", ": “)))

After executing this we will get an output that will create an backlog

<img width="1191" height="186" alt="image" src="https://github.com/user-attachments/assets/2263aeff-8940-4c9b-af97-6b0c0996104a" />

<img width="2491" height="1117" alt="image" src="https://github.com/user-attachments/assets/fd828b7a-052c-42c2-b927-d1f2ecf4827a" />




