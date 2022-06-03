# DRF - Authentication

## Admin

After running the server, use the following URL to enter the local admin 

    http://127.0.0.1:8000/admin

Enter the following credentials:

    Admin: admin
    Password: admin

## Testing 

After adding some items from the admin side, try to get the full list by this URL:

    http://127.0.0.1:8000/api/party-list 

## Requiring a token

enter the token URL we have specified before in the ThunderClient URL field:

    http://127.0.0.1:8000/api/token

Go to the (Body) tab and add your superuser info as a JSON object:

    {
    "username": "admin",
    "password": "admin"
    }

Change the method of request to (POST) instead of GET, then click on (send) button. That will provide you with two JWT tokens:

    {
    "refresh": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ0b2tlbl90eXBlIjoicmVmcmVzaCIsImV4cCI6MTY1NDA2Njk4NCwiaWF0IjoxNjUzOTgwNTg0LCJqdGkiOiIzM2U4ZGNiZDVmNWY0YWQwYWRlMjU4ZmQ2ZTBlZjAwYSIsInVzZXJfaWQiOjF9.4zSs8oX3eSEYUERJ_MXIMrsS_80XbttyxHM77-0doWc",
    "access": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ0b2tlbl90eXBlIjoiYWNjZXNzIiwiZXhwIjoxNjUzOTgwODg0LCJpYXQiOjE2NTM5ODA1ODQsImp0aSI6IjJjZTIyMTRkM2VlZTQzM2Y5NmIxYjA1MWNhOGE2MDY5IiwidXNlcl9pZCI6MX0.s-Fg7wlNGnO7AIBwRpEb0nJDxjJ78DaooOVpT7Qbie4"
    }

The first token is the one we use to refresh the key at any time. 
The second one is used to access the protected API.

## Consuming authentication 

We need to ask the server to provide the (party-list) only for authenticated users.

Change the method of request to (GET), then enter the URL for getting the full list of items that we had specified before:

    http://127.0.0.1:9001/api/v1/party-list

Now go to the (Auth) tab, select the (Bearer) method, and enter the (access) token we got before inside the (Bearer Token) field:

    eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ0b2tlbl90eXBlIjoiYWNjZXNzIiwiZXhwIjoxNjUzOTgwODg0LCJpYXQiOjE2NTM5ODA1ODQsImp0aSI6IjJjZTIyMTRkM2VlZTQzM2Y5NmIxYjA1MWNhOGE2MDY5IiwidXNlcl9pZCI6MX0.s-Fg7wlNGnO7AIBwRpEb0nJDxjJ78DaooOVpT7Qbie4 

You will get all the saved items in the database:

    [
    {
        "id": 1,
        "title": "item 1",
        "description": "description of the item 1"
    },
    {
        "id": 2,
        "title": "item 2",
        "description": "description of the item 2"
    }
    ]

## Expired token

If we try to get the result and we have got a message that tells us that the token is expired or not valid, we need to refresh that token to get a new access one.

Requiring a new token: enter the refresh URL we have specified before in the ThunderClient URL field:

    http://127.0.0.1:8000/api/refresh

Make sure you delete the old Bearer token in the (Auth) tab.
Go to the (Body) tab and enter the (refresh) token we got before as a JSON object:

    {
        "refresh": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ0b2tlbl90eXBlIjoicmVmcmVzaCIsImV4cCI6MTY1NDA2Njk4NCwiaWF0IjoxNjUzOTgwNTg0LCJqdGkiOiIzM2U4ZGNiZDVmNWY0YWQwYWRlMjU4ZmQ2ZTBlZjAwYSIsInVzZXJfaWQiOjF9.4zSs8oX3eSEYUERJ_MXIMrsS_80XbttyxHM77-0doWc"
    }

Change the method of request to (POST), then click on (send) button. That will provide you with the (access) JWT token:

    {
    "access": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ0b2tlbl90eXBlIjoiYWNjZXNzIiwiZXhwIjoxNjUzOTgyOTc1LCJpYXQiOjE2NTM5ODA1ODQsImp0aSI6ImJiODdiZmIxNWI2MjQzNGQ5YTk1YTdkNjZhNTQ4ZDZmIiwidXNlcl9pZCI6MX0.2PYp_TE6a0AlhmLnKdCWuW0PspjjvZtPn6akaJMHlPE"
    }

Now we got a new (access) token we can use to get the (party-list) again.





