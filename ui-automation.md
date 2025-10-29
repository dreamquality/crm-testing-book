# UI Automation

## Overview

UI automation testing ensures that the web application's user interface works correctly across different scenarios and browsers. This section covers automated testing of the Employee Management CRM web application using Cypress or Playwright.

## Prerequisites

Before starting UI automation:
- The Employee Management CRM application should be running (see Project Launch section)
- **Cypress** (v12+) or **Playwright** (v1.30+) installed
- Node.js and npm installed
- Basic understanding of JavaScript/TypeScript
- Familiarity with CSS selectors and DOM manipulation

## Choosing Your Framework

### Cypress
- Easy to set up and use
- Great developer experience with time-travel debugging
- Real-time test execution visualization
- Built-in waiting and retry logic

### Playwright
- Cross-browser support (Chrome, Firefox, Safari, Edge)
- Powerful API for complex scenarios
- Better performance for large test suites
- Built-in test runner and reporters

**Choose one framework and stick with it for this assignment.**

---

## Setting Up Your Test Framework

### Cypress Setup

1. Create a new project directory for your tests
2. Initialize npm project
3. Install Cypress as a dev dependency
4. Open Cypress to generate initial folder structure
5. Configure Cypress settings in config file

**Project Structure:**
- `cypress/e2e/` - Test files
- `cypress/fixtures/` - Test data files
- `cypress/support/` - Custom commands and setup
- `cypress.config.js` - Configuration file

### Playwright Setup

1. Create a new project directory
2. Initialize npm project
3. Run Playwright initialization wizard
4. Configure browser settings
5. Set up test directory structure

**Project Structure:**
- `tests/` - Test files
- `playwright.config.js` - Configuration file
- Test runner and reporters configured

---

## Test Scenarios to Automate

### 1. Employee Creation Flow

**Objective:** Verify that a new employee can be created through the UI

**Test Steps:**
1. Navigate to the application homepage
2. Click on "Add Employee" button
3. Fill in all required fields (name, email, phone, department, position)
4. Submit the form
5. Verify success message is displayed
6. Navigate to employee list
7. Verify new employee appears in the list

**Assertions to Include:**
- Form fields accept valid input
- Success message contains expected text
- New employee is visible in the list with correct information

---

### 2. Employee List Verification

**Objective:** Verify that the employee list displays correctly

**Test Steps:**
1. Navigate to employees list page
2. Verify table/list element is displayed
3. Check table headers are present
4. Verify at least one employee row exists
5. Check pagination controls (if applicable)

**Assertions to Include:**
- Table headers match expected columns (Name, Email, Department, etc.)
- Employee data is displayed correctly
- Pagination works properly

---

### 3. Employee Details View

**Objective:** Verify that employee details can be viewed

**Test Steps:**
1. Navigate to employee list
2. Click on a specific employee
3. Verify details page loads
4. Check all employee information is displayed

**Assertions to Include:**
- URL changes to employee detail page
- All employee fields are visible and contain data
- Back/navigation buttons work correctly

---

### 4. Employee Update Flow

**Objective:** Verify that an employee's information can be updated

**Test Steps:**
1. Navigate to employee list
2. Click on an employee to view details
3. Click edit button
4. Modify one or more fields (e.g., phone number, department)
5. Save changes
6. Verify success message
7. Confirm changes are reflected in employee details

**Assertions to Include:**
- Edit form pre-populates with current data
- Form validation works for updated fields
- Success message appears after save
- Updated data persists and displays correctly

---

### 5. Employee Deletion Flow

**Objective:** Verify that an employee can be deleted

**Test Steps:**
1. Navigate to employee list
2. Select an employee to delete
3. Click delete button
4. Confirm deletion in confirmation dialog
5. Verify success message
6. Confirm employee is no longer in the list

**Assertions to Include:**
- Confirmation dialog appears before deletion
- Success message confirms deletion
- Deleted employee does not appear in search results

---

### 6. Form Validation Tests

**Objective:** Verify that form validation works correctly

**Test Scenarios:**

**a) Empty Form Submission**
- Navigate to employee creation page
- Click submit without filling fields
- Verify validation error messages appear for required fields

**b) Invalid Email Format**
- Enter invalid email format (e.g., "notanemail")
- Attempt to submit form
- Verify email validation error appears

**c) Invalid Phone Number**
- Enter invalid phone number format
- Attempt to submit form
- Verify phone validation error appears

**Assertions to Include:**
- Error messages are displayed for each invalid field
- Form cannot be submitted with validation errors
- Error messages are clear and helpful

---

## Implementing Page Object Model (POM)

### What is Page Object Model?

Page Object Model is a design pattern that:
- Creates an object repository for UI elements
- Separates test logic from page-specific code
- Improves test maintainability
- Reduces code duplication

### Structure

**Page Objects should contain:**
- Element locators (selectors for UI elements)
- Methods to interact with page elements
- Methods to perform common page actions
- No test assertions (those belong in test files)

**Example Structure:**
- `pages/EmployeePage.js` - Employee list page object
- `pages/EmployeeFormPage.js` - Employee form page object
- `pages/EmployeeDetailPage.js` - Employee detail page object

**Test files should:**
- Import and use page objects
- Contain test assertions
- Focus on test logic, not element locations

---

## Test Data Management

### Using Fixtures

**Benefits:**
- Centralized test data
- Reusable across tests
- Easy to maintain
- Supports multiple data sets

**Test Data to Include:**
- Valid employee data (complete profiles)
- Invalid data (for negative testing)
- Edge cases (boundary values)
- Special characters and unicode

### Data Generation

**Strategies:**
- Generate unique data for each test run (timestamps, UUIDs)
- Use faker libraries for realistic data
- Maintain test data separately from test logic

---

## Test Cleanup

### Why Test Cleanup Matters

- Prevents test data accumulation
- Ensures tests can run repeatedly
- Maintains test independence
- Prevents false failures

### Cleanup Strategies

**After Each Test:**
- Delete created test data
- Reset application state if needed
- Clear browser storage/cookies

**Using Hooks:**
- `beforeEach` - Set up test data
- `afterEach` - Clean up test data
- `before` - One-time setup
- `after` - One-time cleanup

---

## Best Practices

### Selectors
- Use `data-testid` attributes for stable selectors
- Avoid CSS classes that might change frequently
- Use semantic HTML elements when possible
- Create reusable selector constants

### Waits and Timing
- Use framework's built-in waiting mechanisms
- Avoid fixed waits (sleep/hardcoded delays)
- Wait for specific conditions (visibility, text content, enabled state)
- Set appropriate timeouts for slow operations

### Test Organization
- One test file per feature or page
- Use descriptive test names that explain what is being tested
- Group related tests using describe blocks
- Keep tests independent of each other

### Test Data
- Use fixtures for complex or repeated test data
- Generate unique data to avoid conflicts
- Clean up test data after execution
- Separate test data from test logic

### Error Handling
- Use clear, descriptive assertions
- Add meaningful error messages
- Take screenshots on failure automatically
- Log relevant information for debugging

---

## Tips for Effective UI Automation

1. **Start Small:** Begin with critical user journeys, add more tests incrementally
2. **Keep Tests Fast:** Optimize test execution time, run tests in parallel when possible
3. **Make Tests Reliable:** Eliminate flakiness through proper waits and selectors
4. **Use Debugging Tools:** Leverage browser dev tools and framework debugging features
5. **Run Tests Locally:** Validate tests work before committing
6. **CI/CD Integration:** Set up continuous integration to run tests automatically
7. **Maintain Tests:** Update tests when UI changes, refactor regularly

---

## Deliverables

Submit the following for UI automation:

1. **Automated Test Code**
   - Complete test suite covering all scenarios
   - Page Object Model implementation
   - Test data fixtures
   - Configuration files

2. **README with Instructions**
   - Prerequisites and setup instructions
   - How to install dependencies
   - How to run tests
   - How to view test reports

3. **Test Execution Report**
   - Screenshots or HTML reports
   - Test execution summary
   - Pass/fail statistics
   - Any identified issues

4. **Video Recording (Optional)**
   - Video demonstrating test execution
   - Showing key test scenarios

---

## Running Tests

### Local Execution

**Cypress:**
- Open Cypress Test Runner for interactive mode
- Run tests in headless mode for CI/CD
- Generate reports and screenshots

**Playwright:**
- Run tests in headed or headless mode
- Execute tests across multiple browsers
- Generate HTML reports with traces

### CI/CD Integration

**Benefits:**
- Automated test execution on code changes
- Early detection of issues
- Consistent test environment
- Automatic report generation

**Setup Steps:**
1. Configure test scripts in package.json
2. Set up CI/CD pipeline (GitHub Actions, Jenkins, etc.)
3. Configure test execution triggers
4. Set up report publishing

---

## Evaluation Criteria

Your UI automation will be evaluated on:

- **Code Quality (30%):** Clean, maintainable code following best practices
- **Test Coverage (25%):** Comprehensive coverage of important scenarios
- **Page Object Model (20%):** Proper implementation and usage
- **Test Stability (15%):** Tests run reliably without flakiness
- **Documentation (10%):** Clear instructions and comments

---

## Resources

### Cypress Resources
- [Cypress Documentation](https://docs.cypress.io/)
- [Cypress Best Practices](https://docs.cypress.io/guides/references/best-practices)
- [Cypress Examples](https://example.cypress.io/)

### Playwright Resources
- [Playwright Documentation](https://playwright.dev/)
- [Playwright Best Practices](https://playwright.dev/docs/best-practices)
- [Playwright API Reference](https://playwright.dev/docs/api/class-playwright)

### General Resources
- [Page Object Model Pattern](https://martinfowler.com/bliki/PageObject.html)
- [Test Automation Patterns](https://testautomationpatterns.org/)
- [JavaScript Testing Best Practices](https://github.com/goldbergyoni/javascript-testing-best-practices)
