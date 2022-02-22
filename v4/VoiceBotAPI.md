  | Change Version | API Version | Change nots | Change Date | Author |
  | - | - | - | - | - |
  | 2.0 | v1 | Voice Bot API | 2022-2-22 | Leon |  
 



# Summary
  - Voicebot
    - [VoiceBotSession](#VoiceBotsession-object)
       - [VoiceBotResponse](#VoiceBotresponse-object) 
          -[VoiceBotAction](#VoiceBotAction-object) 


## Voice Bot API
  - `POST /voicebots/{chatbotId}/sessions` - [Create session](#create-session)
  - `POST /sessions/{sessionId}:recieveMessage` - [Recieved Message](#Recieved-Message)
## Twillio Adapter  

## Sip Adapter



# Endpoints

### Create A New VoiceBot Session
`POST /bot/VoiceBotSessions`

#### Parameters
Request body

The request body contains data with the follow structure:

  | Name | Type | Required | Default | Description |    
  | - | - | :-: | :-: | - | 
  | `VoiceBotId` | Guid | yes | |  the unique id of the bot |
  |`visitor`  |  [Visitor](#visitor-object) Object  |no |   |  |

example:
```Json 
  {
    "VoiceBotId": "f9928d68-92e6-4487-a2e8-8234fc9d1f48",
    "channel": "LiveChat",
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
  |`greeting`  |  [VoiceBotOutput](#VoiceBotoutput-object) Object    |  |


#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "VoiceBotId": "f9928d68-92e6-4487-a2e8-8234fc9d1f48", 
    "visitor": {
      "name":"Kart",
      "email":"kart@yahoo.com",
      "phone":"123-4355-212",
    }
  }' -X POST https://domain.comm100.com/api/v4/bot/VoiceBotSessions
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
              "type":"VoiceBotActionSendMessage",
              "content":{
                      "VoiceBotActionSendMessageLinks": [],
                    "message": "Hi there! I'm a VoiceBot, here to help answer your questions.",
                    "nextActionId": "00000000-0000-0000-0000-000000000000",
                    "typingDelay": 1
              }
    }]
    }

  }
```

# Model

### VoiceBotSession Object
   

  |Name| Type | Default | Description | 
  | - | - | :-: | - | 
  | `id` | Guid  | | sessionId |
  | `interactions` |  [VoiceBotInteraction](#VoiceBotinteraction-object)[] Object |  |  |
  | `context` | VoiceBotSessionContext Object  |   |  |
### VoiceBotInteraction Object

  |Name| Type | Default | Description | 
  | - | - | :-: | - | 
  | `id` | Guid  | | dialogId |
  | `input` |  [VoiceBotInput](#VoiceBotinput-object) Object|  |  |
  | `output` |  [VoiceBotOutput](#VoiceBotoutput-object) Object |  |  |
### VoiceBotInput Object

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
### VoiceBotOutput Object
  VoiceBotMessage Object is represented as simple flat JSON objects with the following keys:  

  |Name| Type| Default | Description     |
  | - | - | :-: | - |
  | `id` | Guid  |  | the unique id of the response |
  | `content` | [VoiceBotResponse](#VoiceBotresponse-object)[]|  |   |


### VoiceBotResponse Object
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
  |`VoiceBotActionSendMessageLinks` | [button](#button-object) object []|  |   |
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
