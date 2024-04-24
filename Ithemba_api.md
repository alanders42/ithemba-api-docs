# External api
## Meta
This document has been updated at 2024-04-24
## Contact
Please contact shane.vanniekerk@drakkentech.co.za
## Authentication
Add the following header to your API calls to authenticate
```
Authorization: Bearer your-token-here
```
The token is configured in the production database table name bearer_token sid 1
## Format
The API expects data to be posted in JSON format and will reply with JSON data.
The `Content-Type: application/json` header should be set on requests.
## Location
The API is available at https://ithemba.drakkentech.co.za/send_message/
## Endpoints
Please note the trailing slashes on the URLs.
### Health Check
Health check to see whether the API is online and authentication succeeds.
Request:
```
GET /health-check/
```
Response:
```
{"message": "The server is alive!"}
```
# SEND A MESSAGE

Request
```
POST /send_message/
{
    "message": "str",
    "title": "str",
    "message_type_fk": "int",
    "message_subject": "str",
    "body_html": "str",
    "resend": "Optional[int]",
    "unit_list": "List",
    "sid": "Optional[int]"
  }
```
```
Field Name           | Description
---------------------|--------------------------------------------------------------------
message              | Content of the message you're sending.
title                | Brief description or subject of the message.
message_type_fk      | Type of message: [0] Normal message, [1] Automated message, [2] Scheduled message.
message_subject      | Subject of the message (can be same as title).
body_html            | HTML body of the content you're sending.
resend               | Flag for resending Firebase notifications (optional).
unit_list            | List of units to which the message will be sent. Example: [{"unit_number": "the_unit_number"}].
sid                  | SID of the message if you're sending a resend (optional).
```
Success Response
```
{"messages": "sent successfully"}
```
Validation Error Response (400):
```
{"error": "User ID or Unit ID is required."}
{"error": "Message body and title are required."}
{"error: No user or unit ids provided"}
{"error": "Bearer Token does not exist"}
```

Error Response (500):
```
{"error": "An unexpected error occurred"}
```
