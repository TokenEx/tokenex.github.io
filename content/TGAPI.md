
# Transparent Gateway API

The Transparent Gateway API allows customers interact with 3rd party API's without the need interact with sensitive data. In effect, this is Transparent Tokenization/Detokenization. 

You can think of this service as an HTTP relay almost like a forward proxy. Rather than interacting directly to a 3rd parties api, you route your traffic through TokenEx with the addition of a few additional HTTP headers. TokenEx will inspect the request or response body, and either tokenize or detokenize, based on the endpoint you POSTed to. 

## Detokenization

 Transparent Detokenization is useful if you send sensitive data to 3rd party API's(payment gateways, order fulfillment, etc.). In this model, your application will construct the same HTTPs POST that it does today, with a few minor changes used to authenticate you and locate the token in your request. TokenEx will replace the token, with the sensitive data, before it reaches the 3rd party. Your application would receive the same response that it currently does.

### Integration
To begin using this service you simply need to make a few modifications your code that is constructing the HTTPs POST to the payment gateway.


1. Update the URL to POST to TokenEx
	* https://test-api.tokenex.com/TransparentGatewayAPI/Detokenize
2. Add HTTP Header for the intended URL
	* TX_URL 
3. Add your Authentication Headers
	* TX_TokenExID
	* TX_APIKey 
4. Wrap the field in the HTTP Body with three curly braces
	* example: {{{4242424242424242}}}
	
**HTTP Request Headers**
Header | Description
---|---
TX_TokenExID | Your TokenEx ID.
TX_APIKey | Your API Key.
TX_URL | The end point URL that TokenEx should POST to.



### Examples

```bash
POST https://test-api.tokenex.com/TransparentGatewayAPI HTTP/1.1
Content-Type: application/json
tx_URL: https://www.example.com
TX_TokenExID: XXXXXXXXXX
TX_APIKey: XXXXXXXXXX


{
	"card": {
		"type": "MC ",
		"number": "{{{5454545454545454}}}",
		"expDate": "1112",
		"cardValidationNum": "123"
	}
}
```

```bash
POST https://test-api.tokenex.com/TransparentGatewayAPI HTTP/1.1
Content-Type: text/xml
tx_URL: https://www.example.com
TX_TokenExID: XXXXXXXXXX
TX_APIKey: XXXXXXXXXX


<card>
	<type>MC</type>
	<number>{{{5454545454545454}}}</number>
	<expDate>1112</expDate>
	<cardValidationNum>123</cardValidationNum>
</card>
```

```bash
POST https://test-api.tokenex.com/TransparentGatewayAPI HTTP/1.1
Content-Type: application/x-www-form-URLencoded
tx_URL: https://www.example.com
TX_TokenExID: XXXXXXXXXX
TX_APIKey: XXXXXXXXXX


type=MC&number={{{5454545454545454}}}&expDate=1112&cardValidationNum=123
```

## Tokenization

Transparent Tokenization is useful if you retrieve sensitive data from 3rd party API's(booking engines, partners, etc.). In this model, your application will construct the same HTTPs POST that it does today, with a few minor changes used to authenticate you and locate the token in the 3rd party's response. TokenEx will issue the request to the 3rd party API and replace the sensitive data in the response before it reaches your application. Your application would receive the same response that it currently does, only it will contain tokens in place of the sens data.

### Integration
To begin using this service you simply need to make a few modifications your application that is constructing the HTTPs POST.


1. Update the URL to POST to TokenEx
	* https://test-api.tokenex.com/TransparentGatewayAPI/Tokenize
2. Add HTTP Header for the intended URL
	* TX_URL 
3. Add your Authentication Headers
	* TX_TokenExID
	* TX_APIKey 
4. Add the [Token Scheme][ts] of your choice.
	* TX_TokenScheme
5. Add the Regular Expression used to select the sensitive data in the response.
	* TX_Field
	
**HTTP Request Headers**
Header | Description
---|---
TX_TokenExID|Your TokenEx ID.
TX_APIKey | Your API Key.
TX_URL | The end point URL that TokenEx should POST to. 
TX_TokenScheme | see  [Token Schemes][ts]
TX_Field | Regular Expression used to select the data in the response payload to tokenize

**HTTP Response Headers**
Header | Description
---|---
tx_Message | Informational message about the request. Number of possible matches based on Regular Expression, etc.
tx_tokenize_error_xxxx | reports any errors in tokenization.


### Examples

The following example would tokenize data in the cc_number xml element.

```bash
POST https://test-api.tokenex.com/TransparentGatewayAPI/Tokenize HTTP/1.1
Content-Type: text/xml
tx_URL: https://www.example.com
TX_TokenExID: XXXXXXXXXX
TX_APIKey: XXXXXXXXXX
TX_TokenScheme: fourTOKENfour
TX_Field:(?:<cc_number>)([0-9]{13,19})(?:<\/cc_number>)

<SomeXMLRequest>
…removed for brevity
</SomeXMLRequest>


```

## Error Handling

Errors are reported back to the client by way of a HTTP 400 status code. However, it is important to note that the payment gateway itself could also return a HTTP 400 status code. With that, TokenEx will add error information as HTTP return headers as well as in a JSON object in the HTTP body. It is important that your application extract the error details from the HTTP headers or the body.

 
```bash
HTTP Response Headers:
tx_Code = Error Code
tx_Message: Error Message
tx_refNumber: Reference number returned on each call
```

``` javascript
Error JSON:
 {
	 "Code":"Error Code",
	 "Message":"Error Message",
	 "RefNumber":"Reference number returned on each call"
 }
```

## Debugging

To aid in the development process, TokenEx has enabled an echo endpoint to allow you to test Detokenization before sending the request to the gateway test server. To enable echo mode for your request simple update the url to https://test-api.tokenex.com/TransparentGatewayAPI{Tokenize or Detokenize}?test=true. 

If this process is successful, the value "\*\*\*SUCCESS\*\*\*" will appear in place of the token(see [Error Handling][tgapiError]). Once the request has been tested successfully, simply remove the query string(?test=true) from the URL.

**Approved Hosts**

Before you begin using the Transparent Gateway API, you need to check to see if TokenEx has allowed communication with the host. This is accomplished by a GET request to https://test-api.tokenex.com/TransparentGatewayAPI/Hosts. 


[portal]: #appendix-customer-portal
[tgapiError]: #transparent-gateway-api-error-handling
[ts]: #appendix-token-schemes