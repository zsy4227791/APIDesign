  | Change Version | API Version | Change nots | Change Date | Author |
  | - | - | - | - | - |
  | 4.0 | v4 | Bot API | 2021-9-8 | Leon |  
 




# Summary
  - Chatbot
    - [ChatbotSession](#chatbotsession-object)
      - [ChatbotDialog](#chatbotdialog-object)
        - [ChatbotQuestion](#chatbotquestion-object) 
        - [ChatbotAnswer](#chatbotanswer-object) 
          - [ChatbotResponse](#chatbotresponse-object) : text ,htmlText ,button,quickReply ,image ,video,form


## ChatbotSession
  - `POST /bot/chatbotSessions` - [Create a new Chatbot Session](#create-a-new-chatbot-session)
   - `DELETE /bot/chatbotSessions/{id}` - [Delete the Chatbot Session](#delete-the-chatbot-session)
## ChatbotDialog  
  - `POST /bot/chatbotSessions/{id}/dialogs` - [Send a  Chatbot Question and get a Chatbot Answer](#create-a-chatbot-dialog)


# Endpoints

### Create A New Chatbot Session
`POST /bot/chatbotSessions`

#### Parameters


Request body

The request body contains data with the follow structure:

  | Name | Type | Required | Default | Description |    
  | - | - | :-: | :-: | - | 
  | `chatbotId` | Guid | yes | |  the unique id of the bot |
  |visitor  |  [Visitor](#visitor-object) Object  |no |   |  |

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
  | `sessionId` | Guid | the unique id of the session |
  |greeting  |  [ChatbotAnswer](#chatbotanswer-object) Object    |  |


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
      "content":{
        "responses":[
          {
            "type":"text",
            "content": {
              "text":"Hi, I'm Peely, I'm glad to help you.",
            }
          },
          {
            "type":"text",
            "content": {
              "text":"You can ask any questions. If you want to know what I can help with, you can say Menu or Options",
            }
          }
        ]
      }
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

### Create a Chatbot Dialog
`POST /bot/chatbotSession/{chatbotSessionId}/dialogs`

#### Parameters

Request body

The request body  is: [ChatbotQuestion](#chatbotquestion-object) Object

example:
```Json 
  {
    "textInput":"i want to buy NBN"
  }
```

#### Response
the response is: [ChatbotAnswer](#chatbotanswer-object) Object

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
    "content":{
      "responses":[
        {
          "type":"htmlText",
          "content": {
            "text":"<div>Hi, what can i do for you?</div>",
          }
        },
        {
          "type":"image",
          "content": {
            "name":"greeting.png",
            "url": "https://bot.comm100.com/botapi/images/greeting.png"
          }
        }
      ]
    }   
  }
```

# Model

### ChatbotSession Object
   

  |Name| Type | Default | Description | 
  | - | - | :-: | - | 
  | `id` | Guid  | | sessionId |
  | `dialogs` |  [ChatbotDialog](#chatbotdialog-object)[] Object |  |  |
  | `context` | [ChatbotSessionContext](#chatbotsessioncontext-object) Object  |   |  |
### ChatbotDialog Object

  |Name| Type | Default | Description | 
  | - | - | :-: | - | 
  | `id` | Guid  | | dialogId |
  | `question` |  [ChatbotQuestion](#chatbotquestion-object) Object|  |  |
  | `answer` |  [ChatbotAnswer](#chatbotanswer-object) Object |  |  |
### ChatbotQuestion Object

  |Name| Type | Default | Description | 
  | - | - | :-: | - | 
  | `id` | Guid  | | questionId |
  | `TextInput` | String  | |  |
  | `AudioInput` | String  | |  |
  | `Location` | String  | |  |
  | `Authentication` | string  | | authentication data |
  | `OptionId` | String  | |  |
  | `FormValues` | [FieldValue](#FieldValue-object)[]  | |  an array of [FieldValue](#FieldValue-object) objects |
### ChatbotAnswer Object
  ChatbotMessage Object is represented as simple flat JSON objects with the following keys:  

  |Name| Type| Default | Description     |
  | - | - | :-: | - |
  | `id` | Guid  |  | the unique id of the response |
  | `content` | [ChatbotResponse](#chatbot-response-object)[]|  |   |

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
### FieldValue Object

|Name| Type|  Default |  Description     |
| - | - | :-: |  - | 
|`name` | string |  | the name of a field in a form. |
|`value` | string |  | the value of a field. |


### ChatbotResponse Object
  Response is represented as simple flat json objects with the following keys:

  |Name| Type| Default | Description     | 
  | - | - | :-: | - | 
  |`type` | string | | enums: `text` ,`htmlText` ,`button`,`quickReply` ,`image` ,`video`,`form` |
  | `content` | object | | response's content. when type is `text` or `htmlText`, it represents [Text Response](#text-response-object); when type is `image` ,it represents [ImageResponse](#imageresponse-object);when type is `video`, it represents [VideoResponse](#videoresponse-object), it represents string; when type is `button`,it represents [ButtonResponse](#buttonresponse-object);when type is `quickReply`, it represents [QuickReplyResponse](#quickreplyresponse-object); when type is `form`, it represents [FormReplyResponse](#formreplyresponse-object); |
  |`disableChatInputArea` | bool | false | Only available when channel is  `Live Chat`. |
  |`delayTime` | decimal | 1 | how many seconds delay to show  |

#### Text Response Object
  Text Response is represented as simple flat json objects with the following keys:

  |Name| Type| Default | Description     | 
  | - | - | :-: | - | 
  |`text` | string |  | string  |

### ImageResponse Object
  Image is represented as simple flat JSON objects with the following keys:  

  | Name | Type |  Default | Description |    
  | - | - | :-: | - | 
  | `name` | string  |  | name of the image |
  | `url` | string  | | url of the image | 
### VideoResponse Object
  Video is represented as simple flat JSON objects with the following keys:  

  | Name | Type |  Default | Description |    
  | - | - | :-: | - | 
  | `name` | string  |  | name of the video |
  | `url` | string  | | url of the video |

#### ButtonResponse Object
ButtonResponse is represented as simple flat json objects with the following keys:

|Name| Type|  Default | Description   |   
| - | - | :-: | - | 
|`message` | string |  |text above buttons,this text will be sent before buttons.  | 
|`buttons` | [Button](#button-Object)[] | |an array of [Button](#button-Object).  | 

#### Button Object
Button is represented as simple flat json objects with the following keys:

|Name| Type| Default | Description     | 
| - | - | :-: | - | 
|`buttonText` | string |  |text on button.  | 
|`type` | string |  |enums contain `triggerAnIntent`,`link` and `webView`,type of buttons  | 
|`linkUrl` | string |  |url of the web page you want to open.  | 
|`openIn` | string |  |enums contain `sideWindow`,`newWindow`,`currentWindow`, it represents the way that a page will be opened.  | 
|`openStyle` | string | |enums contain `compact`,`tall` and `full`,it represents the size of the webview that will be opened.  |

#### QuickReplyResponse Object
QuickReplyResponse is represented as simple flat json objects with the following keys:

|Name| Type| Default | Description     | 
| - | - | :-: | - | 
|`message` | string | |text sent before quickreplys.  |  
|`quickReplyItems` | [QuickReplyItem](#QuickReplyItem-object)[]  | |an array of [QuickReplyItem](#QuickReplyItem-Object).  | 

#### QuickReplyItem Object
|Name| Type   |Default | Description     | 
| - | - | :-: | - | 
|`type` | string |  |enum values, `triggerAnIntent`,`contactAnAgent`  | 
|`text` | string |  |text of quickreply item .  | 
|`optionid` | string |  |id of quickreply item .  | 

### FormReplyResponse Object
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


