# In Band SQL Injection - Lab notes

### Manual Identification
1. Find entry points via Burp Proxy (History). Look for `?id=`, `?category=`, etc.
2. Send to Repeater and test with `' OR 1=1--`. Check for logic changes in the response.

### Login Bypass
- Intercept the login request.
- Inject `administrator'--` in the username field to bypass the password check.

### WAF Bypass (XML Filter)
- For POST requests with XML data:
- Test for injection: `<storeId>1+1</storeId>`.
- If blocked, highlight the payload -> Right click -> Extensions -> Hackvertor -> Encode -> hex_entities.
- Final Payload: `1 UNION SELECT username || '~' || password FROM users`.
