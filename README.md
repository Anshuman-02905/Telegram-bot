# Telegram-bot

# # Problem / Goal Definition
A telegram Bot that accepts user message optionally interprets commands such as /topic and /phrase , constructs an appropriate AI prompt sends it to OPEN AI receives the Response and replies to the correct Telegram chat/message

A Go based Telegram Bot that integrates with the OPEN API

This BOT:
- recieves Telegram message
- identifies supported commands
- constructs an AI Prompt
- sends the Prompt to OPEN AI
- receives the generated response
- sends the response to the originating Telegram Chat

Requirements
FR-001 : The Bot shall receiv Telegram Messages
FR-002 : The Bot shall identify the originating ID
FR-003 : The bot shall identify the originatiing message ID
FR-004 : The Bot shall recognize /Topic
FR-005 : The Bot shall recognize /Phrase
FR-006 : The Bot shall construct THE AI Prompt
FR-007 : The Bot shall send the Prompt to OPEN AI
FR-008 : The Bot shjall extract the AI Response
FR-009 : The Bot shall send the Response to the originatng Telegram chat
FR-0010: The Bot shall reply to the originatiung Telegram message

Feasability Study
Telegram:
Can Telegram provide : CHAT ID, MessageID, UserInformation, Commands, ReplyInformation
YES

OPENAI
Can the application send a prompt and recieve generated  text
YES

GO
CAN GO handle both the APIs

COST:
TELEGRAM API itself is available for bot interaction while OPEN API USAGE IS Billed according to the API/service terms rather than being equivalent to CHAT GPT subscription usage

Infrastucture
FOR MVP
MAC -> GO PROCESS -> TelegramAPI -> GO PROCESS ->OPEN API -> GOPROCESS-> MAC
No database required.
No Redis required.
No Kafka required.
No Kubernetes required.


IDENTIFY USE CASES:
UC-01 Normal Question
User
 ↓
"Explain goroutines in Go"
 ↓
Bot
 ↓
OpenAI
 ↓
Response
 ↓
Telegram

UC-002 — Topic command
/topic golang concurrency
The System might constuct
System prompt:
You are an expert Go tutor...

User prompt:
Explain golang concurrency

UC-003 — Phrase command
/phrase explain goroutines simply
Different prompt construction.

UC-004 — Empty command
Bot should not call OPEN AI
Instead
Please provide a topic.

Example:
/topic Go concurrency

UC-005 - OPENAI Failure
Telegram
   ↓
Go
   ↓
OpenAI
   X
   ↓
error
   ↓
Telegram
   ↓
"Sorry, I couldn't process that request."

UC-006 — Telegram failure
OpenAI successfully responds:
OpenAI
 ↓
Response
 ↓
Telegram API
 X
 Your application needs to log that failure.