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
  - `POST /bot/chatbotSessions/{id}/interactions` - [Send a  Chatbot Input and get a Chatbot ](#create-a-chatbot-interaction)


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
  |`greeting`  |  [ChatbotAnswer](#chatbotanswer-object) Object    |  |


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
    "sessionid": "f9928d68-92e6-4487-a2e8-8234fc9d1f48",
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
    "textInput":"i want to buy NBN"
  }
```

#### Response
the response is: [ChatbotOutput](#chatbotoutput-object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "textInput":"i want to buy NBN"
  }' -X POST https://domain.comm100.com/api/v4/bot/chatbotSessions/f9928d68-92e6-4487-a2e8-8234fc9d1f48/dialogs
```
Response
```Json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  {    
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
  | `type` | String  | | 	type of the response,including`text`,`audio`,`location`,`form`,`option` |
  | `content` | object  | | [textInput](#textinput-object), [audioInput](#audioinput-object), [locationInput](#locationinput-object), [optionInput](#optioninput-object), [formInput](#forminput-object),  |

  ### TextInput Object
  |Name| Type | Default | Description | 
  | - | - | :-: | - | 
  | `text` | String  | |  |
  | `isNewQuestion` | bool  | | is a new Question or not |
  ### AudioInput Object
  |Name| Type | Default | Description | 
  | - | - | :-: | - | 
  | `text` | String  | |  |
  | `audio` | String  | |  |
  | `isNewQuestion` | bool  | | is a new Question or not |
  ### LocationInput Object
  |Name| Type | Default | Description | 
  | - | - | :-: | - | 
  | `location` | String  | | the longitude and latitude of the location, e.g. "-39.900000,116.300000" |
  ### OptionInput Object
  |Name| Type | Default | Description | 
  | - | - | :-: | - | 
| `optionId` | String  | |optionId |
  ### FormInput Object
  |Name| Type | Default | Description | 
  | - | - | :-: | - |
  | `formValues` | [FieldValue](#FieldValue-object)[]  | |  an array of [FieldValue](#FieldValue-object) objects |
  ### FieldValue Object

|Name| Type|  Default |  Description     |
| - | - | :-: |  - | 
|`name` | string |  | the name of a field in a form. |
|`value` | string |  | the value of a field. |

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
  |`type` | string | | type of the response,including `chatbotActionSendMessage`,`chatbotActionQuickReply`、 `chatbotActionSendImage`、`chatbotSendVideo`、`chatbotActionSSOLoginButton`,`chatbotActionCollectLocation`, `chatbotCollectCompany`, `chatbotCollectEmail`, `chatbotCollectName`, `chatbotActionCollectPhoneNumber`, `chatbotActionCollectComment`,`chatbotActionCollectVariableData`,`sendAForm`,`chatbotActionTransferChat`,`chatbotActionGotoTaskbot` |
  | `content` | object | |  response's content. when type is `chatbotActionSendMessage`, it represents [SendMessage](#sendmessage-object); when type is `chatbotActionQuickReply`,it represents [QuickReply](#quickreply-object);when type is `chatbotActionSendImage`,it represents [SendImage](#sendimage-object);when type is `chatbotActionSendVideo`,it represents [SendVideo](#sendvideo-object); when type is `chatbotActionSSOLoginButton`, it represents [SSOLoginButton](#ssologinbutton-object);when type is `chatbotActionCollectLocation`, it represents [CollectLocation](#collectlocation-object);when type is `chatbotActionCollectCompany`, it represents [CollectCompany](#collectcompany-object);when type is `chatbotActionCollectEmail`, it represents [CollectEmail](#collectemail-object);when type is `chatbotActionCollectName`, it represents [CollectName](#collectname-object);when type is `chatbotActionCollectPhoneNumber`, it represents [CollectPhoneNumber](#collectphonenumber-object);when type is `chatbotActionCollectComment`, it represents [CollectComment](#collectcomment-object);when type is `chatbotActionCollectVariableData`, it represents [CollectVariableData](#collectvariabledata-object);when type is `sendAForm`, it represents [SendAForm](#sendform-object);when type is `chatbotActionTransferChat`, it represents [TransferChat](#transferchat-object);when type is `chatbotActionGotoTaskbot`,  it represents [GotoTaskbot](#gototaskbot-object); |
  |`disableChatInputArea` | bool | false | Only available when channel is  `Live Chat`. |
  |`delayTime` | decimal | 1 | how many seconds delay to show  |

#### SendMessage Object
  Text Response is represented as simple flat json objects with the following keys:

  |Name| Type| Default | Description     | 
  | - | - | :-: | - | 
  |`message` | string |  | string  |
  |`chatbotActionSendMessageLinks` | [button](#button-object) object |  |   |
 #### QuickReply Object
Text Response is represented as simple flat json objects with the following keys:

  |Name| Type| Default | Description     | 
  | - | - | :-: | - | 
  |`isInputAreaEnabled` | bool |  |   |
  |`message` | string |  | string  |
  |`options` | [option](#option-object) |  |   |
  |`otherResponseToActionId` | Guid |  |   |
   #### Option Object
Text Response is represented as simple flat json objects with the following keys:

  |Name| Type| Default | Description     | 
  | - | - | :-: | - | 
  |`optionId` | Guid |  |   |
  |`order` | int |  |   |
  |`text` | String |  |   |
  |`type` | String | text |   |
#### SendImage Object
  Text Response is represented as simple flat json objects with the following keys:

  |Name| Type| Default | Description     | 
  | - | - | :-: | - | 
  |`imageUrl` | string |  | string  |
  |`message` | string |  | string  |
  #### SendVideo Object
  Text Response is represented as simple flat json objects with the following keys:

  |Name| Type| Default | Description     | 
  | - | - | :-: | - | 
  |`videoUrl` | string |  | string  |
  |`message` | string |  | string  |
  #### SSOLoginButton Object
Text Response is represented as simple flat json objects with the following keys:

  |Name| Type| Default | Description     | 
  | - | - | :-: | - | 
  |`failedOptionId` | Guid |  |   |
  |`isInputAreaEnabled` | bool |  |   |
  |`loginButtonText` | string |  | string  |
  |`loginUrl` | string |  | string  |
  |`loginInOptionId` | Guid |  |   |
  |`message` | string |  | string  |
 #### CollectLocation Object
Text Response is represented as simple flat json objects with the following keys:

  |Name| Type| Default | Description     | 
  | - | - | :-: | - | 
  |`buttonText` | string |  | string  |
  |`failedOptionId` | Guid |  |   |
  |`isInputAreaEnabled` | bool |  |   |
  |`successedOptionId` | Guid |  |   |
  |`message` | string |  | string  |
#### CollectComment Object
Text Response is represented as simple flat json objects with the following keys:

  |Name| Type| Default | Description     | 
  | - | - | :-: | - | 
  |`isInputAreaEnabled` | bool |  |   |
  |`message` | string |  | string  |
  #### CollectName Object
Text Response is represented as simple flat json objects with the following keys:

  |Name| Type| Default | Description     | 
  | - | - | :-: | - | 
  |`isInputAreaEnabled` | bool |  |   |
  |`message` | string |  | string  |
  #### CollectEmail Object
Text Response is represented as simple flat json objects with the following keys:

  |Name| Type| Default | Description     | 
  | - | - | :-: | - | 
  |`isInputAreaEnabled` | bool |  |   |
  |`message` | string |  | string  |
  #### CollectCompany Object
Text Response is represented as simple flat json objects with the following keys:

  |Name| Type| Default | Description     | 
  | - | - | :-: | - | 
  |`isInputAreaEnabled` | bool |  |   |
  |`message` | string |  | string  |
  #### CollectPhoneNumber Object
Text Response is represented as simple flat json objects with the following keys:

  |Name| Type| Default | Description     | 
  | - | - | :-: | - | 
  |`isInputAreaEnabled` | bool |  |   |
  |`message` | string |  | string  |
  #### CollectVariableData Object
Text Response is represented as simple flat json objects with the following keys:

  |Name| Type| Default | Description     | 
  | - | - | :-: | - | 
  |`isInputAreaEnabled` | bool |  |   |
  |`message` | string |  | string  |
  |`options` | array |  |   |
  |`type` | string |  | type:integer,singleselect,multiselect,text,textarea，decimal，email，password，date，time |
  |`variableName` | string |  | string  |
  #### TransferChat Object
Text Response is represented as simple flat json objects with the following keys:

  |Name| Type| Default | Description     | 
  | - | - | :-: | - | 
  |`transferTo` | Guid |  |   |
  |`isInputAreaEnabled` | bool |  |   |
  |`type` | string |  | type:transferToAgent,transferToDepartment  |
  #### GotoTaskbot Object
Text Response is represented as simple flat json objects with the following keys:

  |Name| Type| Default | Description     | 
  | - | - | :-: | - | 
  |`buttonText` | string |  | string  |
  |`failedOptionId` | Guid |  |   |
  |`successedOptionId` | Guid |  |   |
  |`isInputAreaEnabled` | bool |  |   |
  |`message` | string |  | string  |

### SendForm Object
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


