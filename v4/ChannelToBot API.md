  | Change Version | API Version | Change nots | Change Date | Author |
  | - | - | - | - | - |
  | 4.0 | v4 | Bot API | 2021-9-8 | Leon |  
 




# Summary
  - Chatbot
    - [ChatbotSession](#chatbotsession)
        - [ChatbotQuestion](#chatbotquestion) 
        - [ChatbotAnswer](#chatbotanswer) 


# ChatbotSession
  - `POST /bot/ChatbotSessions` - [Create a new Chatbot Session](#create-a-new-chatbot-session)
   - `Delete /bot/ChatbotSessions/{id}` - [Delete the Chatbot Session](#delete-the-chatbot-session)
# ChatbotQuestion
  - `POST /bot/ChatbotQuestions` - [Create a new Chatbot Question and get a Chatbot Answer](#create-a-chatbot-question)
# ChatbotAnswer
  - `POST /bot/ChatbotAnswers/{ChatbotAnswerId}/score` - [Create a new Chatbot Question's score](#create-a-chatbot-answer-score)
  - `PUT /bot/ChatbotAnswers/{ChatbotAnswerId}/score` - [Update the  Chatbot Question's score](#update-the-chatbot-answer-score)


# Model

### ChatbotSession Object
  ChatbotSession Object is represented as simple flat JSON objects with the following keys:  

  |Name| Type | Default | Description | 
  | - | - | :-: | - | 
  | `id` | Guid  | | sessionId |
  | `questions` |  [ChatbotQuestion](#chatbotquestion-object)[] Object |  |  |
  | `answers` |  [ChatbotAnswer](#chatbotanswer-object)[] Object |  |  |
  | `context` | [ChatbotSessionContext](#chatbotsessioncontext-object) Object  |   |  |
### ChatbotQuestion Object
ChatbotQuestion Object is represented as simple flat JSON objects with the following keys:
  |Name| Type | Default | Description | 
  | - | - | :-: | - | 
  | `id` | Guid  | | questionId |
  | `Sessionid` | Guid  | | sessionId |
  | `TextInput` | String  | |  |
  | `AudioInput` | String  | |  |
  | `Location` | String  | |  |
  | `FormValues` | [FieldValue](#FieldValue-object)[]  | |  an array of [FieldValue](#FieldValue-object) objects |
### ChatbotAnswer Object
  ChatbotMessage Object is represented as simple flat JSON objects with the following keys:  

  |Name| Type| Default | Description     |
  | - | - | :-: | - |
  | `id` | Guid  |  | the unique id of the response |
  | `sessionid` | Guid  |  | the unique id of the session |
  | `questionid` | Guid  |  | the unique id of the question |
  | `answer` | List<MessageData>  |  | MessageData  |
  | `score` | String  |  |   |
  | `disableChatInputArea` | bool  | false | Only available when channel is  `Live Chat`. |
### ChatbotSessionContext Object
  ChatbotSessionContext Object is represented as simple flat JSON objects with the following keys:  

  |Name| Type | Default | Description     | 
  | - | - | :-: | - |   
  | `chatbotId` | Guid  | | chatbotId |
  | `authentication` | string  | | authentication data |
  | `location` | string  | | the longitude and latitude of the location, e.g. "-39.900000,116.300000" |
  | `formValues` | [FieldValue](#FieldValue-object)[] |  | an array of [FieldValue](#FieldValue-object) objects |
  | `isFormSubmitted` | bool  | false |  |
  | `consecutiveTimesOfPossibleAnswers` | int  | 0 |  |
  | `invalidInputTimes` | int  | 0 |  |
  | `customData` | Object  |   | Custom data |

### FieldValue Object
FieldValue is represented as simple flat json objects with the following keys:

|Name| Type|  Default |  Description     |
| - | - | :-: |  - | 
|`name` | string |  | the name of a field in a form. |
|`value` | string |  | the value of a field. |





 MessageData Object is represented as simple flat JSON objects with the following keys: 
  |Name| Type| Default | Description     | 
  | - | - | :-: | - | 
  | `type` | string  |  | type of the response:[GreetingMessage](#greetingmessage-object),[HighConfidenceAnswer](#highconfidenceanswer-object),[HighConfidenceAnswer](#highconfidenceanswer-object),[PossibleAnswer](#possibleanswer-object),[NoAnswer](#noanswer-object)|
  | `content` | object |  | response's content. |




### GreetingMessage Object
  GreetingMessage is represented as simple flat json objects with the following keys:

  |Name| Type | Default | Description     | 
  | - | - | :-: | - | 
  |`responses`| [ChatbotResponse](#chatbot-response-object)[] | | an array of [ChatbotResponse](#chatbot-response-object) object. |

### HighConfidenceAnswer Object

  HighConfidenceAnswer is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Default | Description |    
  | - | - | - | - |  
  | `responses`| [ChatbotResponse](#chatbot-response-object)[] |  | an array of [ChatbotResponse](#chatbot-response-object) object. |

### PossibleAnswer Object

  PossibleAnswer is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Default | Description |    
  | - | - | - | - | 
  | `message` | string | | Text of the Possible Answer message | 
  | `audio` | string |  | base64 string, convert the message text to speech |  

### NoAnswer Object

  NoAnswer is represented as simple flat JSON objects with the following keys:  

  | Name | Type |  Default | Description |    
  | - | - | - | - | 
  |`message` | string |  | text of the No Answer message  |
  |`audio` | string |  | base64 string, convert the message text to speech | 
  | `ifIncludeContactAgentOption` | bool  |  |  |


### AuthenticationRequest Object

  AuthenticationRequest is represented as simple flat JSON objects with the following keys:  

  | Name | Type  | Default | Description |    
  | - | - | :-: | - | 
  | `signInMessage` | string  |  | message of the sign in |
  | `audio` | string |  | base64 string, convert the signInMessage text to speech |   
  | `signInButtonText` | string  |  | text of the sign in link |
  | `signInURL` | string  |  | url of the sign in |


### LocationRequest Object

  LocationRequest is represented as simple flat JSON objects with the following keys:  

  | Name | Type  | Default | Description |    
  | - | - | :-: | - | 
  | `message` | string  |  | message of the sign in |
  | `buttonText` | string  |  | text of the sign in link |


### Prompt Object

  Prompt is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Default | Description |    
  | - | - | :-: | - | 
  |`question` | string | | |
  | `audio` | string |  | base64 string, convert the signInMessage text to speech |   
  |`options` | string[] |  | an array of string |


### FormRequest Object
FormRequest is represented as simple flat json objects with the following keys:

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

### NotHelpfulMessage Object
NotHelpfulMessage is represented as simple flat json objects with the following keys:

|Name| Type| Default | Description     | 
| - | - | :-: | - | 
|`message` | string |  | text of the message  | 
|`ifIncludeContactAgentOption` | bool |  | include Contact An Agent or not . |  


### Chatbot Response Object
  Response is represented as simple flat json objects with the following keys:

  |Name| Type| Default | Description     | 
  | - | - | :-: | - | 
  |`type` | string | | enums: `text` ,`htmlText` ,`button`,`quickReply` ,`image` ,`video` ,`ivrMenu` ,`transferCall` . |
  | `content` | object | | response's content. when type is `text` or `htmlText`, it represents [Text Response](#Text-Response-Object); when type is `image` ,it represents [ImageResponse](#ImageResponse-Object);when type is `video`, the content is the video url, it represents string; when type is `button`,it represents [ButtonResponse](#buttonresponse-object);when type is `quickReply`, it represents [QuickReplyResponse](#QuickReplyResponse); when type is `ivrMenu`, it represents [IVRMenu Response](#IVRMenu-Response-Object);when type is `transferCall`, it represents [TransferCall Response](#TransferCall-Response-Object); |
  |`disableChatInputArea` | bool | false | Only available when channel is  `Live Chat`. |
  |`delayTime` | decimal | 1 | how many seconds delay to show  |

#### Text Response Object
  Text Response is represented as simple flat json objects with the following keys:

  |Name| Type| Default | Description     | 
  | - | - | :-: | - | 
  |`text` | string |  | string  |
  |`audio` | string | | base64 string, convert the text to speech |

### ImageResponse Object
  Image is represented as simple flat JSON objects with the following keys:  

  | Name | Type |  Default | Description |    
  | - | - | :-: | - | 
  | `name` | string  |  | name of the image |
  | `url` | string  | | url of the image | 


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

#### QuickReplyResponse
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


#### IVRMenu Response Object
  IVRMenu Response is represented as simple flat json objects with the following keys:

  |Name| Type|  Default | Description     | 
  | - | - | :-: | - | 
  |`message` | string |  | The message sent to visitor before the options.This message will be transferred to IVR and read to visitor  |
  |`audio` | string |  | base64 string, convert the message text to speech  |  
  |`invalidInputActionRepeatTime` | integer |  | How many times will this IVR Menu repeat if there is invalid input   | 
  | `keys` | [IVRMenuKey](#IVRMenuKey-object)[]  |  | The valid keys for visitor to choose options. the key contains: `1`, `2`, `3`, `4`, `5`, `6`, `7`, `8`, `9`, `0`, `*`, `#`. Each key can only be used once in an IVR menu. Visitor can press the key to choose the option.  |


#### IVRMenuKey Object
|Name| Type   |Default | Description     | 
| - | - | :-: | - | 
|`key` | string |  | The valid keys for visitor to choose options. the key contains: `1`, `2`, `3`, `4`, `5`, `6`, `7`, `8`, `9`, `0`, `*`, `#`. Each key can only be used once in an IVR menu. Visitor can press the key to choose the option.  | 
|`text` | string |  |text of quickreply item .  | 
|`intentId` | Guid |  |    | 


#### TransferCall Response Object
  TransferCall Response is represented as simple flat json objects with the following keys:

  |Name| Type| Default | Description     | 
  | - | - | :-: | - | 
  |`targetNumber` | string |  | phone number. |



  # Endpoints

### Create A New Chatbot Session
`POST /bot/ChatbotSessions`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `chatbotId` | Guid | yes  |  the unique id of the bot |  

Request body

The request body contains data with the follow structure:

  | Name | Type | Required | Default | Description |    
  | - | - | :-: | :-: | - | 
  | `chatbotId` | Guid | yes | |  the unique id of the bot |
  | `id` | Guid | yes | |  id of the session, you must generate the unique sessionId  |
  | `context` | [ChatbotSessionContext](#ChatbotSessionContext-Object) Object  | no  |  |

example:
```Json 
  {
    "id": "f9928d68-92e6-4487-a2e8-8234fc9d1f48",
    "context": {   
      "customData": {
        "name":"Kart",
        "email":"kart@yahoo.com",
        "phone":"123-4355-212",
      }
    }
  }
```

#### Response
the response is: [ChatbotAnswer](#chatbotanswer-object) Object


#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "channel":"IVR",
    "id": "f9928d68-92e6-4487-a2e8-8234fc9d1f48",
    "context": {   
      "customData": {
        "name":"Kart",
        "email":"kart@yahoo.com",
        "phone":"123-4355-212",
      }
    }
  }' -X POST https://domain.comm100.com/chatbots/a9928d68-92e6-4487-a2e8-8234fc9d1f48/sessions
```
Response
```Json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  {    
    "id": "f9928d68-92e6-4487-a2e8-8234fc9d1f48",
    "message":{
      "id":"d3f5b968-ad51-42af-b759-64c0afc40b84",
      "visitorQuestion":"",
      "type":"greetingMessage",
      "content":{
        "responses":[
          {
            "type":"text",
            "content": {
              "text":"Hi, I'm Peely, I'm glad to help you.",
              "audio":"UklGRrj2AQBXQVZFZm10IBAAAAABAAEAwF0AAIC7AAACABAAZGF0YZT2AQA..."
            }
          },
          {
            "type":"text",
            "content": {
              "text":"You can ask any questions. If you want to know what I can help with, you can say Menu or Options",
              "audio":"UklGRrj2AQBXQVZFZm10IBAAAAABAAEAwF0AAIC7AAACABAAZGF0YZT2AQA..."
            }
          }
        ]
      }
    }    
  }
```
### Delete The Chatbot Session
`DELETE /bot/ChatbotSessions/{ChatbotSessionId}`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `ChatbotSessionId` | Guid | yes  |  the unique id of the Chatbot Session |  


example:
```Json 
  {
  }
```

#### Response
the response is: [ChatbotAnswer](#chatbotanswer-object) Object


#### Example
Using curl
```
curl -X DELETE https://domain.comm100.com/ChatbotSessions/a9928d68-92e6-4487-a2e8-8234fc9d1f48/sessions
```
Response
```Json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  {    
      "id":"d3f5b968-ad51-42af-b759-64c0afc40b84",
      "visitorQuestion":"",
      "type":"byeMessage",
      "content":{
        "responses":[
          {
            "type":"text",
            "content": {
              "text":"goodbuy, I'm glad to help you.",
              "audio":"UklGRrj2AQBXQVZFZm10IBAAAAABAAEAwF0AAIC7AAACABAAZGF0YZT2AQA..."
            }
          },
          {
            "type":"text",
            "content": {
              "text":"nice to meet you",
              "audio":"UklGRrj2AQBXQVZFZm10IBAAAAABAAEAwF0AAIC7AAACABAAZGF0YZT2AQA..."
            }
          }
        ]
      }   
  }
```

### Create a Chatbot Question
`POST /bot/ChatbotQuestions`

#### Parameters


Request body

The request body  is: [ChatbotQuestion](#chatbotquestion-object) Object:

example:
```Json 
  {
    "Sessionid":"",
    "textInput":"i want to buy NBN",
    "AudioInput":"String",		
    "Location":	"String",		
  "FormValues":	[]
  }
```

#### Response
the response is: [ChatbotAnswer](#chatbotanswer-object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "channel":"Facebook Messenger",
    "textInput":"i want to buy NBN",
    "context": {
      "chatbotId": "a9928d68-92e6-4487-a2e8-8234fc9d1f48",
      "customData": {
        "name":"Kart",
        "email":"kart@yahoo.com",
        "phone":"123-4355-212",
      }
    },
  }' -X POST https://domain.comm100.com/sessions/f9928d68-92e6-4487-a2e8-8234fc9d1f48:detectIntent
```
Response
```Json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  {    
    "id":"d3f5b968-ad51-42af-b759-64c0afc40b84",
    "visitorQuestion":"i want to buy NBN",
    "type":"highConfidenceAnswer",
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


### Create a Chatbot Answer score

  `POST /ChatbotAnswers/{ChatbotAnswerId}/score`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `chatbotAnswerId` | Guid | yes  |  the id of the [ChatbotAnswer](#chatbotanswer-object) |

Request body

The request body contains data with the follow structure:

  | Name | Type | Required  | Default | Description |    
  | - | - | :-: | :-: |  - | 
  | `score` | string  | yes  | | `helpful` or `notHelpful` |

  example:
```Json 
  {
    "chatbotAnswerId":"4487fc9d-92e6-4487-a2e8-92e68d6892e6",
    "score": "notHelpful",
  }
```
#### Response

#### Example
- Rate the bot as not helpful

  Using curl
```
curl -H "Content-Type: application/json" -d '{
    "score": "notHelpful",
  }' -X POST https://domain.comm100.com/chatbotAnswers/f9928d68-92e6-4487-a2e8-8234fc9d1f48/score
```
  Response
```Json
  HTTP/1.1 200 OK
  Content-Type:  application/json
  {    
    "id":"d3f5b968-ad51-42af-b759-64c0afc40b84",
    "visitorQuestion":"",
    "type":"notHelpfulMessage",
    "content":{
      "messageWhenNotHelpful":"I am sorry that this doesn't answer your question. Please click on following button to connect to an agent.",
      "ifIncludeContactAgentOptionWhenNotHelpful": true,
    }
  }  
```

- Rate the bot as helpful

  Using curl
```
curl -H "Content-Type: application/json" -d '{
    "score": "helpful",
  }' -X POST https://domain.comm100.com/ChatbotAnswers/1487fc9d-92e6-4487-a2e8-92e68d6892e6/score
```
  Response
```Json
HTTP/1.1 200 OK
  Content-Type:  application/json
  {    
    "id": "f9928d68-92e6-4487-a2e8-8234fc9d1f48",
    "context": {
      "chatbotId": "a9928d68-92e6-4487-a2e8-8234fc9d1f48",
      "customData": {
        "name":"Kart",
        "email":"kart@yahoo.com",
        "phone":"123-4355-212",
      }
    }       
  }
```

### Update the Chatbot Answer score

  `PUT /ChatbotAnswers/{ChatbotAnswerId}/score`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `chatbotAnswerId` | Guid | yes  |  the id of the [ChatbotAnswer](#chatbotanswer-object) |

Request body

The request body contains data with the follow structure:

  | Name | Type | Required  | Default | Description |    
  | - | - | :-: | :-: |  - | 
  | `score` | string  | yes  | | `helpful` or `notHelpful` |

  example:
```Json 
  {
    "chatbotAnswerId":"4487fc9d-92e6-4487-a2e8-92e68d6892e6",
    "score": "notHelpful",
  }
```
#### Response

#### Example
- Rate the bot as not helpful

  Using curl
```
curl -H "Content-Type: application/json" -d '{
    "score": "notHelpful",
  }' -X PUT https://domain.comm100.com/chatbotAnswers/f9928d68-92e6-4487-a2e8-8234fc9d1f48/score
```
  Response
```Json
  HTTP/1.1 200 OK
  Content-Type:  application/json
  {    
    "id":"d3f5b968-ad51-42af-b759-64c0afc40b84",
    "visitorQuestion":"",
    "type":"notHelpfulMessage",
    "content":{
      "messageWhenNotHelpful":"I am sorry that this doesn't answer your question. Please click on following button to connect to an agent.",
      "ifIncludeContactAgentOptionWhenNotHelpful": true,
    }
  }  
```

- Rate the bot as helpful

  Using curl
```
curl -H "Content-Type: application/json" -d '{
    "score": "helpful",
  }' -X PUT https://domain.comm100.com/ChatbotAnswers/1487fc9d-92e6-4487-a2e8-92e68d6892e6/score
```
  Response
```Json
HTTP/1.1 200 OK
  Content-Type:  application/json
  {    
    "id": "f9928d68-92e6-4487-a2e8-8234fc9d1f48",
    "context": {
      "chatbotId": "a9928d68-92e6-4487-a2e8-8234fc9d1f48",
      "customData": {
        "name":"Kart",
        "email":"kart@yahoo.com",
        "phone":"123-4355-212",
      }
    }       
  }
```

