# Appendix
##Token Schemes

TokenEx designed 'Token Schemes' to  facilitate multi-data set acceptance without obstructing business processes or existing applications. Simply put, a Token Scheme encapsulates the validation of the input data as well as the format of the token returned to you.

For instance, if you have business requirements that hinge upon the BIN number of a credit card, you could use a format preserving Token Scheme that will retain the first 6 digits of the input data. This allows your existing business logic to remain intact while still securing your data with a tokenized environment. 

Token Schemes can be either multi use or single use. With a multi-use token scheme, the relationship between the token and input data has a one to one mapping. In order words, if you send the same input data multiple times, you'll always be returned the same token value. In contrast, with a single use token scheme, you would receive a new token value ever time.  

###sixTOKENfour
**Description:** This format will return a LUHN compliant token retaining the original first 6 and last 4 digits of the card number.

**Validation:** Numeric(0-9), Luhn compliant

**Length:** 13-19

**Token Mapping:** 1:1

**JSON value:** 1


###fourTOKENfour
**Description:** This format will return a LUHN compliant token retaining the original first 4 and last 4 digits of the card number.

**Validation:** Numeric(0-9), Luhn compliant

**Length:** 13-19

**Token Mapping:** 1:1

**JSON value:** 2


### TOKENfour

**Description:**  This format will return a LUHN compliant token retaining the original last 4 digits of the card number.

**Validation:** Numeric(0-9), Luhn compliant

**Length:** 13-19

**Token Mapping:** 1:1

**JSON value:** 3

### GUID

**Description:**  This format requires no validation and will return a GUID as the token.

**Validation:** none

**Length:** 1-1000

**Token Mapping:** 1:Many

**JSON value:** 4

### SSN

**Description:**  This format is used to tokenize a social security number.

**Validation:** Numeric(0-9)

**Length:** 9

**Token Mapping:** 1:1

**JSON value:** 5

### nGUID

**Description:**  This format is used to tokenize any number combination.

**Validation:** Numeric(0-9)

**Length:** n/a

**Token Mapping:** 1:1

**JSON value:** 6

### nTOKENfour

**Description:**  This format returns a numeric token while retaining the last 4 digits of the input data.

**Validation:** Numeric(0-9)

**Length:** 8-38

**Token Mapping:** 1:Many

**JSON value:** 7

### nTOKEN

**Description:**  This format returns a numeric, length preserving token.

**Validation:** Numeric(0-9)

**Length:** 8-38

**Token Mapping:** 1:Many

**JSON value:** 8

### sixANTOKENfour

**Description:**  This format returns an alpha numeric, length preserving token retaining the original first 6 and last 4 digits of the input data.

**Validation:** Alpha-Numeric(a-Z,0-9)

**Length:** 14-38

**Token Mapping:** 1:1

**JSON value:** 9

### fourANTOKENfour

**Description:**  This format returns an alpha numeric, length preserving token retaining the original first 4 and last 4 digits of the input data.

**Validation:** Alpha-Numeric(a-Z,0-9)

**Length:** 12-38

**Token Mapping:** 1:1

**JSON value:** 10

### ANTOKENfour

**Description:**  This format returns an alpha numeric, length preserving token retaining the original last 4 digits of the input data.

**Validation:** Alpha-Numeric(a-Z,0-9)

**Length:** 8-38

**Token Mapping:** 1:1

**JSON value:** 11

### ANTOKEN

**Description:**  This format returns an alpha numeric token, length preserving token.

**Validation:** Alpha-Numeric(a-Z,0-9)

**Length:** 4-38

**Token Mapping:** 1:1

**JSON value:** 12


### ANTOKENAUTO

**Description:**  This format automatically selects an ANTOKEN type token scheme that will retain the maximum number of original characters.

**Validation:** Alpha-Numeric(a-Z,0-9)

**Length:** 4-38

**Token Mapping:** 1:1

**JSON value:** 13


### sixASCIITOKENfour

**Description:**  This format returns an ASCII, length preserving token retaining the original first 6 and last 4 digits of the input data.

**Validation:** Accepts any ASCII characters

**Length:** 14-38

**Token Mapping:** 1:1

**JSON value:** 16


### fourASCIITOKENfour

**Description:**   This format returns an ASCII, length preserving token retaining the original first 4 and last 4 digits of the input data.

**Validation:** Accepts any ASCII characters

**Length:** 12-38

**Token Mapping:** 1:1

**JSON value:** 17

### ASCIITOKENfour

**Description:**  This format returns an ASCII, length preserving token retaining the original last 4 digits of the input data.

**Validation:** Accepts any ASCII characters

**Length:** 8-38

**Token Mapping:** 1:1

**JSON value:** 14

### ASCIITOKEN

**Description:**   This format returns an ASCII, length preserving token

**Validation:** Accepts any ASCII characters

**Length:** 4-38

**Token Mapping:** 1:1

**JSON value:** 15

### ASCIITOKENAUTO

**Description:**  This format automatically selects an ASCIITOKEN type token scheme that will retain the maximum number of original characters.

**Validation:** Accepts any ASCII characters

**Length:** 4-38

**Token Mapping:** 1:1

**JSON value:** 18

### sixNTOKENfour

**Description:**  This format will return a numeric legth preserving token retaining the original first 6 and last 4 digits of the card number. 

**Validation:** Numeric(0-9)

**Length:** 14-38

**Token Mapping:** 1:1

**JSON value:** 19

### fourNTOKENfour

**Description:**  This format will return a numeric legth preserving token retaining the original first 4 and last 4 digits of the card number. 

**Validation:** Numeric(0-9)

**Length:** 12-38

**Token Mapping:** 1:1

**JSON value:** 20

### NTOKENAUTO

**Description:**  This format automatically selects the NTOKEN type token scheme that will retain the maximum number of original characters.

**Validation:** Numeric(0-9)

**Length:** 12-38

**Token Mapping:** 1:1

**JSON value:** 21

### TOKEN

**Description:**  This format requires no validation and will return a random 38 character alpha-numeric token.

**Validation:** None

**Length:** 1-1000

**Token Mapping:** 1:1

**JSON value:** 22

### Examples

Token Scheme| Example Data  | Example Token
---|---|---
sixTOKENfour| 4242424242424242  | 424242925864242
fourTOKENfour| 4242424242424242  | 424276925864242
TOKENfour| 4242424242424242  | 635276925864242
GUID| ThisIsATest | 25892e17-80f6-415f-9c65-7395632f0223
SSN| 123456789| 958475126
nGUID| 25947582| 25892e17-80f6-415f-9c65-7395632f0223
nTOKENfour| 9876543210| 1234563210
nTOKEN| 9876543210| 8631457809
sixANTOKENfour| 4242424242424242 | 424242AV5124242 
fourANTOKENfour| 4242424242424242 | 4242ZYAV5124242 
ANTOKENfour| 4242424242424242 | 9TY2ZYAV5124242 
ANTOKEN| 9876543210| 5FR962FGT0
sixASCIITOKENfour| 1324-123-4845796| 1324-1TFTFO5796
fourASCIITOKENfour| 1324-123-484| 1324DI2-484
ASCIITOKEN| 1324-123-484| D258G4F7R4FG
sixNTOKENfour| 999999999999999 |999999685129999
fourNTOKENfour | 9999999999999 | 9999017819999
TOKEN | ThisIsATest | DUH3JSLDTAYHUCO51MXY7IINZ8HLNDU90FMTTM

## IP Addresses

**Inbound to TokenEx**

Host Name | IP Address | Port
----|----|----
test-batch.tokenex.com | 162.218.139.219 | TCP/22
test-api.tokenex.com | 199.79.51.211 | TCP/443
test-htp.tokenex.com | 199.79.51.212 |TCP/443
test-portal.tokenex.com| 199.79.51.213 |TCP/443

**Outbound from TokenEx**

If you are using TokenEx to communicate to 3rd party service providers that utilize IP filtering, you'll need to update their white list accordingly 

Service | Source IP
----|-----
Transparent Gateway API | 199.79.48.171
Transparent Gateway API | 199.79.48.163
Payment Services | 199.79.48.228
Batch File Processing | 162.218.139.219


## Code Examples

To view sample code please visit our [Github repo][samples]. Contributions are welcome!

## Glossary

**LUHN:** - The Luhn algorithm or Luhn formula, also known as the "modulus 10" or "mod 10" algorithm, is a simple checksum formula used to validate a variety of identification numbers, such as credit card numbers, IMEI numbers, National Provider Identifier numbers in US and Canadian Social Insurance Numbers.

The formula verifies a number against its included check digit, which is usually appended to a partial account number to generate the full account number. This account number must pass the following test:

From the rightmost digit, which is the check digit, moving left, double the value of every second digit; if the product of this doubling operation is greater than 9 (e.g., 7 * 2 = 14), then sum the digits of the products (e.g., 10: 1 + 0 = 1, 14: 1 + 4 = 5).

Take the sum of all the digits.  If the total modulo 10 is equal to 0 (if the total ends in zero) then the number is valid according to the Luhn formula; else it is not valid.

[samples]: https://github.com/tokenex