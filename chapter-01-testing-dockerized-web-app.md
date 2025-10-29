# Chapter 1: Testing a Dockerized Web App

## 🧩 Assignment Overview

**Application Under Test:** [Employee Management CRM](https://github.com/dreamquality/employee-management-crm)

**Objective:** Demonstrate comprehensive testing skills including manual testing, API testing, and UI automation for a Dockerized web application.

**Estimated Time:** 8-12 hours

**Difficulty Level:** Intermediate

## 🎯 Goals

By completing this assignment, you will demonstrate your ability to:

1. **Set up and launch** a Dockerized application
2. **Perform manual testing** of web application features
3. **Execute API testing** using Postman or similar tools
4. **Create automated UI tests** using Cypress or Playwright
5. **Document findings** in professional test reports

## 🛠️ Required Tools

- **Docker** (v20.10+) and **Docker Compose** (v2.0+)
- **Postman** (latest version) or alternative API testing tool
- **Cypress** (v12+) or **Playwright** (v1.30+) for UI automation
- **Git** for cloning the repository
- Text editor or IDE of your choice
- Web browser (Chrome, Firefox, or Edge)

## 📋 Assignment Stages

### Stage 1: Project Launch

#### 1.1 Environment Setup

**Tasks:**
1. Clone the Employee Management CRM repository:
   ```bash
   git clone https://github.com/dreamquality/employee-management-crm.git
   cd employee-management-crm
   ```

2. Review the project documentation:
   - Read the README.md file
   - Understand the application architecture
   - Identify the technologies used

3. Launch the application using Docker:
   ```bash
   docker-compose up -d
   ```

4. Verify the application is running:
   - Check Docker containers are up: `docker-compose ps`
   - Access the web interface (typically at `http://localhost:3000` or as specified)
   - Verify the API is accessible (typically at `http://localhost:3000/api` or as specified)

**Deliverables:**
- Screenshot of running Docker containers
- Screenshot of the application homepage
- Notes on any setup issues encountered and how you resolved them

#### 1.2 Application Exploration

**Tasks:**
1. Explore the user interface:
   - Navigate through all available pages
   - Test basic interactions (clicks, form inputs, navigation)
   - Document the main features and workflows

2. Explore the API:
   - Identify available API endpoints (check API documentation or network tab)
   - Test basic API calls using curl or browser
   - Understand the data models (Employee structure, etc.)

**Deliverables:**
- List of identified features and pages
- List of discovered API endpoints
- Application architecture diagram (optional but recommended)

---

### Stage 2: API Testing

#### 2.1 Postman Collection Creation

**Tasks:**
1. Create a new Postman collection named "Employee Management CRM API Tests"

2. Implement API test cases for the following scenarios:

   **Employee CRUD Operations:**
   - **Create Employee** (POST)
     - Test case: Create employee with valid data
     - Test case: Create employee with invalid data (validation)
     - Test case: Create employee with missing required fields
   
   - **Read Employee(s)** (GET)
     - Test case: Get all employees
     - Test case: Get single employee by ID
     - Test case: Get non-existent employee (404 handling)
   
   - **Update Employee** (PUT/PATCH)
     - Test case: Update employee with valid data
     - Test case: Update employee with invalid data
     - Test case: Update non-existent employee
   
   - **Delete Employee** (DELETE)
     - Test case: Delete existing employee
     - Test case: Delete non-existent employee
     - Test case: Verify deletion (GET after DELETE)

3. Add assertions for:
   - HTTP status codes (200, 201, 400, 404, etc.)
   - Response time (should be under reasonable threshold)
   - Response body structure and data types
   - Data validation and business rules

4. Set up environment variables for:
   - Base URL
   - API endpoints
   - Test data (employee IDs, etc.)

**Deliverables:**
- Postman collection (exported as JSON file)
- Environment file with variables
- Screenshot of test execution results
- Summary of test coverage (number of tests, pass/fail rate)

#### 2.2 API Test Coverage

**Additional Test Scenarios:**
- Authentication/Authorization tests (if applicable)
- Search and filter functionality tests
- Pagination tests (if applicable)
- Boundary value tests (e.g., maximum field lengths)
- Data persistence verification

**Deliverables:**
- Extended test cases documentation
- Test execution results with pass/fail status

---

### Stage 3: UI Testing

#### 3.1 Manual UI Testing

**Tasks:**
1. Create a test plan covering:
   - User registration/login (if applicable)
   - Employee creation workflow
   - Employee list viewing and filtering
   - Employee details viewing
   - Employee editing workflow
   - Employee deletion workflow
   - Form validation
   - Error handling
   - Navigation and usability

2. Execute manual test cases and document:
   - Test case ID
   - Test description
   - Prerequisites
   - Test steps
   - Expected results
   - Actual results
   - Status (Pass/Fail)
   - Screenshots of defects (if any)

**Deliverables:**
- Manual test cases document (Excel, Google Sheets, or Markdown table)
- Test execution report
- Bug reports (if defects found)
- Screenshots demonstrating test execution

#### 3.2 Automated UI Tests

**Tasks:**

Choose either **Cypress** or **Playwright** for automation.

**Test Scenarios to Automate:**

1. **Employee Creation Flow:**
   ```
   - Navigate to employee creation page
   - Fill in all required fields
   - Submit the form
   - Verify success message
   - Verify employee appears in the list
   ```

2. **Employee List Verification:**
   ```
   - Navigate to employees list
   - Verify table/list is displayed
   - Verify employee data is shown
   - Verify pagination (if applicable)
   ```

3. **Employee Details View:**
   ```
   - Navigate to employee list
   - Click on an employee
   - Verify details page loads
   - Verify all employee information is displayed
   ```

4. **Employee Update Flow:**
   ```
   - Navigate to an employee's edit page
   - Modify employee information
   - Save changes
   - Verify success message
   - Verify changes are reflected
   ```

5. **Employee Deletion Flow:**
   ```
   - Navigate to employee list
   - Delete an employee
   - Confirm deletion
   - Verify employee is removed from list
   ```

6. **Form Validation Tests:**
   ```
   - Try to submit empty form
   - Try to submit with invalid email
   - Try to submit with invalid phone number
   - Verify validation error messages
   ```

**Best Practices to Follow:**
- Use Page Object Model (POM) pattern
- Implement proper waits and assertions
- Use test data fixtures
- Implement proper test cleanup (delete created test data)
- Add meaningful test descriptions
- Handle dynamic elements properly

**Deliverables:**
- Automated test code (pushed to a Git repository)
- README with instructions to run the tests
- Test execution report/screenshots
- Video recording of test execution (optional but recommended)

---

### Stage 4: Report Preparation

#### 4.1 Test Documentation

**Tasks:**
1. Create a comprehensive Test Report including:

   **Executive Summary:**
   - Project overview
   - Testing scope
   - Testing timeline
   - Overall test results

   **Test Environment:**
   - Application version/commit hash
   - Docker environment details
   - Browser versions tested
   - Tools used

   **Test Execution Summary:**
   - Total test cases (manual + automated)
   - Test cases passed
   - Test cases failed
   - Test cases blocked/skipped
   - Pass rate percentage

   **API Testing Results:**
   - Number of API endpoints tested
   - Test scenarios covered
   - Issues found
   - API performance observations

   **UI Testing Results:**
   - Manual test execution summary
   - Automated test execution summary
   - Browser compatibility notes
   - Issues found

   **Defects Summary:**
   - List of defects found (if any)
   - Severity and priority classification
   - Steps to reproduce
   - Screenshots/evidence

   **Recommendations:**
   - Quality assessment
   - Suggestions for improvement
   - Additional test scenarios to consider
   - Test automation recommendations

   **Appendices:**
   - Test case details
   - API test results
   - Screenshots
   - Test artifacts references

**Deliverables:**
- Professional test report (PDF or Markdown format)
- Supporting documents and screenshots
- Test metrics and coverage summary

---

## 📦 What to Submit

Organize your submission in the following structure:

```
employee-crm-testing-assignment/
├── README.md                          # Overview and instructions
├── 01-setup/
│   ├── docker-containers.png          # Screenshot of running containers
│   ├── application-homepage.png       # Screenshot of app homepage
│   └── setup-notes.md                 # Setup experience notes
├── 02-api-testing/
│   ├── postman-collection.json        # Postman collection export
│   ├── postman-environment.json       # Environment variables
│   ├── api-test-results.png           # Screenshot of test run
│   └── api-test-summary.md            # API testing summary
├── 03-manual-testing/
│   ├── test-cases.xlsx (or .md)       # Manual test cases
│   ├── test-execution-report.md       # Execution results
│   ├── bug-reports.md                 # Bug reports (if any)
│   └── screenshots/                   # Test execution screenshots
├── 04-automated-testing/
│   ├── cypress/ (or playwright/)      # Test automation code
│   ├── package.json                   # Dependencies
│   ├── README.md                      # How to run tests
│   ├── test-results/                  # Test execution results
│   └── test-recording.mp4             # Optional video
└── 05-test-report/
    ├── final-test-report.pdf          # Comprehensive test report
    └── supporting-documents/          # Additional artifacts
```

### Submission Checklist:

- [ ] Docker setup screenshots and notes
- [ ] Postman collection with API tests
- [ ] API test execution results
- [ ] Manual test cases document
- [ ] Manual test execution report
- [ ] Automated test code (Cypress or Playwright)
- [ ] Automated test execution results
- [ ] Comprehensive final test report
- [ ] All screenshots and supporting documents
- [ ] README with instructions to run your tests

### Submission Methods:

1. **GitHub Repository:** Push all artifacts to a public GitHub repository and share the link
2. **Compressed Archive:** Create a ZIP file with all artifacts
3. **Google Drive/Dropbox:** Upload all artifacts and share the folder link

---

## 💡 Additional Tips

### Docker Tips:
- Use `docker-compose logs` to view application logs
- Use `docker-compose down` to stop containers
- Use `docker-compose up --build` to rebuild containers if needed
- Check `docker-compose.yml` to understand the services

### API Testing Tips:
- Use Postman's collection runner for batch execution
- Implement tests using Postman's scripting (pre-request and test scripts)
- Use environment variables to make tests reusable across environments
- Consider negative testing scenarios
- Test boundary conditions and edge cases

### UI Automation Tips:
- Start with simple tests and gradually add complexity
- Use selectors that are less likely to change (data-testid, IDs)
- Implement explicit waits rather than arbitrary sleeps
- Run tests in headless mode for CI/CD integration
- Keep tests independent and idempotent

### Reporting Tips:
- Be clear and concise in your reporting
- Include visual evidence (screenshots, videos)
- Categorize issues by severity
- Provide actionable recommendations
- Use tables and charts for better readability

### Best Practices:
- Keep test data separate from test logic
- Version control all your test artifacts
- Document any assumptions or limitations
- Note any application bugs or unexpected behaviors
- Include test coverage metrics where applicable

---

## 📊 Evaluation Criteria

Your submission will be evaluated on:

1. **Completeness (25%):** All required deliverables submitted
2. **Test Coverage (25%):** Breadth and depth of test scenarios
3. **Quality of Automation (20%):** Code quality, maintainability, best practices
4. **Documentation (20%):** Clarity, professionalism, attention to detail
5. **Defect Reporting (10%):** Quality of bug reports and observations

---

## 🎓 Learning Resources

### Docker:
- [Docker Official Documentation](https://docs.docker.com/)
- [Docker Compose Documentation](https://docs.docker.com/compose/)

### API Testing:
- [Postman Learning Center](https://learning.postman.com/)
- [REST API Testing Guide](https://www.postman.com/api-platform/api-testing/)

### UI Automation:
- [Cypress Documentation](https://docs.cypress.io/)
- [Playwright Documentation](https://playwright.dev/)

### Testing Best Practices:
- [Testing Best Practices by Google](https://testing.googleblog.com/)
- [Test Automation Patterns](https://testautomationpatterns.org/)

---

## ❓ Frequently Asked Questions

**Q: What if I can't launch the Docker application?**  
A: Document the issue in detail (error messages, logs, troubleshooting steps). Attempt to resolve it and document your resolution process. If you cannot resolve it, explain what you tried.

**Q: Can I use tools other than Postman for API testing?**  
A: Yes, you can use alternatives like REST Client, Insomnia, or even custom scripts, but provide clear documentation on how to run your tests.

**Q: Do I need to automate all manual test cases?**  
A: No, focus on the most critical and repeatable scenarios for automation. Document why you chose specific tests to automate.

**Q: What if I find bugs in the application?**  
A: Great! Document them thoroughly in your bug reports. This demonstrates your testing skills.

**Q: How long should my test report be?**  
A: Quality over quantity. Be thorough but concise. Typically 10-20 pages is appropriate for this assignment.

**Q: Can I work in a team?**  
A: This is typically an individual assignment, but check with your instructor or evaluator.

---

## 🏆 Bonus Challenges (Optional)

If you want to go beyond the basic requirements:

1. **Performance Testing:** Use tools like JMeter or Artillery to perform load testing on the API
2. **Security Testing:** Perform basic security tests (SQL injection, XSS, etc.)
3. **CI/CD Integration:** Set up GitHub Actions to run your automated tests
4. **Visual Testing:** Implement visual regression testing using Percy or similar
5. **Accessibility Testing:** Test the application for WCAG compliance
6. **Mobile Testing:** Test the responsive design on different screen sizes
7. **API Documentation:** Create OpenAPI/Swagger documentation for the API
8. **Test Data Management:** Implement a sophisticated test data generation and cleanup strategy

---

Good luck with your testing assignment! Remember, the goal is not just to complete the tasks, but to demonstrate professional QA skills and thinking. 🚀
