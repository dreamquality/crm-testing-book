# Chapter 1: Testing a Dockerized Web App

## 🧩 Assignment Overview

**Application Under Test:** [Employee Management CRM](https://github.com/dreamquality/employee-management-crm)

**Objective:** Demonstrate comprehensive testing skills including manual testing, API testing, and UI automation for a Dockerized web application.

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

### Stage 2: API Automation

Automated API testing using Postman to verify the functionality and reliability of the Employee Management CRM REST API.

**📖 [Go to API Automation Guide →](./api-automation.md)**

**Key Topics Covered:**
- Postman collection creation and configuration
- Employee CRUD operations testing
- Request/response validation and assertions
- Environment variables and test data management
- Running tests with Collection Runner and Newman

---

### Stage 3: Manual Testing

Manual testing of the web application to identify usability issues and verify functionality from an end-user perspective.

**📖 [Go to Manual Testing Guide →](./manual-testing.md)**

**Key Topics Covered:**
- Test plan creation and execution
- Employee workflow testing (create, read, update, delete)
- Form validation and error handling
- Bug reporting and documentation
- Test execution templates

---

### Stage 4: UI Automation

Automated UI testing using Cypress or Playwright to ensure the web interface works correctly across different scenarios.

**📖 [Go to UI Automation Guide →](./ui-automation.md)**

**Key Topics Covered:**
- Cypress or Playwright setup
- Employee workflow automation
- Page Object Model implementation
- Test data fixtures and cleanup
- Best practices for stable UI tests

---

### Stage 5: Report Preparation

#### 5.1 Test Documentation

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
