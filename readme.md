# BenTwi API Documentation

Welcome to the BenTwi API! This API enables you to store, retrieve, and manage application data for users, check stream states, and retrieve Twitch user information. Below, you'll find endpoint details, including required requests, responses, and example calls.

---

## Base URL

All endpoints use the following base URL:

https://bentwi.skykopf.com/api


---

## Endpoints

### 1. **Store Data**

#### `POST /bentwi/store/set`

Stores custom data for a specified `tile` and authenticates with the `bentwiToken`.

- **Request Body:**
  ```json
  {
    "tile": "example",
    "store": {
      "someData": "someString",
      "orSomeNumber": 42,
      "orSomeArray": ["i", "like", "trains"]
    },
    "bentwiToken": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
  }


Then you should get the response:
//collapse section

{
  "ID": "API2OF_RESPONSE",
  "CODE": 200,
  "MESSAGE": "Yup! Saved it successfully",
  "DATA": {}
}

---

POST /bentwi/store/get

Retrieves stored data for a specified tile.

//code block
{
  "tile": "example",
  "bentwiToken": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
}

A response from this could look like that:
//collapse section
{
  "ID": "API2OF_RESPONSE",
  "CODE": 200,
  "MESSAGE": "Here you go buddy!",
  "DATA": {
    "id": "example",
    "store": {
      "someData": "someString",
      "orSomeNumber": 42,
      "orSomeArray": ["i", "like", "trains"]
    },
    "lastSavedAt": "2024-11-09 16:11:23"
  }
}


---

### 2. **Receive Data**

GET /bentwi/streamstate

Retrieves the stream state for a Twitch user by their ID or username.

    Parameters:
        id: Twitch User ID
        username: Twitch Username
        Supports multiple users by adding additional username or id parameters.

//code block
/bentwi/streamstate/?id=942417144
/bentwi/streamstate/?username=skytro_pixl
/bentwi/streamstate/?username=byseli&username=dpommeslord


---

### 3. **The real sh!t**

POST /bentwi/userAccess

Retrieves user access details by checking for bentwiToken. Verifies if the user has ultraAccess and returns associated Twitch credentials if found.

//code block
{
  "bentwiToken": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
}


then you will receive this response
//collapse section
{
  "access_token": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
  "oAuthPlan": "PSYCHOPATHIC",
  "streamerID": "519155335",
  "streamerName": "redstone_kopf_live",
  "clientID": "otceqd3d4ywv51m0nhi8lu5bq0v80t"
}


### 4. **We live in an EMULATION**

GET /bentwi/emulate

Provides access to the emulation API. Currently, this endpoint is disabled and may be removed in the future.

5. Get Twitch User
GET /twitch/getUser

Retrieves Twitch user information by userID or username.

    Parameters:
        id: Twitch User ID
        username: Twitch Username

//code block
/twitch/getUser/?id=942417144
/twitch/getUser/?username=skytro_pixl



---

### **Error Handeling**

BenTwi will provide API errors the same way for all endpoints

{
	"ID": "API2OF_ERROR",
	"CODE": 418,
	"MESSAGE": "A relatively detailed thing about what the hell did go wrong in your request",
	"DATA": {"info": "I am a teapod"}
}

when you see an error like this, you can either try to do the query again, or don't use it


## **Common Errors**

    200: Everything went well
    404: Resource not found
    400: Invalid or non-exsistant token
    500: Internal server error.


## **In case of downtime/endpoints that previously worked but now don't/you would find those endpoints usefull**

In case of downtime and/or endpoints not working
We recommend to wait at least 15 Minutes, when the Endpoint or server still isn't available reach out to
support@skykopf.de
When you want to get fast support please include "[BENTWI-Support]" in your emails subject!
Our system will then automatically skip the normal queue and send it to the staff of BenTwi.

Or (if possible, and discord server got opened - if the discord is open and this still is in the docs tell Skytro // Felix about it please)
Go to our discord
Under "Support" get in the channel "API" and open a ticket OR write a DM to the BenTwi Discord bot, it should give you instructions then
IMPORTANT: You won't chat with the actuall supporter, the bot will play "man in the middle" means messages sent by you go into our supporting software, the supportes replay via software to you and the bot sends back the message to you in discord.