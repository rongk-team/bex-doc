# overview
API provides public functions to accept requests which come from business systems to delivery messages to users of specific tags. 

API saves requests as tasks and dispatch them to process units.


# API list

## push
Add a task to delivery messages to users of specific tags

### URL
/push


### Method
POST

#### Request parameters

| Param   | Required | Type | Descscription |
|---------|:--------:|:----:|:---------------|
| accessToken | true | String | an access token to verity caller |
| message| true | String | user-defined text that will be deliveried to users. |
| tag | optinal | String | leave it blank for delivery messages to all users, otherwise set a tag name or a formula of tags for calculations of union / intersection / complement.    |
| timing | false | Long | leave it blank for delivery messages ASAP, otherwise to specify a time (in seconds) to do.  |

#### Response properties

| Param   | Type |  Descscription |
|---------|:----:|:---------------|
| taskId | String | Task ID could be used to retrieve task status.  |


## Retrieve information of a specific task
Retrieve a specific task.

### URL
/task/{taskId}


### Method
GET

#### Request parameters

| Param   | Required | Type | Descscription |
|---------|:--------:|:----:|:---------------|
| accessToken | true | String | an access token to verity caller |
| taskId| true | String | to indicate which task to retrieve status of|

#### Response properties

| Param   | Type |  Descscription |
|---------|:----:|:---------------|
| status | String | Available status are - pending, processing, finished, cancelled |
| timing | Long | [Optional] the time in seconds to delivery message. |

## Update task status
Update the status of a task. There is only one operation is allowed - to cancel a task.

### URL
/task/{taskId}/status


### Method
UPDATE

#### Request parameters

| Param   | Required | Type | Descscription |
|---------|:--------:|:----:|:---------------|
| accessToken | true | String | an access token to verity caller |
| taskId| true | String | to indicate which task to retrieve status of|
| status| true | String | Available value: cancelled|

#### Response properties

| Param   | Type |  Descscription |
|---------|:----:|:---------------|
| result | Boolean | true \| false |


