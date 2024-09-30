# Cross-Site Scripting (XSS) Mitigation

Cross-Site Scripting (XSS) is a security vulnerability that allows attackers to inject malicious scripts into webpages viewed by other users. It can lead to browser hijacking, session theft, and various other attacks. This article discusses methods and best practices for mitigating XSS vulnerabilities in web applications.

## Understanding XSS Types

XSS vulnerabilities are generally categorized into three types:
1. **Stored XSS**: The malicious script is stored permanently on the target server (e.g., in a database) and delivered to users when they request the stored data.
2. **Reflected XSS**: The script is reflected off a web server and immediately executed in the user's browser, typically via a URL or form submission. 
3. **DOM-Based XSS**: This occurs when client-side scripts write data provided by a user to the Document Object Model (DOM) without proper sanitization.

## Input Validation and Output Encoding

The first line of defense against XSS is to validate and sanitize all user inputs. 

```javascript
function sanitize(input) {
    return input.replace(/<[^>]*>/g, ''); // Simple Sanitization Example
}
const userInput = sanitize('<script>alert(
