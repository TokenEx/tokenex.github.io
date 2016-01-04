#Transparent Gateway API

The Transparent Gateway API allows merchants to leverage their existing gateway intergrations without detokenizing data. You can think of this service as a HTTP relay almost like a forward proxy. Rather that POSTing the transaction payload to the gateway, you post it to TokenEx with a few additional http headers. Our service inspects the http body and replaces the token with the PAN, then forwards to the gateway. TokenEx receives the response and returns it in the same format you receive today. Simply put, your application code remains the same(sans the HTTP headers)!
               
The TokenEx Transparent Gateway API supports JSON, XML, and url-form-encoded; basically this solution will work for just about any http POST. 


## Integration
To begin using this service you simply need to make a few modifications your code that is constructing the HTTPs POST to the payment gateway.


1. Update the URL to POST to TokenEx
	* https://test-api.tokenex.com/TransparentGatewayAPI
2. Add HTTP Header for the intended URL
	* TX_URL 
3. Add your Authentication Headers
	* TX_TokenExID
	* TX_APIKey 
4. Wrap the field in the HTTP Body with three curley braces
	* example: {{{4242424242424242}}}
	
**HTTP Request Headers**
Header | Description
---|---
TX_TokenExID|Your TokenEx ID.
TX_APIKey | Your API Key.
TX_URL | The end point URL that TokenEx should POST to. 

**Debugging**

To aid in the development process, TokenEx has enabled an echo endpoint to allow you to test Detokenization before sending the request to the gateway test server. To enable echo mode for your request simple update the url to https://test-api.tokenex.com/TransparentGatewayAPI?test=true. 

If this process is successful, the value "\*\*\*SUCCESS\*\*\*" will appear in place of the token(see [Error Handling][tgapiError]). Once the request has been tested successfully, simply remove the query string(?test=true) from the URL.

**Approved Hosts**

Before you begin using the Transparent Gateway API, you need to check to see if TokenEx has allowed communication with host. This is accomplished by a GET request to https://test-api.tokenex.com/TransparentGatewayAPI/Hosts. 

If the remote API's host name is not in the list, please contact support@tokenex.com to have it added. 



##Error Handling 
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

[tgapiError]: #transparent-gateway-api-error-handling