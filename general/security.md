## Security

### XXS: Cross site scripting

It consist on injecting malicious code into a website. It’s an attack that happened in the front end.
Malicious code is injected into a website, usually the evil entity use user input to inject script tags which later are inserted on a page and executed when a client access the page.

### CSRF: Cross site request forgery

￼Cross-site request forgery (also known as CSRF) is a web security vulnerability that allows an attacker to induce users to perform actions that they do not intend to perform. It allows an attacker to partly circumvent the same origin policy, which is designed to prevent different websites from interfering with each other.

For a CSRF attack to be possible, three key conditions must be in place:

- A relevant action. There is an action within the application that the attacker has a reason to induce. This might be a privileged action (such as modifying permissions for other users) or any action on user-specific data (such as changing the user's own password).
- Cookie-based session handling. Performing the action involves issuing one or more HTTP requests, and the application relies solely on session cookies to identify the user who has made the requests. There is no other mechanism in place for tracking sessions or validating user requests.
- No unpredictable request parameters. The requests that perform the action do not contain any parameters whose values the attacker cannot determine or guess. For example, when causing a user to change their password, the function is not vulnerable if an attacker needs to know the value of the existing password.

For example, suppose an application contains a function that lets the user change the email address on their account. When a user performs this action, they make an HTTP request like the following:

```
POST /email/change HTTP/1.1
Host: vulnerable-website.com
Content-Type: application/x-www-form-urlencoded
Content-Length: 30
Cookie: session=yvthwsztyeQkAPzeQ5gHgTvlyxHfsAfE

email=wiener@normal-user.com
```

This meet all the requirements.
With these conditions in place, the attacker can construct a web page containing the following HTML:

```html
<html>
  <body>
    <form action="https://vulnerable-website.com/email/change" method="POST">
      <input type="hidden" name="email" value="pwned@evil-user.net" />
    </form>
    <script>
      document.forms[0].submit();
    </script>
  </body>
</html>
```

### If the hacker has access to the computer

Remember that everything we write on local storage it's also wrote in a file on a computer. Stealing the computer would allow an hacker to get the content from there. A solution could be to encrypt those data with a key that you ask the backend and you don’t store on local storage

### Solutions

- Validate input on the backend and be sure malicious code is not being submitted.
- Be careful when we use `setTimeout`, `setInterval`, `Function`, `eval`. Whenever we put into those need to be sanitize. This is valid code that is executed:

```js
setTimeout("document.body.innerHTML = 'TEST'", 1000);
```

- Randomize every request with a token the request to avoid CSRF
- Don’t expose user token in the url, session token should timeout so in case the token is stolen its validity is limited in time
- Enforce proper cookie scope
