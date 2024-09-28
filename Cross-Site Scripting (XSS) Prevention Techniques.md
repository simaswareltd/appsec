# Cross-Site Scripting (XSS) Prevention Techniques

Cross-Site Scripting (XSS) is a prevalent security vulnerability that allows attackers to inject malicious scripts into web applications, potentially compromising user data and session security. This article explores various XSS prevention techniques along with code snippets to ensure robust security against XSS attacks.

## Understanding XSS Types

1. **Stored XSS**: The attacker injects a script that is stored on the server and served to users.
2. **Reflected XSS**: The injected script passes through the server and is reflected off immediate user requests.
3. **DOM-based XSS**: The vulnerability lies in the client-side scripts and can be exploited within the browser without server interaction.

## Input Validation

Input validation is critical in preventing XSS. Ensure user inputs are properly validated and sanitized before being processed or stored.

```javascript
function sanitizeInput(input) {
    const textArea = document.createElement('textarea');
    textArea.textContent = input;
    return textArea.innerHTML;
}
```

## Output Encoding

Always encode output to prevent execution of malicious scripts. For HTML output, use the following encoding:

```javascript
function escapeHTML(html) {
    return html.replace(/&/g, '&amp;')
               .replace(/</g, '&lt;')
               .replace(/>/g, '&gt;')
               .replace(/"/g, '&quot;')
               .replace(/'/g, '&#x27;');
}
```

## Content Security Policy (CSP)

Implementing a Content Security Policy can greatly mitigate XSS risks. Use the following HTTP header:

```
Content-Security-Policy: default-src 'self'; script-src 'self';
```

This policy only allows scripts from the same origin.

## HTTP-only and Secure Cookies

Make use of HTTP-only cookies to ensure that cookies can't be accessed via JavaScript.

```javascript
Set-Cookie: sessionId=abc123; HttpOnly;
```

This ensures cookies are securely sent and help mitigate the impact of XSS.

## Framework Security Mechanisms

Modern web frameworks offer built-in mechanisms to prevent XSS. For example, using Angular:

```javascript
const app = angular.module('myApp', []);
app.controller('myController', ($scope) => {
    $scope.text = '<p>This will be sanitized.</p>';
});
```

Angular automatically escapes expressions interpolated into the HTML.

## Conclusion

XSS presents significant security challenges for web applications. By implementing effective input validation, output encoding, strict CSP, and using secure cookies, application developers can mitigate risks associated with XSS attacks effectively. Always remember to stay updated on emerging threats and apply security best practices for web development.
