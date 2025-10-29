# API Automation

## Overview

API automation testing is essential for verifying the functionality, reliability, and performance of backend services. This section covers automated testing of the Employee Management CRM REST API using Postman or similar tools.

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

Create a new environment with variables for:
- Base URL (e.g., `http://localhost:3000/api`)
- Employee ID (for storing created test data)
- Test employee data (email, name, etc.)

---

### 2. Employee CRUD Operations

#### 2.1 Create Employee (POST)

**Test Scenarios:**

1. **Create Employee with Valid Data**
   - Endpoint: `/employees` (POST)
   - Test status code is 201 (Created)
   - Verify response contains employee ID
   - Validate response contains correct employee data
   - Check response time is acceptable (under 500ms)
   - Store employee ID in environment variable for later use

2. **Create Employee with Invalid Data**
   - Test with empty required fields
   - Test with invalid email format
   - Test with invalid phone format
   - Verify status code is 400 (Bad Request)
   - Verify error message indicates validation failure

3. **Create Employee with Missing Required Fields**
   - Submit request without required fields
   - Verify status code is 400
   - Verify error indicates missing fields

---

#### 2.2 Read Employee(s) (GET)

**Test Scenarios:**

1. **Get All Employees**
   - Endpoint: `/employees` (GET)
   - Verify status code is 200
   - Verify response is an array
   - Check each employee has required properties (id, name, email)
   - Verify response time is acceptable

2. **Get Single Employee by ID**
   - Endpoint: `/employees/{id}` (GET)
   - Use stored employee ID from previous test
   - Verify status code is 200
   - Verify response contains complete employee details
   - Validate employee ID matches requested ID

3. **Get Non-Existent Employee**
   - Use invalid/non-existent employee ID
   - Verify status code is 404 (Not Found)
   - Verify error message indicates employee not found

---

#### 2.3 Update Employee (PUT/PATCH)

**Test Scenarios:**

1. **Update Employee with Valid Data**
   - Endpoint: `/employees/{id}` (PUT or PATCH)
   - Modify one or more employee fields
   - Verify status code is 200
   - Verify updated data is returned in response
   - Validate changes are persisted

2. **Update Employee with Invalid Data**
   - Submit invalid email or phone format
   - Verify status code is 400
   - Verify validation error is returned

3. **Update Non-Existent Employee**
   - Use invalid employee ID
   - Verify status code is 404
   - Verify appropriate error message

---

#### 2.4 Delete Employee (DELETE)

**Test Scenarios:**

1. **Delete Existing Employee**
   - Endpoint: `/employees/{id}` (DELETE)
   - Verify status code is 200 or 204
   - Verify success message if applicable

2. **Delete Non-Existent Employee**
   - Use invalid employee ID
   - Verify status code is 404
   - Verify error indicates employee not found

3. **Verify Deletion**
   - Attempt to GET the deleted employee
   - Verify status code is 404
   - Confirm employee no longer exists

---

### 3. Additional Test Scenarios

#### 3.1 Authentication/Authorization Tests (if applicable)

- Test API access without authentication token
- Verify status code is 401 (Unauthorized)
- Test with invalid authentication credentials
- Test with expired tokens

#### 3.2 Search and Filter Tests

- Test employee search by department
- Test employee filtering by various criteria
- Verify only matching results are returned
- Validate search query parameters work correctly

#### 3.3 Pagination Tests (if applicable)

- Test pagination with page and limit parameters
- Verify response contains pagination metadata
- Validate correct number of results per page
- Test navigation between pages

#### 3.4 Boundary Value Tests

- Test maximum field lengths
- Test minimum values
- Test special characters in fields
- Verify appropriate error handling for boundary violations

#### 3.5 Data Persistence Tests

- Create an employee
- Update the employee
- Retrieve the employee
- Verify data persists correctly across operations

---

### 4. Test Assertions to Include

For each API test, include assertions for:

- **Status Codes:** Verify correct HTTP status codes (200, 201, 400, 404, etc.)
- **Response Structure:** Validate JSON structure and required fields
- **Data Types:** Check field data types match expectations
- **Data Values:** Verify returned values match expected values
- **Response Time:** Ensure responses are within acceptable time limits
- **Error Messages:** Validate error messages are clear and appropriate

---

### 5. Running Tests

#### Using Postman Collection Runner

1. Open Collection Runner in Postman
2. Select your test collection
3. Select the environment
4. Configure iterations if needed
5. Click "Run" to execute all tests
6. Review results and export report

#### Using Newman (CLI)

Newman allows running Postman collections from command line:
1. Install Newman globally via npm
2. Export your collection and environment
3. Run collection via Newman command
4. Generate reports in various formats (CLI, JSON, HTML)

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
- Each test should be independent when possible
- Don't rely on specific execution order
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
- **Test Organization (20%):** Well-structured and maintainable
- **Documentation (15%):** Clear descriptions and comments
- **Error Handling (10%):** Coverage of negative scenarios

---

## Resources

- [Postman Learning Center](https://learning.postman.com/)
- [Writing Tests in Postman](https://learning.postman.com/docs/writing-scripts/test-scripts/)
- [Newman Documentation](https://learning.postman.com/docs/running-collections/using-newman-cli/command-line-integration-with-newman/)
- [API Testing Best Practices](https://www.postman.com/api-platform/api-testing/)
- [REST API Testing Guide](https://www.ministryoftesting.com/dojo/lessons/api-testing-guide)
