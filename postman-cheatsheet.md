---
id: 17
date: 2025-06-27T00:00:00Z
title: Postman Cheatsheet
author: Jeremy Novak
summary: Cheatsheet for Postman API testing and development
slug: postman-cheatsheet
tags:
  - postman
  - api
  - testing
  - rest
  - http
published: true
---

# Postman Cheatsheet

---

## Installation

### Desktop App
- **Windows**: Download from [postman.com](https://www.postman.com/downloads/)
- **macOS**: `brew install --cask postman` or download from website
- **Linux**: Download AppImage or use Snap: `snap install postman`

### Web Version
- Access at [web.postman.co](https://web.postman.co)
- Requires Postman account

---

## Getting Started

### Create Account
1. Sign up at [postman.com](https://www.postman.com)
2. Verify email
3. Create workspace

### Basic Concepts
- **Workspace**: Container for your API work
- **Collection**: Group of related requests
- **Request**: Individual API call
- **Environment**: Set of variables for different contexts

---

## Making Requests

### HTTP Methods
```
GET     - Retrieve data
POST    - Create new resource
PUT     - Update entire resource
PATCH   - Partial update
DELETE  - Remove resource
HEAD    - GET without response body
OPTIONS - Check allowed methods
```

### Request Components
- **URL**: `https://api.example.com/users/123`
- **Headers**: Key-value pairs for metadata
- **Body**: Data sent with request (POST, PUT, PATCH)
- **Params**: Query parameters and path variables

### URL Structure
```
https://api.example.com/users?page=1&limit=10
├── Protocol: https://
├── Host: api.example.com
├── Path: /users
└── Query: ?page=1&limit=10
```

---

## Request Headers

### Common Headers
```
Content-Type: application/json
Authorization: Bearer <token>
Accept: application/json
User-Agent: Postman
X-API-Key: <api-key>
Cache-Control: no-cache
```

### Setting Headers
1. Go to **Headers** tab
2. Add key-value pairs
3. Use autocomplete for common headers
4. Toggle headers on/off with checkbox

---

## Request Body

### JSON Body
```json
{
  "name": "John Doe",
  "email": "john@example.com",
  "age": 30
}
```

### Form Data
```
name: John Doe
email: john@example.com
file: [Select File]
```

### URL Encoded
```
name=John%20Doe&email=john%40example.com
```

### Raw Text
```
Plain text content
XML content
Custom format
```

---

## Variables

### Variable Types
- **Global**: Available across all workspaces
- **Collection**: Available within collection
- **Environment**: Context-specific values
- **Local**: Temporary, request-specific

### Setting Variables
```javascript
// In Pre-request Script or Tests
pm.globals.set("baseUrl", "https://api.example.com");
pm.collectionVariables.set("userId", "123");
pm.environment.set("token", "abc123");
```

### Using Variables
```
URL: {{baseUrl}}/users/{{userId}}
Headers: Authorization: Bearer {{token}}
Body: {"name": "{{userName}}"}
```

### Dynamic Variables
```
{{$guid}}           - Generate GUID
{{$timestamp}}      - Current timestamp
{{$randomInt}}      - Random integer
{{$randomFirstName}} - Random first name
{{$randomEmail}}    - Random email
```

---

## Pre-request Scripts

### Common Use Cases
```javascript
// Set timestamp
pm.globals.set("timestamp", Date.now());

// Generate random data
pm.globals.set("randomId", Math.floor(Math.random() * 1000));

// Set authentication token
pm.sendRequest({
    url: "{{baseUrl}}/auth/login",
    method: "POST",
    header: {
        "Content-Type": "application/json"
    },
    body: {
        mode: "raw",
        raw: JSON.stringify({
            username: "admin",
            password: "password"
        })
    }
}, function(err, response) {
    if (!err) {
        const token = response.json().token;
        pm.environment.set("authToken", token);
    }
});
```

---

## Tests and Assertions

### Basic Tests
```javascript
// Status code tests
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});

pm.test("Status code is in 200 range", function () {
    pm.expect(pm.response.code).to.be.within(200, 299);
});

// Response time test
pm.test("Response time is less than 200ms", function () {
    pm.expect(pm.response.responseTime).to.be.below(200);
});

// Header tests
pm.test("Content-Type is JSON", function () {
    pm.expect(pm.response.headers.get("Content-Type")).to.include("application/json");
});
```

### JSON Response Tests
```javascript
// Parse JSON response
const jsonData = pm.response.json();

// Test JSON structure
pm.test("Response has required fields", function () {
    pm.expect(jsonData).to.have.property("id");
    pm.expect(jsonData).to.have.property("name");
    pm.expect(jsonData).to.have.property("email");
});

// Test values
pm.test("User ID is correct", function () {
    pm.expect(jsonData.id).to.eql(123);
});

// Test arrays
pm.test("Users array is not empty", function () {
    pm.expect(jsonData.users).to.be.an("array").that.is.not.empty;
});
```

### Schema Validation
```javascript
// Define schema
const schema = {
    type: "object",
    properties: {
        id: { type: "number" },
        name: { type: "string" },
        email: { type: "string", format: "email" }
    },
    required: ["id", "name", "email"]
};

// Validate response
pm.test("Response matches schema", function () {
    pm.response.to.have.jsonSchema(schema);
});
```

---

## Collections

### Creating Collections
1. Click **New** → **Collection**
2. Name your collection
3. Add description and variables
4. Organize with folders

### Collection Variables
```javascript
// Access collection variables
pm.collectionVariables.get("baseUrl");
pm.collectionVariables.set("apiVersion", "v1");
```

### Collection Scripts
- **Pre-request**: Runs before every request
- **Test**: Runs after every response

---

## Environments

### Creating Environments
1. Click **Environments** (eye icon)
2. Click **Add**
3. Name environment
4. Add variables

### Environment Variables
```
Variable: baseUrl
Initial Value: https://api-dev.example.com
Current Value: https://api-dev.example.com
```

### Switching Environments
- Use dropdown in top-right
- Different environments for dev/staging/prod

---

## Authentication

### API Key
```
Header: X-API-Key
Value: {{apiKey}}
```

### Bearer Token
```
Header: Authorization
Value: Bearer {{token}}
```

### Basic Auth
```
Username: {{username}}
Password: {{password}}
```

### OAuth 2.0
1. Select **OAuth 2.0** in Authorization tab
2. Configure grant type
3. Set callback URL
4. Get new access token

---

## Mock Servers

### Creating Mock Server
1. Click **...** on collection
2. Select **Mock Collection**
3. Configure mock server
4. Get mock URL

### Mock Examples
```javascript
// Example response
{
  "id": 1,
  "name": "John Doe",
  "email": "john@example.com"
}
```

---

## Monitors

### Creating Monitor
1. Click **...** on collection
2. Select **Monitor Collection**
3. Set schedule
4. Configure notifications

### Monitor Schedule
- Every 5 minutes
- Hourly
- Daily
- Weekly
- Custom cron expression

---

## Documentation

### Auto-generated Docs
1. Click **View Documentation**
2. Postman generates docs from collection
3. Include request/response examples
4. Publish to web

### Custom Documentation
```markdown
# API Endpoint
This endpoint creates a new user.

## Request
- Method: POST
- URL: /users
- Body: JSON object with user data

## Response
- Status: 201 Created
- Body: Created user object
```

---

## Newman (CLI)

### Installation
```bash
npm install -g newman
```

### Run Collection
```bash
# Basic run
newman run collection.json

# With environment
newman run collection.json -e environment.json

# With custom options
newman run collection.json \
  -e environment.json \
  -r html \
  --reporter-html-export report.html
```

### CI/CD Integration
```yaml
# GitHub Actions example
- name: Run Postman Tests
  run: |
    newman run collection.json \
      -e environment.json \
      --reporters cli,junit \
      --reporter-junit-export results.xml
```

---

## Keyboard Shortcuts

### Navigation
- `Ctrl/Cmd + N`: New request
- `Ctrl/Cmd + O`: Open
- `Ctrl/Cmd + S`: Save
- `Ctrl/Cmd + Enter`: Send request
- `Ctrl/Cmd + /`: Search

### Editing
- `Ctrl/Cmd + D`: Duplicate request
- `Ctrl/Cmd + Z`: Undo
- `Ctrl/Cmd + Y`: Redo
- `Tab`: Move between fields

---

## Tips and Best practices

### Organization
- Use folders to group related requests
- Name requests descriptively
- Add descriptions to requests
- Use consistent variable naming

### Testing
- Test status codes first
- Validate response structure
- Test edge cases
- Use meaningful test names

### Variables
- Use environments for different stages
- Store sensitive data in environment variables
- Use collection variables for shared data
- Leverage dynamic variables for test data

### Scripts
- Keep scripts simple and focused
- Add comments to complex logic
- Handle errors gracefully
- Use console.log() for debugging

---

## Common Patterns

### Authentication Flow
```javascript
// Pre-request script for auto-login
if (!pm.environment.get("authToken")) {
    pm.sendRequest({
        url: "{{baseUrl}}/auth/login",
        method: "POST",
        header: {"Content-Type": "application/json"},
        body: {
            mode: "raw",
            raw: JSON.stringify({
                username: pm.environment.get("username"),
                password: pm.environment.get("password")
            })
        }
    }, function(err, response) {
        if (!err && response.json().token) {
            pm.environment.set("authToken", response.json().token);
        }
    });
}
```

### Data Cleanup
```javascript
// Test script for cleanup
pm.test("Cleanup test data", function() {
    const userId = pm.environment.get("createdUserId");
    if (userId) {
        pm.sendRequest({
            url: `{{baseUrl}}/users/${userId}`,
            method: "DELETE",
            header: {"Authorization": `Bearer {{authToken}}`}
        }, function(err, response) {
            console.log("Cleanup completed");
        });
    }
});
```

---

## Troubleshooting

### Common Issues
- **CORS errors**: Use Postman Desktop app
- **SSL errors**: Disable SSL verification in settings
- **Timeout**: Increase timeout in settings
- **Large responses**: Use streaming for large files

### Debug Console
- View `console.log()` output
- See network requests
- Check for errors
- Access: View → Show Postman Console

---

## Resources

- [Postman Learning Center](https://learning.postman.com/)
- [Postman API Documentation](https://documenter.getpostman.com/)
- [Newman Documentation](https://github.com/postmanlabs/newman)
- [Postman Community](https://community.postman.com/)
- [Postman Public API Network](https://www.postman.com/explore)