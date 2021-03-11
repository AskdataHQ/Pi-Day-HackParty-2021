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

WARN : If you don't Askdata password or your regisrterd using Social login, you must reset the password and request a new one.

## Select Workspace "pi_day" 
Use the API for switching workspace. Include your user token. <br />
`curl --location --request POST 'https://api.askdata.com/smartfeed/askdata/agent/switch' \
--header 'Authorization: Bearer {{token}}' \
--header 'Content-Type: application/json' \
--data-raw '{
	"agent_id":"d53912d3-5d44-460a-8a38-abb200ede4f9"
}`

The referring workspace link is https://askdata.com/pi_day
