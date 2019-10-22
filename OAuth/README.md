# Definition:
OAuth (Open Authorization) is an open standard for token-based authentication and authorization on the Internet. It allows an end user's account information to be used by third-party services, such as Facebook, without exposing the user's password. OAuth acts as an intermediary on behalf of the end user, providing the service with an access token that authorizes specific account information to be shared. The process for obtaining the token is called a flow.

# Authentication

## Two ways:
* Cookie based authentication:

    1. The traditional approach of auth
    
    2. Stateful. The authentication record or session must be kept both server and client-side. The server needs to keep track of active sessions in a database (momery / local store), while on the front-end a cookie is created that holds a session identifier, thus the name cookie-based authentication.
    3. Steps：
        1. User enters their login credentials
        2. Server verifies the credentials are correct and creates a session which is then stored in a database
        3. A cookie with the session ID is placed in the users browser
        4. On subsequent requests, the session ID is verified against the database and if valid the request processed
        5. Once a user logs out of the app, the session is destroyed both client and server side


* Token-based authentication:
    1. The user enters their login credentials (username+password)
    2. Server verifies the credentials are correct and returns an encrypted and signed token with a private key.
        1. Text: (JSON = {username: “abcd”, uuid=”1.2.3.4”}, private key) => token
        2. Code: abccdeedddee
        3. Decode: JSON = {username: “abcd”,  uuid=”1.2.3.4”}
        4. Symmetric vs Asymmetric encryption.
        5. This token is stored client-side, most commonly in local storage - but can be stored in session storage or a cookie as well
    3. Subsequent requests to the server include this token as an additional Authorization header or through one of the other methods mentioned above
    4. The server decodes the JWT and if the token is valid processes the request
    5. Once a user logs out, the token is destroyed client-side, no interaction with the server

## Pros and Cons:
* Advantages of Token-Based Authentication
    * Stateless, Scalable and Decoupled
        1. Stateless: The back-end does not need to keep a record of tokens
        2. Self-contained, containing all the data required to check its validity.
        3. No DB look up is needed.
 
    * Store Data in the JWT
        1. With a cookie based approach, you simply store the session id in a cookie.
        2. JWT's on the other hand allow you to store any type of metadata, as long as it's valid JSON. (username in our project, for example)
 
    * Mobile Friendly
        1. Native mobile platforms and cookies do not mix well.
        2. In our project, the same Go backend will serve traffic to both iOS and browser (React JS)

* Disadvantages of Token-Based Authentication

    Usually the size of token is larger than a session id.
