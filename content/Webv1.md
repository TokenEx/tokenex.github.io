
#Iframve v1
## Iframe
The iframe model provides maximum flexibility to the merchant, by only including the input for the PAN in the Iframe. The form will reside on your server, but the input for the Credit Card number will be replaced with an iframe that points to the TokenEx secure environment. 


**High Level Flow**

 1. Your application will establish a "session" with your HTP. This is a server side call to the HTP API where you provide any dynamic content and details used to authenticate the user/consumer.
 2. Your application will add the iframe source as the HTP url.
 4. Your page, the "parent", will use [postMessage][postmessageLink] to invoke the Tokenization process from within the iframe.
 5. The HTP iframe will use [postMessage][postmessageLink] to send the token back to your application.
 
**Integration**

The steps to integrate have been broken into two parts. 

1. [Create a single use session][createsession]
2. [Using the Iframe(Client Side)][useiframe]

A working demo of illustrating these step 2 can be found [here][iframedemo] 

**Note:** You must complete step 1 first and update the iframe src with the HTP url you were provided. For testing with JS fiddle, you will need to use "https://fiddle.jshell.net" as the OriginURL.



###Create a single use session###

The first step in using the iframe is to create a single use session. This allows you to provide the styling and prevents your TokenEx credentials from being exposed to the browser. 

The session is created by POSTing a json payload to the endpoint listed below. 

**URI:** https://test-htp.tokenex.com/api/v1

**content-type:** application/json

**Request Parameters**
Parameter  | Type | Description
------ | ------- | ------
APIKey  | string |See   [Auth Model][auth]
TokenExID  | string| Your TokenEx ID
HMACKey  | string| customer provided [HMAC][hmac] key used by TokenEx to sign the response message.
TokenScheme  | Enum | See   [Token Schemes][ts]
OriginURL | string | fully qualified [Orign][origin]
CustomerDefinedRefNumber | string | reference number from your application. This can be whatever you like
CSS | string | CSS to apply to the iframe. See [Styling the Iframe][syle]

```javascript
{
    "HMACKey": "YourSuperSecretHMACKey",
    "TokenScheme": "fourTOKENfour",
    "OriginURL": "https://YourDomain.com",
    "CustomerRefnumber": "CustomerDefinedRefNumber",
    "CSS":"input {Your CSS Here }input:focus {Your CSS Here} input.error {Your CSS Here }",
    "APIKey": "YourAPIKey",
    "TokenExID": "YourtokenExID"
}
```

**Response Parameters**
Parameter  | Type | Description
------ | ------- | ------
HTPURL  | string | The URL to use as the Iframe Source
SessionID  | string| HTP Session ID
Success  | bool| Indicator if the result was successful or not.
ReferenceNumber  | string| Reference number for the TokenEx transaction.
Error  | string | Error Code and human readable description.

```javascript
{
  "HTPURL": "https://test-htp.tokenex.com/iframe/v1/14372391da774048a5f283e6f6538a6d",
  "SessionID": "14372391da774048a5f283e6f6538a6d",
  "ReferenceNumber": "16060812561806163476",
  "Success": true,
  "Error": ""
}
```

###Using the iframe### 

After you have created the single use session and rendered the HTP Iframe, all communication between parent and HTP iframe occur using postMessage. The iframe will send a JSON object back to the parent widow with 'events' containing information regarding the state of the iframe. 
At a high level, your user will enter the credit card number into the iframe and you will invoke the the submit process by sending a tokenize 'command' to the iframe. 

**Integration Steps**

 1. Add the iframe to your page. The source should be dynamic based on the HTP URL returned when you created the session.
 2. Add an event listener for the the "message" event.
 3. Interact with the iframe by sending 'comands'
 


#### Events and Commands###

**Commands**

to send a command to the iframe, you must obtain a reference to the iframe, then use postMessage to send the command. After the command is sent, the iframe will respond with the appriorate 'event'.

Command  |  Description
------ |  ------
reset | clears the input and resets the validations
validate | validates the user input
tokenize | tokenizes the user imput

```javascript
var iframe = document.getElementById("tokenExIframe");
iframe.contentWindow.postMessage('tokenize', 'https://test-htp.tokenex.com');
```



**Events Descriptions**

Each 'event' object returned from the iframe will contain properties relavant to the type of message or 'event'.

event  | Description
------ | ------
load | the iframe has loaded
focus | the input in the iframe has focus or not
change | has the input changed
validation | event containing the validation state of the input data
post | event returned after the iframe's form has been submitted

```javascript
{"event":"load"}
{"event":"focus","data":{"value":true}}
{"event":"change"}
{"event":"validation","data":{"isValid":false,"validator":"required"}}
{"event":"post","hmac":"hmacValue","data":{"success":true,"error":"","cardType":"masterCard","token":"tokenValue","sesssionID":"123","customerRefNumber":"abc"}}
```
**Field Descriptions**

event  | parent | Field | type | Description
------ | ------ | ------ | ------ | ------
load | self | n/a  | string | iframe has loaded
focus | data | n/a  | object  | object of additional properties
focus | data | value | bool | true if the field obtained focus, false on blur
validation | self | n/a  |  string |client side validation from the iframe
validation | data | n/a  | object | object of additional properties
validation | data | isValid | bool |true if the input data is valid, false if not
validation | data | validator | string |'required' if the value is empty, 'invalid' if the data is invalid
post | self | n/a  | string | server side message from the iframe
post | self | hmac  | string | HMACSHA256 of the data hash
post | data | n/a  | object | object of additional properties
post | data | success | bool |true or false 
post | data | error | string |if success == false, this will contain a human readable error message
post | data | cardType | string |type of the credit card, 'masterCard','amex', 'discover', 'visa', 'diners','jcb'
post | data | token | string |Token value
post | data | sesssionID | string |HTP Session ID
post | data | customerRefNumber | string | Reference number provided when the HTP session was established

```javascript
if (window.addEventListener) {
  addEventListener("message", listener, false)
} else {
  attachEvent("onmessage", listener)
}

function listener(event) {
  if (event.origin === 'https://test-htp.tokenex.com') {
    var message = JSON.parse(event.data);
    switch (message.event) {
      case 'focus':
        if (message.data.value) {
          //field has focus
        } else {
          //field does not have focus(blur)
        }
      case 'change':
        // field changed
        break;
      case 'validation':
        if (!message.data.isValid) {
          //field failed validation
        } else {
          //validation valid!
        }
        break;
      case 'post':
        if (!message.data.success) {
          // use message.data.error 
        } else {
          //get token! message.data.token
        }
        break;
    }
```



### Styling the Iframe

The iframe is styled by passing in the CSS on the server-side call to create the single use session. In general you should provide a class for the input, as well as an error class.

The TokenEx Iframe will automatically append the error CSS class when the validation fails.

**Note:** there is a 500 character max on the CSS paramter. 

```CSS
innput {
  font-family: Arial, sans-serif;
  padding: 0 8px;
  border: 1px solid rgba(0, 0, 0, 0.2);
  width: 100%;
  font-size: 13px;
  height: 32px;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
}

input:focus {
  box-shadow: 0 0 6px 0 rgba(0, 132, 255, 0.5);
  border: 2px solid rgba(0, 132, 255, 0.5);
  outline: 0;
}

input.error {
  box-shadow: 0 0 6px 0 rgba(224, 57, 57, 0.5);
  border: 1px solid rgba(224, 57, 57, 0.5);
}
```

[postmessageLink]: https://developer.mozilla.org/en-US/docs/Web/API/Window/postMessage
[bbejsfiddle]: https://jsfiddle.net/TokenEx/pdx9qLqh/
[origin]: https://developer.mozilla.org/en-US/docs/Web/Security/Same-origin_policy
[syle]: #iframve-v1-iframe-styling-the-iframe
[createsession]: #iframve-v1-iframe-create-a-single-use-session
[useiframe]: #iframve-v1-iframe-using-the-iframe
[hmac]: https://en.wikipedia.org/wiki/Hash-based_message_authentication_code
[iframedemo]: https://jsfiddle.net/TokenEx/16zs8w63/