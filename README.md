# Pi Day HackParty 2021


Welcome to Pi Day HackParty 2021!

Follows the steps for start using Askdata. 

# Askdata quick start:

* **1. SignUp:** Register to [Askdata](https://app.askdata.com/login) with your own email  ⚠️  Do not use the Social Login with Google/Slack.
* **2. Login to Askdata using REST API:** Get the token that will be used for all the other APIs
* **3. Select Workspace:** Switch to the Pi Day workspace.
* **4. Check current Workspace:** Check your workspace is the one provided for Pi Day 2021.
* **5. How to ask data:** Use Natural language queries for getting data.
* **HINT: Sample queries**


## SignUp
Register to [Askdata](https://app.askdata.com/login) with your own email or signing-in with Google.

**Landing page**![image](https://user-images.githubusercontent.com/74064313/110775123-d959a680-825e-11eb-94ba-ab2173b07f02.png)

**Signup with mail**![image](https://user-images.githubusercontent.com/74064313/110775513-4705d280-825f-11eb-892b-576dde234455.png)
After signing-up you will receive an email with the link for confirming your registration. 

**User activated**![image](https://user-images.githubusercontent.com/74064313/110776912-d52e8880-8260-11eb-8475-7b136dc0bdf6.png)

## Login to Askdata using REST API (for getting token)
Request: <br />
```bash
curl --location --request POST 'https://api.askdata.com/security/domain/askdata/oauth/token' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--header 'Authorization: Basic ZmVlZDpmZWVk' \
--data-urlencode 'grant_type=password' \
--data-urlencode 'username={{youremail}}' \
--data-urlencode 'password={{yourpassword}}'
```

:warning: **If you don't Askdata password or your regisrterd using Social login**: You must reset the password and request a new one!

Response: <br />
```json
{
    "access_token": "{{token}}",
    "token_type": "bearer",
    "refresh_token": "xxxxx",
    "expires_in": 2629799,
    "scope": "write openid read"
}
```

## Select Workspace "pi_day" 
Use the API for switching workspace. Include your user token. <br />
Request: <br />
```bash
curl --location --request POST 'https://api.askdata.com/smartfeed/askdata/workspace/switch' \
--header 'Authorization: Bearer {{token}}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "agent_slug": "pi_day"
}'
```

Response: <br />
```json
{
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
}
```

## Check current Workspace
Request: <br />
```bash
curl --location --request GET 'https://api.askdata.com/smartfeed/askdata/workspace/current' \
--header 'Authorization: Bearer {{token}}' \
--header 'Content-Type: application/json' \
--data-raw
```

Response: <br />
```json
{
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
}
```

The referring workspace link is https://askdata.com/pi_day
  
## Ask data 
Request: <br />
```bash
curl --location --request POST 'https://api.askdata.com/smartinsight/data/nl/result' \
--header 'authorization: Bearer {{token}}' \
--header 'Content-Type: application/json' \
--data-raw ' {"nl":"Total cases by state","language":"en"}'
```

Response (Sample): <br />
```json
{
    "id": null,
    "dataset": {
        "id": "d3976c00-0763-4494-9ac1-140b8f8ae586-MYSQL-f97e5f82-4ed3-440d-b842-590b6e7c2f48",
        "name": "Covid-19 US Counties",
        "icon": "https://askdata-prod.s3.amazonaws.com/dataset/gjkVMelR_400x400.png"
    },
    "connection": "",
    "executedSQLQuery": "SELECT `state`, SUM(`cases`) AS `cases` FROM `innaas-dev`.covid_us_counties WHERE `date` = '2021-03-10' GROUP BY `state` ORDER BY `cases` DESC",
    "schema": [
        {
            "id": "d3976c00-0763-4494-9ac1-140b8f8ae586-ENTITY_TYPE-STATE",
            "dataset": "d3976c00-0763-4494-9ac1-140b8f8ae586-MYSQL-f97e5f82-4ed3-440d-b842-590b6e7c2f48",
            "type": "ENTITY_TYPE",
            "code": "STATE",
            "name": "State",
            "aggregation": "",
            "icon": null,
            "format": "",
            "locale": "",
            "dataType": "text",
            "internalDataType": "STRING",
            "measurementUnit": null,
            "searchable": true,
            "measure": false,
            "dimension": true
        },
        {
            "id": "d3976c00-0763-4494-9ac1-140b8f8ae586-MEASURE-CASES",
            "dataset": "d3976c00-0763-4494-9ac1-140b8f8ae586-MYSQL-f97e5f82-4ed3-440d-b842-590b6e7c2f48",
            "type": "MEASURE",
            "code": "CASES",
            "name": "Total Cases",
            "aggregation": "SUM",
            "icon": null,
            "format": "###,##0",
            "locale": "en",
            "dataType": "bigint",
            "internalDataType": "NUMERIC",
            "measurementUnit": null,
            "searchable": false,
            "measure": true,
            "dimension": false
        }
    ],
    "data": [
        {
            "cells": [
                {
                    "rawValue": "California",
                    "value": "California"
                },
                {
                    "rawValue": "3,611,008",
                    "value": "3,611,008"
                }
            ]
        },
        {
            "cells": [
                {
                    "rawValue": "Texas",
                    "value": "Texas"
                },
                {
                    "rawValue": "2,710,622",
                    "value": "2,710,622"
                }
            ]
        },
        {
            "cells": [
                {
                    "rawValue": "Florida",
                    "value": "Florida"
                },
                {
                    "rawValue": "1,957,578",
                    "value": "1,957,578"
                }
            ]
        },
        {
            "cells": [
                {
                    "rawValue": "New York",
                    "value": "New York"
                },
                {
                    "rawValue": "1,713,287",
                    "value": "1,713,287"
                }
            ]
        },
        {
            "cells": [
                {
                    "rawValue": "Illinois",
                    "value": "Illinois"
                },
                {
                    "rawValue": "1,206,362",
                    "value": "1,206,362"
                }
            ]
        },
        {
            "cells": [
                {
                    "rawValue": "Georgia",
                    "value": "Georgia"
                },
                {
                    "rawValue": "1,003,181",
                    "value": "1,003,181"
                }
            ]
        },
        {
            "cells": [
                {
                    "rawValue": "Ohio",
                    "value": "Ohio"
                },
                {
                    "rawValue": "983,487",
                    "value": "983,487"
                }
            ]
        },
        {
            "cells": [
                {
                    "rawValue": "Pennsylvania",
                    "value": "Pennsylvania"
                },
                {
                    "rawValue": "960,877",
                    "value": "960,877"
                }
            ]
        },
        {
            "cells": [
                {
                    "rawValue": "North Carolina",
                    "value": "North Carolina"
                },
                {
                    "rawValue": "882,489",
                    "value": "882,489"
                }
            ]
        },
        {
            "cells": [
                {
                    "rawValue": "Arizona",
                    "value": "Arizona"
                },
                {
                    "rawValue": "828,630",
                    "value": "828,630"
                }
            ]
        },
        {
            "cells": [
                {
                    "rawValue": "New Jersey",
                    "value": "New Jersey"
                },
                {
                    "rawValue": "822,817",
                    "value": "822,817"
                }
            ]
        },
        {
            "cells": [
                {
                    "rawValue": "Tennessee",
                    "value": "Tennessee"
                },
                {
                    "rawValue": "772,634",
                    "value": "772,634"
                }
            ]
        },
        {
            "cells": [
                {
                    "rawValue": "Indiana",
                    "value": "Indiana"
                },
                {
                    "rawValue": "672,439",
                    "value": "672,439"
                }
            ]
        },
        {
            "cells": [
                {
                    "rawValue": "Michigan",
                    "value": "Michigan"
                },
                {
                    "rawValue": "662,553",
                    "value": "662,553"
                }
            ]
        },
        {
            "cells": [
                {
                    "rawValue": "Wisconsin",
                    "value": "Wisconsin"
                },
                {
                    "rawValue": "623,150",
                    "value": "623,150"
                }
            ]
        },
        {
            "cells": [
                {
                    "rawValue": "Massachusetts",
                    "value": "Massachusetts"
                },
                {
                    "rawValue": "595,264",
                    "value": "595,264"
                }
            ]
        },
        {
            "cells": [
                {
                    "rawValue": "Virginia",
                    "value": "Virginia"
                },
                {
                    "rawValue": "589,375",
                    "value": "589,375"
                }
            ]
        },
        {
            "cells": [
                {
                    "rawValue": "Missouri",
                    "value": "Missouri"
                },
                {
                    "rawValue": "572,148",
                    "value": "572,148"
                }
            ]
        },
        {
            "cells": [
                {
                    "rawValue": "South Carolina",
                    "value": "South Carolina"
                },
                {
                    "rawValue": "528,473",
                    "value": "528,473"
                }
            ]
        },
        {
            "cells": [
                {
                    "rawValue": "Alabama",
                    "value": "Alabama"
                },
                {
                    "rawValue": "501,398",
                    "value": "501,398"
                }
            ]
        },
        {
            "cells": [
                {
                    "rawValue": "Minnesota",
                    "value": "Minnesota"
                },
                {
                    "rawValue": "493,081",
                    "value": "493,081"
                }
            ]
        },
        {
            "cells": [
                {
                    "rawValue": "Colorado",
                    "value": "Colorado"
                },
                {
                    "rawValue": "441,611",
                    "value": "441,611"
                }
            ]
        },
        {
            "cells": [
                {
                    "rawValue": "Louisiana",
                    "value": "Louisiana"
                },
                {
                    "rawValue": "435,514",
                    "value": "435,514"
                }
            ]
        },
        {
            "cells": [
                {
                    "rawValue": "Oklahoma",
                    "value": "Oklahoma"
                },
                {
                    "rawValue": "430,250",
                    "value": "430,250"
                }
            ]
        },
        {
            "cells": [
                {
                    "rawValue": "Kentucky",
                    "value": "Kentucky"
                },
                {
                    "rawValue": "416,402",
                    "value": "416,402"
                }
            ]
        },
        {
            "cells": [
                {
                    "rawValue": "Maryland",
                    "value": "Maryland"
                },
                {
                    "rawValue": "389,748",
                    "value": "389,748"
                }
            ]
        },
        {
            "cells": [
                {
                    "rawValue": "Utah",
                    "value": "Utah"
                },
                {
                    "rawValue": "376,327",
                    "value": "376,327"
                }
            ]
        },
        {
            "cells": [
                {
                    "rawValue": "Washington",
                    "value": "Washington"
                },
                {
                    "rawValue": "349,881",
                    "value": "349,881"
                }
            ]
        },
        {
            "cells": [
                {
                    "rawValue": "Iowa",
                    "value": "Iowa"
                },
                {
                    "rawValue": "341,378",
                    "value": "341,378"
                }
            ]
        },
        {
            "cells": [
                {
                    "rawValue": "Arkansas",
                    "value": "Arkansas"
                },
                {
                    "rawValue": "325,700",
                    "value": "325,700"
                }
            ]
        },
        {
            "cells": [
                {
                    "rawValue": "Kansas",
                    "value": "Kansas"
                },
                {
                    "rawValue": "300,261",
                    "value": "300,261"
                }
            ]
        },
        {
            "cells": [
                {
                    "rawValue": "Mississippi",
                    "value": "Mississippi"
                },
                {
                    "rawValue": "298,445",
                    "value": "298,445"
                }
            ]
        },
        {
            "cells": [
                {
                    "rawValue": "Nevada",
                    "value": "Nevada"
                },
                {
                    "rawValue": "297,216",
                    "value": "297,216"
                }
            ]
        },
        {
            "cells": [
                {
                    "rawValue": "Connecticut",
                    "value": "Connecticut"
                },
                {
                    "rawValue": "288,657",
                    "value": "288,657"
                }
            ]
        },
        {
            "cells": [
                {
                    "rawValue": "Nebraska",
                    "value": "Nebraska"
                },
                {
                    "rawValue": "204,144",
                    "value": "204,144"
                }
            ]
        },
        {
            "cells": [
                {
                    "rawValue": "New Mexico",
                    "value": "New Mexico"
                },
                {
                    "rawValue": "187,487",
                    "value": "187,487"
                }
            ]
        },
        {
            "cells": [
                {
                    "rawValue": "Idaho",
                    "value": "Idaho"
                },
                {
                    "rawValue": "174,381",
                    "value": "174,381"
                }
            ]
        },
        {
            "cells": [
                {
                    "rawValue": "Oregon",
                    "value": "Oregon"
                },
                {
                    "rawValue": "158,360",
                    "value": "158,360"
                }
            ]
        },
        {
            "cells": [
                {
                    "rawValue": "Puerto Rico",
                    "value": "Puerto Rico"
                },
                {
                    "rawValue": "135,666",
                    "value": "135,666"
                }
            ]
        },
        {
            "cells": [
                {
                    "rawValue": "West Virginia",
                    "value": "West Virginia"
                },
                {
                    "rawValue": "134,158",
                    "value": "134,158"
                }
            ]
        },
        {
            "cells": [
                {
                    "rawValue": "Rhode Island",
                    "value": "Rhode Island"
                },
                {
                    "rawValue": "129,595",
                    "value": "129,595"
                }
            ]
        },
        {
            "cells": [
                {
                    "rawValue": "South Dakota",
                    "value": "South Dakota"
                },
                {
                    "rawValue": "113,962",
                    "value": "113,962"
                }
            ]
        },
        {
            "cells": [
                {
                    "rawValue": "Montana",
                    "value": "Montana"
                },
                {
                    "rawValue": "101,374",
                    "value": "101,374"
                }
            ]
        },
        {
            "cells": [
                {
                    "rawValue": "North Dakota",
                    "value": "North Dakota"
                },
                {
                    "rawValue": "100,645",
                    "value": "100,645"
                }
            ]
        },
        {
            "cells": [
                {
                    "rawValue": "Delaware",
                    "value": "Delaware"
                },
                {
                    "rawValue": "88,891",
                    "value": "88,891"
                }
            ]
        },
        {
            "cells": [
                {
                    "rawValue": "New Hampshire",
                    "value": "New Hampshire"
                },
                {
                    "rawValue": "77,463",
                    "value": "77,463"
                }
            ]
        },
        {
            "cells": [
                {
                    "rawValue": "Alaska",
                    "value": "Alaska"
                },
                {
                    "rawValue": "59,451",
                    "value": "59,451"
                }
            ]
        },
        {
            "cells": [
                {
                    "rawValue": "Wyoming",
                    "value": "Wyoming"
                },
                {
                    "rawValue": "55,014",
                    "value": "55,014"
                }
            ]
        },
        {
            "cells": [
                {
                    "rawValue": "Maine",
                    "value": "Maine"
                },
                {
                    "rawValue": "46,254",
                    "value": "46,254"
                }
            ]
        },
        {
            "cells": [
                {
                    "rawValue": "District of Columbia",
                    "value": "District of Columbia"
                },
                {
                    "rawValue": "42,006",
                    "value": "42,006"
                }
            ]
        },
        {
            "cells": [
                {
                    "rawValue": "Hawaii",
                    "value": "Hawaii"
                },
                {
                    "rawValue": "27,944",
                    "value": "27,944"
                }
            ]
        },
        {
            "cells": [
                {
                    "rawValue": "Vermont",
                    "value": "Vermont"
                },
                {
                    "rawValue": "16,371",
                    "value": "16,371"
                }
            ]
        },
        {
            "cells": [
                {
                    "rawValue": "Guam",
                    "value": "Guam"
                },
                {
                    "rawValue": "8,725",
                    "value": "8,725"
                }
            ]
        },
        {
            "cells": [
                {
                    "rawValue": "Virgin Islands",
                    "value": "Virgin Islands"
                },
                {
                    "rawValue": "2,755",
                    "value": "2,755"
                }
            ]
        },
        {
            "cells": [
                {
                    "rawValue": "Northern Mariana Islands",
                    "value": "Northern Mariana Islands"
                },
                {
                    "rawValue": "146",
                    "value": "146"
                }
            ]
        }
    ],
    "filters": null,
    "sortedBy": null,
    "page": 0,
    "limit": 1000,
    "totalRecords": 55,
    "queryId": "q1"
}
```

## HINT: Sample queries
- Total cases by state
- Total cases by county // you'll get also the lat and long data for being used in maps
- Total deaths by country as map
- Total Deaths
- Total Deaths split by months
- Total Deaths february 2021

