#Browser Based Encryption

Sometimes a client may want to encrypt data before sending it to TokenEx.  In this case, a TokenEx generated  RSA public encryption key is used to encrypt credit card information from within the client's browser.  The user will then submit the encrypted information to your website.  Once this step is complete, the encrypted value can be passed to TokenEx to be tokenized.  At this point, it is up to the merchant software to validate the inputs (like order total) and execute any further TokenEx Web-Service functions (like those for payment processing).  

## Integration Steps

1. Reference the TokenEx Javascript.  This must be referenced in the header of the application web page.
2. Add your public key to a hidden field.
3. Encrypt.  Call the TokenEx Javascript function to encrypt the sensitive data.
4. Remove the sensitive data from the POST to your web server and add the encrypted value.  
5. Obtain your token.  From your web server, you will make a call to the TokenEx API to [Tokenize][tokenizeencrypted], or [Process Transaction and Tokenize][processtransactionandtokenize] if you plan to send a transaction directly to an integrated payment processor

A working demo of illustrating these steps can be found [here][bbejsfiddle]


```javascript
{
  //grab the public key from the hidden field
  var key = document.getElementById('TxEncryptionKey').value;
  //grab the PAN
  var creditCard = document.getElementById("txtCreditCard").value;

  //encrypt the data 
  var cipherText = TxEncrypt(key, creditCard);
  
  //add the cipherText value to your form
  document.getElementById('cpihertext').value = cipherText;
  
  //remove the PAN data from your form
  document.getElementById("txtCreditCard").value = "";
  
  //post your form to your server.
}
```

### Public Key

The public key for the test environment is below

MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAvWpIQFjQQCPpaIlJKpeg
irp5kLkzLB1AxHmnLk73D3TJbAGqr1QmlsWDBtMPMRpdzzUM7ZwX3kzhIuATV4Pe
7RKp3nZlVmcrT0YCQXBrTwqZNh775z58GP2kZs+gVfNqBampJPzSB/hB62KkByhE
Cn6grrRjiAVwJyZVEvs/2vrxaEpO+aE16emtX12RgI5JdzdOiNyZEQteU6zRBRJE
ocPWVxExaOpVVVJ5+UnW0LcalzA+lRGRTrQJ5JguAPiAOzRPTK/lYFFpCAl/F8wt
oAVG1c8zO2NcQ0Pko+fmeidRFxJ/did2btV+9Mkze3mBphwFmvnxa35LF+Cs/XJHDwIDAQAB


#Tokenization Iframe

The Tokenization Iframe provides maximum flexibility to the merchant, by only including the input for the sensitive data to tokenize in the Iframe. The form will reside on your server, but the input for the sensitive data will be replaced with an iframe that points to the TokenEx secure environment.

The iframe can be used to collect virtually any dataset. Customers who wish to use the iframe for collecting PCI data should use the "PCI" variant.


**High Level Flow**

1. Your application will establish a "session" with your HTP. This is a server side call to the HTP API where you provide any dynamic content and details used to authenticate the user/consumer.
2. Your application will add the iframe source as the HTP url.
4. Your page, the "parent", will use [postMessage][postmessageLink] to invoke the Tokenization process from within the iframe.
5. The HTP iframe will use [postMessage][postmessageLink] to send the token back to your application.

**Integration**

The steps to integrate have been broken into two parts.

1. [Create a single use session][createsession]
2. [Using the Iframe(Client Side)][useiframe]


##Create a single use session##

The first step in using the iframe is to create a single use session. This allows you to provide the styling and prevents your TokenEx credentials from being exposed to the browser.

The session is created by POSTing a json payload to the endpoint listed below.

**note:** Customers who wish to use the Iframe for PCI data should send 'true' in the PCI field in JSON request object.

**URI:** https://test-htp.tokenex.com/api/v2

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
PlaceHolder | string | Optionally sets the placeholder attribute of the input.
PCI | bool | specifies if the PCI version of the iframe should be rendered. defaults to true.

```javascript
{
    "HMACKey": "YourSuperSecretHMACKey",
    "TokenScheme": "fourTOKENfour",
    "OriginURL": "https://YourDomain.com",
    "CustomerRefnumber": "CustomerDefinedRefNumber",
    "CSS":"input {Your CSS Here }input:focus {Your CSS Here} input.error {Your CSS Here }",
    "APIKey": "YourAPIKey",
    "TokenExID": "YourtokenExID",
    "PlaceHolder": "Credit Card",
    "PCI": true
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
  "HTPURL": "https://test-htp.tokenex.com/iframe/v2/14372391da774048a5f283e6f6538a6d",
  "SessionID": "14372391da774048a5f283e6f6538a6d",
  "ReferenceNumber": "16060812561806163476",
  "Success": true,
  "Error": ""
}
```

##Using the iframe##

After you have created the single use session and rendered the HTP Iframe, all communication between parent and HTP iframe occur using postMessage. The iframe will send a JSON object back to the parent widow with 'events' containing information regarding the state of the iframe.
At a high level, your user will enter the sensitive data into the iframe and you will invoke the submit process by sending a tokenize 'command' to the iframe.

There are two variants of the iframe, one specifically designed for PCI data, and one for virtually any dataset.

**Integration Steps**

1. Add the iframe to your page. The source should be dynamic based on the HTP URL returned when you created the session.
2. Add an event listener for the "message" event.
3. Interact with the iframe by sending 'commands'

### Events and Commands##

####Commands####

To send a command to the iframe, you must obtain a reference to the iframe, then use postMessage to send the command. After the command is sent, the iframe will respond with the appropriate 'event'.

**Note:** PCI/Non-PCI indicate if each variant of the iframe supports that feature.

Command  |  Description | PCI | NON-PCI
------ |  ------
reset | clears the input and resets the validations | X | X
validate | validates the user input | X | X
tokenize | tokenizes the user input | X | X
focus | sets the focus to the input | X | X
enablePrettyFormat | formats the credit card number as it would appear on the physical card | X |

```javascript
var iframe = document.getElementById("tokenExIframe");
iframe.contentWindow.postMessage('tokenize', 'https://test-htp.tokenex.com');
```

####Events####

Each 'event' object returned from the iframe will contain properties relevant to the type of message or 'event'.

**Note:** PCI/Non-PCI indicate if each variant of the iframe supports that feature.

event  | Description | PCI | NON-PCI
------ | ------ | ------ | ------
load | the iframe has loaded | X | X
focus | the input in the iframe has focus or not | X | X
change | has the input changed | X | X
validation | event containing the validation state of the input data | X | X
cardTypeChange | the possible cardtype entered by the user has changed. | X |
post | event returned after the iframe's form has been submitted  | X | X

```javascript
{"event":"load"}
{"event":"focus","data":{"value":true}}
{"event":"change"}
{"event":"validation","data":{"isValid":false,"validator":"required"}}
{"event":"cardTypeChange","data":{"possibleCardType":"masterCard"}}
{"event":"post","hmac":"hmacValue","data":{"success":true,"error":"","cardType":"masterCard","token":"tokenValue","sesssionID":"123","customerRefNumber":"abc"}}
```

**Event Field Descriptions**

**Note:** PCI/Non-PCI indicate if each variant of the iframe supports that feature.

event  | parent | Field | type | Description | PCI | NON-PCI
------ | ------ | ------ | ------ | ------ | ------ | ------
load | self | n/a  | string | iframe has loaded | X | X
focus | data | n/a  | object  | object of additional properties | X | X
focus | data | value | bool | true if the field obtained focus, false on blur | X | X
validation | self | n/a  |  string |client side validation from the iframe  | X | X
validation | data | n/a  | object | object of additional properties  | X | X
validation | data | isValid | bool |true if the input data is valid, false if not  | X | X
validation | data | lastFour | string | last 4 characters of input data | X |
validation | data | firstSix | string | first 6 characters of input data | X |
validation | data | cardType | string |type of the credit card, 'masterCard','americanExpress', 'discover', 'visa', 'diners','jcb' | X |
validation | data | characterCount | int | legth of the input data |  | X
validation | data | validator | string |'required' if the value is empty, 'invalid' if the data is invalid, 'posted' if the iframe session has already been used. | X | X
post | self | n/a  | string | server side message from the iframe | X | X
post | self | hmac  | string | HMACSHA256 of the data hash | X | X
post | data | n/a  | object | object of additional properties | X | X
post | data | success | bool |true or false | X | X
post | data | error | string |if success == false, this will contain a human readable error message | X | X
post | data | cardType | string |type of the credit card, 'masterCard','americanExpress', 'discover', 'visa', 'diners','jcb' | X |
post | data | characterCount | int | legth of the input data |  | X
post | data | token | string |Token value | X | X
post | data | sesssionID | string |HTP Session ID | X | X
post | data | customerRefNumber | string | Reference number provided when the HTP session was established | X | X

```javascript
if (window.addEventListener) {
  addEventListener("message", listener, false)
} else {
  attachEvent("onmessage", listener)
}

function listener(event) {
  if (event.origin === 'http://test-htp.tokenex.com') {
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


### Styling the Iframe ###

The iframe is styled by passing in the CSS on the server-side call to create the single use session. In general you should provide a class for the input, as well as an error class.

The TokenEx Iframe will automatically append the error CSS class when the validation fails.

**Note:** there is a 500 character max on the CSS parameter.

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


### Testing ###

We have provided working demos to illustrate the client side portion of using the iframe.

Since there is specific functionality included for credit card brand detection and validation requirements, we have provided two separate demos.

[NON-PCI][nonpciiframedemo] version and a [PCI][pciiframedemo] version

**Note:** You must complete step 1 first and update the iframe src with the HTP url you were provided. For testing with JS fiddle, you will need to use "https://fiddle.jshell.net" as the OriginURL.


[postmessageLink]: https://developer.mozilla.org/en-US/docs/Web/API/Window/postMessage
[tokenizeencrypted]: #tokenex-api-token-services-tokenizefromencryptedvalue
[processtransactionandtokenize]:#tokenex-api-payment-services-process-transaction-and-tokenize
[bbejsfiddle]: https://jsfiddle.net/TokenEx/pdx9qLqh/
[origin]: https://developer.mozilla.org/en-US/docs/Web/Security/Same-origin_policy
[syle]: #tokenization-iframe-using-the-iframe-styling-the-iframe
[createsession]: #tokenization-iframe-create-a-single-use-session
[useiframe]: #tokenization-iframe-using-the-iframe
[hmac]: https://en.wikipedia.org/wiki/Hash-based_message_authentication_code
[pciiframedemo]: https://jsfiddle.net/TokenEx/rb8f53ac/
[nonpciiframedemo]: https://jsfiddle.net/TokenEx/g9t3u2dk/
