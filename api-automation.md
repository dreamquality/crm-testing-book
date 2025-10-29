# API Automation

## Overview

API automation testing is essential for verifying the functionality, reliability, and performance of backend services. This section covers automated testing of the Employee Management CRM REST API using Postman.

## Prerequisites

Before starting API automation:
- The Employee Management CRM application should be running (see Project Launch section)
- **Postman** (latest version) installed or alternative API testing tool
- Basic understanding of REST APIs and HTTP methods
- Access to the API (typically at `http://localhost:3000/api`)

## API Testing with Postman

### 1. Postman Collection Setup

#### Create a New Collection

1. Open Postman
2. Create a new collection named "Employee Management CRM API Tests"
3. Add a description: "Automated API tests for Employee Management CRM"
4. Configure collection-level settings:
   - Authorization (if required)
   - Pre-request scripts (if needed)
   - Tests (common assertions)

#### Set Up Environment Variables

Create a new environment with the following variables:

```javascript
{
  "baseUrl": "http://localhost:3000/api",
  "employeeId": "",
  "testEmployeeEmail": "test@example.com",
  "testEmployeeName": "Test Employee"
}
```

---

### 2. Employee CRUD Operations

#### 2.1 Create Employee (POST)

**Endpoint:** `{{baseUrl}}/employees`  
**Method:** POST

**Test Case 1: Create Employee with Valid Data**

Request Body:
```json
{
  "name": "John Doe",
  "email": "john.doe@example.com",
  "phone": "+1234567890",
  "department": "Engineering",
  "position": "Software Engineer",
  "salary": 75000
}
```

Postman Tests:
```javascript
pm.test("Status code is 201", function () {
    pm.response.to.have.status(201);
});

pm.test("Response has employee ID", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData).to.have.property('id');
    pm.environment.set("employeeId", jsonData.id);
});

pm.test("Response contains correct employee data", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData.name).to.eql("John Doe");
    pm.expect(jsonData.email).to.eql("john.doe@example.com");
});

pm.test("Response time is less than 500ms", function () {
    pm.expect(pm.response.responseTime).to.be.below(500);
});
```

---

**Test Case 2: Create Employee with Invalid Data**

Request Body:
```json
{
  "name": "",
  "email": "invalid-email",
  "phone": "123"
}
```

Postman Tests:
```javascript
pm.test("Status code is 400", function () {
    pm.response.to.have.status(400);
});

pm.test("Error message indicates validation failure", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData).to.have.property('error');
    pm.expect(jsonData.error).to.include('validation');
});
```

---

**Test Case 3: Create Employee with Missing Required Fields**

Request Body:
```json
{
  "email": "test@example.com"
}
```

Postman Tests:
```javascript
pm.test("Status code is 400", function () {
    pm.response.to.have.status(400);
});

pm.test("Error indicates missing required fields", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData).to.have.property('error');
});
```

---

#### 2.2 Read Employee(s) (GET)

**Test Case 1: Get All Employees**

**Endpoint:** `{{baseUrl}}/employees`  
**Method:** GET

Postman Tests:
```javascript
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});

pm.test("Response is an array", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData).to.be.an('array');
});

pm.test("Each employee has required properties", function () {
    var jsonData = pm.response.json();
    if (jsonData.length > 0) {
        pm.expect(jsonData[0]).to.have.property('id');
        pm.expect(jsonData[0]).to.have.property('name');
        pm.expect(jsonData[0]).to.have.property('email');
    }
});

pm.test("Response time is less than 1000ms", function () {
    pm.expect(pm.response.responseTime).to.be.below(1000);
});
```

---

**Test Case 2: Get Single Employee by ID**

**Endpoint:** `{{baseUrl}}/employees/{{employeeId}}`  
**Method:** GET

Postman Tests:
```javascript
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});

pm.test("Response contains employee details", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData).to.have.property('id');
    pm.expect(jsonData).to.have.property('name');
    pm.expect(jsonData).to.have.property('email');
});

pm.test("Employee ID matches requested ID", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData.id).to.eql(pm.environment.get("employeeId"));
});
```

---

**Test Case 3: Get Non-Existent Employee**

**Endpoint:** `{{baseUrl}}/employees/99999`  
**Method:** GET

Postman Tests:
```javascript
pm.test("Status code is 404", function () {
    pm.response.to.have.status(404);
});

pm.test("Error message indicates not found", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData).to.have.property('error');
    pm.expect(jsonData.error).to.include('not found');
});
```

---

#### 2.3 Update Employee (PUT/PATCH)

**Test Case 1: Update Employee with Valid Data**

**Endpoint:** `{{baseUrl}}/employees/{{employeeId}}`  
**Method:** PUT or PATCH

Request Body:
```json
{
  "name": "John Doe Updated",
  "phone": "+9876543210",
  "department": "Management"
}
```

Postman Tests:
```javascript
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});

pm.test("Employee data is updated", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData.name).to.eql("John Doe Updated");
    pm.expect(jsonData.phone).to.eql("+9876543210");
});

pm.test("Response time is acceptable", function () {
    pm.expect(pm.response.responseTime).to.be.below(500);
});
```

---

**Test Case 2: Update Employee with Invalid Data**

**Endpoint:** `{{baseUrl}}/employees/{{employeeId}}`  
**Method:** PUT or PATCH

Request Body:
```json
{
  "email": "invalid-email-format"
}
```

Postman Tests:
```javascript
pm.test("Status code is 400", function () {
    pm.response.to.have.status(400);
});

pm.test("Validation error is returned", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData).to.have.property('error');
});
```

---

**Test Case 3: Update Non-Existent Employee**

**Endpoint:** `{{baseUrl}}/employees/99999`  
**Method:** PUT or PATCH

Request Body:
```json
{
  "name": "Test"
}
```

Postman Tests:
```javascript
pm.test("Status code is 404", function () {
    pm.response.to.have.status(404);
});

pm.test("Error indicates employee not found", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData).to.have.property('error');
});
```

---

#### 2.4 Delete Employee (DELETE)

**Test Case 1: Delete Existing Employee**

**Endpoint:** `{{baseUrl}}/employees/{{employeeId}}`  
**Method:** DELETE

Postman Tests:
```javascript
pm.test("Status code is 200 or 204", function () {
    pm.expect(pm.response.code).to.be.oneOf([200, 204]);
});

pm.test("Success message is returned", function () {
    if (pm.response.code === 200) {
        var jsonData = pm.response.json();
        pm.expect(jsonData).to.have.property('message');
    }
});
```

---

**Test Case 2: Delete Non-Existent Employee**

**Endpoint:** `{{baseUrl}}/employees/99999`  
**Method:** DELETE

Postman Tests:
```javascript
pm.test("Status code is 404", function () {
    pm.response.to.have.status(404);
});

pm.test("Error indicates not found", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData).to.have.property('error');
});
```

---

**Test Case 3: Verify Deletion (GET after DELETE)**

**Endpoint:** `{{baseUrl}}/employees/{{employeeId}}`  
**Method:** GET

Postman Tests:
```javascript
pm.test("Status code is 404", function () {
    pm.response.to.have.status(404);
});

pm.test("Employee no longer exists", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData).to.have.property('error');
});
```

---

### 3. Additional Test Scenarios

#### 3.1 Authentication/Authorization Tests (if applicable)

**Test Case: Access API Without Authentication**

Postman Tests:
```javascript
pm.test("Status code is 401 Unauthorized", function () {
    pm.response.to.have.status(401);
});
```

---

#### 3.2 Search and Filter Tests

**Endpoint:** `{{baseUrl}}/employees?department=Engineering`  
**Method:** GET

Postman Tests:
```javascript
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});

pm.test("All returned employees are from Engineering", function () {
    var jsonData = pm.response.json();
    jsonData.forEach(function(employee) {
        pm.expect(employee.department).to.eql("Engineering");
    });
});
```

---

#### 3.3 Pagination Tests (if applicable)

**Endpoint:** `{{baseUrl}}/employees?page=1&limit=10`  
**Method:** GET

Postman Tests:
```javascript
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});

pm.test("Response contains pagination metadata", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData).to.have.property('page');
    pm.expect(jsonData).to.have.property('limit');
    pm.expect(jsonData).to.have.property('total');
});

pm.test("Results limited to specified number", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData.data.length).to.be.at.most(10);
});
```

---

#### 3.4 Boundary Value Tests

**Test Case: Maximum Field Length**

Request Body:
```json
{
  "name": "A".repeat(256),
  "email": "test@example.com"
}
```

Postman Tests:
```javascript
pm.test("Status code is 400", function () {
    pm.response.to.have.status(400);
});

pm.test("Error indicates field length exceeded", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData).to.have.property('error');
});
```

---

#### 3.5 Data Persistence Tests

**Test Case: Verify Data Persistence After Update**

1. Update an employee
2. Get the employee details
3. Verify the updated data persists

Postman Tests:
```javascript
pm.test("Updated data persists", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData.name).to.eql(pm.environment.get("updatedName"));
});
```

---

### 4. Collection-Level Configuration

#### Pre-request Script (Collection Level)

```javascript
// Set timestamp for unique test data
pm.environment.set("timestamp", Date.now());

// Set content type
pm.request.headers.add({
    key: 'Content-Type',
    value: 'application/json'
});
```

#### Test Script (Collection Level)

```javascript
// Common test for all requests
pm.test("Response has valid JSON", function () {
    pm.response.to.be.json;
});

// Log response time
console.log("Response time: " + pm.response.responseTime + "ms");
```

---

### 5. Running Tests

#### Using Postman Collection Runner

1. Open Collection Runner in Postman
2. Select the "Employee Management CRM API Tests" collection
3. Select the environment
4. Set the number of iterations
5. Click "Run"

#### Using Newman (CLI)

Install Newman:
```bash
npm install -g newman
```

Run collection:
```bash
newman run collection.json -e environment.json --reporters cli,json
```

---

## Deliverables

Submit the following for API automation:

1. **Postman Collection**
   - Exported as JSON file
   - Include all test cases with assertions
   - Well-organized with folders and descriptions

2. **Environment File**
   - Exported environment variables
   - Include base URLs and test data variables

3. **Test Execution Results**
   - Screenshot of Collection Runner results
   - Newman HTML report (if using Newman)
   - Summary of test coverage

4. **Test Summary Document**
   - Number of API endpoints tested
   - Test scenarios covered
   - Pass/fail counts
   - Any issues or observations

---

## Best Practices

### Test Organization
- Group related tests into folders
- Use meaningful names for requests and tests
- Add descriptions to collections and requests
- Order tests logically (create before update/delete)

### Test Data Management
- Use environment variables for dynamic data
- Generate unique test data to avoid conflicts
- Clean up test data after execution
- Use realistic test data

### Assertions
- Test status codes
- Validate response structure
- Check data types and values
- Verify business logic
- Test error scenarios

### Test Independence
- Each test should be independent
- Don't rely on specific execution order (when possible)
- Handle test data setup and cleanup
- Use pre-request scripts for data preparation

### Performance
- Check response times
- Test under different loads
- Monitor for memory leaks or slowdowns
- Use reasonable thresholds

---

## Tips for Effective API Testing

1. **Start Simple:** Begin with basic happy path tests, then add edge cases
2. **Use Variables:** Leverage environment and collection variables for flexibility
3. **Chain Requests:** Use test scripts to extract data for subsequent requests
4. **Negative Testing:** Don't forget to test error scenarios
5. **Documentation:** Add descriptions to help others understand your tests
6. **Version Control:** Keep your collections in Git
7. **Automation:** Integrate with CI/CD pipelines using Newman

---

## Evaluation Criteria

Your API automation will be evaluated on:

- **Test Coverage (30%):** Breadth and depth of test scenarios
- **Quality of Assertions (25%):** Comprehensive and meaningful validations
- **Code Organization (20%):** Well-structured and maintainable
- **Documentation (15%):** Clear descriptions and comments
- **Error Handling (10%):** Coverage of negative scenarios

---

## Resources

- [Postman Learning Center](https://learning.postman.com/)
- [Writing Tests in Postman](https://learning.postman.com/docs/writing-scripts/test-scripts/)
- [Newman Documentation](https://learning.postman.com/docs/running-collections/using-newman-cli/command-line-integration-with-newman/)
- [API Testing Best Practices](https://www.postman.com/api-platform/api-testing/)
- [REST API Testing Guide](https://www.ministryoftesting.com/dojo/lessons/api-testing-guide)
