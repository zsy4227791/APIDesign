  | Change Version | API Version | Change nots | Change Date | Author |
  | - | - | - | - | - |
  | 4.0 | v4 | Bot API | 2021-11-1 | Leon |  
# Learning Grouping 
  - [LearningGroupingTask](#learning-grouping-task-object)
     - [LearningGroup](#learning-group-object)
        - [LearningQuestion](#learning-question-object)

## AiGrouping Server Api
   - `POST /AiGrouping/groups` - [Create a new grouping task](#create-a-new-grouping-task)
## BotAi Server Api
   - `POST /botai/group/time` - [Create a new grouping time estimate](#create-a-new-grouping-time-estimate)
   - `POST /botai/group/groups` - [Return a grouping task result](#return-a-grouping-task-result)   

# QuickReply Matching
## AiQuickReply Server Api
- `POST /AiQuickReply/quickreplies` - [Create a new quickreply task](#create-a-new-quickreply-task)
# Endpoints
## AiGrouping Server Api
### Create a new grouping task
`POST /AiGrouping/groups`
#### Parameters
Request body

The request body contains data with the follow structure:

  | Name | Type | Required | Default | Description |    
  | - | - | :-: | :-: | - | 
  |`taskId` |  int | yes | |  the unique id of the grouping task |
  |`siteId` |  int | yes | |  the site id of the grouping task |
  |`mode`  |  String |yes |   | type of the response,including`accurate`,`normal`,`rough` |
  |`questions`  |  list<[Question](#learningquestiondto-object)> |yes |   | list of the question|  
example:
```Json 
  {
    "taskId": "10000",
    "siteId": "10000",    
    "mode":"accurate",
    "questions": [{
        "id":"121",
        "question":"are you ok?",
      },{
        "id":"122",
        "question":"are you ok?",  
      }]
    }
  }
```

#### Response
The Response body contains data with the follow structure:
HTTP/1.1 200 OK
  | Name | Type |  Description |    
  | - | - | :-: | 
  |`code` | int |  |
  |`msg`  | string   |  |
#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '  {
    "taskId": "10000",
    "mode":"accurate",
    "questions": [{
        "id":"121",
        "question":"are you ok?",
      },{
        "id":"122",
        "question":"are you okdd?",  
      }]
    }
  }' -X POST https://algorithm.comm100.com/api/groups
```
Response
```Json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  {    
    "code": 0,
    "msg": "success"
  }
```
## Bot Server Api
### Return a grouping task result
`POST /botai/group/groups?siteId=10000`
#### Parameters
Request body

The request body contains data with the follow structure:

  | Name | Type | Required | Default | Description |    
  | - | - | :-: | :-: | - | 
  |`taskId` |  int | yes | |  the unique id of the task |
  |`siteId` |  int | yes | |  the unique id of the site |
  |`result`  |  list<[GroupingResult](#grouping-result-object)> |yes |   | list of the grouping result| 
  |`code` |  int | yes | |  0 success -1 failed | 
  |`msg` |  int | yes | |  fail reason | 
example:
```Json 
  {
    "taskId": "10000",
    "code": 0 ,
    "msg" : "success" ,
    "result":  [{
            "groupId":"1",
            "groupName":"are you ok",
            "questions": [{
                    "id":"121",
                    "question":"are you ok?",
                },{
                    "id":"122",
                    "question":"are you ok?",  
                }],
        },
        {
            "groupid":"2",
            "groupName":"are you ok",
            "questions": [{
                    "id":"121",
                    "question":"are you ok?",
                },{
                    "id":"121",
                    "question":"are you ok?",  
                }]
        }]
  }
```

#### Response
The Response body contains data with the follow structure:
HTTP/1.1 200 OK
  | Name | Type |  Description |    
  | - | - | :-: | 
  |`code` | int |  |
  |`msg`  | string   |  |
#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '     {
    "taskId": "10000",
    "result":  [{
            "groupId":"1",
            "groupName":"are you ok",
            "questions": [{
                    "id":"121",
                    "question":"are you ok?",
                },{
                    "id":"122",
                    "question":"are you ok?",  
                }],
        },
        {
            "groupid":"2",
            "groupName":"are you ok",
            "questions": [{
                    "id":"121",
                    "question":"are you ok?",
                },{
                    "id":"121",
                    "question":"are you ok?",  
                }]
        }]
  }' -X POST https://domain.comm100.com/api/botai/group/groups
```
Response
```Json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  {    
    "code": 0,
    "msg": "success"
  }
```
### Create a new grouping time estimate
`POST /botai/group/time`
#### Parameters
Request body

The request body contains data with the follow structure:

  | Name | Type | Required | Default | Description |    
  | - | - | :-: | :-: | - | 
  |`num` |  int | yes | |  the num  of the grouping questions |

example:
```Json 
  {
    "num": "10000",
  }
```

#### Response
The Response body contains data with the follow structure:
HTTP/1.1 200 OK
  | Name | Type |  Description |    
  | - | - | :-: | 
  |`time` | int | the seconds of grouping time |
#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '   {
    "num": "10000",
  }' -X POST https://domain.comm100.com/api/botai/group/time
```
Response
```Json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  {    
    "time": 1900,
  }
```
### Create a new quickreply task
`POST /AiQuickReply/quickreplies`
#### Parameters
Request body

The request body contains data with the follow structure:

  | Name | Type | Required | Default | Description |    
  | - | - | :-: | :-: | - | 
  |`quickreplies` |  sting[] | yes | |  the quickreplies array |
  |`input` |  sting | yes | |  the user input |
example:
```Json 
  {
    "quickreplies": ["yes","no"],
    "input":"ok",
  }
```

#### Response
The Response body contains data with the follow structure:
  | Name | Type |  Description |    
  | - | - | :-: | 
  |`replyName` | string | the match reply|
  |`score` | float | the score of match|
#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '     {
    "quickreplies": ["yes","no"],
    "input":"ok",
  }' -X POST https://domain.comm100.com/api/AiQuickReply/quickreplies
```
Response
```Json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  {    
    "replyName": "yes",
    "score": 0.98
  }
```

# Model
### Learning Grouping Task Object
  |Name| Type | Default | Description | 
  | - | - | :-: | - | 
  | `id` | int  | | taskId |
  | `chatbotid` | Guid  | | It means which Chatbot this learning grouping belongs to.   |
  | `lastGroupingTime` | datetime  | | The last time when the Grouping Algorithm was completed. |
  | `groupsCreated` | int  | | The number of how many groups were created during last grouping.   |
  | `questionsCheckedInTotal` | int  | |The number of how many learning questions were checked during last grouping.  |
  | `questionsGroupedInTotal` | int  | |The number of how many learning questions were grouped  during last grouping.  |
  | `status` | string  | |type of the response,including`submit`,`grouping`,`complete`, `failed`|
  | `mode` | string  | |type of the response,including`Accurate`,`Normal`,`Rough`|
  | `startTime` | datetime  |   | the start time of questions |
  | `endTime` | datetime  |   | the end time of questions |
### Learning Group Object
  |Name| Type | Default | Description | 
  | - | - | :-: | - | 
  | `id` | int  | | groupId |
  | `taskid` | int  | | taskid |
  | `chatbotid` | Guid  | | It means which Chatbot this learning grouping belongs to.   |
  | `name` | string  | |group name |
 
### Learning Question Object
  |Name| Type | Default | Description | 
  | - | - | :-: | - | 
  | `id` | int  | | questionId |
  | `chatbotid` | Guid  | | It means which Chatbot this learning grouping belongs to.   |
  | `type` | string  | |type of the response,including`No Answer`,`Not Helpful,`,`Possible Answer` |
  | `originalChatOrTicket` | Guid  | | chatId   |
  | `question:` | string  | |  |
  | `topScoreIntentId` | Guid  | |topScoreIntentId  |
  | `topScore` | float  | ||
  | `createTime` | datetime  | | |
### Learning Question Dto Object
  |Name| Type | Default | Description | 
  | - | - | :-: | - | 
  | `id` | int  | | questionId |
  | `question` | string |  |  |

### Grouping Result Object
  |Name| Type | Default | Description | 
  | - | - | :-: | - | 
  | `groupId` | int  | | groupId |
  | `groupName` | string |  |  |
  | `questions` | list<[Question](#learning-question-dto-object)> |  |  |
