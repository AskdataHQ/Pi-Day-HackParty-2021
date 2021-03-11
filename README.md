# Pi Day HackParty 2021


Welcome to Pi Day HackParty 2021!

Follows the steps for start using Askdata. 

# Askdata quick start:

* **SignUp:** Register to [Askdata](https://app.askdata.com/login) with your own email WARN -> Do not use the Social Login with Google/Slack.
* **Login to Askdata using REST API:** Get the token that will be used for all the other APIs
* **Select Workspace:** Switch to the Pi Day workspace.


## SignUp / Social Login 
Register to [Askdata](https://app.askdata.com/login) with your own email or signing-in with Google.

**Landing page**![image](https://user-images.githubusercontent.com/74064313/110775123-d959a680-825e-11eb-94ba-ab2173b07f02.png)


**Signup with mail**![image](https://user-images.githubusercontent.com/74064313/110775513-4705d280-825f-11eb-892b-576dde234455.png)
After signing-up you will receive an email with the link for confirming your registration. 


**Sign-in with Google**![image](https://user-images.githubusercontent.com/74064313/110775775-9946f380-825f-11eb-9fcd-d93d27ea01d1.png)

**User activated**![image](https://user-images.githubusercontent.com/74064313/110776912-d52e8880-8260-11eb-8475-7b136dc0bdf6.png)

## Login to Askdata using REST API (for getting token)
`curl --location --request POST 'https://api.askdata.com/security/domain/askdata/oauth/token' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--header 'Authorization: Basic ZmVlZDpmZWVk' \
--data-urlencode 'grant_type=password' \
--data-urlencode 'username={{youremail}}' \
--data-urlencode 'password={{yourpassword}}'`

:warning: **If you don't Askdata password or your regisrterd using Social login**: You must reset the password and request a new one!

## Select Workspace "pi_day" 
Use the API for switching workspace. Include your user token. <br />
`curl --location --request POST 'https://api.askdata.com/smartfeed/askdata/agent/switch' \
--header 'Authorization: Bearer {{token}}' \
--header 'Content-Type: application/json' \
--data-raw '{
	"agent_id":"d53912d3-5d44-460a-8a38-abb200ede4f9"
}`

You should get a response like
`{
    "id": "d53912d3-5d44-460a-8a38-abb200ede4f9",
    "domain": "d45834e9-7642-4011-9869-f942faa79e9b",
    "label": "pi day",
    "description": "Workspace for Pi Day HackParty 2021",
    "icon": "https://askdata-prod.s3.amazonaws.com/agent/pi_campus.jpg",
    "count": 0,
    "language": "en",
    "time": 1615453633400,
    "datasets": [
        {
            "id": "d3976c00-0763-4494-9ac1-140b8f8ae586-MYSQL-f97e5f82-4ed3-440d-b842-590b6e7c2f48",
            "type": "MYSQL"
        },
        {
            "id": "a87aa80c-fe00-422e-94fd-043056a13dce-MYSQL-4c9f03f2-6d3d-404b-9515-d8a937526069",
            "type": "MYSQL"
        },
        {
            "id": "f5f552d5-89a1-4f64-bb86-ed03d0d322f3-MYSQL-1f8980f4-a58f-4a14-a9ad-b424a9283faf",
            "type": "MYSQL"
        }
    ],
    "accessLevel": "READER",
    "slug": "pi_day"
}`

The referring workspace link is https://askdata.com/pi_day

## Suggestions 
`curl 'https://api.askdata.com/smartfeed/search?agentId=d53912d3-5d44-460a-8a38-abb200ede4f9&q=dec&types=QUERY,ENTITY&lang=en&browse=false' \
  -H 'authority: api.askdata.com' \
  -H 'accept: application/json, text/plain, */*' \
  -H 'authorization: Bearer 74c1b5f4-012d-45c7-b6b3-1a3f604950da' \
  -H 'user-agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/88.0.4324.192 Safari/537.36' \
  -H 'content-type: application/json' \
  -H 'origin: https://askdata.com' \
  -H 'sec-fetch-site: same-site' \
  -H 'sec-fetch-mode: cors' \
  -H 'sec-fetch-dest: empty' \
  -H 'referer: https://askdata.com/' \
  -H 'accept-language: it-IT,it;q=0.9,en-US;q=0.8,en;q=0.7' \
  --compressed`
  
  
