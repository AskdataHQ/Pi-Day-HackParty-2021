# Pi Day HackParty 2021


Welcome to Pi Day HackParty 2021!

Follows the steps for start using Askdata. 

# Askdata quick start:

* **SignUp:** Register to [Askdata](https://app.askdata.com/login) with your own email  ⚠️  Do not use the Social Login with Google/Slack.
* **Login to Askdata using REST API:** Get the token that will be used for all the other APIs
* **Select Workspace:** Switch to the Pi Day workspace.
* **Check current Workspace:** Check your workspace is the one provided for Pi Day 2021.
* **Ask data:** Use Natural language queries for getting data.
* **Sample queries:** Explore datasets starting from some sample queries


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
--data-raw ' {"nl":"dimessi guariti denominazione regione","language":"en"}'
```

Response (Sample): <br />
```json
{
    "id": null,
    "dataset": {
        "id": "a87aa80c-fe00-422e-94fd-043056a13dce-MYSQL-4c9f03f2-6d3d-404b-9515-d8a937526069",
        "name": "Dati regionali",
        "icon": "https://askdata-prod.s3.amazonaws.com/dataset/d_ProtezioneCivile%20%281%29.png"
    },
    "connection": "",
    "executedSQLQuery": "SELECT `denominazione_regione`, SUM(`variazione_dimessi_guariti`) AS `variazione_dimessi_guariti` FROM `innaas-dev`.covid_it_regione WHERE `data` = '2021-03-11T17:00:00' GROUP BY `denominazione_regione` ORDER BY `variazione_dimessi_guariti` DESC",
    "schema": [
        {
            "id": "a87aa80c-fe00-422e-94fd-043056a13dce-ENTITY_TYPE-DENOMINAZIONE_REGIONE",
            "dataset": "a87aa80c-fe00-422e-94fd-043056a13dce-MYSQL-4c9f03f2-6d3d-404b-9515-d8a937526069",
            "type": "ENTITY_TYPE",
            "code": "DENOMINAZIONE_REGIONE",
            "name": "Denominazione regione",
            "aggregation": "",
            "icon": null,
            "format": "",
            "locale": "",
            "dataType": "text",
            "internalDataType": "STRING",
            "measurementUnit": null,
            "searchable": false,
            "measure": false,
            "dimension": true
        },
        {
            "id": "a87aa80c-fe00-422e-94fd-043056a13dce-MEASURE-VARIAZIONE_DIMESSI_GUARITI",
            "dataset": "a87aa80c-fe00-422e-94fd-043056a13dce-MYSQL-4c9f03f2-6d3d-404b-9515-d8a937526069",
            "type": "MEASURE",
            "code": "VARIAZIONE_DIMESSI_GUARITI",
            "name": "Variazione dimessi guariti",
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
                    "rawValue": "Lombardia",
                    "value": "Lombardia"
                },
                {
                    "rawValue": "2,167",
                    "value": "2,167"
                }
            ]
        },
        {
            "cells": [
                {
                    "rawValue": "Campania",
                    "value": "Campania"
                },
                {
                    "rawValue": "1,674",
                    "value": "1,674"
                }
            ]
        },
        {
            "cells": [
                {
                    "rawValue": "Emilia-Romagna",
                    "value": "Emilia Romagna"
                },
                {
                    "rawValue": "1,558",
                    "value": "1,558"
                }
            ]
        },
        {
            "cells": [
                {
                    "rawValue": "Lazio",
                    "value": "Lazio"
                },
                {
                    "rawValue": "1,322",
                    "value": "1,322"
                }
            ]
        },
        {
            "cells": [
                {
                    "rawValue": "Puglia",
                    "value": "Puglia"
                },
                {
                    "rawValue": "1,226",
                    "value": "1,226"
                }
            ]
        },
        {
            "cells": [
                {
                    "rawValue": "Piemonte",
                    "value": "Piemonte"
                },
                {
                    "rawValue": "952",
                    "value": "952"
                }
            ]
        },
        {
            "cells": [
                {
                    "rawValue": "Abruzzo",
                    "value": "Abruzzo"
                },
                {
                    "rawValue": "906",
                    "value": "906"
                }
            ]
        },
        {
            "cells": [
                {
                    "rawValue": "Toscana",
                    "value": "Toscana"
                },
                {
                    "rawValue": "882",
                    "value": "882"
                }
            ]
        },
        {
            "cells": [
                {
                    "rawValue": "Sicilia",
                    "value": "Sicilia"
                },
                {
                    "rawValue": "813",
                    "value": "813"
                }
            ]
        },
        {
            "cells": [
                {
                    "rawValue": "Veneto",
                    "value": "Veneto"
                },
                {
                    "rawValue": "769",
                    "value": "769"
                }
            ]
        },
        {
            "cells": [
                {
                    "rawValue": "Marche",
                    "value": "Marche"
                },
                {
                    "rawValue": "724",
                    "value": "724"
                }
            ]
        },
        {
            "cells": [
                {
                    "rawValue": "Friuli Venezia Giulia",
                    "value": "Friuli Venezia Giulia"
                },
                {
                    "rawValue": "472",
                    "value": "472"
                }
            ]
        },
        {
            "cells": [
                {
                    "rawValue": "Liguria",
                    "value": "Liguria"
                },
                {
                    "rawValue": "355",
                    "value": "355"
                }
            ]
        },
        {
            "cells": [
                {
                    "rawValue": "Umbria",
                    "value": "Umbria"
                },
                {
                    "rawValue": "322",
                    "value": "322"
                }
            ]
        },
        {
            "cells": [
                {
                    "rawValue": "P.A. Bolzano",
                    "value": "P.A. Bolzano"
                },
                {
                    "rawValue": "285",
                    "value": "285"
                }
            ]
        },
        {
            "cells": [
                {
                    "rawValue": "P.A. Trento",
                    "value": "P.A. Trento"
                },
                {
                    "rawValue": "252",
                    "value": "252"
                }
            ]
        },
        {
            "cells": [
                {
                    "rawValue": "Molise",
                    "value": "Molise"
                },
                {
                    "rawValue": "102",
                    "value": "102"
                }
            ]
        },
        {
            "cells": [
                {
                    "rawValue": "Calabria",
                    "value": "Calabria"
                },
                {
                    "rawValue": "92",
                    "value": "92"
                }
            ]
        },
        {
            "cells": [
                {
                    "rawValue": "Basilicata",
                    "value": "Basilicata"
                },
                {
                    "rawValue": "73",
                    "value": "73"
                }
            ]
        },
        {
            "cells": [
                {
                    "rawValue": "Sardegna",
                    "value": "Sardegna"
                },
                {
                    "rawValue": "43",
                    "value": "43"
                }
            ]
        },
        {
            "cells": [
                {
                    "rawValue": "Valle d'Aosta",
                    "value": "Valle d'Aosta"
                },
                {
                    "rawValue": "11",
                    "value": "11"
                }
            ]
        }
    ],
    "filters": null,
    "sortedBy": null,
    "page": 0,
    "limit": 1000,
    "totalRecords": 21,
    "queryId": "q1"
}
```

## HINT: Sample queries
- Total cases by state
- Total cases by county
- Total deaths by country as map
- Total Deaths
- Total Deaths split by months
- Total Deaths february 2021;

