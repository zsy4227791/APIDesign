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
  | `channel` | string | yes | |  the channel of the bot |
  | `visitor`  |  [SessionVisitorInfo](#sessionvisitorinfo-object)  |no |   |  |

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
  |`sessionId` | string | the unique id of the session |
  |`content`  |  [GeneralResponse](#GeneralResponse-object)[]     |  |


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
    "content":[{
              "type":"text",
              "content":{
                    "links": [{
                      "buttonText":"ok",
                      "url":"http://baidu.com",
                      "type":"intent",
                      "openStyle":"tail",
                      "openIn":"sideWindow",
                      "order":1,
                    }],
                    "message": "Hi there! I'm a chatbot, here to help answer your questions.",                        
              },
              "delayTime": 1   
    }]
  }
```
### Delete The Chatbot Session
`DELETE /bot/chatbotSessions/{ChatbotSessionId}`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `chatbotSessionId` | string | yes  |  the unique id of the Chatbot Session |  


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
                "type":"text",
                "content": {
                    "links": [{
                      "buttonText":"ok",
                      "url":"http://baidu.com",
                      "type":"intent",
                      "openStyle":"tail",
                      "openIn":"sideWindow",
                      "order":1,
                    }],
                    "message": "Hi there! I'm a chatbot, here to help answer your questions.",                        
              },
                "delaytime":1
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
|`variables` |[VariableValue](#variablevalue-object)[]  | |  an array of [VariableValue](#variablevalue-object)  |

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
|`variables` |[VariableValue](#variablevalue-object)[]  | |  an array of [VariableValue](#variablevalue-object)  |
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
### CreateChatbotSessionRequest Object
   

  |Name| Type | Default | Description | 
  | - | - | :-: | - | 
  | `chatbotId` | Guid  | | chatbotId |  
  | `channel` | string  | | including`Live Chat`,`Facebook Messager`,`Twitter Direct Message`,`WeChat`,`WhatsApp`,`IVR`,`SMS`,`Default` | 
  | `visitor` | [SessionVisitorInfo](#sessionvisitorinfo-object)  |   |  |

### CreateChatbotSessionResponse Object
   

  |Name| Type | Default | Description | 
  | - | - | :-: | - | 
  | `sessionId` | string  | | sessionId |  
  | `content` | [GeneralResponse](#generalResponse-object)[]  |   |  |
### InteractionRequest Object

  |Name| Type | Default | Description | 
  | - | - | :-: | - |   
  | `input` |  [ChatbotInput](#chatbotinput-object)|  |  |  
### InteractionResponse Object

  |Name| Type | Default | Description | 
  | - | - | :-: | - |     
  | `output` |  [ChatbotOutput](#chatbotoutput-object)|  |  |

### ChatbotInput Object

  |Name| Type | Default | Description | 
  | - | - | :-: | - |   
  | `type` | String  | | 	type of the response,including`text`,`audio`,`location`,`option`,`form`,`transferchat`|
  | `content` | object  | | [InputText](#inputText-object), [InputAudio](#inputAudio-object), [InputLocation](#inputLocation-object), [InputOption](#inputOption-object), [InputForm](#inputForm-object) , [InputTransferChat](#inputTransferChat-object)|

  ### InputText Object
  |Name| Type | Default | Description | 
  | - | - | :-: | - | 
  | `text` | String  | |  |
  ### InputAudio Object
  |Name| Type | Default | Description | 
  | - | - | :-: | - | 
  | `text` | String  | |  |
  | `audio` | String  | |  |
  ### InputLocation Object
  |Name| Type | Default | Description | 
  | - | - | :-: | - | 
  | `location` | String  | | the longitude and latitude of the location, e.g. "-39.900000,116.300000" |
  | `action` | string  | | submit, cancel |

  ### InputOption Object
  |Name| Type | Default | Description | 
  | - | - | :-: | - | 
  | `optionId` | String  | |optionId |
  ### InputForm Object
  |Name| Type | Default | Description | 
  | - | - | :-: | - |
  | `formValues` | [FieldValue](#FieldValue-object)[]  | |  an array of [FieldValue](#FieldValue-object) |
  | `formId` | Guid  | |  |
  | `action` | string  | | submit, cancel |
  ### InputTransferChat Object
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
  | `content` | [GeneralResponse](#generalResponse-object)[]|  |   |


### GeneralResponse Object
  Response is represented as simple flat json objects with the following keys:

  |Name| Type| Default | Description     | 
  | - | - | :-: | - | 
  |`type` | string | | type of the response,including `Text`,`QuickReply`、 `Image`、`Video`、`Authentication`,`Location`,`VariableData`,`Form`,`TransferChat`|
  | `content` | object | |  response's content. when type is `Text`, it represents [OutputText](#outputtext-object); when type is `QuickReply`,it represents [OutputQuickReply](#outputquickreply-object);when type is `Image`,it represents [OutputImage](#outputimage-object);when type is `Video`,it represents [OutputVideo](#outputvideo-object); when type is `Authentication`, it represents [OutputAuthentication](#outputauthentication-object);when type is `Location`, it represents [OutputLocation](#outputLocation-object);when type is `VariableData`, it represents [OutputVariableData](#outputvariabledata-object);when type is `Form`, it represents [OutputForm](#form-object);when type is `TransferChat`, it represents [OutputTransferChat](#transferchat-object);|
  |`delayTime` | decimal | 1 | how many seconds delay to show  |

### OutputText Object
  Text Response is represented as simple flat json objects with the following keys:

  |Name| Type| Default | Description     | 
  | - | - | :-: | - | 
  |`message` | string |  | string  |
  |`Links` | [TextLink](#textLink-object)[]|  |   |
 #### TextLink Object
Text Response is represented as simple flat json objects with the following keys:

  |Name| Type| Default | Description     | 
  | - | - | :-: | - | 
  |`buttonText` | String |  |   |
  |`url` | String |  |   |
  |`type` | String |  | webPage,webview|
  |`openStyle` | String |  | full,tall,compact  |
  |`openIn` | String |  | newWindow, sideWindow,currentWindow|
  |`order` | int |  |   |
 ### OutputQuickReply Object
Text Response is represented as simple flat json objects with the following keys:

  |Name| Type| Default | Description     | 
  | - | - | :-: | - |   
  |`message` | string |  | string  |
  |`options` | [option](#option-object)[] |  |   |
  |`isForce` | bool |  | must select and can not input  text  |
   
### OutputImage Object
  Text Response is represented as simple flat json objects with the following keys:

  |Name| Type| Default | Description     | 
  | - | - | :-: | - | 
  |`imageUrl` | string |  | string  |
  |`message` | string |  | string  |
### OutputVideo Object
  Text Response is represented as simple flat json objects with the following keys:

  |Name| Type| Default | Description     | 
  | - | - | :-: | - | 
  |`videoUrl` | string |  | string  |
  |`message` | string |  | string  |
### OutputAuthentication Object
Text Response is represented as simple flat json objects with the following keys:

  |Name| Type| Default | Description     | 
  | - | - | :-: | - | 
  |`isForce` | bool |  | must login and can not input  text  |
  |`loginButtonText` | string |  | string  |
  |`loginUrl` | string |  | string  |
  |`message` | string |  | string  |

 ### OutputLocation Object
Text Response is represented as simple flat json objects with the following keys:

  |Name| Type| Default | Description     | 
  | - | - | :-: | - | 
  |`buttonText` | string |  | string  |
  |`isForce` | bool |  | must location and can not input  text  |
  |`message` | string |  | string  |


  ### OutputVariableData Object
Text Response is represented as simple flat json objects with the following keys:

  |Name| Type| Default | Description     | 
  | - | - | :-: | - | 
  |`isForce` | bool |  | must input variable  |
  |`message` | string |  | string  |
  |`options` | [option](#option-object)[] |  |   |
  |`type` | string |  | type:`text`,`textarea`,`singleselect`,`checkbox`,`multiselect`,`email`,`password`,`date`，`time` ,`integer`,`decimal`|
  |`variableName` | string |  | string  |
  ### OutputTransferChat Object
Text Response is represented as simple flat json objects with the following keys:

  |Name| Type| Default | Description     | 
  | - | - | :-: | - | 
  |`transferTo` | Guid |  |   |
  |`isForce` | bool |  | must transfer chat  |
  |`type` | string |  | type:`transferToAgent`,`transferToDepartment`,`transferRoutingRules`  |

### OutputForm Object
FormReplyResponse is represented as simple flat json objects with the following keys:

|Name| Type| Default | Description     | 
| - | - | :-: | - | 
|`message` | string |   | A separate message which is sent before the button is sent.|
|`title` | string |  | when a button is sent to visitor, clicking this button will open a form that contains information bot wants to collect from the visitor. the title refers to the title of that form, and it is also placed on the button as a name.|
|`isConfirmationRequired` | bool |   | whether visitor needs to click confirm after filling out the information in a form.|
|`fields` | [ChatbotActionSendFormField](#ChatbotActionSendFormField-object)[] | | an array of [ChatbotActionSendFormField](#ChatbotActionSendFormField-object)  |
|`submitButtonText` | string |   | |
|`cancelButtonText` | string |   | |
|`confirmButtonText` | string |   | |
|`isforce` | string |   | |


#### ChatbotActionSendFormField Object
Field is represented as simple flat json objects with the following keys:

|Name| Type| Default | Description     | 
| - | - | :-: | - | 
|`type` | string | | enums: `text` ,`textArea`,`radio` ,`checkBox` ,`dropDownList` ,`checkBoxList`,`email` type refers to the different kinds of fields which can be used in a form. |
|`name` | string |  | a field’s name in a form. |
|`value` | string | | a field’s value |
|`isRequired` | bool |  | to mark whether a field in a form is required or not. |
|`isMasked` | bool |  | if this is true, visitor information will be masked with symbols in chat logs. |
|`options` | string[] |  | an array of of string when the fieldType is `radio` ,`dropDownList` ,`checkBoxList`|
|`order` | integer |  | must greater than or equal 0, ascending sort |
|`variableName` | string |  |  |

### Option Object
Text Response is represented as simple flat json objects with the following keys:

  |Name| Type| Default | Description     | 
  | - | - | :-: | - | 
  |`optionId` | Guid |  |   |
  |`order` | int |  |   |
  |`text` | String |  |   |
  |`type` | String | text | type of the option,including `TriggerAnIntent`,`ContactAnAgent`、 `Text`  |
### SessionVisitorInfo Object

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
|`longitude` | number |  |  |
|`latitude` | number |  |  |
|`pageViews` | integer |  |  |
|`browser` | integer |  |  |
|`chats` | integer |  |  |
|`company` | string |  |  |
|`currentBrowsing` | string |  |  |
|`department` | string |  |  |
|`firstVisitTime` | time |  |  |
|`flashVersion` | string |  |  |
|`keywords` | string |  |  |
|`landingPage` | string |  |  |
|`language` | string |  |  |
|`operatingSystem` | string |  |  |
|`productService` | string |  |  |
|`ticketId` | string |  |  |
|`referrerUrl` | string |  |  |
|`screenResolution` | string |  |  |
|`searchEngine` | string |  |  |
|`state` | string |  |  |
|`status` | integer |  |  |
|`timeZone` | string |  |  |
|`visitTime` | time |  |  |
|`visits` | integer |  |  |
|`ssoId` | integer |  |  |
|`chatRequestingPageUrl` | integer |  |  |
|`campaignId` | string |  |  |
|`channelAccountId` | string |  |  |


