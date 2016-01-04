#Browser Based Encryption

Sometimes a client may want to encrypt data before sending it to TokenEx.  In this case, a TokenEx generated  RSA public encryption key is used to encrypt credit card information from within the client's browser.  The user will then submit the encrypted information to your website.  Once this step is complete, the encrypted value can be passed to TokenEx to be tokenized.  At this point, it is up to the merchant software to validate the inputs (like order total) and execute any further TokenEx Web-Service functions (like those for payment processing).  

**PCI Compliance**

TokenEx’s Browser-Based Encryption implementation model allows e-commerce payment card data to be secured before it ever leaves the consumer’s system. The merchant’s website does not receive unsecured cardholder data while still allowing for maximum customization, flexibility, and a positive user experience. While the merchant no longer receives unencrypted payment card data, the webserver is still partial responsible for the secure processing of card holder data which leads to increased PCI compliance requirements.   Merchants using TokenEx’s Browser-Based encryption for payment card acceptance may qualify to use Self-Assessment Questionnaire A-EP to validate PCI compliance.

## Integration Steps

 1. Reference the TokenEx Javascript.  This must be referenced in the header of the application web page.
 2. Add your public key to a hidden field.
 3. Encrypt.  Call the TokenEx Javascript function to encrypt the sensitive data.
 4. Remove the sensitive data from the POST to your web server and add the encrypted value.  
 5. Obtain your token.  From your web server, you will make a call to the TokenEx API to [Tokenize][tokenizeencrypted], or [Process Transaction and Tokenize][processtransactionandtokenize] if you plan to send a transaction directly to an integrated payment processor

A working demo of illustrating these steps can be found [here][bbejsfiddle]


#Hosted Tokenization Page

The TokenEx HTP is a fully customized, managed "payment" page. This is NOT a traditional hosted payment page where the merchant has very few knobs to turn over the look and feel. This is NOT a "cookie cutter solution"; it's completely customized to suit your needs. Key capabilities include: 

 - Responsive Design
 - Custom domain name/TLS cert
	 - example: secure.yourdomain.com
 - Marketing analytics
	 - most analytical tools remain unaffected as page is hosted off of a sub domain.
 - Dynamic Data
	 - To support continuity in the check out flow, you can send dynamic data from your application to your HTP. 
	 - Example: You have the ability to display the customers name, order details, or any other data on the HTP.
 - Multiple "views" or variants of your HTP.
	 - Example: You have different brands/products and need to show the HTP to reflect the proper brand.
	 - 

**PCI Compliance**
TokenEx’s Hosted Payment Page integration model provides a 100% fully managed card acceptance channel. The entirety of all payment pages are delivered to consumer’s browser originating directly from TokenEx. Payment Card data is stored, processed, and transmitted entirely within TokenEx’s secure environment thereby fully removing your entire network and systems from PCI scope. Merchants using the Hosted Payment Page may qualify to use Self-Assessment Questionnaire A to validate PCI compliance.

## Full Page(redirect)

With the full page variant of the TokenEx HTP, the consumer is actually redirected your payment page that resides in the TokenEx secure environment.  

 1. Your application will establish a "session" with your HTP. This is a server side call to the HTP API where you provide any dynamic content and details used to authenticate the user/consumer.
 2. Your application will redirect the user/consumer to the HTP URL
 3. User/consumer completes the HTP form.
 4. HTP sends the Token and any other data captured to your application
 5. User/Consumer is redirected back to your application

## Iframe

The iframe model provides maximum flexibility to the merchant, by only include the input for the PAN in the Iframe. The form will reside on your server, but the input for the Credit Card number will be replaced with an iframe that points to the TokenEx secure environment. 

 1. Your application will establish a "session" with your HTP. This is a server side call to the HTP API where you provide any dynamic content and details used to authenticate the user/consumer.
 2. Your application will add the iframe source as the HTP url
 3. User/consumer completes the HTP form.
 4. Your page, the "parent" will use [postMessage][postmessageLink] to invoke the Tokenization process from within the iframe.
 5. The HTP iframe will use [postMessage][postmessageLink] to send the token back to your application
 
[postmessageLink]: [https://developer.mozilla.org/en-US/docs/Web/API/Window/postMessage]
[tokenizeencrypted]: #tokenex-api-token-services-tokenizefromencryptedvalue
[processtransactionandtokenize]:#tokenex-api-payment-services-process-transaction-and-tokenize
[bbejsfiddle]: https://jsfiddle.net/TokenEx/0eepaxL1/