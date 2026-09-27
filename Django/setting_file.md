
### 1. What is `SECRET_KEY`?
- `SECRET_KEY` is a unique secret value used by Django for cryptographic signing and security-related operations.  
- It should be kept private because exposing it can create security risks.

### 2. What is Middleware?
- Middleware is a layer between the request and response in Django.  
- It can process, modify, allow, or reject requests and responses.

### 3. What is `CsrfViewMiddleware`?
- It protects Django applications from CSRF attacks by checking CSRF tokens in unsafe requests like POST.  
- If the token is invalid or missing, Django rejects the request.

### 4. What is `AuthenticationMiddleware`?
- It identifies the currently logged-in user in a Django application.  
- The user can be accessed using `request.user`.

### 5. What is `MessageMiddleware`?
- It allows Django to display temporary messages such as success, error, and warning messages.  
- These messages are usually shown to the user after an action.

### 6. What is `XFrameOptionsMiddleware`?
- It protects Django applications from clickjacking attacks.  
- It controls whether a Django page can be loaded inside a frame.

### 7. What is CSRF?
- CSRF is an attack where an attacker tricks an authenticated user's browser into making an unwanted request.  
- Django protects against it using CSRF tokens.

### 8. What is XSS?
- XSS is an attack where malicious JavaScript is injected into a webpage.  
- The script can then execute in another user's browser.

### 9. What is Clickjacking?
- Clickjacking tricks a user into clicking something different from what they think they are clicking.  
- Django provides protection using `XFrameOptionsMiddleware`.

### 10. What is WSGI?
- WSGI stands for Web Server Gateway Interface and connects Python applications like Django with web servers.  
- Django provides the WSGI application through `wsgi.py`.