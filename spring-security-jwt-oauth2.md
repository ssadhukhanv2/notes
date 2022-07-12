## JWT


* [What is JWT. Explain the structure of JWT](https://jwt.io/introduction) JSON web token(JWT) is a open standard which defines a compact and selfcontained way of transfering information across parties as a JSON object. 
  * **JWT Verification**: This information within a jwt may be verified and trusted as it's digitally signed. JWT may be signed using:
    * ``secret private key`` (HMAC)
    * ``public/private key`` (RSA or EDSA)
  * **Structure of JWT**: In it's compact form JWT consists of 3 parts separated by dots (.)
    * **Header** : Header typically consists of 2 parts. 
      1. ``Type of the token``, which is JWT
      2. ``Signing algorithm used``, such as HMAC, SHA256 or RSA.

                {
                    "alg": "HS256",
                    "typ": "JWT"
                }

      The header is then Base64 encoded.
    * **Payload**: The second part of the token is the payload. This contains the claims. Claims are statements about the entity(typically the user) and additional data. 
    
            {
                "sub": "1234567890",
                "name": "John Doe",
                "admin": true
            }
      The payload is the Base64 encoded.
    * **Signature**: To create the signature part you have to take the encoded header, the encoded payload, a secret, the algorithm specfied in the header and sign it.
    
            HMACSHA256(base64UrlEncode(header) + "." + base64UrlEncode(payload),secret)
      The signature is used to verify the message wasn't changed along the way.
  <br/>
  
    The output is three Base64-URL strings separated by dots that can be easily passed in HTML and HTTP environments, while being more compact when compared to XML-based standards such as SAML.
    
            Example: xxxxx.yyyyy.zzzzz
