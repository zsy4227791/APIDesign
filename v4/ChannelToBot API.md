  | Change Version | API Version | Change nots | Change Date | Author |
  | - | - | - | - | - |
  | 4.0 | v4 | Bot API | 2021-9-8 | Leon |  
 




# Summary
  - Chatbot
    - [ChatbotSession](#chatbotsession-object)
      - [ChatbotInteraction](#chatbotinteraction-object)
        - [ChatbotInput](#chatbotinput-object) 
        - [ChatbotOutput](#chatbotoutput-object) 
          - [ChatbotResponse](#chatbotresponse-object) 


## ChatbotSession
  - `POST /bot/chatbotSessions` - [Create a new Chatbot Session](#create-a-new-chatbot-session)
   - `DELETE /bot/chatbotSessions/{id}` - [Delete the Chatbot Session](#delete-the-chatbot-session)
## ChatbotInteraction  
  - `POST /bot/chatbotSessions/{id}/interactions` - [Send a  Chatbot Input and get a Chatbot Output](#create-a-chatbot-interaction)
## ChatbotSessionVariable
  - `GET /bot/chatbotSessions/{id}/variables` - [get the variables of the Chatbot Session ](#get-the-variables)
  - `PUT /bot/chatbotSessions/{id}/variables` - [Update the variables of the Chatbot Session ](#update-the-variables)

# Endpoints

### Create A New Chatbot Session
`POST /bot/chatbotSessions`

#### Parameters
Request body

The request body contains data with the follow structure:

  | Name | Type | Required | Default | Description |    
  | - | - | :-: | :-: | - | 
  | `chatbotId` | Guid | yes | |  the unique id of the bot |
  |`visitor`  |  [Visitor](#visitor-object) Object  |no |   |  |

example:
```Json 
  {
    "chatbotId": "f9928d68-92e6-4487-a2e8-8234fc9d1f48",
    "visitor": {
        "name":"Kart",
        "email":"kart@yahoo.com",
        "phone":"123-4355-212",
      }
    }
  }
```

#### Response
The Response body contains data with the follow structure:

  | Name | Type |  Description |    
  | - | - | :-: | 
  |`sessionId` | Guid | the unique id of the session |
  |`greeting`  |  [ChatbotOutput](#chatbotoutput-object) Object    |  |


#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "chatbotId": "f9928d68-92e6-4487-a2e8-8234fc9d1f48", 
    "visitor": {
      "name":"Kart",
      "email":"kart@yahoo.com",
      "phone":"123-4355-212",
    }
  }' -X POST https://domain.comm100.com/api/v4/bot/chatbotSessions
```
Response
```Json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  {    
    "sessionId": "f9928d68-92e6-4487-a2e8-8234fc9d1f48",
    "greeting":{
          "id":"d3f5b968-ad51-42af-b759-64c0afc40b84",
          "content":[{
              "type":"chatbotActionSendMessage",
              "content":{
                      "chatbotActionSendMessageLinks": [],
                    "message": "Hi there! I'm a chatbot, here to help answer your questions.",
                    "nextActionId": "00000000-0000-0000-0000-000000000000",
                    "typingDelay": 1
              }
    }]
    }

  }
```
### Delete The Chatbot Session
`DELETE /bot/chatbotSessions/{ChatbotSessionId}`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `chatbotSessionId` | Guid | yes  |  the unique id of the Chatbot Session |  


#### Response
This method does not specify any sample responses.

#### Example
Using curl
```
curl -X DELETE https://domain.comm100.com/api/v4/bot/chatbotSessions/a9928d68-92e6-4487-a2e8-8234fc9d1f48
```
Response
```Json
  HTTP/1.1 200 OK

```

### Create a Chatbot Interaction
`POST /bot/chatbotSession/{chatbotSessionId}/interactions`

#### Parameters

Request body

The request body  is: [ChatbotInput](#chatbotinput-object) Object

example:
```Json 
  {
    "input":{
      "type":"text",
      "content":{
        "text":"i want to buy NBN"
      }
    }
  }
```

#### Response
the response is: [ChatbotOutput](#chatbotoutput-object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "input":{
      "type":"text",
      "content":{
        "text":"i want to buy NBN"
      }
    }
  }' -X POST https://domain.comm100.com/api/v4/bot/chatbotSessions/f9928d68-92e6-4487-a2e8-8234fc9d1f48/dialogs
```
Response
```Json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  { 
    "output":{
          "id":"d3f5b968-ad51-42af-b759-64c0afc40b84",
          "content":[
              {
                "type":"chatbotActionSendMessage",
                "content": {
                  "chatbotActionSendMessageLinks": [],
                  "message": "Hi there! I'm a chatbot, here to help answer your questions.",
                  "nextActionId": "00000000-0000-0000-0000-000000000000",
                  "typingDelay": 1
                }
              }
          ]
    }   
  }
```
### Get The Variables
`GET /bot/chatbotSession/{chatbotSessionId}/variables`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `chatbotSessionId` | Guid | yes  |  the unique id of the Chatbot Session |  

Request body

#### Response
  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
|`variables` |[VariableValue](#variablevalue-object)[]  | |  an array of [VariableValue](#variablevalue-object) objects  |

```Json 
  {
    "variables":[
      {
        "name":"ename",
        "value":"leon"
      }
    ]
  }
```

#### Example
Using curl
```
curl -H "Content-Type: application/json"  -X GET https://domain.comm100.com/api/v4/bot/chatbotSessions/f9928d68-92e6-4487-a2e8-8234fc9d1f48/variables
```
Response
```Json
  HTTP/1.1 200 OK
    {
    "variables":[
      {
        "name":"ename",
        "value":"leon"
      }
    ]
  }
```
### Update The Variables
`PUT /bot/chatbotSession/{chatbotSessionId}/variables`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `chatbotSessionId` | Guid | yes  |  the unique id of the Chatbot Session |  

Request body
  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
|`variables` |[VariableValue](#variablevalue-object)[]  | |  an array of [VariableValue](#variablevalue-object) objects  |
example:
```Json 
  {
    "variables":[
      {
        "name":"ename",
        "value":"leon"
      }
    ]
  }
```

#### Response


#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '  {
    "variables":[
      {
        "name":"ename",
        "value":"leon"
      }
    ]
  }' -X PUT https://domain.comm100.com/api/v4/bot/chatbotSessions/f9928d68-92e6-4487-a2e8-8234fc9d1f48/variables
```
Response
```Json
  HTTP/1.1 200 OK
```

# Model

### ChatbotSession Object
   

  |Name| Type | Default | Description | 
  | - | - | :-: | - | 
  | `id` | Guid  | | sessionId |
  | `interactions` |  [ChatbotInteraction](#chatbotinteraction-object)[] Object |  |  |
  | `context` | ChatbotSessionContext Object  |   |  |
### ChatbotInteraction Object

  |Name| Type | Default | Description | 
  | - | - | :-: | - | 
  | `id` | Guid  | | dialogId |
  | `input` |  [ChatbotInput](#chatbotinput-object) Object|  |  |
  | `output` |  [ChatbotOutput](#chatbotoutput-object) Object |  |  |
### ChatbotInput Object

  |Name| Type | Default | Description | 
  | - | - | :-: | - | 
  | `id` | Guid  | | questionId |
  | `type` | String  | | 	type of the response,including`text`,`audio`,`location`,`option`,`form`,`transferchat`|
  | `content` | object  | | [textInput](#textinput-object), [audioInput](#audioinput-object), [locationInput](#locationinput-object), [optionInput](#optioninput-object), [formInput](#forminput-object) , [Transferchat](#transferchat-object)|

  ### TextInput Object
  |Name| Type | Default | Description | 
  | - | - | :-: | - | 
  | `text` | String  | |  |
  ### AudioInput Object
  |Name| Type | Default | Description | 
  | - | - | :-: | - | 
  | `text` | String  | |  |
  | `audio` | String  | |  |
  ### LocationInput Object
  |Name| Type | Default | Description | 
  | - | - | :-: | - | 
  | `location` | String  | | the longitude and latitude of the location, e.g. "-39.900000,116.300000" |
  | `action` | string  | | submit, cancel |

  ### OptionInput Object
  |Name| Type | Default | Description | 
  | - | - | :-: | - | 
| `optionId` | String  | |optionId |
  ### FormInput Object
  |Name| Type | Default | Description | 
  | - | - | :-: | - |
  | `formValues` | [FieldValue](#FieldValue-object)[]  | |  an array of [FieldValue](#FieldValue-object) objects |
  | `formId` | Guid  | |  |
 | `action` | string  | | submit, cancel |
  ### Transferchat Object
  |Name| Type | Default | Description | 
  | - | - | :-: | - | 
  | `action` | string  | | submit, cancel |
  
### FieldValue Object

|Name| Type|  Default |  Description     |
| - | - | :-: |  - | 
|`name` | string |  | the name of a field in a form. |
|`value` | string |  | the value of a field. |
### VariableValue Object
|Name| Type|  Default |  Description     |
| - | - | :-: |  - | 
|`name` | string |  | the name of a variable in a form. |
|`value` | string |  | the value of a variable. |
### ChatbotOutput Object
  ChatbotMessage Object is represented as simple flat JSON objects with the following keys:  

  |Name| Type| Default | Description     |
  | - | - | :-: | - |
  | `id` | Guid  |  | the unique id of the response |
  | `content` | [ChatbotResponse](#chatbotresponse-object)[]|  |   |


### ChatbotResponse Object
  Response is represented as simple flat json objects with the following keys:

  |Name| Type| Default | Description     | 
  | - | - | :-: | - | 
  |`type` | string | | type of the response,including `Message`,`QuickReply`、 `Image`、`Video`、`Authentication`,`Location`,`VariableData`,`Form`,`TransferChat`|
  | `content` | object | |  response's content. when type is `Message`, it represents [Message](#message-object); when type is `QuickReply`,it represents [QuickReply](#quickreply-object);when type is `Image`,it represents [Image](#image-object);when type is `Video`,it represents [Video](#video-object); when type is `Authentication`, it represents [Authentication](#authentication-object);when type is `Location`, it represents [Location](#collectlocation-object);when type is `VariableData`, it represents [VariableData](#variabledata-object);when type is `Form`, it represents [Form](#form-object);when type is `TransferChat`, it represents [TransferChat](#transferchat-object);|
  |`delayTime` | decimal | 1 | how many seconds delay to show  |

#### Message Object
  Text Response is represented as simple flat json objects with the following keys:

  |Name| Type| Default | Description     | 
  | - | - | :-: | - | 
  |`message` | string |  | string  |
  |`chatbotActionSendMessageLinks` | [button](#button-object) object |  |   |
 #### Button Object
Text Response is represented as simple flat json objects with the following keys:

  |Name| Type| Default | Description     | 
  | - | - | :-: | - | 
  |`buttonText` | String |  |   |
  |`url` | String |  |   |
  |`type` | String |  | webPage,webview|
  |`openStyle` | String |  | full,tall,compact  |
  |`openIn` | String |  | newWindow, sideWindow,currentWindow|
  |`order` | int |  |   |
 #### QuickReply Object
Text Response is represented as simple flat json objects with the following keys:

  |Name| Type| Default | Description     | 
  | - | - | :-: | - | 
  |`isForce` | bool |  | must select and can not input  text  |
  |`message` | string |  | string  |
  |`options` | [option](#option-object) |  |   |
   #### Option Object
Text Response is represented as simple flat json objects with the following keys:

  |Name| Type| Default | Description     | 
  | - | - | :-: | - | 
  |`optionId` | Guid |  |   |
  |`order` | int |  |   |
  |`text` | String |  |   |
  |`type` | String | text |   |
#### Image Object
  Text Response is represented as simple flat json objects with the following keys:

  |Name| Type| Default | Description     | 
  | - | - | :-: | - | 
  |`imageUrl` | string |  | string  |
  |`message` | string |  | string  |
#### Video Object
  Text Response is represented as simple flat json objects with the following keys:

  |Name| Type| Default | Description     | 
  | - | - | :-: | - | 
  |`videoUrl` | string |  | string  |
  |`message` | string |  | string  |
#### Authentication Object
Text Response is represented as simple flat json objects with the following keys:

  |Name| Type| Default | Description     | 
  | - | - | :-: | - | 
  |`isForce` | bool |  | must login and can not input  text  |
  |`loginButtonText` | string |  | string  |
  |`loginUrl` | string |  | string  |
  |`message` | string |  | string  |

 #### CollectLocation Object
Text Response is represented as simple flat json objects with the following keys:

  |Name| Type| Default | Description     | 
  | - | - | :-: | - | 
  |`buttonText` | string |  | string  |
  |`isForce` | bool |  | must location and can not input  text  |
  |`message` | string |  | string  |


  #### CollectVariableData Object
Text Response is represented as simple flat json objects with the following keys:

  |Name| Type| Default | Description     | 
  | - | - | :-: | - | 
  |`isForce` | bool |  | must input variable  |
  |`message` | string |  | string  |
  |`options` | array |  |   |
  |`type` | string |  | type:`integer`,`singleselect`,`multiselect`,`text`,`textarea`，`decimal`，`email`，`password`，`date`，`time` |
  |`variableName` | string |  | string  |
  #### TransferChat Object
Text Response is represented as simple flat json objects with the following keys:

  |Name| Type| Default | Description     | 
  | - | - | :-: | - | 
  |`transferTo` | Guid |  |   |
  |`isForce` | bool |  | must transfer chat  |
  |`type` | string |  | type:`transferToAgent`,`transferToDepartment`  |

### Form Object
FormReplyResponse is represented as simple flat json objects with the following keys:

|Name| Type| Default | Description     | 
| - | - | :-: | - | 
|`message` | string |   | A separate message which is sent before the button is sent.|
|`title` | string |  | when a button is sent to visitor, clicking this button will open a form that contains information bot wants to collect from the visitor. the title refers to the title of that form, and it is also placed on the button as a name.|
|`isConfirmationRequired` | bool |   | whether visitor needs to click confirm after filling out the information in a form.|
|`fields` | [Field](#field-object)[] | | an array of [Field](#field-object) Object |
|`submitButtonText` | string |   | |
|`cancelButtonText` | string |   | |
|`confirmButtonText` | string |   | |


### Field Object
Field is represented as simple flat json objects with the following keys:

|Name| Type| Default | Description     | 
| - | - | :-: | - | 
|`type` | string | | enums: `text` ,`textArea`,`radio` ,`checkBox` ,`dropDownList` ,`checkBoxList`,`email` type refers to the different kinds of fields which can be used in a form. |
|`name` | string |  | a field’s name in a form. |
|`defaultValue` | string | | a field’s value |
|`isRequired` | bool |  | to mark whether a field in a form is required or not. |
|`isMasked` | bool |  | if this is true, visitor information will be masked with symbols in chat logs. |
|`options` | string[] |  | an array of of string when the fieldType is `radio` ,`dropDownList` ,`checkBoxList`|
|`order` | integer |  | must greater than or equal 0, ascending sort |

### Visitor Object

|Name| Type|  Default |  Description     |
| - | - | :-: |  - | 
|`name` | string |  |  |
|`email` | string |  |  |
|`phone` | string |  |  |
|`state/province` | string |  |  |
|`country/region` | string |  |  |
|`city` | string |  |  |
|`ip` | string |  |  |
|`email` | string |  |  |
|`currentPageURL` | string |  |  |
|`searchEngine` | string |  |  |
|`searchKeywords` | string |  |  |


