## Gateway Parameters
### Authorize.Net

**URL:** http://www.authorize.net

**Default Currency:** USD

**Developer Documentation:** http://developer.authorize.net

**Supported Parameters**

Parent|Field Name|Type|Notes
---|---|---|---
gateway|name|string|**AuthorizeNetGateway**
gateway|login|string|Authorize.Net API Login
gateway|password|string|Authorize.Net Transaction Key
credit_card|number|string|This is your TokenEx Token - Tokenex will replace the Token with the Detokenized number
credit_card|month|string|1 or 2 digit value. Example: 11
credit_card|year|string|4 digit value. Example: 2017
credit_card|verification_value|string|CVV/CSC
credit_card|track_data|string|Track 1/Track 2 data
credit_card|track_1_data|string|Track 1 data
credit_card|track_2_data|string|track 2 data
check|routing_number|string|
check|account_number|string|This is your TokenEx Token - Tokenex will replace the Token with the Detokenized number
check|bank_name|string|
check|name|string|Name under which the account is maintained at the bank
check|account_type|string|
check|number|string|
transaction|amount|integer|Transaction amount in cents. Example: $10.00 should be sent as 1000
transaction|currency|string|
transaction|authorization|string|Required only for capture, refund, and void transactions. Obtained from the authorize or purchase actions
transaction|order_id|string|
transaction|description|string|
transaction|email|string|
transaction|ip|string|
transaction|customer|string|
transaction|cavv|string|
transaction|eci|string|
transaction|disable_partial_auth|string|desc
transaction|billing_address|hash|
transaction|shipping_address|hash|
billing_address|name|string|
billing_address|company|string|
billing_address|address1|string|
billing_address|city|string|
billing_address|state|string|
billing_address|zip|string|
billing_address|country|string|
shipping_address|name|string|
shipping_address|company|string|
shipping_address|address1|string|
shipping_address|city|string|
shipping_address|state|string|
shipping_address|zip|string|
shipping_address|country|string|

```javascript
Authorize Sample:
{
  "APIKey": "XXXXXXXXXX",
  "TokenExID": "XXXXXXXXXX",
  "TransactionType": 1,
  "TransactionRequest": {
    "gateway": {
      "name": "AuthorizeNetGateway",
      "login": "XXXXXXXXXX",
      "password": "XXXXXXXXXX"
    },
    "credit_card": {
      "number": "4111114356431111",
      "month": "4",
      "year": "2016",
      "verification_value": "111"
    },
    "transaction": {
      "amount": 1000,
      "order_id": "12345",
      "billing_address": {
        "name": "Bob Smith",
        "address1": "123 Maple Street",
        "city": "Tulsa",
        "state": "OK",
        "zip": "74119"
      }
    }
  }
}
```
```javascript
Capture Sample:
{
  "APIKey": "XXXXXXXXXX",
  "TokenExID": "XXXXXXXXXX",
  "TransactionType": 2,
  "TransactionRequest": {
    "gateway": {
      "name": "AuthorizeNetGateway",
      "login": "XXXXXXXXXX",
      "password": "XXXXXXXXXX"
    },
    "transaction": {
      "authorization": "359308705#1111",
      "amount": 1000
    }
  }
}
```


### Beanstream

**URL:** http://www.beanstream.com

**Developer Documentation:** http://developer.beanstream.com

* A username and password is required for capture, void and refund transactions and can be added to your account under Administration -> Account settings -> Order settings -> Use username/password validation
* API passcode and hash validation features are not supported and must not be enabled.

**Supported Parameters**

Parent|Field Name|Type|Notes
---|---|---|---
gateway|name|string|**BeanstreamGateway**
gateway|login|string|Beanstream Merchant ID
gateway|user|string|Beanstream Username. Required for capture, void, and refund transactions.
gateway|password|string|Beanstream Password. Required for capture, void, and refund transactions.
credit_card|number|string|This is your TokenEx Token - Tokenex will replace the Token with the Detokenized number
credit_card|month|string|1 or 2 digit value. Example: 11
credit_card|year|string|4 digit value. Example: 2017
credit_card|verification_value|string|CVV/CSC
credit_card|first_name|string|Cardholder first name
credit_card|last_name|string|Cardholder last name
transaction|amount|integer|Transaction amount in cents. Example: $10.00 should be sent as 1000
transaction|authorization|string|Required only for capture, void, and refund transactions. Obtained from the authorize or purchase transactions
transaction|order_id|string|
transaction|email|string|
transaction|ip|string|Customer IP address
transaction|description|string|Transaction comment
transaction|custom|string|Gateway field: ref1
transaction|billing_address|hash|
transaction|shipping_address|hash|
billing_address|name|string|
billing_address|phone|string|
billing_address|address1|string|
billing_address|address2|string|
billing_address|city|string|
billing_address|state|string|
billing_address|zip|string|
billing_address|country|string|
shipping_address|name|string|
shipping_address|phone|string|
shipping_address|address1|string|
shipping_address|address2|string|
shipping_address|city|string|
shipping_address|state|string|
shipping_address|zip|string|
shipping_address|country|string|
shipping_address|shipping_method|string|
shipping_address|delivery_estimate|string|

```javascript
Authorize Sample:
{
  "APIKey": "XXXXXXXXX",
  "TokenExID": "XXXXXXXXX",
  "TransactionType": 1,
  "TransactionRequest": {
    "gateway": {
      "name": "BeanstreamGateway",
      "login": "XXXXXXXXX",
      "user": "XXXXXXXXX",
      "password": "XXXXXXXXX"
    },
    "credit_card": {
      "number": "4030006537191234",
      "month": "4",
      "year": "2016",
      "verification_value": "123",
      "first_name": "Bob",
      "last_name": "Smith"
    },
    "transaction": {
      "amount": 1200,
      "billing_address": {
        "address1": "123 Maple Street",
        "city": "Tulsa",
        "state": "OK",
        "zip": "74119",
        "country": "US"
      }
    }
  }
}
```
```javascript
Capture Sample:
{
  "APIKey": "XXXXXXXXX",
  "TokenExID": "XXXXXXXXX",
  "TransactionType": 2,
  "TransactionRequest": {
    "gateway": {
      "name": "BeanstreamGateway",
      "login": "XXXXXXXXX",
      "user": "XXXXXXXXX",
      "password": "XXXXXXXXX"
    },
    "transaction": {
      "amount": 1200,
      "authorization": "10000019;12.00;PA"
    }
  }
}
```


### Braintree (Blue Platform)

**URL:** https://developers.braintreepayments.com/

**Supported Parameters**

Parent|Field Name|Type|Notes
---|---|---|---
gateway|name|string|**BraintreeBlueGateway**
gateway|merchant_id|string|Braintree API Merchant ID
gateway|public_key|string|Braintree API Public Key
gateway|private_key|string|Braintree API Private Key
gateway|acctid|string|Optional Braintree Merchant Account ID
credit_card|number|string|This is your TokenEx Token - Tokenex will replace the Token with the Detokenized number
credit_card|month|string|1 or 2 digit value. Example: 11
credit_card|year|string|4 digit value. Example: 2017
credit_card|verification_value|string|CVV/CSC
credit_card|first_name|string|Cardholder first name
credit_card|last_name|string|Cardholder last name
transaction|amount|integer|Transaction amount in cents. Example: $10.00 should be sent as 1000
transaction|authorization|string|Required only for capture, void, and refund transactions. Obtained from the authorize or purchase transactions.
transaction|order_id|string|
transaction|email|string|
transaction|billing_address|hash|
transaction|shipping_address|hash|
billing_address|company|string|
billing_address|address1|string|
billing_address|address2|string|
billing_address|city|string|
billing_address|state|string|
billing_address|zip|string|
billing_address|country|string|
shipping_address|company|string|
shipping_address|address1|string|
shipping_address|address2|string|
shipping_address|city|string|
shipping_address|state|string|
shipping_address|zip|string|
shipping_address|country|string|

```javascript
Authorize Sample:
{
  "APIKey": "XXXXXXXXX",
  "TokenExID": "XXXXXXXXX",
  "TransactionType": 1,
  "TransactionRequest": {
    "gateway": {
      "name": "BraintreeBlueGateway",
      "merchant_id": "XXXXXXXXX",
      "public_key": "XXXXXXXXX",
      "private_key": "XXXXXXXXX"
    },
    "credit_card": {
      "number": "4111111111111111",
      "month": "4",
      "year": "2016",
      "verification_value": "123",
      "first_name": "Bob",
      "last_name": "Smith"
    },
    "transaction": {
      "amount": 1200,
      "billing_address": {
        "address1": "123 Maple Street",
        "city": "Tulsa",
        "state": "OK",
        "zip": "74119",
        "country": "US"
      }
    }
  }
}
```
```javascript
Capture Sample:
{
  "APIKey": "XXXXXXXXX",
  "TokenExID": "XXXXXXXXX",
  "TransactionType": 2,
  "TransactionRequest": {
    "gateway": {
      "name": "BraintreeBlueGateway",
      "merchant_id": "XXXXXXXXX",
      "public_key": "XXXXXXXXX",
      "private_key": "XXXXXXXXX"
    },
    "transaction": {
      "amount": 1200,
      "authorization": "1561516564"
    }
  }
}
```


### Chase NetConnect

**URL:** https://www.chase.com

**Developer Documentation:** https://secure.paymentech.com/developercenter

* ChaseNetConnect supports the 'reverse' action which can be used to perform a 'reverse advice' or 'partial authorization reverse' transaction
* Chase responses containing token data will be returned as multiple params of the format token_XX, where XX is the two letter token code"

**Supported Parameters**

Parent|Field Name|Type|Notes
---|---|---|---
gateway|name|string|**ChaseNetConnectGateway**
gateway|login|string|NetConnect Username
gateway|password|string|NetConnect Password
gateway|mid|string|The 12-digit Chase Merchant ID
gateway|tid|string|The 1 to 3 digit Chase Terminal ID
gateway|cid|string|The 4 digit Chase Client ID
credit_card|number|string|This is your TokenEx Token - Tokenex will replace the Token with the Detokenized number
credit_card|month|string|1 or 2 digit value. Example: 11
credit_card|year|string|4 digit value. Example: 2017
credit_card|verification_value|string|CVV/CSC
transaction|amount|integer|Transaction amount in cents. Example: $10.00 should be sent as 1000
transaction|authorization|string|Required only for capture, partial authoriation reverse, and void transactions. Obtained from the authorize or purchase transactions
transaction|order_id|string|The first 12 characters must be unique. Capture, partial authorization reverse, and reverse advice transaactions must match the orginal transaction order_id
transaction|goods_type|string|D = Digital goods purchased, P = Physical goods purchased
transaction|eci|string|Ecommerce Indicator
transaction|cavv|string|Cardholder authentication value
transaction|reverse_reason|string|Token RR: Reversal Reason Code
transaction|partial_auth_reverse|string|Used to indicate the type of reverse transposaction. Set value to '1' to send a 'partial authorization reverse' transaction otherwise a 'reverse advise' transaction is performed.
transaction|authorization_type|string|Token P8: Authorization Type Requested: Default value '00'
transaction|billing_address|hash|
billing_address|address1|string|Cardholder Street Address
billing_address|address2|string|Extended Cardholder Street Address (ChaseNet and Visa only)
billing_address|zip|string|

```javascript
Authorize Sample:
{
  "APIKey": "XXXXXXXXXX",
  "TokenExID": "XXXXXXXXXX",
  "TransactionType": 1,
  "TransactionRequest": {
    "gateway": {
      "name": "ChaseNetConnectGateway",
      "login": "XXXXXXXXXX",
      "password": "XXXXXXXXXX",
      "mid": "XXXXXXXXXX",
      "tid": "001",
      "cid": "0001"
    },
    "credit_card": {
      "number": "4111114356431111",
      "month": "4",
      "year": "2016",
      "verification_value": "111"
    },
    "transaction": {
      "amount": 1000,
      "order_id": "123456789012",
      "billing_address": {
        "address1": "123 Maple Street",
        "zip": "74119"
      }
    }
  }
}
```
```javascript
Capture Sample:
{
  "APIKey": "XXXXXXXXXX",
  "TokenExID": "XXXXXXXXXX",
  "TransactionType": 2,
  "TransactionRequest": {
    "gateway": {
      "name": "ChaseNetConnectGateway",
      "login": "XXXXXXXXXX",
      "password": "XXXXXXXXXX",
      "mid": "XXXXXXXXXX",
      "tid": "001",
      "cid": "0001"
    },
    "credit_card": {
      "number": "4111114356431111",
      "month": "4",
      "year": "2016",
      "verification_value": "111"
    },
    "transaction": {
      "authorization": "099579;00000003",
      "amount": 1000,
      "order_id": "123456789012",
      "billing_address": {
        "address1": "123 Maple Street",
        "zip": "74119"
      }
    }
  }
}
```


### CyberSource

**URL:** http://www.cybersource.com

**Default Currency:** USD

**Developer Documentation:** SOAP Toolkit API http://www.cybersource.com/developers/download/

**Supported Parameters**

Parent|Field Name|Type|Notes
---|---|---|---
gateway|name|string|**CyberSourceGateway**
gateway|login|string|CyberSource Merchant ID
gateway|password|string|CyberSource Transaction Security Key
gateway|ignore_avs|string|Set this field to any value to enable
gateway|ignore_cvv|string|Set this field to any value to enable
gateway|decline_avs_flags|string|
credit_card|number|string|This is your TokenEx Token - Tokenex will replace the Token with the Detokenized number
credit_card|month|string|1 or 2 digit value. Example: 11
credit_card|year|string|4 digit value. Example: 2017
credit_card|verification_value|string|CVV/CSC
credit_card|first_name|string|Cardholder first name
credit_card|last_name|string|Cardholder last name
check|routing_number|string|
check|account_number|string|This is your TokenEx Token - Tokenex will replace the Token with the Detokenized number
check|name|string|Name under which the account is maintained at the bank
check|account_type|string|
transaction|amount|integer|Transaction amount in cents. Example: $10.00 should be sent as 1000
transaction|currency|string|
transaction|authorization|string|Required only for capture, refund, and void transactions. Obtained from the authorize or purchase actions
transaction|order_id|string|
transaction|email|string|
transaction|drivers_license_number|string|
transaction|drivers_license_state|string|
transaction|billing_address|hash|
transaction|shipping_address|hash|
billing_address|company|string|
billing_address|phone|string|
billing_address|address1|string|
billing_address|address2|string|
billing_address|city|string|
billing_address|state|string|
billing_address|zip|string|
billing_address|country|string|
shipping_address|company|string|
shipping_address|phone|string|
shipping_address|address1|string|
shipping_address|address2|string|
shipping_address|city|string|
shipping_address|state|string|
shipping_address|zip|string|
shipping_address|country|string|

```javascript
Authorize Sample:
{
  "APIKey": "XXXXXXXXX",
  "TokenExID": "XXXXXXXXX",
  "TransactionType": 1,
  "TransactionRequest": {
    "gateway": {
      "name": "CyberSourceGateway",
      "login": "XXXXXXXXX",
      "password": "XXXXXXXXX"
    },
    "credit_card": {
      "number": "4030006537191234",
      "month": "4",
      "year": "2016",
      "verification_value": "123",
      "first_name": "Bob",
      "last_name": "Smith"
    },
    "transaction": {
      "amount": 1200,
      "email", "null@cybersource.com",
      "billing_address": {
        "address1": "123 Maple Street",
        "city": "Tulsa",
        "state": "OK",
        "zip": "74119",
        "country": "US"
      }
    }
  }
}
```
```javascript
Capture Sample:
{
  "APIKey": "XXXXXXXXX",
  "TokenExID": "XXXXXXXXX",
  "TransactionType": 2,
  "TransactionRequest": {
    "gateway": {
      "name": "CyberSourceGateway",
      "login": "XXXXXXXXX",
      "password": "XXXXXXXXX"
    },
    "transaction": {
      "amount": 1200,
      "authorization": "10000019;12.00;PA"
    }
  }
}
```


### Elavon My Virtual Merchant

**URL:** http://www.elavon.com

**Developer Documentation:** https://demo.myvirtualmerchant.com/VirtualMerchantDemo/download/developerGuide.pdf

**Supported Parameters**

Parent|Field Name|Type|Notes
---|---|---|---
gateway|name|string|**ElavonGateway**
gateway|login|string|Elavon SSL Merchant ID
gateway|user|string|Elavon User ID
gateway|password|string|Elavon PIN
credit_card|number|string|This is your TokenEx Token - Tokenex will replace the Token with the Detokenized number
credit_card|month|string|1 or 2 digit value. Example: 11
credit_card|year|string|4 digit value. Example: 2017
credit_card|verification_value|string|CVV/CSC
credit_card|first_name|string|Cardholder first name
credit_card|last_name|string|Cardholder last name
transaction|amount|integer|Transaction amount in cents. Example: $10.00 should be sent as 1000
transaction|authorization|string|Required only for capture, refund, and void transactions. Obtained from the authorize or purchase actions
transaction|order_id|string|
transaction|description|string|
transaction|email|string|
transaction|customer|string|
transaction|tax|string|
transaction|eci|string|
transaction|cavv|string|
transaction|xid|string|
transaction|billing_address|hash|
transaction|shipping_address|hash|
billing_address|company|string|
billing_address|phone|string|
billing_address|address1|string|
billing_address|address2|string|
billing_address|city|string|
billing_address|state|string|
billing_address|zip|string|
billing_address|country|string|
shipping_address|name|string|
shipping_address|address1|string|
shipping_address|address2|string|
shipping_address|company|string|
shipping_address|city|string|
shipping_address|state|string|
shipping_address|zip|string|
shipping_address|country|string|

```javascript
Authorize Sample:
{
  "APIKey": "XXXXXXXXX",
  "TokenExID": "XXXXXXXXX",
  "TransactionType": 1,
  "TransactionRequest": {
    "gateway": {
      "name": "ElavonGateway",
      "login": "XXXXXXXXX",
      "user": "XXXXXXXXX",
      "password": "XXXXXXXXX"
    },
    "credit_card": {
      "number": "4030006537191234",
      "month": "4",
      "year": "2016",
      "verification_value": "123",
      "first_name": "Bob",
      "last_name": "Smith"
    },
    "transaction": {
      "amount": 1200,
      "billing_address": {
        "address1": "123 Maple Street",
        "city": "Tulsa",
        "state": "OK",
        "zip": "74119",
        "country": "US"
      }
    }
  }
}
```
```javascript
Capture Sample:
{
  "APIKey": "XXXXXXXXX",
  "TokenExID": "XXXXXXXXX",
  "TransactionType": 2,
  "TransactionRequest": {
    "gateway": {
      "name": "ElavonGateway",
      "login": "XXXXXXXXX",
      "user": "XXXXXXXXX",
      "password": "XXXXXXXXX"
    },
    "transaction": {
      "amount": 1200,
      "authorization": "10000019;1234"
    }
  }
}
```


### Federated Payments

**Default Currency:** USD

**URL:** http://www.federatedpayments.com

* The Federated gateway does not support a test API. You must enable or disable test mode on an account by account basis with Federated Payments.

**Supported Parameters**

Parent|Field Name|Type|Notes
---|---|---|---
gateway|name|string|**FederatedGateway**
gateway|login|string|Federated Payments Login
gateway|password|string|Federated Payments Password
credit_card|number|string|This is your TokenEx Token - Tokenex will replace the Token with the Detokenized number
credit_card|month|string|1 or 2 digit value. Example: 11
credit_card|year|string|4 digit value. Example: 2017
credit_card|verification_value|string|CVV/CSC
credit_card|first_name|string|Cardholder first name
credit_card|last_name|string|Cardholder last name
transaction|amount|integer|Transaction amount in cents. Example: $10.00 should be sent as 1000
transaction|currency|string|
transaction|authorization|string|Required only for capture, void, and refund transactions. Obtained from the authorize or purchase transactions.
transaction|order_id|string|
transaction|email|string|
transaction|description|string|
transaction|billing_address|hash|
transaction|shipping_address|hash|
billing_address|company|string|
billing_address|phone|string|
billing_address|address1|string|
billing_address|address2|string|
billing_address|city|string|
billing_address|state|string|
billing_address|zip|string|
billing_address|country|string|
shipping_address|first_name|string|
shipping_address|last_name|string|
shipping_address|company|string|
shipping_address|address1|string|
shipping_address|address2|string|
shipping_address|city|string|
shipping_address|state|string|
shipping_address|zip|string|
shipping_address|country|string|

```javascript
Authorize Sample:
{
  "APIKey": "XXXXXXXXX",
  "TokenExID": "XXXXXXXXX",
  "TransactionType": 1,
  "TransactionRequest": {
    "gateway": {
      "name": "FederatedGateway",
      "login": "XXXXXXXXX",
      "password": "XXXXXXXXX"
    },
    "credit_card": {
      "number": "4111111111111111",
      "month": "4",
      "year": "2016",
      "verification_value": "123",
      "first_name": "Bob",
      "last_name": "Smith"
    },
    "transaction": {
      "amount": 1200,
      "billing_address": {
        "address1": "123 Maple Street",
        "city": "Tulsa",
        "state": "OK",
        "zip": "74119",
        "country": "US"
      }
    }
  }
}
```
```javascript
Capture Sample:
{
  "APIKey": "XXXXXXXXX",
  "TokenExID": "XXXXXXXXX",
  "TransactionType": 2,
  "TransactionRequest": {
    "gateway": {
      "name": "FederatedGateway",
      "login": "XXXXXXXXX",
      "password": "XXXXXXXXX"
    },
    "transaction": {
      "amount": 1200,
      "authorization": "1561516564"
    }
  }
}
```


### Federated Payments Canada

**Default Currency:** CAD

**URL:** http://www.federatedcanada.com/

* The Federated Canada gateway does not support a test API. You must enable or disable test mode on an account by account basis with Federated Payments.

**Supported Parameters**

Parent|Field Name|Type|Notes
---|---|---|---
gateway|name|string|**FederatedCanadaGateway**
gateway|login|string|Federated Payments Canada Login
gateway|password|string|Federated Payments Canada Password
credit_card|number|string|This is your TokenEx Token - Tokenex will replace the Token with the Detokenized number
credit_card|month|string|1 or 2 digit value. Example: 11
credit_card|year|string|4 digit value. Example: 2017
credit_card|verification_value|string|CVV/CSC
credit_card|first_name|string|Cardholder first name
credit_card|last_name|string|Cardholder last name
transaction|amount|integer|Transaction amount in cents. Example: $10.00 should be sent as 1000
transaction|currency|string|
transaction|authorization|string|Required only for capture, void, and refund transactions. Obtained from the authorize or purchase transactions.
transaction|order_id|string|
transaction|email|string|
transaction|description|string|
transaction|billing_address|hash|
transaction|shipping_address|hash|
billing_address|company|string|
billing_address|phone|string|
billing_address|address1|string|
billing_address|address2|string|
billing_address|city|string|
billing_address|state|string|
billing_address|zip|string|
billing_address|country|string|
shipping_address|first_name|string|
shipping_address|last_name|string|
shipping_address|company|string|
shipping_address|address1|string|
shipping_address|address2|string|
shipping_address|city|string|
shipping_address|state|string|
shipping_address|zip|string|
shipping_address|country|string|

```javascript
Authorize Sample:
{
  "APIKey": "XXXXXXXXX",
  "TokenExID": "XXXXXXXXX",
  "TransactionType": 1,
  "TransactionRequest": {
    "gateway": {
      "name": "FederatedCanadaGateway",
      "login": "XXXXXXXXX",
      "password": "XXXXXXXXX"
    },
    "credit_card": {
      "number": "4111111111111111",
      "month": "4",
      "year": "2016",
      "verification_value": "123",
      "first_name": "Bob",
      "last_name": "Smith"
    },
    "transaction": {
      "amount": 1200,
      "billing_address": {
        "address1": "123 Maple Street",
        "city": "Tulsa",
        "state": "OK",
        "zip": "74119",
        "country": "US"
      }
    }
  }
}
```
```javascript
Capture Sample:
{
  "APIKey": "XXXXXXXXX",
  "TokenExID": "XXXXXXXXX",
  "TransactionType": 2,
  "TransactionRequest": {
    "gateway": {
      "name": "FederatedCanadaGateway",
      "login": "XXXXXXXXX",
      "password": "XXXXXXXXX"
    },
    "transaction": {
      "amount": 1200,
      "authorization": "1561516564"
    }
  }
}
```


### FirstData Compass Gateway

**URL:** http://www.firstdata.com

**Default Currency:** 840

* The Compass Gateway supports the 'authorize' and 'reverse' functions only.
* A zero 'amount' value performs a credit card verify.

**Supported Parameters**

Parent|Field Name|Type|Notes
---|---|---|---
gateway|name|string|**FirstdataCompassGateway**
gateway|login|string|Username provided by FirstData
gateway|password|string|Password provided by FirstData
gateway|ssl_cert|string|Client SSL certification provided by FirstData. The certificate must be in valid PEM format.
gateway|ssl_key|string|Client SSL key provided by FirstData. The key should must be in valid PEM format.
gateway|ssl_key_password|string|Optional ssl key encryption password. Must be provided if 'ssl_key' is encrypted.
credit_card|number|string|This is your TokenEx Token - Tokenex will replace the Token with the Detokenized number
credit_card|month|string|1 or 2 digit value. Example: 11
credit_card|year|string|4 digit value. Example: 2017
credit_card|verification_value|string|CVV/CSC
credit_card|first_name|string|Cardholder first name
credit_card|last_name|string|Cardholder last name
transaction|amount|integer|Transaction amount in cents. Example: $10.00 should be sent as 1000
transaction|currency|string|Currency is provided as a 3 digit numeric code. Please note that this field should be a string value.
transaction|authorization|string|Required only for 'reverse' transactions. Value is obtained from the 'authorize' transaction.
transaction|order_id|string|Required
transaction|division_id|string|Required
transaction|moto_ecommerce_ind|string|Defaults to '7'
transaction|email|string|
transaction|ip|string|
billing_address|name|string|
billing_address|phone|string|
billing_address|address1|string|
billing_address|city|string|
billing_address|state|string|
billing_address|zip|string|
billing_address|country|string|

```javascript
Authorize Sample:
{
  "APIKey": "XXXXXXXXX",
  "TokenExID": "XXXXXXXXX",
  "TransactionType": 1,
  "TransactionRequest": {
    "gateway": {
      "name": "FirstdataCompassGateway",
      "login": "XXXXXXXXX",
      "password": "XXXXXXXXX",
      "ssl_cert": "CLIENT SSL CERTIFICATE (PEM FORMAT)",
      "ssl_key": "CLIENT SSL KEY (PEM FORMAT)"
    },
    "credit_card": {
      "number": "4012000033330026",
      "month": "4",
      "year": "2016",
      "verification_value": "123",
      "first_name": "Bob",
      "last_name": "Smith"
    },
    "transaction": {
      "amount": 1200,
      "division_id": "XXXXXXXXX",
      "order_id": "1212",
      "billing_address": {
        "address1": "123 Maple Street",
        "city": "Tulsa",
        "state": "OK",
        "zip": "74119",
        "country": "US"
      }
    }
  }
}
```
```javascript
Capture Sample:
Note: This gateway does not support the 'capture' action. 
This example is a 'reverse' transaction.

{
  "APIKey": "XXXXXXXXX",
  "TokenExID": "XXXXXXXXX",
  "TransactionType": 6,
  "TransactionRequest": {
    "gateway": {
      "name": "FirstdataCompassGateway",
      "login": "XXXXXXXXX",
      "password": "XXXXXXXXX",
      "ssl_cert": "CLIENT SSL CERTIFICATE (PEM FORMAT)",
      "ssl_key": "CLIENT SSL KEY (PEM FORMAT)"
    },
    "transaction": {
      "amount": 1200,
      "division_id": "XXXXXXXXX",
      "order_id": "1212",
      "authorization": "OK885C;150116""
    }
  }
}
```


### FirstData Global Gateway e4

**URL:** http://www.firstdata.com

**Default Currency:** USD

**Developer Documentation:** https://firstdata.zendesk.com/entries/407571-First-Data-Global-Gateway-e4-Web-Service-API-Reference-Guide

* Global Gateway e4 supports both open and tagged refunds. TokenEx by default creates a tagged refund. If a credit_card hash object is included in a refund request, then a open refund request is created.

**Supported Parameters**

Parent|Field Name|Type|Notes
---|---|---|---
gateway|name|string|**FirstdataE4Gateway**
gateway|login|string|Gateway ID (Found in your administration terminal settings)
gateway|password|string|The terminal password
gateway|user|string|Optional user name associated with the transasction
credit_card|number|string|This is your TokenEx Token - Tokenex will replace the Token with the Detokenized number
credit_card|month|string|1 or 2 digit value. Example: 11
credit_card|year|string|4 digit value. Example: 2017
credit_card|verification_value|string|CVV/CSC
credit_card|first_name|string|Cardholder first name
credit_card|last_name|string|Cardholder last name
transaction|amount|integer|Transaction amount in cents. Example: $10.00 should be sent as 1000
transaction|authorization|string|Required only for capture, refund, and void transactions. Obtained from the authorize or purchase actions
transaction|order_id|string|
transaction|description|string|
transaction|email|string|
transaction|ip|string|
transaction|customer|string|
transaction|cavv|string|
transaction|eci|string|
transaction|xid|string|
billing_address|address1|string|
billing_address|city|string|
billing_address|state|string|
billing_address|zip|string|
billing_address|country|string|

```javascript
Authorize Sample:
{
  "APIKey": "XXXXXXXXX",
  "TokenExID": "XXXXXXXXX",
  "TransactionType": 1,
  "TransactionRequest": {
    "gateway": {
      "name": "FirstdataE4Gateway",
      "login": "XXXXXXXXX",
      "password": "XXXXXXXXX"
    },
    "credit_card": {
      "number": "4030006537191234",
      "month": "4",
      "year": "2016",
      "verification_value": "123",
      "first_name": "Bob",
      "last_name": "Smith"
    },
    "transaction": {
      "amount": 1200,
      "billing_address": {
        "address1": "123 Maple Street",
        "city": "Tulsa",
        "state": "OK",
        "zip": "74119",
        "country": "US"
      }
    }
  }
}
```
```javascript
Capture Sample:
{
  "APIKey": "XXXXXXXXX",
  "TokenExID": "XXXXXXXXX",
  "TransactionType": 2,
  "TransactionRequest": {
    "gateway": {
      "name": "FirstdataE4Gateway",
      "login": "XXXXXXXXX",
      "password": "XXXXXXXXX"
    },
    "transaction": {
      "amount": 1200,
      "authorization": "10000019;142"
    }
  }
}
```


### Global Cloud Pay

**Default Currency:** USD

**URL:** http://www.globalcloudpay.com

**Supported Parameters**

Parent|Field Name|Type|Notes
---|---|---|---
gateway|name|string|**GlobalCloudPayGateway**
gateway|merchant_id|string|GlobalCloudPay Merchant Number
gateway|acctid|string|GlobalCloudPay Gateway Number
gateway|password|string|GlobalCloudPay  Sign Key
credit_card|number|string|This is your TokenEx Token - Tokenex will replace the Token with the Detokenized number
credit_card|month|string|1 or 2 digit value. Example: 11
credit_card|year|string|4 digit value. Example: 2017
credit_card|verification_value|string|CVV/CSC
credit_card|first_name|string|Cardholder first name
credit_card|last_name|string|Cardholder last name
transaction|amount|integer|Transaction amount in cents. Example: $10.00 should be sent as 1000
transaction|currency|string|
transaction|order_id|string|
transaction|email|string|
transaction|ip|string|
transaction|card_issue|string|Issuing bank
transaction|description|string|
transaction|custom|string|Global Cloud Pay 'csid' field
transaction|billing_address|hash|
billing_address|phone|string|
billing_address|address1|string|
billing_address|city|string|
billing_address|state|string|
billing_address|zip|string|
billing_address|country|string|

```javascript
Authorize Sample:
{
  "APIKey": "XXXXXXXXX",
  "TokenExID": "XXXXXXXXX",
  "TransactionType": 1,
  "TransactionRequest": {
    "gateway": {
      "name": "GlobalCloudPayGateway",
      "merchant_id": "XXXXXXXXX",
      "acctid": "XXXXXXXXX",
      "password": "XXXXXXXXX"
    },
    "credit_card": {
      "number": "4111111111111111",
      "month": "4",
      "year": "2016",
      "verification_value": "123",
      "first_name": "Bob",
      "last_name": "Smith"
    },
    "transaction": {
      "amount": 1200,
      "email": "example@tokenex.com",
      "ip": "127.0.0.1",
      "order_id": "1",
      "card_issue": "Bank of china",
      currency: "USD",
      "billing_address": {
        "address1": "123 Maple Street",
        "city": "Tulsa",
        "state": "OK",
        "zip": "74119",
        "country": "US"
      }
    }
  }
}
```
```javascript
Capture Sample:
This gateway implementation does not support the 'capture' method
```


### Global Payments

**URL:** https://www.globalpaymentsinc.com

**Developer Documentation:** https://www.gpdevportal.com/

* Global Payments supports the 'reverse' action 

**Supported Parameters**

Parent|Field Name|Type|Notes
---|---|---|---
gateway|name|string|**GlobalPaymentsGateway**
gateway|login|string|Global Payments Username
gateway|password|string|Global Payments Password
credit_card|number|string|This is your TokenEx Token - Tokenex will replace the Token with the Detokenized number
credit_card|month|string|1 or 2 digit value. Example: 11
credit_card|year|string|4 digit value. Example: 2017
credit_card|verification_value|string|CVV/CSC
credit_card|first_name|string|Cardholder first name
credit_card|last_name|string|Cardholder last name
transaction|amount|integer|Transaction amount in cents. Example: $10.00 should be sent as 1000
transaction|currency|string|ISO 4217 3-letter currency codes. Default: USD
transaction|authorization|string|Required only for capture, refund, reverse, and void transactions. Obtained from the authorize or purchase transactions
transaction|order_id|string|
transaction|customer|string|
transaction|cavv|string|Cardholder authentication value
transaction|billing_address|hash|
billing_address|address1|string|
billing_address|city|string|
billing_address|state|string|
billing_address|zip|string|

```javascript
Authorize Sample:
{
  "APIKey": "XXXXXXXXXX",
  "TokenExID": "XXXXXXXXXX",
  "TransactionType": 1,
  "TransactionRequest": {
    "gateway": {
      "name": "GlobalPaymentsGateway",
      "login": "XXXXXXXXXX",
      "password": "XXXXXXXXXX"
    },
    "credit_card": {
      "number": "4111114356431111",
      "month": "4",
      "year": "2016",
      "verification_value": "111",
      "first_name": "Bob",
      "last_name": "Smith"
    },
    "transaction": {
      "amount": 1000,
      "currency": "USD",
      "order_id": "12345",
      "billing_address": {
        "address1": "123 Maple Street",
        "city": "Tulsa",
        "state": "OK",
        "zip": "74119"
      }
    }
  }
}
```
```javascript
Capture Sample:
{
  "APIKey": "XXXXXXXXXX",
  "TokenExID": "XXXXXXXXXX",
  "TransactionType": 2,
  "TransactionRequest": {
    "gateway": {
      "name": "GlobalPaymentsGateway",
      "login": "XXXXXXXXXX",
      "password": "XXXXXXXXXX"
    },
    "transaction": {
      "authorization": "099579;00000003",
      "amount": 1000
    }
  }
}
```


### Litle & Co

**URL:** http://www.litle.com

**Default Currency:** USD

**Developer Documentation:** http://litleco.github.io

**Supported Parameters**

Parent|Field Name|Type|Notes
---|---|---|---
gateway|name|string|**LitleGateway**
gateway|merchant_id|string|Litle Merchant ID
gateway|login|string|Litle User
gateway|password|string|Litle Password
gateway|endpoint|string|Set to 'prelive' to set the gateway endpoint to Litle's prelive test environment. Can only be enabled in TokenEx's TEST environment.
credit_card|number|string|This is your TokenEx Token - Tokenex will replace the Token with the Detokenized number
credit_card|month|string|1 or 2 digit value. Example: 11
credit_card|year|string|4 digit value. Example: 2017
credit_card|verification_value|string|CVV/CSC
credit_card|first_name|string|Cardholder first name
credit_card|last_name|string|Cardholder last name
credit_card|track_data|string|Track 1/Track 2 data
check|routing_number|string|
check|account_number|string|This is your TokenEx Token - Tokenex will replace the Token with the Detokenized number
check|number|string|
check|account_type|string|
transaction|amount|integer|Transaction amount in cents. Example: $10.00 should be sent as 1000
transaction|authorization|string|Required only for capture, refund, and void transactions. Obtained from the authorize or purchase actions
transaction|order_id|string|
transaction|email|string|
transaction|customer|string|
transaction|report_group|string|
transaction|order_source|string|
transaction|merchant_affiliate|string|
transaction|merchant_campaign|string|
transaction|merchant_grouping_id|string|
transaction|billing_address|hash|
transaction|shipping_address|hash|
billing_address|company|string|
billing_address|address1|string|
billing_address|address2|string|
billing_address|city|string|
billing_address|state|string|
billing_address|zip|string|
billing_address|country|string|
billing_address|phone|string|
shipping_address|company|string|
shipping_address|address1|string|
shipping_address|address2|string|
shipping_address|city|string|
shipping_address|state|string|
shipping_address|zip|string|
shipping_address|country|string|
shipping_address|phone|string|

```javascript
Authorize Sample:
{
  "APIKey": "XXXXXXXXX",
  "TokenExID": "XXXXXXXXX",
  "TransactionType": 1,
  "TransactionRequest": {
    "gateway": {
      "name": "LitleGateway",
      "merchant_id": "XXXXXXXXX",
      "login": "XXXXXXXXX",
      "password": "XXXXXXXXX"
    },
    "credit_card": {
      "number": "4030006537191234",
      "month": "4",
      "year": "2016",
      "verification_value": "123",
      "first_name": "Bob",
      "last_name": "Smith"
    },
    "transaction": {
      "amount": 1200,
      "billing_address": {
        "address1": "123 Maple Street",
        "city": "Tulsa",
        "state": "OK",
        "zip": "74119",
        "country": "US"
      }
    }
  }
}
```
```javascript
Capture Sample:
{
  "APIKey": "XXXXXXXXX",
  "TokenExID": "XXXXXXXXX",
  "TransactionType": 2,
  "TransactionRequest": {
    "gateway": {
      "name": "LitleGateway",
      "merchant_id": "XXXXXXXXX",
      "login": "XXXXXXXXX",
      "password": "XXXXXXXXX"
    },
    "transaction": {
      "amount": 1200,
      "authorization": "10000019"
    }
  }
}
```


### Lucy

**URL:** https://www.cynergydata.com

**Supported Parameters**

Parent|Field Name|Type|Notes
---|---|---|---
gateway|name|string|**LucyGateway**
gateway|login|string|Lucy Gateway Login
gateway|password|string|Lucy Gateway Password
credit_card|number|string|This is your TokenEx Token - Tokenex will replace the Token with the Detokenized number
credit_card|month|string|1 or 2 digit value. Example: 11
credit_card|year|string|4 digit value. Example: 2017
credit_card|verification_value|string|CVV/CSC
credit_card|first_name|string|Cardholder first name
credit_card|last_name|string|Cardholder last name
credit_card|track_data|string|Track 1/Track 2 data
transaction|amount|integer|Transaction amount in cents. Example: $10.00 should be sent as 1000
transaction|authorization|string|Required only for capture, refund, and void transactions. Obtained from the authorize or purchase actions
transaction|order_id|string|
transaction|customer|string|
transaction|billing_address|hash|
billing_address|address1|string|
billing_address|city|string|
billing_address|state|string|
billing_address|zip|string|

```javascript
Authorize Sample:
{
  "APIKey": "XXXXXXXXX",
  "TokenExID": "XXXXXXXXX",
  "TransactionType": 1,
  "TransactionRequest": {
    "gateway": {
      "name": "LucyGateway",
      "login": "XXXXXXXXX",
      "password": "XXXXXXXXX"
    },
    "credit_card": {
      "number": "4030006537191234",
      "month": "4",
      "year": "2016",
      "verification_value": "123",
      "first_name": "Bob",
      "last_name": "Smith"
    },
    "transaction": {
      "amount": 1200,
      "billing_address": {
        "address1": "123 Maple Street",
        "city": "Tulsa",
        "state": "OK",
        "zip": "74119"
      }
    }
  }
}
```
```javascript
Capture Sample:
{
  "APIKey": "XXXXXXXXX",
  "TokenExID": "XXXXXXXXX",
  "TransactionType": 2,
  "TransactionRequest": {
    "gateway": {
      "name": "LucyGateway",
      "login": "XXXXXXXXX",
      "password": "XXXXXXXXX"
    },
    "transaction": {
      "amount": 1200,
      "authorization": "10000019;397"
    }
  }
}
```


### Maxiopago

**URL:** http://www.maxipago.com/

**Developer Documentation:** http://www.maxipago.com/docs/maxiPago_API_Latest.pdf

**Supported Parameters**

Parent|Field Name|Type|Notes
---|---|---|---
gateway|name|string|**MaxipagoGateway**
gateway|login|string|Maxipago Merchant ID
gateway|password|string|Maxipago Merchant Key
credit_card|number|string|This is your TokenEx Token - Tokenex will replace the Token with the Detokenized number
credit_card|month|string|1 or 2 digit value. Example: 11
credit_card|year|string|4 digit value. Example: 2017
credit_card|verification_value|string|CVV/CSC
credit_card|first_name|string|Cardholder first name
credit_card|last_name|string|Cardholder last name
transaction|amount|integer|Transaction amount in cents. Example: $10.00 should be sent as 1000
transaction|authorization|string|Required only for capture, refund, and void transactions. Obtained from the authorize or purchase actions
transaction|order_id|string|
transaction|processor|string|Defaults to "1" in the sandbox environment and "4" in the production environment
transaction|ip|string|
transaction|billing_address|hash|
billing_address|address1|string|
billing_address|address2|string|
billing_address|city|string|
billing_address|state|string|
billing_address|zip|string|
billing_address|country|string|
billing_address|phone|string|

```javascript
Authorize Sample:
{
  "APIKey": "XXXXXXXXXX",
  "TokenExID": "XXXXXXXXXX",
  "TransactionType": 1,
  "TransactionRequest": {
    "gateway": {
      "name": "MaxipagoGateway",
      "login": "XXXXXXXXXX",
      "password": "XXXXXXXXXX"
    },
    "credit_card": {
      "first_name": "Bob",
      "last_name": "Smith",
      "number": "4111114356431111",
      "month": "4",
      "year": "2016",
      "verification_value": "111"
    },
    "transaction": {
      "amount": 1000,
      "order_id": "12345",
      "billing_address": {
        "address1": "123 Maple Street",
        "city": "Tulsa",
        "state": "OK",
        "zip": "74119"
      }
    }
  }
}
```
```javascript
Capture Sample:
{
  "APIKey": "XXXXXXXXXX",
  "TokenExID": "XXXXXXXXXX",
  "TransactionType": 2,
  "TransactionRequest": {
    "gateway": {
      "name": "MaxipagoGateway",
      "login": "XXXXXXXXXX",
      "password": "XXXXXXXXXX"
    },
    "transaction": {
      "authorization": "359308705;12345;3632456",
      "amount": 1000
    }
  }
}
```


### Merchant e-Solutions

**URL:** https://www.merchante-solutions.com/

**Supported Parameters**

Parent|Field Name|Type|Notes
---|---|---|---
gateway|name|string|**MerchantESolutionsGateway**
gateway|login|string|MerchantESolutionsGateway Profile ID
gateway|password|string|MerchantESolutionsGateway Key
credit_card|number|string|This is your TokenEx Token - Tokenex will replace the Token with the Detokenized number
credit_card|month|string|1 or 2 digit value. Example: 11
credit_card|year|string|4 digit value. Example: 2017
credit_card|verification_value|string|CVV/CSC
transaction|amount|integer|Transaction amount in cents. Example: $10.00 should be sent as 1000
transaction|authorization|string|Required only for capture, refund, and void transactions. Obtained from the authorize or purchase actions
transaction|order_id|string|
transaction|customer|string|
transaction|moto_ecommerce_ind|string|
transaction|billing_address|hash|
billing_address|address1|string|
billing_address|zip|string|

```javascript
Authorize Sample:
{
  "APIKey": "XXXXXXXXX",
  "TokenExID": "XXXXXXXXX",
  "TransactionType": 1,
  "TransactionRequest": {
    "gateway": {
      "name": "MerchantESolutionsGateway",
      "login": "XXXXXXXXX",
      "password": "XXXXXXXXX"
    },
    "credit_card": {
      "number": "4030006537191234",
      "month": "4",
      "year": "2016",
      "verification_value": "123"
    },
    "transaction": {
      "amount": 1200,
      "billing_address": {
        "address1": "123 Maple Street",
        "zip": "74119"
      }
    }
  }
}
```
```javascript
Capture Sample:
{
  "APIKey": "XXXXXXXXX",
  "TokenExID": "XXXXXXXXX",
  "TransactionType": 2,
  "TransactionRequest": {
    "gateway": {
      "name": "MerchantESolutionsGateway",
      "login": "XXXXXXXXX",
      "password": "XXXXXXXXX"
    },
    "transaction": {
      "amount": 1200,
      "authorization": "10000019"
    }
  }
}
```


### Merchant Link TV2G Payment Gateway

**URL:** http://www.merchantlink.com

* The 'reverse' action can be used to send a CCTimeout message

**Supported Parameters**

Parent|Field Name|Type|Notes
---|---|---|---
gateway|name|string|**MerchantLinkGateway**
gateway|login|string|Company Code assigned by Merchant Link
gateway|subid|string|Site Code assigned by Merchant Link
gateway|ssl_cert|string|Client SSL certificate provided by Merchant Link. The certificate must be in valid PEM format.
gateway|ssl_key|string|Client SSL key provided by Merchant Link. The key should must be in valid PEM format.
gateway|ssl_key_password|string|Optional SSL key encryption password. Must be provided if 'ssl_key' is encrypted.
credit_card|number|string|This is your TokenEx Token - Tokenex will replace the Token with the Detokenized number
credit_card|month|string|1 or 2 digit value. Example: 11
credit_card|year|string|4 digit value. Example: 2017
credit_card|verification_value|string|CVV/CSC
credit_card|track_1_data|string|Track 1 data
credit_card|track_2_data|string|track 2 data
transaction|amount|integer|Transaction amount in cents. Example: $10.00 should be sent as 1000
transaction|authorization|string|Required only for 'capture' transactions. Value is obtained from the 'authorize' transaction.
transaction|terminal_id|string|Terminal ID assigned by Merchant Link
transaction|lane_id|string|Lane ID assigned by Merchant Link
transaction|transaction_index|string|POS Transaction Identifer
transaction|pos_version|string|
transaction|posts|string|
transaction|date|string|Local transaction date
transaction|time|string|Local transaction time
transaction|order_id|string|The ID or number generated by the POS system that identifies the customer check / ticket / receipt.
transaction|moto_ecommerce_ind|string|Defaults to '0'
transaction|input_method|string|Defaults to 'K'
transaction|input_capability|string|Defaults to 'B'
transaction|authentication_method|string|Defaults to 'S'
transaction|operating_environment|string|Defaults to '1'
transaction|pin_capability|string|Defaults to 'N'
transaction|output_capability|string|Defaults to 'B'
transaction|prior_transaction_index|string|Used for 'reverse' transactions
transaction|prior_posts|string|Used for 'reverse' transactions
transaction|prior_tranaction_type|string|Used for 'reverse' transactions
billing_address|address1|string|
billing_address|zip|string|

```javascript
Authorize Sample:
{
  "APIKey": "XXXXXXXXX",
  "TokenExID": "XXXXXXXXX",
  "TransactionType": 1,
  "TransactionRequest": {
    "gateway": {
      "name": "MerchantLinkGateway",
      "login": "XXXXXXXXX",
      "subid": "XXXXXXXXX",
      "ssl_cert": "CLIENT SSL CERTIFICATE (PEM FORMAT)",
      "ssl_key": "CLIENT SSL KEY (PEM FORMAT)"
    },
    "credit_card": {
      "number": "4012000033330026",
      "month": "4",
      "year": "2016",
      "verification_value": "123"
    },
    "transaction": {
      "amount": 1200,
      "terminal_id": "1",
      "lane_id": "01",
      "transaction_index": "916637035224",
      "pos_version": "v1.0",
      "date": "150706",
      "time": "225439",
      "posts":"2015-07-07T03:54:39.620Z",
      "order_id": "12128127161234",
      "billing_address": {
        "address1": "123 Maple Street",
        "zip": "74119"
      }
    }
  }
}
```
```javascript
Capture Sample:
{
  "APIKey": "XXXXXXXXX",
  "TokenExID": "XXXXXXXXX",
  "TransactionType": 2,
  "TransactionRequest": {
    "gateway": {
      "name": "MerchantLinkGateway",
      "login": "XXXXXXXXX",
      "subid": "XXXXXXXXX",
      "ssl_cert": "CLIENT SSL CERTIFICATE (PEM FORMAT)",
      "ssl_key": "CLIENT SSL KEY (PEM FORMAT)"
    },
    "transaction": {
      "authorization":"MV0008881815;1111",
      "amount": 1200,
      "terminal_id": "1",
      "lane_id": "01",
      "transaction_index": "916637035224",
      "pos_version": "v1.0",
      "date": "150706",
      "time": "225439",
      "posts":"2015-07-07T03:54:39.620Z",
      "order_id": "12128127161234"
    }
  }
} 
```


### Moneris eSelect Plus

**URL:** http://www.moneris.com

**Developer Documentation:** https://developer.moneris.com/

**Supported Parameters**

Parent|Field Name|Type|Notes
---|---|---|---
gateway|name|string|**MonerisGateway**
gateway|login|string|Moneris Store ID
gateway|password|string|Moneris API Token
gateway|cvv_enabled|string|Enable CVV support. Default is false.
gateway|avs_enabled|string|Enable AVS support. Default is false.
credit_card|number|string|This is your TokenEx Token - Tokenex will replace the Token with the Detokenized number
credit_card|month|string|1 or 2 digit value. Example: 11
credit_card|year|string|4 digit value. Example: 2017
credit_card|verification_value|string|CVV/CSC
transaction|amount|integer|Transaction amount in cents. Example: $10.00 should be sent as 1000
transaction|authorization|string|Required only for capture, refund, and void transactions
transaction|order_id|string|
transaction|customer|string|
transaction|cavv|string|
transaction|crypt_type|string|Default value is 7
transaction|billing_address|hash|
billing_address|address1|string|
billing_address|zip|string|

```javascript
Authorize Sample:
{
  "APIKey": "XXXXXXXXX",
  "TokenExID": "XXXXXXXXX",
  "TransactionType": 1,
  "TransactionRequest": {
    "gateway": {
      "name": "MonerisGateway",
      "login": "XXXXXXXXX",
      "password": "XXXXXXXXX",
      "avs_enabled": "true"
    },
    "credit_card": {
      "number": "4030006537191234",
      "month": "4",
      "year": "2016",
      "verification_value": "123"
    },
    "transaction": {
      "amount": 1200,
      "billing_address": {
        "address1": "123 Maple Street",
        "zip": "74119"
      }
    }
  }
}
```
```javascript
Capture Sample:
{
  "APIKey": "XXXXXXXXX",
  "TokenExID": "XXXXXXXXX",
  "TransactionType": 2,
  "TransactionRequest": {
    "gateway": {
      "name": "MonerisGateway",
      "login": "XXXXXXXXX",
      "password": "XXXXXXXXX"
    },
    "transaction": {
      "amount": 1200,
      "authorization": "10000019;12"
    }
  }
}
```


### Moneris (US) eSelect Plus

**URL:** http://www.monerisusa.com

**Developer Documentation:** https://developer.moneris.com/

**Supported Parameters**

Parent|Field Name|Type|Notes
---|---|---|---
gateway|name|string|**MonerisUsGateway**
gateway|login|string|Moneris Store ID
gateway|password|string|Moneris API Token
gateway|cvv_enabled|string|Enable CVV support. Default is false.
gateway|avs_enabled|string|Enable AVS support. Default is false.
credit_card|number|string|This is your TokenEx Token - Tokenex will replace the Token with the Detokenized number
credit_card|month|string|1 or 2 digit value. Example: 11
credit_card|year|string|4 digit value. Example: 2017
credit_card|verification_value|string|CVV/CSC
transaction|amount|integer|Transaction amount in cents. Example: $10.00 should be sent as 1000
transaction|authorization|string|Required only for capture, refund, and void transactions
transaction|order_id|string|
transaction|customer|string|
transaction|cavv|string|
transaction|crypt_type|string|Default value is 7
transaction|billing_address|hash|
billing_address|address1|string|
billing_address|zip|string|

```javascript
Authorize Sample:
{
  "APIKey": "XXXXXXXXX",
  "TokenExID": "XXXXXXXXX",
  "TransactionType": 1,
  "TransactionRequest": {
    "gateway": {
      "name": "MonerisUsGateway",
      "login": "XXXXXXXXX",
      "password": "XXXXXXXXX",
      "avs_enabled": "true"
    },
    "credit_card": {
      "number": "4030006537191234",
      "month": "4",
      "year": "2016",
      "verification_value": "123"
    },
    "transaction": {
      "amount": 1200,
      "billing_address": {
        "address1": "123 Maple Street",
        "zip": "74119"
      }
    }
  }
}
```
```javascript
Capture Sample:
{
  "APIKey": "XXXXXXXXX",
  "TokenExID": "XXXXXXXXX",
  "TransactionType": 2,
  "TransactionRequest": {
    "gateway": {
      "name": "MonerisUsGateway",
      "login": "XXXXXXXXX",
      "password": "XXXXXXXXX"
    },
    "transaction": {
      "amount": 1200,
      "authorization": "10000019;12"
    }
  }
}
```


### NMI

**URL:** http://www.nmi.com

**Default Currency:** USD

**Supported Parameters**

Parent|Field Name|Type|Notes
---|---|---|---
gateway|name|string|**NmiGateway**
gateway|login|string|NMI Login
gateway|password|string|NMI Password
credit_card|number|string|This is your TokenEx Token - Tokenex will replace the Token with the Detokenized number
credit_card|month|string|1 or 2 digit value. Example: 11
credit_card|year|string|4 digit value. Example: 2017
credit_card|verification_value|string|CVV/CSC
credit_card|first_name|string|Cardholder first name
credit_card|last_name|string|Cardholder last name
check|routing_number|string|
check|account_number|string|This is your TokenEx Token - Tokenex will replace the Token with the Detokenized number
check|bank_name|string|
check|name|string|Name under which the account is maintained at the bank
check|account_type|string|
check|number|string|
transaction|amount|integer|Transaction amount in cents. Example: $10.00 should be sent as 1000
transaction|currency|string|
transaction|authorization|string|Required only for capture, refund, and void transactions. Obtained from the authorize or purchase actions
transaction|order_id|string|
transaction|description|string|
transaction|email|string|
transaction|ip|string|
transaction|customer|string|
transaction|billing_address|hash|
transaction|shipping_address|hash|
transaction|card_number|string|Required only for refund transactions. Last 4 numbers of the credit card
transaction|first_name|string|Optional for refund transactions
transaction|last_name|string|Optional for refund transactions
transaction|zip|string|Optional for refund transactions
billing_address|company|string|
billing_address|phone|string|
billing_address|address1|string|
billing_address|city|string|
billing_address|state|string|
billing_address|zip|string|
billing_address|country|string|
shipping_address|first_name|string|
shipping_address|last_name|string|
shipping_address|company|string|
shipping_address|phone|string|
shipping_address|address1|string|
shipping_address|city|string|
shipping_address|state|string|
shipping_address|zip|string|
shipping_address|country|string|

```javascript
Authorize Sample:
{
  "APIKey": "XXXXXXXXX",
  "TokenExID": "XXXXXXXXX",
  "TransactionType": 1,
  "TransactionRequest": {
    "gateway": {
      "name": "NmiGateway",
      "login": "XXXXXXXXX",
      "password": "XXXXXXXXX"
    },
    "credit_card": {
      "number": "4030006537191234",
      "month": "4",
      "year": "2016",
      "verification_value": "123",
      "first_name": "Bob",
      "last_name": "Smith"
    },
    "transaction": {
      "amount": 1200,
      "billing_address": {
        "address1": "123 Maple Street",
        "city": "Tulsa",
        "state": "OK",
        "zip": "74119",
        "country": "US"
      }
    }
  }
}
```
```javascript
Capture Sample:
{
  "APIKey": "XXXXXXXXX",
  "TokenExID": "XXXXXXXXX",
  "TransactionType": 2,
  "TransactionRequest": {
    "gateway": {
      "name": "NmiGateway",
      "login": "XXXXXXXXX",
      "password": "XXXXXXXXX"
    },
    "transaction": {
      "amount": 1200,
      "authorization": "10000019"
    }
  }
}
```


### Optimal Payments NETBANX

**URL:** http://www.optimalpayments.com

**Developer Documentation:** https://developer.optimalpayments.com

**Supported Parameters**

Parent|Field Name|Type|Notes
---|---|---|---
gateway|name|string|**OptimalPaymentNetbanxGateway**
gateway|acctid|string|Optimal Payments Account Number
gateway|password|string|Optimal Payments API Key
credit_card|number|string|This is your TokenEx Token - Tokenex will replace the Token with the Detokenized number
credit_card|month|string|1 or 2 digit value. Example: 11
credit_card|year|string|4 digit value. Example: 2017
credit_card|verification_value|string|CVV/CSC
credit_card|first_name|string|Cardholder first name
credit_card|last_name|string|Cardholder last name
transaction|amount|integer|Transaction amount in cents. Example: $10.00 should be sent as 1000
transaction|authorization|string|Required only for capture, refund, and void transactions. Obtained from the authorize or purchase actions
transaction|order_id|string|
transaction|email|string|
transaction|ip|string|
transaction|description|string|
transaction|billing_address|hash|
transaction|shipping_address|hash|
billing_address|phone|string|
billing_address|address1|string|
billing_address|address2|string|
billing_address|city|string|
billing_address|state|string|
billing_address|zip|string|
billing_address|country|string|
shipping_address|address1|string|
shipping_address|city|string|
shipping_address|state|string|
shipping_address|zip|string|
shipping_address|country|string|

```javascript
Authorize Sample:
{
  "APIKey": "XXXXXXXXX",
  "TokenExID": "XXXXXXXXX",
  "TransactionType": 1,
  "TransactionRequest": {
    "gateway": {
      "name": "OptimalPaymentNetbanxGateway",
      "acctid": "XXXXXXXXX",
      "password": "XXXXXXXXX"
    },
    "credit_card": {
      "number": "4030006537191234",
      "month": "4",
      "year": "2016",
      "verification_value": "123",
      "first_name": "Bob",
      "last_name": "Smith"
    },
    "transaction": {
      "amount": 1200,
      "billing_address": {
        "address1": "123 Maple Street",
        "city": "Tulsa",
        "state": "OK",
        "zip": "74119",
        "country": "US"
      }
    }
  }
}
```
```javascript
Capture Sample:
{
  "APIKey": "XXXXXXXXX",
  "TokenExID": "XXXXXXXXX",
  "TransactionType": 2,
  "TransactionRequest": {
    "gateway": {
      "name": "OptimalPaymentNetbanxGateway",
      "acctid": "XXXXXXXXX",
      "password": "XXXXXXXXX"
    },
    "transaction": {
      "amount": 1200,
      "authorization": "c95ad35b-3d39-451f-8d82-46e1f9033e20""
    }
  }
}
```


### Orbital Chase

**URL:** http://chasepaymentech.com

**Default Currency:** CAD

**Developer Documentation:** http://download.chasepaymentech.com

AVS is only supported for countries: US CA UK GB
**Supported Parameters**

Parent|Field Name|Type|Notes
---|---|---|---
gateway|name|string|**OrbitalGateway**
gateway|merchant_id|string|Orbital Merchant ID
gateway|login|string|Orbital User
gateway|password|string|Orbital Password
gateway|bin|string|Default (salem) is 000001 otherwise 000002 is used
credit_card|number|string|This is your TokenEx Token - Tokenex will replace the Token with the Detokenized number
credit_card|month|string|1 or 2 digit value. Example: 11
credit_card|year|string|4 digit value. Example: 2017
credit_card|verification_value|string|CVV/CSC
credit_card|first_name|string|Cardholder first name
credit_card|last_name|string|Cardholder last name
credit_card|track_data|string|Track 1/Track 2 data
transaction|amount|integer|Transaction amount in cents. Example: $10.00 should be sent as 1000
transaction|currency|string|Default value is used if this value is not set. Format ISO alpha code
transaction|authorization|string|Required only for capture, refund, and void transactions. Obtained from the authorize or purchase actions
transaction|order_id|string|
transaction|terminal_id|string|Default 001
transaction|industry_type|string|
transaction|comments|string|
transaction|eci|string|
transaction|cavv|string|
transaction|xid|string|
transaction|aav|string|
transaction|recurring_ind|string|
transaction|transaction_index|string|Void requests only; TxRefIdx
transaction|reversal_retry_number|string|Void requests only; ReversalRetryNumber
transaction|online_reversal_ind|string|Void requests only; OnlineReversalInd
transaction|dwwalletid|string|
transaction|dwsli|string|
transaction|dwincentiveind|string|
transaction|digitalwallettype|string|
transaction|billing_address|hash|
billing_address|address1|string|
billing_address|address2|string|
billing_address|city|string|
billing_address|state|string|
billing_address|zip|string|
billing_address|country|string|To enable AVS, this value mut be a supported country value: US CA UK GB
billing_address|phone|string|
billing_address|dest_address1|string|
billing_address|dest_address2|string|
billing_address|dest_city|string|
billing_address|dest_state|string|
billing_address|dest_zip|string|
billing_address|dest_country|string|
billing_address|dest_phone|string|
billing_address|dest_name|string|

```javascript
Authorize Sample:
{
  "APIKey": "XXXXXXXXX",
  "TokenExID": "XXXXXXXXX",
  "TransactionType": 1,
  "TransactionRequest": {
    "gateway": {
      "name": "OrbitalGateway",
      "merchant_id": "XXXXXXXXX",
      "login": "XXXXXXXXX",
      "password": "XXXXXXXXX"
    },
    "credit_card": {
      "number": "4030006537191234",
      "month": "4",
      "year": "2016",
      "verification_value": "123",
      "first_name": "Bob",
      "last_name": "Smith"
    },
    "transaction": {
      "amount": 1200,
      "billing_address": {
        "address1": "123 Maple Street",
        "city": "Tulsa",
        "state": "OK",
        "zip": "74119",
        "country": "US"
      }
    }
  }
}
```
```javascript
Capture Sample:
{
  "APIKey": "XXXXXXXXX",
  "TokenExID": "XXXXXXXXX",
  "TransactionType": 2,
  "TransactionRequest": {
    "gateway": {
      "name": "OrbitalGateway",
      "merchant_id": "XXXXXXXXX",
      "login": "XXXXXXXXX",
      "password": "XXXXXXXXX"
    },
    "transaction": {
      "amount": 1200,
      "authorization": "10000019;2345"
    }
  }
}
```


### Pay Dollar

**Default Currency:** 702

**URL:** http://www.paydollar.com

* You must whitelist the TokenEx production IPs with PayDollar to use this integeration in the production environment

**Supported Parameters**

Parent|Field Name|Type|Notes
---|---|---|---
gateway|name|string|**PayDollarGateway**
gateway|merchant_id|string|PayDollar Merchant Number
credit_card|number|string|This is your TokenEx Token - Tokenex will replace the Token with the Detokenized number
credit_card|month|string|1 or 2 digit value. Example: 11
credit_card|year|string|4 digit value. Example: 2017
credit_card|verification_value|string|CVV/CSC
credit_card|first_name|string|Cardholder first name
credit_card|last_name|string|Cardholder last name
transaction|amount|integer|Transaction amount in cents. Example: $10.00 should be sent as 1000
transaction|currency|string|
transaction|order_id|string|
transaction|email|string|
transaction|ip|string|
transaction|description|string|
transaction|billing_address|hash|
billing_address|first_name|string|
billing_address|last_name|string|
billing_address|address1|string|
billing_address|address2|string|
billing_address|city|string|
billing_address|state|string|
billing_address|zip|string|
billing_address|country|string|

```javascript
Authorize Sample:
{
  "APIKey": "XXXXXXXXX",
  "TokenExID": "XXXXXXXXX",
  "TransactionType": 1,
  "TransactionRequest": {
    "gateway": {
      "name": "PayDollarGateway",
      "merchant_id": "XXXXXXXXX"
    },
    "credit_card": {
      "number": "4111111111111111",
      "month": "4",
      "year": "2016",
      "verification_value": "123",
      "first_name": "Bob",
      "last_name": "Smith"
    },
    "transaction": {
      "amount": 1200,
      "email": "example@tokenex.com",
      "ip": "127.0.0.1",
      "order_id": "1",
      currency: "702",
      "billing_address": {
        "address1": "123 Maple Street",
        "city": "Tulsa",
        "state": "OK",
        "zip": "74119",
        "country": "US"
      }
    }
  }
}
```
```javascript
Capture Sample:
This gateway implementation does not support the 'capture' method
```


### PayTrace

**URL:** http://www.paytrace.com

**Developer Documentation:** http://help.paytrace.com/api

**Supported Parameters**

Parent|Field Name|Type|Notes
---|---|---|---
gateway|name|string|**PayTraceGateway**
gateway|login|string|PayTrace Login ID
gateway|password|string|PayTrace Password
credit_card|number|string|This is your TokenEx Token - Tokenex will replace the Token with the Detokenized number
credit_card|month|string|1 or 2 digit value. Example: 11
credit_card|year|string|4 digit value. Example: 2017
credit_card|verification_value|string|CVV/CSC
transaction|amount|integer|Transaction amount in cents. Example: $10.00 should be sent as 1000
transaction|authorization|string|Required only for capture, refund, and void transactions. Obtained from the authorize or purchase actions
transaction|order_id|string|
transaction|email|string|
transaction|description|string|
transaction|billing_address|hash|
transaction|shipping_address|hash|
billing_address|name|string|
billing_address|address1|string|
billing_address|address2|string|
billing_address|city|string|
billing_address|state|string|
billing_address|zip|string|
billing_address|country|string|
shipping_address|name|string|
shipping_address|address1|string|
shipping_address|address2|string|
shipping_address|city|string|
shipping_address|state|string|
shipping_address|zip|string|
shipping_address|country|string|

```javascript
Authorize Sample:
{
  "APIKey": "XXXXXXXXX",
  "TokenExID": "XXXXXXXXX",
  "TransactionType": 1,
  "TransactionRequest": {
    "gateway": {
      "name": "PayTraceGateway",
      "login": "XXXXXXXXX",
      "password": "XXXXXXXXX"
    },
    "credit_card": {
      "number": "4012881888818888",
      "month": "4",
      "year": "2016",
      "verification_value": "999"
    },
    "transaction": {
      "amount": 1200,
      "billing_address": {
        "address1": "123 Maple Street",
        "city": "Tulsa",
        "state": "OK",
        "zip": "74119",
        "country": "US"
      }
    }
  }
}
```
```javascript
Capture Sample:
{
  "APIKey": "XXXXXXXXX",
  "TokenExID": "XXXXXXXXX",
  "TransactionType": 2,
  "TransactionRequest": {
    "gateway": {
      "name": "PayTraceGateway",
      "login": "XXXXXXXXX",
      "password": "XXXXXXXXX"
    },
    "transaction": {
      "amount": 1200,
      "authorization": "10000019"
    }
  }
}
```


### PayPal Payflow Pro

**URL:** https://www.paypal.com/us/webapps/mpp/payflow-payment-gateway

**Developer Documentation:** https://developer.paypal.com/docs/classic/payflow/integration-guide

**Supported Parameters**

Parent|Field Name|Type|Notes
---|---|---|---
gateway|name|string|**PayflowGateway**
gateway|login|string|Payflow Login
gateway|password|string|Payflow Password
gateway|partner|string|Default value is 'Paypal'
credit_card|number|string|This is your TokenEx Token - Tokenex will replace the Token with the Detokenized number
credit_card|month|string|1 or 2 digit value. Example: 11
credit_card|year|string|4 digit value. Example: 2017
credit_card|verification_value|string|CVV/CSC
credit_card|first_name|string|Cardholder first name
credit_card|last_name|string|Cardholder last name
transaction|amount|integer|Transaction amount in cents. Example: $10.00 should be sent as 1000
transaction|authorization|string|Required only for capture, void, and refund transactions. Obtained from the authorize or purchase transactions.
transaction|currency|string|ISO 4217 3-letter currency codes. Default: USD
transaction|order_id|string|
transaction|email|string|
transaction|ip|string|Customer IP address
transaction|customer|string|
transaction|po_number|string|
transaction|description|string|
transaction|comment|string|
transaction|comment2|string|
transaction|taxamt|string|
transaction|freightamt|string|
transaction|dutyamt|string|
transaction|discountamt|string|
transaction|authentication_status|string|
transaction|authentication_id|string|
transaction|eci|string|
transaction|cavv|string|
transaction|xid|string|
transaction|billing_address|hash|
transaction|shipping_address|hash|
billing_address|name|string|
billing_address|phone|string|
billing_address|address1|string|
billing_address|city|string|
billing_address|state|string|
billing_address|zip|string|
billing_address|country|string|
shipping_address|name|string|
shipping_address|phone|string|
shipping_address|address1|string|
shipping_address|city|string|
shipping_address|state|string|
shipping_address|zip|string|
shipping_address|country|string|

```javascript
Authorize Sample:
{
  "APIKey": "XXXXXXXXX",
  "TokenExID": "XXXXXXXXX",
  "TransactionType": 1,
  "TransactionRequest": {
    "gateway": {
      "name": "PayflowGateway",
      "login": "XXXXXXXXX",
      "password": "XXXXXXXXX"
    },
    "credit_card": {
      "number": "4030006537191234",
      "month": "4",
      "year": "2016",
      "verification_value": "123",
      "first_name": "Bob",
      "last_name": "Smith"
    },
    "transaction": {
      "amount": 1200,
      "billing_address": {
        "address1": "123 Maple Street",
        "city": "Tulsa",
        "state": "OK",
        "zip": "74119",
        "country": "US"
      }
    }
  }
}
```
```javascript
Capture Sample:
{
  "APIKey": "XXXXXXXXX",
  "TokenExID": "XXXXXXXXX",
  "TransactionType": 2,
  "TransactionRequest": {
    "gateway": {
      "name": "PayflowGateway",
      "login": "XXXXXXXXX",
      "password": "XXXXXXXXX"
    },
    "transaction": {
      "amount": 1200,
      "authorization": "A70A6D372173"
    }
  }
}
```


### Payment Express

**URL:** https://www.paymentexpress.com

**Developer Documentation:** https://www.paymentexpress.com/technical_resources/ecommerce_nonhosted/pxpost.html

**Supported Parameters**

Parent|Field Name|Type|Notes
---|---|---|---
gateway|name|string|**PaymentExpressGateway**
gateway|login|string|Payment Express PXPOST Username
gateway|password|string|Payment Express PXPOST Password
credit_card|number|string|This is your TokenEx Token - Tokenex will replace the Token with the Detokenized number
credit_card|month|string|1 or 2 digit value. Example: 11
credit_card|year|string|4 digit value. Example: 2017
credit_card|verification_value|string|CVV/CSC
credit_card|first_name|string|Cardholder first name
credit_card|last_name|string|Cardholder last name
transaction|amount|integer|Transaction amount in cents. Example: $10.00 should be sent as 1000
transaction|authorization|string|Required only for captureand refund transactions. Obtained from the authorize or purchase actions
transaction|order_id|string|
transaction|description|string|
transaction|currency|string|
transaction|moto_ecommerce_ind|string|Can be used to set Payment Express field ClientType
transaction|user_data_1|string|Can be used to set Payment Express field TxnData1
transaction|user_data_2|string|Can be used to set Payment Express field TxnData2
transaction|user_data_3|string|Can be used to set Payment Express field TxnData3
transaction|billing_address|hash|
billing_address|address1|string|
billing_address|zip|string|

```javascript
Authorize Sample:
{
  "APIKey": "XXXXXXXXXX",
  "TokenExID": "XXXXXXXXXX",
  "TransactionType": 1,
  "TransactionRequest": {
    "gateway": {
      "name": "PaymentExpressGateway",
      "login": "XXXXXXXXXX",
      "password": "XXXXXXXXXX"
    },
    "credit_card": {
      "first_name": "Bob",
      "last_name": "Smith",
      "number": "4111114356431111",
      "month": "4",
      "year": "2016",
      "verification_value": "111"
    },
    "transaction": {
      "amount": 1000,
      "currency", "AUD",
      "order_id": "12345",
      "billing_address": {
        "address1": "123 Maple Street",
        "city": "Tulsa",
        "state": "OK",
        "zip": "74119"
      }
    }
  }
}
```
```javascript
Capture Sample:
{
  "APIKey": "XXXXXXXXXX",
  "TokenExID": "XXXXXXXXXX",
  "TransactionType": 2,
  "TransactionRequest": {
    "gateway": {
      "name": "PaymentExpressGateway",
      "login": "XXXXXXXXXX",
      "password": "XXXXXXXXXX"
    },
    "transaction": {
      "authorization": "359308705",
      "amount": 1000
    }
  }
}
```


### Paymill

**Default Currency:** EUR

**URL:** https://www.paymill.com

**Developer Documentation:** https://developers.paymill.com

**Supported Parameters**

Parent|Field Name|Type|Notes
---|---|---|---
gateway|name|string|**PaymillGateway**
gateway|public_key|string|Paymill API Public Key
gateway|private_key|string|Paymill API Private Key
credit_card|number|string|This is your TokenEx Token - Tokenex will replace the Token with the Detokenized number
credit_card|month|string|1 or 2 digit value. Example: 11
credit_card|year|string|4 digit value. Example: 2017
credit_card|verification_value|string|CVV/CSC
transaction|amount|integer|Transaction amount in cents. Example: $10.00 should be sent as 1000
transaction|currency|string|
transaction|authorization|string|Required only for capture, void, and refund transactions. Obtained from the authorize or purchase transactions.
transaction|description|string|

```javascript
Authorize Sample:
{
  "APIKey": "XXXXXXXXX",
  "TokenExID": "XXXXXXXXX",
  "TransactionType": 1,
  "TransactionRequest": {
    "gateway": {
      "name": "PaymillGateway",
      "public_key": "XXXXXXXXX",
      "private_key": "XXXXXXXXX"
    },
    "credit_card": {
      "number": "4111111111111111",
      "month": "4",
      "year": "2016",
      "verification_value": "123"
    },
    "transaction": {
      "amount": 1200
    }
  }
}
```
```javascript
Capture Sample:
{
  "APIKey": "XXXXXXXXX",
  "TokenExID": "XXXXXXXXX",
  "TransactionType": 2,
  "TransactionRequest": {
    "gateway": {
      "name": "PaymillGateway",
      "public_key": "XXXXXXXXX",
      "private_key": "XXXXXXXXX"
    },
    "transaction": {
      "amount": 1200,
      "authorization": "1561516564;234234234"
    }
  }
}
```


### QuickBooks Merchant Services

**URL:** http://payments.intuit.com/

**Developer Documentation:** https://developer.intuit.com/docs/030_qbms/0060_documentation

* In order to access the TokenEx integration for QuickBooks, you must create an Intuit account and login to the following URLs to create a QuickBooks connection ticket. Please note that the QuickBooks tickets are different between TEST and PROD environments.
  * [Test Environment](https://merchantaccount.ptc.quickbooks.com/j/sdkconnection?appid=1053321811&sessionEnabled=false)
  * [Production Environment](https://merchantaccount.quickbooks.com/j/sdkconnection?appid=1148168705&sessionEnabled=false)

**Supported Parameters**

Parent|Field Name|Type|Notes
---|---|---|---
gateway|name|string|**QbmsGateway**
gateway|login|string|Set value to **qbms-test.tokenex.com** for TEST and set value to **qbms.tokenex.com** for LIVE
gateway|ticket|string|QBMS Connection Ticket. Please use the URLs above to create your Connection Ticket.
credit_card|number|string|This is your TokenEx Token - Tokenex will replace the Token with the Detokenized number
credit_card|month|string|1 or 2 digit value. Example: 11
credit_card|year|string|4 digit value. Example: 2017
credit_card|verification_value|string|CVV/CSC
credit_card|first_name|string|Cardholder first name
credit_card|last_name|string|Cardholder last name
transaction|amount|integer|Transaction amount in cents. Example: $10.00 should be sent as 1000
transaction|authorization|string|Required only for capture, refund, and void transactions. Obtained from the authorize or purchase actions
transaction|billing_address|hash|
billing_address|address1|string|
billing_address|zip|string|

```javascript
Authorize Sample:
{
  "APIKey": "XXXXXXXXX",
  "TokenExID": "XXXXXXXXX",
  "TransactionType": 1,
  "TransactionRequest": {
    "gateway": {
      "name": "QbmsGateway",
      "login": "XXXXXXXXX",
      "ticket": "XXXXXXXXX"
    },
    "credit_card": {
      "number": "4030006537191234",
      "month": "4",
      "year": "2016",
      "verification_value": "123",
      "first_name": "Bob",
      "last_name": "Smith"
    },
    "transaction": {
      "amount": 1200,
      "billing_address": {
        "address1": "123 Maple Street",
        "zip": "74119"
      }
    }
  }
}
```
```javascript
Capture Sample:
{
  "APIKey": "XXXXXXXXX",
  "TokenExID": "XXXXXXXXX",
  "TransactionType": 2,
  "TransactionRequest": {
    "gateway": {
      "name": "QbmsGateway",
      "login": "XXXXXXXXX",
      "ticket": "XXXXXXXXX"
    },
    "transaction": {
      "amount": 1200,
      "authorization": "10000019"
    }
  }
}
```


### Qvalent (Westpac/PayWay)

**URL:** https://www.payway.com.au

**Default Currency:** AUD

**Developer Documentation:** https://www.payway.com.au/core/DownloadsView

* You must add the TokenEx TEST and PROD environment IP addresses to your account

**Supported Parameters**

Parent|Field Name|Type|Notes
---|---|---|---
gateway|name|string|**QvalentGateway**
gateway|login|string|PayWay API Username
gateway|password|string|PayWay API Password
gateway|merchant_id|string|PayWay Merchant ID
gateway|ssl_cert|string|Client SSL certification provided by PayWay. The certificate must be in valid PEM format.
gateway|ssl_key|string|Client SSL key provided by PayWay. The key should must be in valid PEM format.
gateway|ssl_key_password|string|Optional ssl key encryption password. Must be provided if 'ssl_key' is encrypted.
credit_card|number|string|This is your TokenEx Token - Tokenex will replace the Token with the Detokenized number
credit_card|month|string|1 or 2 digit value. Example: 11
credit_card|year|string|4 digit value. Example: 2017
credit_card|verification_value|string|CVV/CSC
credit_card|first_name|string|Cardholder first name
credit_card|last_name|string|Cardholder last name
transaction|amount|integer|Transaction amount in cents. Example: $10.00 should be sent as 1000
transaction|currency|string|
transaction|authorization|string|Required only for capture, refund, and void transactions. Obtained from the authorize or purchase actions
transaction|order_id|string|
transaction|ip|string|
transaction|customer|string|
transaction|cavv|string|
transaction|xid|string|
transaction|eci|string|

```javascript
Authorize Sample:
{
  "APIKey": "XXXXXXXXXX",
  "TokenExID": "XXXXXXXXXX",
  "TransactionType": 1,
  "TransactionRequest": {
    "gateway": {
      "name": "QvalentGateway",
      "login": "XXXXXXXXXX",
      "password": "XXXXXXXXXX",
      "merchant_id": "XXXX",
      "ssl_cert": "CLIENT SSL CERTIFICATE (PEM FORMAT)",
      "ssl_key": "CLIENT SSL KEY (PEM FORMAT)"
    },
    "credit_card": {
      "number": "4111114356431111",
      "month": "4",
      "year": "2016",
      "verification_value": "111",
      "first_name": "Bob",
      "last_name": "Smith"
    },
    "transaction": {
      "amount": 1000,
      "order_id": "1234512345",
    }
  }
}
```
```javascript
Capture Sample:
{
  "APIKey": "XXXXXXXXXX",
  "TokenExID": "XXXXXXXXXX",
  "TransactionType": 2,
  "TransactionRequest": {
    "gateway": {
      "name": "QvalentGateway",
      "login": "XXXXXXXXXX",
      "password": "XXXXXXXXXX",
      "merchant_id": "XXXX",
      "ssl_cert": "CLIENT SSL CERTIFICATE (PEM FORMAT)",
      "ssl_key": "CLIENT SSL KEY (PEM FORMAT)"          
    },
    "transaction": {
      "authorization": "359308705",
      "amount": 1000
    }
  }
}
```


### Sage Payments

**URL:** https://www.sage.com

**Developer Documentation:** https://www.sagepayments.net/developer/

* The Sage gateway does not support a test API. You must enable or disable test mode on an account by account basis with Sage.

**Supported Parameters**

Parent|Field Name|Type|Notes
---|---|---|---
gateway|name|string|**SageGateway**
gateway|login|string|Sage Username
gateway|password|string|Sage Password
credit_card|number|string|This is your TokenEx Token - Tokenex will replace the Token with the Detokenized number
credit_card|month|string|1 or 2 digit value. Example: 11
credit_card|year|string|4 digit value. Example: 2017
credit_card|verification_value|string|CVV/CSC
credit_card|first_name|string|Cardholder first name
credit_card|last_name|string|Cardholder last name
transaction|amount|integer|Transaction amount in cents. Example: $10.00 should be sent as 1000
transaction|authorization|string|Required only for capture and void transactions. Obtained from the authorize or purchase transactions
transaction|order_id|string|
transaction|customer|string|
transaction|email|string|
transaction|billing_address|hash|
transaction|shipping_address|hash|
billing_address|address1|string|
billing_address|city|string|
billing_address|state|string|
billing_address|zip|string|
billing_address|country|string|
billing_address|phone|string|
billing_address|fax|string|
shipping_address|name|string|
shipping_address|address1|string|
shipping_address|city|string|
shipping_address|state|string|
shipping_address|zip|string|
shipping_address|country|string|

```javascript
Authorize Sample:
{
  "APIKey": "XXXXXXXXXX",
  "TokenExID": "XXXXXXXXXX",
  "TransactionType": 1,
  "TransactionRequest": {
    "gateway": {
      "name": "SageGateway",
      "login": "XXXXXXXXXX",
      "password": "XXXXXXXXXX"
    },
    "credit_card": {
      "number": "4111114356431111",
      "month": "4",
      "year": "2016",
      "verification_value": "111",
      "first_name": "Bob",
      "last_name": "Smith"
    },
    "transaction": {
      "amount": 1000,
      "order_id": "12345",
      "billing_address": {
        "address1": "123 Maple Street",
        "city": "Tulsa",
        "state": "OK",
        "zip": "74119"
      }
    }
  }
}
```
```javascript
Capture Sample:
{
  "APIKey": "XXXXXXXXXX",
  "TokenExID": "XXXXXXXXXX",
  "TransactionType": 2,
  "TransactionRequest": {
    "gateway": {
      "name": "SageGateway",
      "login": "XXXXXXXXXX",
      "password": "XXXXXXXXXX"
    },
    "transaction": {
      "authorization": "F9CELQPXq0;bankcard\"",
      "amount": 1000
    }
  }
}
```


### SagePay

**URL:** http://www.sagepay.co.uk

**Default Currency:** GBP

**Developer Documentation:** http://www.sagepay.co.uk/support/partners-and-developers-support

**Supported Parameters**

Parent|Field Name|Type|Notes
---|---|---|---
gateway|name|string|**SagePayGateway**
gateway|login|string|SagePay Vendor ID
credit_card|number|string|This is your TokenEx Token - Tokenex will replace the Token with the Detokenized number
credit_card|month|string|1 or 2 digit value. Example: 11
credit_card|year|string|4 digit value. Example: 2017
credit_card|verification_value|string|CVV/CSC
credit_card|first_name|string|Cardholder first name
credit_card|last_name|string|Cardholder last name
transaction|amount|integer|Transaction amount in cents. Example: $10.00 should be sent as 1000
transaction|currency|string|
transaction|authorization|string|Required only for capture, refund, and void transactions. Obtained from the authorize or purchase actions
transaction|order_id|string|
transaction|description|string|
transaction|email|string|
transaction|ip|string|
transaction|billing_address|hash|
transaction|shipping_address|hash|
billing_address|name|string|
billing_address|address1|string|
billing_address|address2|string|
billing_address|city|string|
billing_address|state|string|
billing_address|zip|string|
billing_address|country|string|
billing_address|phone|string|
shipping_address|name|string|
shipping_address|address1|string|
shipping_address|address2|string|
shipping_address|city|string|
shipping_address|state|string|
shipping_address|zip|string|
shipping_address|country|string|
shipping_address|phone|string|

```javascript
Authorize Sample:
{
  "APIKey": "XXXXXXXXXX",
  "TokenExID": "XXXXXXXXXX",
  "TransactionType": 1,
  "TransactionRequest": {
    "gateway": {
      "name": "SagePayGateway",
      "login": "XXXXXXXXXX"
    },
    "credit_card": {
      "name": "Bob Smith",
      "number": "4111114356431111",
      "month": "4",
      "year": "2016",
      "verification_value": "111"
    },
    "transaction": {
      "amount": 1000,
      "order_id": "12345",
      "billing_address": {
        "name": "Bob Smith",
        "address1": "123 Maple Street",
        "city": "Tulsa",
        "state": "OK",
        "zip": "74119"
      }
    }
  }
}
```
```javascript
Capture Sample:
{
  "APIKey": "XXXXXXXXXX",
  "TokenExID": "XXXXXXXXXX",
  "TransactionType": 2,
  "TransactionRequest": {
    "gateway": {
      "name": "SagePayGateway",
      "login": "XXXXXXXXXX"
    },
    "transaction": {
      "authorization": "359308705;1111;2342",
      "amount": 1000
    }
  }
}
```


### Secure Net

**URL:** http://www.securenet.com

**Developer Documentation:** http://www.securenet.com/files/Gateway_Implementation_Guide_4_1_5_Final.pdf

**Supported Parameters**

Parent|Field Name|Type|Notes
---|---|---|---
gateway|name|string|**SecureNetGateway**
gateway|login|string|SecureNet ID
gateway|password|string|SecureNet SecureKey
credit_card|number|string|This is your TokenEx Token - Tokenex will replace the Token with the Detokenized number
credit_card|month|string|1 or 2 digit value. Example: 11
credit_card|year|string|4 digit value. Example: 2017
credit_card|verification_value|string|CVV/CSC
credit_card|first_name|string|Cardholder first name
credit_card|last_name|string|Cardholder last name
transaction|amount|integer|Transaction amount in cents. Example: $10.00 should be sent as 1000
transaction|authorization|string|Required only for capture, refund, and void transactions. Obtained from the authorize or purchase actions
transaction|order_id|string|
transaction|invoice_number|string|
transaction|description|string|
transaction|goods_type|string|
transaction|email|string|
transaction|customer|string|
transaction|ip|string|
transaction|billing_address|hash|
transaction|shipping_address|hash|
billing_address|company|string|
billing_address|phone|string|
billing_address|address1|string|
billing_address|city|string|
billing_address|state|string|
billing_address|zip|string|
billing_address|country|string|
shipping_address|first_name|string|
shipping_address|last_name|string|
shipping_address|company|string|
shipping_address|address1|string|
shipping_address|city|string|
shipping_address|state|string|
shipping_address|zip|string|
shipping_address|country|string|

```javascript
Authorize Sample:
{
  "APIKey": "XXXXXXXXXX",
  "TokenExID": "XXXXXXXXXX",
  "TransactionType": 1,
  "TransactionRequest": {
    "gateway": {
      "name": "SecureNetGateway",
      "login": "XXXXXXXXXX",
      "password": "XXXXXXXXXX"
    },
    "credit_card": {
      "first_name": "Bob",
      "last_name": "Smith",
      "number": "4111114356431111",
      "month": "4",
      "year": "2016",
      "verification_value": "111"
    },
    "transaction": {
      "amount": 1000,
      "order_id": "12345",
      "billing_address": {
        "address1": "123 Maple Street",
        "city": "Tulsa",
        "state": "OK",
        "zip": "74119"
      }
    }
  }
}
```
```javascript
Capture Sample:
{
  "APIKey": "XXXXXXXXXX",
  "TokenExID": "XXXXXXXXXX",
  "TransactionType": 2,
  "TransactionRequest": {
    "gateway": {
      "name": "SecureNetGateway",
      "login": "XXXXXXXXXX",
      "password": "XXXXXXXXXX"
    },
    "transaction": {
      "authorization": "114187038|10.00|1111",
      "amount": 1000
    }
  }
}
```


### Six Payment Services (3CWeb2Pay)

**URL:** https://www.3cportal.com

**Default Currency:** USD

**Supported Parameters**

Parent|Field Name|Type|Notes
---|---|---|---
gateway|name|string|**SixGateway**
gateway|login|string|Six Payment Services Merchant ID
gateway|password|string|Six Payment Services Validation Code
transaction|amount|integer|Transaction amount in cents. Example: $10.00 should be sent as 1000
transaction|currency|string|
transaction|authorization|string|Required only for capture transactions
transaction|order_id|string|
transaction|url|string|
transaction|card_issue|string|CardIssueYYMM
transaction|card_issue_no|string|
transaction|user_data_1|string|
transaction|user_data_2|string|
transaction|user_data_3|string|
transaction|user_data_4|string|
transaction|user_data_5|string|
transaction|option_flags|string|
transaction|billing_address|hash|
billing_address|address1|string|
billing_address|city|string|
billing_address|state|string|
billing_address|zip|string|

```javascript
Authorize Sample:
{
  "APIKey": "XXXXXXXXXX",
  "TokenExID": "XXXXXXXXXX",
  "TransactionType": 1,
  "TransactionRequest": {
    "gateway": {
      "name": "SixGateway",
      "login": "XXXXXXXXXX",
      "password": "XXXXXXXXXX"
    },
    "credit_card": {
      "number": "4111114356431111",
      "month": "4",
      "year": "2016",
      "verification_value": "111",
      "first_name": "Bob",
      "last_name": "Smith"
    },
    "transaction": {
      "amount": 1000,
      "order_id": "12345",
      "billing_address": {
        "address1": "123 Maple Street",
        "city": "Tulsa",
        "state": "OK",
        "zip": "74119"
      }
    }
  }
}
```
```javascript
Capture Sample:
{
  "APIKey": "XXXXXXXXXX",
  "TokenExID": "XXXXXXXXXX",
  "TransactionType": 2,
  "TransactionRequest": {
    "gateway": {
      "name": "SixGateway",
      "login": "XXXXXXXXXX",
      "password": "XXXXXXXXXX"
    },
    "transaction": {
      "authorization": "F9CELQPXq0;3435\"",
      "amount": 1000
    }
  }
}
```


### Stripe

**URL:** https://stripe.com

**Default Currency:** USD

**Developer Documentation:** https://stripe.com/docs/

**Supported Parameters**

Parent|Field Name|Type|Notes
---|---|---|---
gateway|name|string|**StripeGateway**
gateway|login|string|Stripe Secret API Key
credit_card|number|string|This is your TokenEx Token - Tokenex will replace the Token with the Detokenized number
credit_card|month|string|1 or 2 digit value. Example: 11
credit_card|year|string|4 digit value. Example: 2017
credit_card|verification_value|string|CVV/CSC
credit_card|track_data|string|Track 1/Track 2 data
credit_card|first_name|string|Cardholder first name
credit_card|last_name|string|Cardholder last name
transaction|amount|integer|Transaction amount in cents. Example: $10.00 should be sent as 1000
transaction|currency|string|
transaction|authorization|string|Required only for capture, refund, and void transactions. Obtained from the authorize or purchase actions
transaction|order_id|string|
transaction|description|string|
transaction|email|string|
transaction|ip|string|
transaction|idempotency_key|string|
transaction|metadata|string|Pipe delimited key value pairs. Ex: key1=value1|key2=value2|key3]value3
transaction|billing_address|hash|
billing_address|address1|string|
billing_address|address2|string|
billing_address|city|string|
billing_address|state|string|
billing_address|zip|string|
billing_address|country|string|

```javascript
Authorize Sample:
{
  "APIKey": "XXXXXXXXXX",
  "TokenExID": "XXXXXXXXXX",
  "TransactionType": 1,
  "TransactionRequest": {
    "gateway": {
      "name": "StripeGateway",
      "login": "XXXXXXXXXX"
    },
    "credit_card": {
      "first_name": "Bob",
      "last_name": "Smith",
      "number": "4111114356431111",
      "month": "4",
      "year": "2016",
      "verification_value": "111"
    },
    "transaction": {
      "amount": 1000,
      "order_id": "12345",
      "billing_address": {
        "address1": "123 Maple Street",
        "city": "Tulsa",
        "state": "OK",
        "zip": "74119"
      }
    }
  }
}
```
```javascript
Capture Sample:
{
  "APIKey": "XXXXXXXXXX",
  "TokenExID": "XXXXXXXXXX",
  "TransactionType": 2,
  "TransactionRequest": {
    "gateway": {
      "name": "StripeGateway",
      "login": "XXXXXXXXXX"
    },
    "transaction": {
      "authorization": "359308705",
      "amount": 1000
    }
  }
}
```


### TransFirst

**URL:** http://www.transfirst.com

* The TransFirst classic gateway does not support the 'authorize' or 'capture' actions.

**Supported Parameters**

Parent|Field Name|Type|Notes
---|---|---|---
gateway|name|string|**TransFirstGateway**
gateway|login|string|TransFirst Merchant ID
gateway|password|string|TransFirst RegKey
credit_card|number|string|This is your TokenEx Token - Tokenex will replace the Token with the Detokenized number
credit_card|month|string|1 or 2 digit value. Example: 11
credit_card|year|string|4 digit value. Example: 2017
credit_card|verification_value|string|CVV/CSC
credit_card|first_name|string|Cardholder first name
credit_card|last_name|string|Cardholder last name
transaction|amount|integer|Transaction amount in cents. Example: $10.00 should be sent as 1000
transaction|authorization|string|Required only for refund and void transactions. Obtained from the purchase action.
transaction|order_id|string|
transaction|description|string|
transaction|billing_address|hash|
billing_address|address1|string|
billing_address|zip|string|

```javascript
Authorize Sample:
Note: This gateway does not support the 'authorize' action. 
This example is a 'purchase' transaction.

{
  "APIKey": "XXXXXXXXXX",
  "TokenExID": "XXXXXXXXXX",
  "TransactionType": 3,
  "TransactionRequest": {
    "gateway": {
      "name": "TransFirstGateway",
      "login": "XXXXXXXXXX",
      "password": "XXXXXXXXXX"
    },
    "credit_card": {
      "number": "4111114356431111",
      "month": "4",
      "year": "2016",
      "verification_value": "111"
    },
    "transaction": {
      "amount": 1000,
      "order_id": "12345",
      "billing_address": {
        "address1": "123 Maple Street",
        "zip": "74119"
      }
    }
  }
}
```
```javascript
Capture Sample:
Note: This gateway does not support the 'capture' action. 
This example is a 'void' transaction.

{
  "APIKey": "XXXXXXXXXX",
  "TokenExID": "XXXXXXXXXX",
  "TransactionType": 5,
  "TransactionRequest": {
    "gateway": {
      "name": "TransFirstGateway",
      "login": "XXXXXXXXXX",
      "password": "XXXXXXXXXX"
    },
    "transaction": {
      "authorization": "3593087051111"
    }
  }
}
```


### TSYS

**URL:** http://www.tsys.com

**Developer Documentation:** https://tsys.force.com/partner/login  (TransITAPI3.0FileSpec)

**Supported Parameters**

Parent|Field Name|Type|Notes
---|---|---|---
gateway|name|string|**TsysGateway**
gateway|login|string|TSYS Device ID
gateway|password|string|TSYS Transaction Key
credit_card|number|string|This is your TokenEx Token - Tokenex will replace the Token with the Detokenized number
credit_card|month|string|1 or 2 digit value. Example: 11
credit_card|year|string|4 digit value. Example: 2017
credit_card|verification_value|string|CVV/CSC
credit_card|first_name|string|Cardholder first name
credit_card|last_name|string|Cardholder last name
transaction|amount|integer|Transaction amount in cents. Example: $10.00 should be sent as 1000
transaction|currency|string|
transaction|authorization|string|Required only for capture and void transactions. Obtained from the authorize or purchase actions
transaction|order_id|string|
transaction|description|string|
transaction|billing_address|hash|
billing_address|address1|string|
billing_address|zip|string|

```javascript
Authorize Sample:
{
  "APIKey": "XXXXXXXXX",
  "TokenExID": "XXXXXXXXX",
  "TransactionType": 1,
  "TransactionRequest": {
    "gateway": {
      "name": "TsysGateway",
      "login": "XXXXXXXXX",
      "password": "XXXXXXXXX"
    },
    "credit_card": {
      "number": "4030006537191234",
      "month": "4",
      "year": "2016",
      "verification_value": "123",
      "first_name": "Bob",
      "last_name": "Smith"
    },
    "transaction": {
      "amount": 1200,
      "billing_address": {
        "address1": "123 Maple Street",
        "zip": "74119"
      }
    }
  }
}
```
```javascript
Capture Sample:
{
  "APIKey": "XXXXXXXXX",
  "TokenExID": "XXXXXXXXX",
  "TransactionType": 2,
  "TransactionRequest": {
    "gateway": {
      "name": "TsysGateway",
      "login": "XXXXXXXXX",
      "password": "XXXXXXXXX"
    },
    "transaction": {
      "amount": 1200,
      "authorization": "03847424452"
    }
  }
}
```


### USA ePay

**URL:** http://www.usaepay.com

**Default Currency:** USD

**Developer Documentation:** http://wiki.usaepay.com/developer/transactionapi

**Supported Parameters**

Parent|Field Name|Type|Notes
---|---|---|---
gateway|name|string|**UsaEpayTransactionGateway**
gateway|login|string|USAePay Source Key
credit_card|number|string|This is your TokenEx Token - Tokenex will replace the Token with the Detokenized number
credit_card|month|string|1 or 2 digit value. Example: 11
credit_card|year|string|4 digit value. Example: 2017
credit_card|verification_value|string|CVV/CSC
credit_card|first_name|string|Cardholder first name
credit_card|last_name|string|Cardholder last name
transaction|amount|integer|Transaction amount in cents. Example: $10.00 should be sent as 1000
transaction|currency|string|
transaction|authorization|string|Required only for capture, void, and refund transactions. Obtained from the authorize or purchase transactions
transaction|order_id|string|
transaction|invoice_number|string|
transaction|description|string|
transaction|customer|string|
transaction|email|string|
transaction|ip|string|
transaction|cavv|string|
transaction|eci|string|
transaction|user_data_1|string|
transaction|user_data_2|string|
transaction|user_data_3|string|
transaction|user_data_4|string|
transaction|user_data_5|string|
transaction|split_2_key|string|Split payment account #2
transaction|split_3_key|string|Split payment account #3
transaction|split_2_amount|integer|Split payment amount #2. Transaction amount in cents. Example: $10.00 should be sent as 1000
transaction|split_3_amount|integer|Split payment amount #3. Transaction amount in cents. Example: $10.00 should be sent as 1000
transaction|split_2_description|string|Split payment description #2
transaction|split_3_description|string|Split payment description #3
transaction|split_on_error|string|Action to take upon error when utilizing split payments
transaction|billing_address|hash|
transaction|shipping_address|hash|
billing_address|company|string|
billing_address|first_name|string|
billing_address|last_name|string|
billing_address|address1|string|
billing_address|address2|string|
billing_address|city|string|
billing_address|state|string|
billing_address|zip|string|
billing_address|country|string|
billing_address|phone|string|
shipping_address|company|string|
shipping_address|address1|string|
shipping_address|address2|string|
shipping_address|city|string|
shipping_address|state|string|
shipping_address|zip|string|
shipping_address|country|string|
shipping_address|phone|string|

```javascript
Authorize Sample:
{
  "APIKey": "XXXXXXXXXX",
  "TokenExID": "XXXXXXXXXX",
  "TransactionType": 1,
  "TransactionRequest": {
    "gateway": {
      "name": "UsaEpayTransactionGateway",
      "login": "XXXXXXXXXX"
    },
    "credit_card": {
      "number": "4111114356431111",
      "month": "4",
      "year": "2016",
      "verification_value": "111",
      "first_name": "Bob",
      "last_name": "Smith"
    },
    "transaction": {
      "amount": 1000,
      "order_id": "12345",
      "billing_address": {
        "address1": "123 Maple Street",
        "city": "Tulsa",
        "state": "OK",
        "zip": "74119"
      }
    }
  }
}
```
```javascript
Capture Sample:
{
  "APIKey": "XXXXXXXXXX",
  "TokenExID": "XXXXXXXXXX",
  "TransactionType": 2,
  "TransactionRequest": {
    "gateway": {
      "name": "UsaEpayTransactionGateway",
      "login": "XXXXXXXXXX"
    },
    "transaction": {
      "authorization": "359308705",
      "amount": 1000
    }
  }
}
```


### WePay

**URL:** http://www.wepay.com

**Developer Documentation:** https://stage.wepay.com/developer

**Default Currency:** USD

* The WePay account must have the tokenization feature enabled. Please enable this feature before using the integration.

**Supported Parameters**

Parent|Field Name|Type|Notes
---|---|---|---
gateway|name|string|**WepayGateway**
gateway|login|string|WePay Client ID
gateway|password|string|WePay Access Token
gateway|acctid|string|WePay Account ID
credit_card|number|string|This is your TokenEx Token - Tokenex will replace the Token with the Detokenized number
credit_card|month|string|1 or 2 digit value. Example: 11
credit_card|year|string|4 digit value. Example: 2017
credit_card|verification_value|string|CVV/CSC
credit_card|first_name|string|Cardholder first name
credit_card|last_name|string|Cardholder last name
transaction|amount|integer|Transaction amount in cents. Example: $10.00 should be sent as 1000
transaction|authorization|string|Required only for capture, refund, and void transactions. Obtained from the authorize or purchase actions
transaction|email|string|
transaction|ip|string|
transaction|order_source|string|WePay original_device
transaction|description|string|WePay short_description
transaction|comment|string|WePay long_description
transaction|goods_type|string|WePay type (Default is 'goods')
transaction|url|string|WePay callback_uri
transaction|order_id|string|WePay reference_id
transaction|invoice_number|string|WePay unique_id
transaction|billing_address|hash|
billing_address|address1|string|
billing_address|address2|string|
billing_address|city|string|
billing_address|state|string|
billing_address|zip|string|
billing_address|country|string|

```javascript
Authorize Sample:
{
  "APIKey": "XXXXXXXXX",
  "TokenExID": "XXXXXXXXX",
  "TransactionType": 1,
  "TransactionRequest": {
    "gateway": {
      "name": "WepayGateway",
      "login": "XXXXXXXXX",
      "password": "XXXXXXXXX",
      "acctid": "XXXXXXXX"
    },
    "credit_card": {
      "number": "4012881888818888",
      "month": "4",
      "year": "2016",
      "verification_value": "999",
      "first_name": "Bob",
      "last_name": "Smith"
    },
    "transaction": {
      "amount": 1200,
      "email": "test@example.com"
      "billing_address": {
        "address1": "123 Maple Street",
        "city": "Tulsa",
        "state": "OK",
        "zip": "74119",
        "country": "US"
      }
    }
  }
}
```
```javascript
Capture Sample:
{
  "APIKey": "XXXXXXXXX",
  "TokenExID": "XXXXXXXXX",
  "TransactionType": 2,
  "TransactionRequest": {
    "gateway": {
      "name": "PayTraceGateway",
      "login": "XXXXXXXXX",
      "password": "XXXXXXXXX",
      "acctid": "XXXXXXXX"
    },
    "transaction": {
      "amount": 0,
      "authorization": "10000019|2332"
    }
  }
}
```


### Worldpay Corporate

**URL:** https://www.worldpay.com

**Default Currency:** GBP

**Developer Documentation:** http://support.worldpay.com/support/kb/gg/pdf/dxml.pdf

**Supported Parameters**

Parent|Field Name|Type|Notes
---|---|---|---
gateway|name|string|**WorldpayGateway**
gateway|login|string|Worldpay XMl Login
gateway|password|string|Worldpay XML Password
credit_card|number|string|This is your TokenEx Token - Tokenex will replace the Token with the Detokenized number
credit_card|month|string|1 or 2 digit value. Example: 11
credit_card|year|string|4 digit value. Example: 2017
credit_card|verification_value|string|CVV/CSC
credit_card|first_name|string|Cardholder first name
credit_card|last_name|string|Cardholder last name
transaction|amount|integer|Transaction amount in cents. Example: $10.00 should be sent as 1000
transaction|currency|string|
transaction|authorization|string|Required only for capture, void, and refund transactions. Obtained from the authorize or purchase transactions
transaction|order_id|string|
transaction|description|string|
transaction|ip|string|
transaction|email|string|
transaction|billing_address|hash|
billing_address|name|string|
billing_address|address1|string|
billing_address|address2|string|
billing_address|city|string|
billing_address|state|string|
billing_address|zip|string|
billing_address|country|string|
billing_address|phone|string|

```javascript
Authorize Sample:
{
  "APIKey": "XXXXXXXXXX",
  "TokenExID": "XXXXXXXXXX",
  "TransactionType": 1,
  "TransactionRequest": {
    "gateway": {
      "name": "WorldpayGateway",
      "login": "XXXXXXXXXX",
      "password": "XXXXXXXXXX"
    },
    "credit_card": {
      "number": "4111114356431111",
      "month": "4",
      "year": "2016",
      "verification_value": "111",
      "first_name": "Bob",
      "last_name": "Smith"
    },
    "transaction": {
      "amount": 1000,
      "order_id": "12345",
      "billing_address": {
        "address1": "123 Maple Street",
        "city": "Tulsa",
        "state": "OK",
        "zip": "74119"
      }
    }
  }
}
```
```javascript
Capture Sample:
{
  "APIKey": "XXXXXXXXXX",
  "TokenExID": "XXXXXXXXXX",
  "TransactionType": 2,
  "TransactionRequest": {
    "gateway": {
      "name": "WorldpayGateway",
      "login": "XXXXXXXXXX",
      "password": "XXXXXXXXXX"
    },
    "transaction": {
      "authorization": "359308705",
      "amount": 1000
    }
  }
}
```


### Worldpay US

**URL:** https://www.worldpay.us

**Default Currency:** USD

**Developer Documentation:** https://www.merchants.worldpay.us/docs

* The Worldpay US gateway does not support a dedicated test API endpoint. Test cards provided by Worldpay can be used for testing.

**Supported Parameters**

Parent|Field Name|Type|Notes
---|---|---|---
gateway|name|string|**WorldpayUsGateway**
gateway|acctid|string|Worldpay Account ID
gateway|subid|string|Worldpay Sub ID
gateway|merchantpin|string|Worldpay Merchant PIN
credit_card|number|string|This is your TokenEx Token - Tokenex will replace the Token with the Detokenized number
credit_card|month|string|1 or 2 digit value. Example: 11
credit_card|year|string|4 digit value. Example: 2017
credit_card|verification_value|string|CVV/CSC
credit_card|first_name|string|Cardholder first name
credit_card|last_name|string|Cardholder last name
transaction|amount|integer|Transaction amount in cents. Example: $10.00 should be sent as 1000
transaction|currency|string|
transaction|authorization|string|Required only for capture, void, and refund transactions. Obtained from the authorize or purchase transactions
transaction|order_id|string|
transaction|customer|string|
transaction|billing_address|hash|
transaction|shipping_address|hash|
billing_address|company|string|
billing_address|address1|string|
billing_address|address2|string|
billing_address|city|string|
billing_address|state|string|
billing_address|zip|string|
billing_address|country|string|
billing_address|phone|string|
billing_address|email|string|
billing_address|ip|string|
shipping_address|address1|string|
shipping_address|address2|string|
shipping_address|city|string|
shipping_address|state|string|
shipping_address|zip|string|
shipping_address|country|string|

```javascript
Authorize Sample:
{
  "APIKey": "XXXXXXXXXX",
  "TokenExID": "XXXXXXXXXX",
  "TransactionType": 1,
  "TransactionRequest": {
    "gateway": {
      "name": "WorldpayUsGateway",
      "acctid": "XXXXXXXXXX",
      "subid": "XXXXXXXXXX",
      "merchantpin": "XXXXXXXXXX"
    },
    "credit_card": {
      "number": "4111114356431111",
      "month": "4",
      "year": "2016",
      "verification_value": "111",
      "first_name": "Bob",
      "last_name": "Smith"
    },
    "transaction": {
      "amount": 1000,
      "order_id": "12345",
      "billing_address": {
        "address1": "123 Maple Street",
        "city": "Tulsa",
        "state": "OK",
        "zip": "74119"
      }
    }
  }
}
```
```javascript
Capture Sample:
{
  "APIKey": "XXXXXXXXXX",
  "TokenExID": "XXXXXXXXXX",
  "TransactionType": 2,
  "TransactionRequest": {
    "gateway": {
      "name": "WorldpayUsGateway",
      "acctid": "XXXXXXXXXX",
      "subid": "XXXXXXXXXX",
      "merchantpin": "XXXXXXXXXX"
    },
    "transaction": {
      "authorization": "359308705|257140011",
      "amount": 1000
    }
  }
}
```


### iATS Payments

**URL:** http://www.iatspayments.com/

* This gateway only supports purchase and refund actions

**Supported Parameters**

Parent|Field Name|Type|Notes
---|---|---|---
gateway|name|string|**IatsPaymentsGateway**
gateway|login|string|iATS agent code
gateway|password|string|iATS password
gateway|region|string|Set to UK to perform transaction against the UK endpoint
credit_card|first_name|string|Cardholder first name
credit_card|last_name|string|Cardholder last name
credit_card|number|string|This is your TokenEx Token - Tokenex will replace the Token with the Detokenized number
credit_card|month|string|1 or 2 digit value. Example: 11
credit_card|year|string|4 digit value. Example: 2017
credit_card|verification_value|string|CVV/CSC
check|routing_number|string|
check|account_number|string|This is your TokenEx Token - Tokenex will replace the Token with the Detokenized number
check|name|string|Name under which the account is maintained at the bank
check|account_type|string|
transaction|amount|integer|Transaction amount in cents. Example: $10.00 should be sent as 1000
transaction|authorization|string|Required only for refund transactions. Obtained from purchase actions
transaction|order_id|string|
transaction|description|string|
transaction|ip|string|
transaction|billing_address|hash|
billing_address|address1|string|
billing_address|city|string|
billing_address|state|string|
billing_address|zip|string|

```javascript
Authorize Sample:
The iATS Gateway dows not support 'authorize'. 
This example is a 'purchase' request.
{
  "APIKey": "XXXXXXXXXX",
  "TokenExID": "XXXXXXXXXX",
  "TransactionType": 3,
  "TransactionRequest": {
    "gateway": {
      "name": "IatsPaymentsGateway",
      "login": "XXXXXXXXXX",
      "password": "XXXXXXXXXX"
    },
    "credit_card": {
      "number": "4111114356431111",
      "month": "4",
      "year": "2016",
      "verification_value": "111"
    },
    "transaction": {
      "amount": 1000,
      "order_id": "12345",
      "billing_address": {
        "address1": "123 Maple Street",
        "city": "Tulsa",
        "state": "OK",
        "zip": "74119"
      }
    }
  }
}
```
```javascript
Capture Sample:
The iATS Gateway dows not support 'capture'. 
This example is a 'refund' request.
{
  "APIKey": "XXXXXXXXXX",
  "TokenExID": "XXXXXXXXXX",
  "TransactionType": 4,
  "TransactionRequest": {
    "gateway": {
      "name": "IatsPaymentsGateway",
      "login": "XXXXXXXXXX",
      "password": "XXXXXXXXXX"
    },
    "transaction": {
      "authorization": "359308705|23",
      "amount": 1000
    }
  }
}
```



