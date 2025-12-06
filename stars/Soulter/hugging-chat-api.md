---
project: hugging-chat-api
stars: 933
description: HuggingChat Python API🤗
url: https://github.com/Soulter/hugging-chat-api
---

hugging-chat-api
================

English | 简体中文

Unofficial HuggingChat Python API, extensible for chatbots etc. It supports:

-   Basic Chat
-   Assistant(Image Generator, etc.)
-   Web search
-   Memorize context
-   Switch LLMs
-   ...

> **Note**
> 
> For the personal reasons, the update of this repo will become slow, and we will ensure that the most basic features can be used normally. Welcome Any PR!

Installation
------------

pip3 install hugchat

Usage
-----

### API

#### Minimal Example

from hugchat import hugchat
from hugchat.login import Login

\# Log in to huggingface and grant authorization to huggingchat
\# DO NOT EXPOSE YOUR EMAIL AND PASSWORD IN CODES, USE ENVIRONMENT VARIABLES OR CONFIG FILES
EMAIL \= "your email"
PASSWD \= "your password"
cookie\_path\_dir \= "./cookies/" \# NOTE: trailing slash (/) is required to avoid errors
sign \= Login(EMAIL, PASSWD)
cookies \= sign.login(cookie\_dir\_path\=cookie\_path\_dir, save\_cookies\=True)

chatbot \= hugchat.ChatBot(cookies\=cookies.get\_dict())

print(chatbot.chat("Hi!").wait\_until\_done())

The following are all common usages of this repo, You may not necessarily use all of them, You can add or delete some as needed :)

from hugchat import hugchat
from hugchat.login import Login

\# Log in to huggingface and grant authorization to huggingchat
EMAIL \= "your email"
PASSWD \= "your password"
cookie\_path\_dir \= "./cookies/" \# NOTE: trailing slash (/) is required to avoid errors
sign \= Login(EMAIL, PASSWD)
cookies \= sign.login(cookie\_dir\_path\=cookie\_path\_dir, save\_cookies\=True)

\# Create your ChatBot
chatbot \= hugchat.ChatBot(cookies\=cookies.get\_dict())  \# or cookie\_path="usercookies/<email>.json"

message\_result \= chatbot.chat("Hi!") \# note: message\_result is a generator, the method will return immediately.

\# Option 1: Non stream
message\_str: str \= message\_result.wait\_until\_done()
\# get files(such as images)
file\_list \= message\_result.get\_files\_created() \# must call wait\_until\_done() first!

\# Option 2: Stream response
for resp in chatbot.chat(
    "Hello",
    stream\=True
):
    print(resp)

\# Web search
query\_result \= chatbot.chat("How many models stored in huggingface?", web\_search\=True).wait\_until\_done()
print(query\_result)
\# You can get the web search results from the query result
for source in query\_result.get\_search\_sources():
    print(source.link, source.title)

\# Create a new conversation
chatbot.new\_conversation(switch\_to \= True) \# switch to the new conversation

\# Get conversations on the server that are not from the current session (all your conversations in huggingchat)
conversation\_list \= chatbot.get\_remote\_conversations(replace\_conversation\_list\=True)
\# Get conversation list(local)
conversation\_list \= chatbot.get\_conversation\_list()

\# Get the available models
models \= chatbot.get\_available\_llm\_models()
\# Switch model with given index
chatbot.switch\_llm(0) \# Switch to the first model
chatbot.switch\_llm(1) \# Switch to the second model

\# Get information about the current conversation
info \= chatbot.get\_conversation\_info()
print(info.id, info.title, info.model, info.system\_prompt, info.history)

\# Assistant
ASSISTANT\_ID \= "66017fca58d60bd7d5c5c26c" \# get the assistant id from https://huggingface.co/chat/assistants
chatbot.new\_conversation(assistant\=ASSISTANT\_ID, switch\_to\=True) \# create a new conversation with assistant

\# \[DANGER\] Delete all the conversations for the logged in user
chatbot.delete\_all\_conversations()

### CLI

Simply run the following command in your terminal to start the CLI mode

python -m hugchat.cli

CLI params:

-   `-u <your huggingface email>` : Provide account email to login.
-   `-p` : Force request password to login, ignores saved cookies.
-   `-s` : Enable streaming mode output in CLI.
-   `-c` : Continue previous conversation in CLI ".

Commands in cli mode:

-   `/new` : Create and switch to a new conversation.
    
-   `/ids` : Shows a list of all ID numbers and ID strings in _current session_.
    
-   `/switch` : Shows a list of all conversations' info in _current session_. Then you can choose one to switch to.
    
-   `/switch all` : Shows a list of all conversations' info in _your account_. Then you can choose one to switch to. (not recommended if your account has a lot of conversations)
    
-   `/del <index>` : Deletes the conversation linked with the index passed. Will not delete active session.
    
-   `/delete-all` : Deletes all the conversations for the logged in user.
    
-   `/clear` : Clear the terminal.
    
-   `/llm` : Get available models you can switch to.
    
-   `/llm <index>` : Switches model to given model index based on `/llm`.
    
-   `/share` : Toggles settings for sharing data with model author. On by default.
    
-   `/exit` : Closes CLI environment.
    
-   `/stream` : Toggles streaming the response.
    
-   `/web` : Toggles web search.
    
-   `/web-hint` : Toggles display web search hint.
    
-   AI is an area of active research with known problems such as biased generation and misinformation. Do not use this application for high-stakes decisions or advice.
    
-   Server resources are precious, it is not recommended to request this API in a high frequency.
    

Donations
---------

❤

Disclaimers
-----------

This is not an official Hugging Face product. This is a **personal project** and is not affiliated with Hugging Face in any way. Don't sue us.

Star History
------------
