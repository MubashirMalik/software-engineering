# Cookies
- small pieces of data
- used as a medium of storage in browser 
- sent to the server with each request (automatically)
- Uses:
    - user personalization (language, settings)
    - session management (what keeps you login?)
    - ad tracking

## Creating Cookies
1. Client-side: 
    - JavaScript (`Document.cookie`)
2. Web server:
    - Server asks client to set cookie for it using response header `set-cookie`

## Cookie Properties
- Sent with every request
- Cookie Scope
    - Domain
    - Path
### Domain
- Cookie set for `example.com` will not be set for `www.example.com`. We can easily see this by setting a cookie and checking storage from browser.

- Cookies are per domain.

- **HOWEVER**, we can specify a property for cookie `domain=.example.com` which will make it available for all domains. (example.com, www.example.com, mail.example.com and so on)


### Path
If we specify a path `path=path1`, then the cookie will only be sent by browser for requests of specified path

### Expires, Max-age
- If we don't specify it then the cookie will expire as soon as we close the browser. It is known as session cookie.
- It can be simple set by using `max-age=3min`

### Same site

#### Why need for this? Problem?
- Logged into my Bank account
- Bank sets the cookie
- Now, we just have to request/type/hit e.g., my-bank.com and all the cookies set by bank that are saved in the browser will be sent to the server.
- We know it!! Cookies are sent with every request!! OK!
- NOW, imagine we visit **scammer.com** (any website) and it has a button/link which hits server/sends request to any address of my-bank.com
- What will happen?
- As request is going from your browser, does the browser send your cookies to my-bank.com?
- YES! As it has no way of knowing whether you actually meant to do that?
- scammer.com won't get access to our cookies but still it has now ability to access our account because we were already logged in. 
- What will happen if requests the URL `transfer-balance?address='scammer-address&amount=20`? 
- YOU MY FRIEND ARE FUCKED!
- <mark>NOTE:</mark> If the above request was POST or GET request using fetch, then CORS will take care of it!

#### Strict
- If we are the in the same site only then the cookie will be sent.

#### Lax
- <mark>Need to explore it more!</mark>

## Cookie Types
1. Session (no max-age/expiry set)
2. Permanent (max-age/expiry is set)
3. Httponly
    - Only be set from server
    - AND, browser can't read them! <- Saves from XSS as they can't steal
    - Can't see using document.cookie
    - Obv, can see in browser manually.
    - Not good if you want to access from JS like for some game settings but perfect for session token.
4. Secure
    - Only available for https site
    - Only be sent to https domains
5. Third party
    - <mark>Need to explore it more!</mark>
6. Zombie
    - <mark>Need to explore it more!</mark>

## Cookie Security
- Stealing cookies
- Cross site requests (XSS)
    - <mark>Need to explore it more!</mark>

**NOTE:** GET requests should be idempotent. These should never change data! HTTP is design for a reason. A link request is a GET request.

