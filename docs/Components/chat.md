# chat

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
Experience seamless communication on the go with our chat-message component, keeping you connected anytime, anywhere.
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-WqoBhXkDyLGY8so3dYBHO-20240806-111124.png" size="78" position="center" caption="Chat" alt="Chat" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-WqoBhXkDyLGY8so3dYBHO-20240806-111124.png"}
:::
::::

## Configuration options

Some properties are common to all components, see [Common component properties](docId\:LLnTD-rxe8FmH7WpC5cZb) for a list and their configuration options.

| **Core Structure** |                                                                                                                                                                                                                                                             |
| ------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `instanceId`       | Used to reference the message data in the action's expression, for example, `=@ctx.components.instanceId.state.message`.                                                                                                                                    |
| `data`             | The array of items you want to display in the chat component.                                                                                                                                                                                               |
| `message`          | The field property used to add the text message in. Referenced for example, `=@ctx.current.item.message`                                                                                                                                                    |
| `sender`           | The `name` property requires the name of the person sending the message and displays at the top of the chat bubble. Expressions can be used to determine the sender, e.g., `=@ctx.current.item.senderName`                                                  |
| `sentAt`           | Provides the date and time the message was sent at in the format defined by your datasource configuration. For example,&#xA; 2024-01-08T06:01:29.863Z. If the `sentAt` property is not configured no date and time shown in the chat bubbles.               |
| `onSend`           | Configure the actions to execute when the send button is tapped in the chat text-editor. The action to send the message data to the database table must be included under `onSend`; usually, the `action: execute-entity` with the `create` method is used. |

| **Other options** |                                                                                                                                                                                                                                         |
| ----------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `isAuthor`        | Used to visually distinguish between the chat participants. When set to `true`, the chat bubble is blue, when set to `false` the bubble is set to white.                                                                                |
| `onPress`         | Configure an action that executes when you press on one of the chat bubbles, for example, `action.go-to`                                                                                                                                |
| `onRefresh`       | Use the `onRefresh` to sync new chat messages to the mobile device by swiping **up (**⬆️) on the screen as new messages load at the bottom of the screen. The `onRefresh` is a jig configuration and is not part of the chat component. |

## Considerations

- The `component.chat` can only be configured in the [jig.full-screen](<./../Jig Types/jig_fullscreen.md>) type.
- Only text messages can be sent in the chat bubbles.
- This component provides basic one-on-one chat-messaging, and is designed to perform basic functions.
- Chat is a chronological list of messages with the most recent ones at the bottom.
- It is best practice not to configure an `actions:` code snippet within the jig as the action will overlap the fullscreen functionality. The best practice is not to use an action with the `component.chat`, as the text field is covered by the action button. The actions should be included in the `onSend` property under the `action:` property.
- A datasource is required with the following :
  - Core data columns to store the data in the chat component. You can specify the column names that will store the data from these fields :
    - message
    - senderName
    - senderId
- *Optional*: To improve performance, limit the number of chat message bubbles displayed on the screen by limiting the number that is returned in the datasource query.

## Examples and code snippets

### Chatbot with OpenAI

In this example, you set up an AI chat experience using the Jigx chat component configured to integrate with the OpenAI ChatGPT REST endpoint - [https://api.openai.com/v1/chat/completions](https://api.openai.com/v1/chat/completions). The REST API is configured in the ai-function.jigx and the chat component in the ai-chat.jigx file. See [OpenAI integration](<./../OpenAI integration.md>) for more examples and information on using OpenAI.

The configuration for the function file called **ai-chat.jigx** contains:

1. The `URL` for the OpenAI REST API for chat.
2. The `outputTransform` specifies what to return from the OpenAI REST call.
3. The `inputTransform` contains the structure and prompts set that the AI requires, in this instance `model`, `response format`, and `messages`.
4. The `parameters` include `Authorization`, which depends on your AI model; in this example, a Bearer token is used; `question`, `author`, and `user`.

Configure the jig file called **ai**-**chat.jigx** with:

1. `onRefresh` action - this allows the chat screen to be cleared/reset by deleting the messages.
2. `datasource` (local data provider) to return chat history while in the app.
3. `component-chat` configured to show the message and sender details.
4. `onSend` action executes the global action that pushes the chat message (input) to the local data provider and then a `sync-entities` action syncs chat with the REST API by executing the function to return the answer (response).

![AI chatbot  ](https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-S4CYksahsIsJkfrCo6d8_-20240806-103549.png "AI chatbot  ")

:::CodeblockTabs
ai-chat.jigx (function)

```yaml
provider: DATA_PROVIDER_REST
method: POST
# Specify the OpenAI REST API URL.
url: https://api.openai.com/v1/chat/completions
# Configure what must be returned (AI response) from the AI server.
# Response configured in the outputTransform.
outputTransform: | 
  $merge([
      $merge([
          $.$eval($.choices[0].message.content),
          {"messageTime": $toMillis($now())}
    ]),
    {"id": $.inputs.mId}
  ]) 
useLocalCall: true
# Send input data to the AI server for the AI model to process
# And generate predictions. 
# Configure the AI model to be used.
# Configure the format in which the response is returned.
# Configure the prompt sets under content. 
inputTransform: |
  $.{
    "model": "gpt-3.5-turbo",
    "response_format": {
      "type": "json_object"
    },
    "messages": [
      {
        "role": "system",
        "content": "you are the chat for the AI Mobile demo app"
      },
      {
        "role": "system",
        "content": "You can participate in conversations about the app, and everything related to the app"
      },      
      {
        "role": "system",
        "content": "Your name is AI Chatbot"
      },      
      {
        "role": "system",
        "content": "Reply in a casual but formal tone when you participate in conversations."
      },           
      {
        "role": "system",
        "content": "always respond with a json object in the following format:
        {
          'message':'the response message to the question',
          'askedBy': 'the user asking the question',
          'author': 'the author of the answer',
          'question': 'the question asked by the user'
        }"
      },
      {
        "role": "system",
        "content": "The history of the conversation so far is " & history
      },    
      {
        "role": "system",
        "content": "The provided tId is " & tId
      },         
      {
        "role": "user",
        "content": question
      },         
      {
        "role": "system",
        "content": "Only reply with the json object as an answer."
      },
      {
        "role": "system",
        "content": "The user asking the question is " & user
      },
      {
        "role": "system",
        "content": "The author of the response is " & author
      }
    ]
  }
# Configure authorization for the AI model.
# Configure the type for each parameter. 
parameters:
  Authorization:
    location: header
    required: true
    type: string
     # Use your own Bearer token or the token required by the openAI REST.
    value: Bearer XX 
  question:  
    type: string
    location: body
    required: true
  mId:
    type: string
    location: body
    required: true
  author:
    type: string
    location: body
    required: true
  user:
    type: string
    location: body
    required: true

forRowsWithMatchingIds: true
```

ai-chat.jigx

```yaml
title: ="Chat"
type: jig.full-screen
# Configure the onRefresh to clear/reset the chat.
# When the screen is pulled up the screen resets. 
onRefresh:
  type: action.execute-entities
  options:
    provider: DATA_PROVIDER_LOCAL
    entity: AIChat
    method: delete
    goBack: stay
    data: =@ctx.datasources.chat-history

datasources:
  chat-history: 
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_LOCAL
  
      entities:
        - entity: AIChat
  
      query: |
        SELECT
          id,
          json_extract(tab.data, '$.author') AS author, 
          json_extract(tab.data, '$.askedBy') AS askedBy, 
          json_extract(tab.data, '$.question') AS question, 
          json_extract(tab.data, '$.message') AS message, 
          json_extract(tab.data, '$.messageTime') AS messageTime 
        FROM 
          [AIChat] AS tab
        ORDER BY 
          CAST(json_extract(tab.data, '$.messageTime') AS INTEGER) ASC

component: 
  type: component.chat
  instanceId: myChat
  options:
    data: =@ctx.datasources.chat-history
    item:
      type: component.chat-message
      options:
        message: =@ctx.current.item.message
        sender:
          name: =@ctx.current.item.author
        isAuthor: =$lowercase(@ctx.current.item.author) = $lowercase(@ctx.user.email)
        sentAt: =@ctx.current.item.messageTime
    # Configure the action to call a global action.
    # Pass the user message/question as a parameter.  
    onSend:
      type: action.execute-action
      options:
        action: ai-chat-action
        parameters:
          author: =@ctx.user.email
          user: =@ctx.user.email
          question: =@ctx.components.myChat.state.message
                
```

ai-chat-action.jigx

```yaml
parameters:
  author: 
    type: string
  user: 
    type: string
  question:
    type: string

action: 
  type: action.action-list
  options:
    isSequential: true
    # Save chat messages to the local data provider on the device.         
    actions:
      - type: action.execute-entity
        options:
          provider: DATA_PROVIDER_LOCAL
          entity: AIChat
          method: create
          goBack: stay
          data:
            author: =@ctx.action.parameters.author
            askedBy: =@ctx.action.parameters.author
            question: =@ctx.action.parameters.question
            message: =@ctx.action.parameters.question
            messageTime: =$toMillis($now())
      # Configure an action to call the AI response (outputTransformer).
      # Called from the REST ai-function.
      - type: action.sync-entities
        options:
          provider: DATA_PROVIDER_REST
          entities:
            - entity: AIChat
              function: ai-chat
              functionParameters:
                # Provide a name for your chat bot response.             
                author: 'JIGX Chatbot'
                user: =@ctx.user.email
                # Use your own Bearer token or the token required
                # by the openAI REST.                
                Authorization: Bearer 
                question: =@ctx.action.parameters.question
                # Configure a unique id for the chatbot message.                
                mId: =$uuid()
```

:::
