# Pi Day HackParty 2021


Welcome to Pi Day HackParty 2021!

Follows the steps for start using Askdata. 

# Askdata quick start:

* **SignUp:** Register to [Askdata](https://app.askdata.com/login) with your own email  ⚠️  Do not use the Social Login with Google/Slack.
* **Login to Askdata using REST API:** Get the token that will be used for all the other APIs
* **Select Workspace:** Switch to the Pi Day workspace.
* **Check current Workspace:** Check your workspace is the one provided for Pi Day 2021.
* **Ask data:** Use Natural language queries for getting data.


## SignUp / Social Login 
Register to [Askdata](https://app.askdata.com/login) with your own email or signing-in with Google.

**Landing page**![image](https://user-images.githubusercontent.com/74064313/110775123-d959a680-825e-11eb-94ba-ab2173b07f02.png)


**Signup with mail**![image](https://user-images.githubusercontent.com/74064313/110775513-4705d280-825f-11eb-892b-576dde234455.png)
After signing-up you will receive an email with the link for confirming your registration. 

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
Request: <br />

`curl --location --request POST 'https://api.askdata.com/smartfeed/askdata/workspace/switch' \
--header 'Authorization: Bearer {{token}}' \
--header 'Content-Type: application/json' \
--data-raw '{
	"agent_slug":"pi_day"
}`

Response (Sample): <br />
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

## Check current Workspace
Request: <br />
`curl --location --request GET 'https://api.askdata.com/smartfeed/askdata/workspace/current' \
--header 'Authorization: Bearer 8faace67-e4f7-4bee-82dc-afeda2edc0ac' \
--header 'Content-Type: application/json' \
--data-raw`

Response: <br />
`{
    "agent": {
        "id": "d53912d3-5d44-460a-8a38-abb200ede4f9",
        "domain": "d45834e9-7642-4011-9869-f942faa79e9b",
        "label": "pi day",
        "description": "Workspace for Pi Day HackParty 2021",
        "icon": "https://askdata-prod.s3.amazonaws.com/agent/pi_campus.jpg",
        "count": 0,
        "language": "en",
        "time": 1615481787877,
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
    }
}`

The referring workspace link is https://askdata.com/pi_day
  
## Ask data 
`curl --location --request POST 'https://api.askdata.com/smartinsight/data/nl/result' \
--header 'authority: api-dev.askdata.com' \
--header 'sec-ch-ua: "Google Chrome";v="89", "Chromium";v="89", ";Not A Brand";v="99"' \
--header 'accept: application/json, text/plain, */*' \
--header 'dnt: 1' \
--header 'authorization: Bearer 8faace67-e4f7-4bee-82dc-afeda2edc0ac' \
--header 'sec-ch-ua-mobile: ?0' \
--header 'user-agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 11_2_1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/89.0.4389.72 Safari/537.36' \
--header 'origin: http://localhost:4200' \
--header 'sec-fetch-site: cross-site' \
--header 'sec-fetch-mode: cors' \
--header 'sec-fetch-dest: empty' \
--header 'referer: http://localhost:4200/' \
--header 'accept-language: en-US,en;q=0.9,ro-RO;q=0.8,ro;q=0.7' \
--header 'Content-Type: application/json' \
--header 'Cookie: JSESSIONID=9E206CE303071A4B3C86BA7E7873009B' \
--data-raw ' {"nl":"dimessi guariti denominazione regione","language":"en"}'`

  
