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

```bash
# Create a new project directory
mkdir employee-crm-ui-tests
cd employee-crm-ui-tests

# Initialize npm project
npm init -y

# Install Cypress
npm install --save-dev cypress

# Open Cypress for first time
npx cypress open
```

Project structure:
```
employee-crm-ui-tests/
├── cypress/
│   ├── e2e/
│   │   └── employee.cy.js
│   ├── fixtures/
│   │   └── employees.json
│   ├── support/
│   │   ├── commands.js
│   │   └── e2e.js
│   └── pages/
│       └── EmployeePage.js
├── cypress.config.js
└── package.json
```

### Playwright Setup

```bash
# Create a new project directory
mkdir employee-crm-ui-tests
cd employee-crm-ui-tests

# Initialize npm project
npm init -y

# Install Playwright
npm init playwright@latest

# This will create:
# - playwright.config.js
# - tests/ directory
# - package.json with dependencies
```

---

## Test Scenarios to Automate

### 1. Employee Creation Flow

**Objective:** Verify that a new employee can be created through the UI

#### Cypress Implementation

```javascript
// cypress/e2e/employee-creation.cy.js
describe('Employee Creation', () => {
  beforeEach(() => {
    cy.visit('http://localhost:3000');
  });

  it('should create a new employee with valid data', () => {
    // Navigate to create employee page
    cy.contains('Add Employee').click();
    
    // Fill in the form
    cy.get('[data-testid="name-input"]').type('John Doe');
    cy.get('[data-testid="email-input"]').type('john.doe@example.com');
    cy.get('[data-testid="phone-input"]').type('+1234567890');
    cy.get('[data-testid="department-select"]').select('Engineering');
    cy.get('[data-testid="position-input"]').type('Software Engineer');
    
    // Submit the form
    cy.get('[data-testid="submit-button"]').click();
    
    // Verify success message
    cy.contains('Employee created successfully').should('be.visible');
    
    // Verify employee appears in the list
    cy.visit('http://localhost:3000/employees');
    cy.contains('John Doe').should('be.visible');
  });
});
```

#### Playwright Implementation

```javascript
// tests/employee-creation.spec.js
import { test, expect } from '@playwright/test';

test.describe('Employee Creation', () => {
  test('should create a new employee with valid data', async ({ page }) => {
    // Navigate to the application
    await page.goto('http://localhost:3000');
    
    // Navigate to create employee page
    await page.click('text=Add Employee');
    
    // Fill in the form
    await page.fill('[data-testid="name-input"]', 'John Doe');
    await page.fill('[data-testid="email-input"]', 'john.doe@example.com');
    await page.fill('[data-testid="phone-input"]', '+1234567890');
    await page.selectOption('[data-testid="department-select"]', 'Engineering');
    await page.fill('[data-testid="position-input"]', 'Software Engineer');
    
    // Submit the form
    await page.click('[data-testid="submit-button"]');
    
    // Verify success message
    await expect(page.locator('text=Employee created successfully')).toBeVisible();
    
    // Verify employee appears in the list
    await page.goto('http://localhost:3000/employees');
    await expect(page.locator('text=John Doe')).toBeVisible();
  });
});
```

---

### 2. Employee List Verification

**Objective:** Verify that the employee list displays correctly

#### Cypress Implementation

```javascript
describe('Employee List', () => {
  it('should display employee list correctly', () => {
    cy.visit('http://localhost:3000/employees');
    
    // Verify table/list is displayed
    cy.get('[data-testid="employee-table"]').should('be.visible');
    
    // Verify table headers
    cy.contains('Name').should('be.visible');
    cy.contains('Email').should('be.visible');
    cy.contains('Department').should('be.visible');
    
    // Verify employee data is shown
    cy.get('[data-testid="employee-row"]').should('have.length.at.least', 1);
    
    // Verify pagination (if applicable)
    cy.get('[data-testid="pagination"]').should('be.visible');
  });
});
```

#### Playwright Implementation

```javascript
test('should display employee list correctly', async ({ page }) => {
  await page.goto('http://localhost:3000/employees');
  
  // Verify table/list is displayed
  await expect(page.locator('[data-testid="employee-table"]')).toBeVisible();
  
  // Verify table headers
  await expect(page.locator('text=Name')).toBeVisible();
  await expect(page.locator('text=Email')).toBeVisible();
  await expect(page.locator('text=Department')).toBeVisible();
  
  // Verify employee data is shown
  const rows = await page.locator('[data-testid="employee-row"]').count();
  expect(rows).toBeGreaterThanOrEqual(1);
  
  // Verify pagination (if applicable)
  await expect(page.locator('[data-testid="pagination"]')).toBeVisible();
});
```

---

### 3. Employee Details View

**Objective:** Verify that employee details can be viewed

#### Cypress Implementation

```javascript
describe('Employee Details', () => {
  it('should display employee details', () => {
    cy.visit('http://localhost:3000/employees');
    
    // Click on first employee
    cy.get('[data-testid="employee-row"]').first().click();
    
    // Verify details page loads
    cy.url().should('include', '/employee/');
    
    // Verify employee information is displayed
    cy.get('[data-testid="employee-name"]').should('be.visible');
    cy.get('[data-testid="employee-email"]').should('be.visible');
    cy.get('[data-testid="employee-phone"]').should('be.visible');
    cy.get('[data-testid="employee-department"]').should('be.visible');
  });
});
```

#### Playwright Implementation

```javascript
test('should display employee details', async ({ page }) => {
  await page.goto('http://localhost:3000/employees');
  
  // Click on first employee
  await page.locator('[data-testid="employee-row"]').first().click();
  
  // Verify details page loads
  await expect(page).toHaveURL(/\/employee\//);
  
  // Verify employee information is displayed
  await expect(page.locator('[data-testid="employee-name"]')).toBeVisible();
  await expect(page.locator('[data-testid="employee-email"]')).toBeVisible();
  await expect(page.locator('[data-testid="employee-phone"]')).toBeVisible();
  await expect(page.locator('[data-testid="employee-department"]')).toBeVisible();
});
```

---

### 4. Employee Update Flow

**Objective:** Verify that an employee's information can be updated

#### Cypress Implementation

```javascript
describe('Employee Update', () => {
  it('should update employee information', () => {
    cy.visit('http://localhost:3000/employees');
    
    // Click on first employee
    cy.get('[data-testid="employee-row"]').first().click();
    
    // Click edit button
    cy.get('[data-testid="edit-button"]').click();
    
    // Modify employee information
    cy.get('[data-testid="phone-input"]').clear().type('+9876543210');
    cy.get('[data-testid="department-select"]').select('Management');
    
    // Save changes
    cy.get('[data-testid="save-button"]').click();
    
    // Verify success message
    cy.contains('Employee updated successfully').should('be.visible');
    
    // Verify changes are reflected
    cy.get('[data-testid="employee-phone"]').should('contain', '+9876543210');
    cy.get('[data-testid="employee-department"]').should('contain', 'Management');
  });
});
```

#### Playwright Implementation

```javascript
test('should update employee information', async ({ page }) => {
  await page.goto('http://localhost:3000/employees');
  
  // Click on first employee
  await page.locator('[data-testid="employee-row"]').first().click();
  
  // Click edit button
  await page.click('[data-testid="edit-button"]');
  
  // Modify employee information
  await page.fill('[data-testid="phone-input"]', '+9876543210');
  await page.selectOption('[data-testid="department-select"]', 'Management');
  
  // Save changes
  await page.click('[data-testid="save-button"]');
  
  // Verify success message
  await expect(page.locator('text=Employee updated successfully')).toBeVisible();
  
  // Verify changes are reflected
  await expect(page.locator('[data-testid="employee-phone"]')).toContainText('+9876543210');
  await expect(page.locator('[data-testid="employee-department"]')).toContainText('Management');
});
```

---

### 5. Employee Deletion Flow

**Objective:** Verify that an employee can be deleted

#### Cypress Implementation

```javascript
describe('Employee Deletion', () => {
  it('should delete an employee', () => {
    cy.visit('http://localhost:3000/employees');
    
    // Get the name of the first employee
    cy.get('[data-testid="employee-row"]').first()
      .find('[data-testid="employee-name"]')
      .invoke('text')
      .as('employeeName');
    
    // Click delete button
    cy.get('[data-testid="employee-row"]').first()
      .find('[data-testid="delete-button"]')
      .click();
    
    // Confirm deletion in modal
    cy.get('[data-testid="confirm-delete"]').click();
    
    // Verify success message
    cy.contains('Employee deleted successfully').should('be.visible');
    
    // Verify employee is removed from list
    cy.get('@employeeName').then((name) => {
      cy.contains(name).should('not.exist');
    });
  });
});
```

#### Playwright Implementation

```javascript
test('should delete an employee', async ({ page }) => {
  await page.goto('http://localhost:3000/employees');
  
  // Get the name of the first employee
  const employeeName = await page.locator('[data-testid="employee-row"]')
    .first()
    .locator('[data-testid="employee-name"]')
    .textContent();
  
  // Click delete button
  await page.locator('[data-testid="employee-row"]')
    .first()
    .locator('[data-testid="delete-button"]')
    .click();
  
  // Confirm deletion in modal
  await page.click('[data-testid="confirm-delete"]');
  
  // Verify success message
  await expect(page.locator('text=Employee deleted successfully')).toBeVisible();
  
  // Verify employee is removed from list
  await expect(page.locator(`text=${employeeName}`)).not.toBeVisible();
});
```

---

### 6. Form Validation Tests

**Objective:** Verify that form validation works correctly

#### Cypress Implementation

```javascript
describe('Form Validation', () => {
  beforeEach(() => {
    cy.visit('http://localhost:3000');
    cy.contains('Add Employee').click();
  });

  it('should show error for empty form submission', () => {
    cy.get('[data-testid="submit-button"]').click();
    
    cy.contains('Name is required').should('be.visible');
    cy.contains('Email is required').should('be.visible');
  });

  it('should show error for invalid email', () => {
    cy.get('[data-testid="name-input"]').type('John Doe');
    cy.get('[data-testid="email-input"]').type('notanemail');
    cy.get('[data-testid="submit-button"]').click();
    
    cy.contains('Invalid email format').should('be.visible');
  });

  it('should show error for invalid phone number', () => {
    cy.get('[data-testid="name-input"]').type('John Doe');
    cy.get('[data-testid="email-input"]').type('john@example.com');
    cy.get('[data-testid="phone-input"]').type('123');
    cy.get('[data-testid="submit-button"]').click();
    
    cy.contains('Invalid phone number').should('be.visible');
  });
});
```

#### Playwright Implementation

```javascript
test.describe('Form Validation', () => {
  test.beforeEach(async ({ page }) => {
    await page.goto('http://localhost:3000');
    await page.click('text=Add Employee');
  });

  test('should show error for empty form submission', async ({ page }) => {
    await page.click('[data-testid="submit-button"]');
    
    await expect(page.locator('text=Name is required')).toBeVisible();
    await expect(page.locator('text=Email is required')).toBeVisible();
  });

  test('should show error for invalid email', async ({ page }) => {
    await page.fill('[data-testid="name-input"]', 'John Doe');
    await page.fill('[data-testid="email-input"]', 'notanemail');
    await page.click('[data-testid="submit-button"]');
    
    await expect(page.locator('text=Invalid email format')).toBeVisible();
  });

  test('should show error for invalid phone number', async ({ page }) => {
    await page.fill('[data-testid="name-input"]', 'John Doe');
    await page.fill('[data-testid="email-input"]', 'john@example.com');
    await page.fill('[data-testid="phone-input"]', '123');
    await page.click('[data-testid="submit-button"]');
    
    await expect(page.locator('text=Invalid phone number')).toBeVisible();
  });
});
```

---

## Implementing Page Object Model (POM)

### Cypress Page Object Example

```javascript
// cypress/pages/EmployeePage.js
export class EmployeePage {
  // Selectors
  addEmployeeButton = 'text=Add Employee';
  nameInput = '[data-testid="name-input"]';
  emailInput = '[data-testid="email-input"]';
  phoneInput = '[data-testid="phone-input"]';
  departmentSelect = '[data-testid="department-select"]';
  submitButton = '[data-testid="submit-button"]';
  successMessage = 'text=Employee created successfully';

  // Methods
  visit() {
    cy.visit('http://localhost:3000');
  }

  clickAddEmployee() {
    cy.contains(this.addEmployeeButton).click();
  }

  fillEmployeeForm(employee) {
    cy.get(this.nameInput).type(employee.name);
    cy.get(this.emailInput).type(employee.email);
    cy.get(this.phoneInput).type(employee.phone);
    cy.get(this.departmentSelect).select(employee.department);
  }

  submitForm() {
    cy.get(this.submitButton).click();
  }

  verifySuccess() {
    cy.contains(this.successMessage).should('be.visible');
  }
}

// Usage in test
import { EmployeePage } from '../pages/EmployeePage';

describe('Employee Creation with POM', () => {
  const employeePage = new EmployeePage();
  
  it('should create employee using page object', () => {
    employeePage.visit();
    employeePage.clickAddEmployee();
    employeePage.fillEmployeeForm({
      name: 'John Doe',
      email: 'john@example.com',
      phone: '+1234567890',
      department: 'Engineering'
    });
    employeePage.submitForm();
    employeePage.verifySuccess();
  });
});
```

### Playwright Page Object Example

```javascript
// pages/EmployeePage.js
export class EmployeePage {
  constructor(page) {
    this.page = page;
    this.addEmployeeButton = page.locator('text=Add Employee');
    this.nameInput = page.locator('[data-testid="name-input"]');
    this.emailInput = page.locator('[data-testid="email-input"]');
    this.phoneInput = page.locator('[data-testid="phone-input"]');
    this.departmentSelect = page.locator('[data-testid="department-select"]');
    this.submitButton = page.locator('[data-testid="submit-button"]');
    this.successMessage = page.locator('text=Employee created successfully');
  }

  async goto() {
    await this.page.goto('http://localhost:3000');
  }

  async clickAddEmployee() {
    await this.addEmployeeButton.click();
  }

  async fillEmployeeForm(employee) {
    await this.nameInput.fill(employee.name);
    await this.emailInput.fill(employee.email);
    await this.phoneInput.fill(employee.phone);
    await this.departmentSelect.selectOption(employee.department);
  }

  async submitForm() {
    await this.submitButton.click();
  }

  async verifySuccess() {
    await expect(this.successMessage).toBeVisible();
  }
}

// Usage in test
import { test } from '@playwright/test';
import { EmployeePage } from '../pages/EmployeePage';

test('should create employee using page object', async ({ page }) => {
  const employeePage = new EmployeePage(page);
  
  await employeePage.goto();
  await employeePage.clickAddEmployee();
  await employeePage.fillEmployeeForm({
    name: 'John Doe',
    email: 'john@example.com',
    phone: '+1234567890',
    department: 'Engineering'
  });
  await employeePage.submitForm();
  await employeePage.verifySuccess();
});
```

---

## Test Data Management

### Using Fixtures (Cypress)

```javascript
// cypress/fixtures/employees.json
{
  "validEmployee": {
    "name": "John Doe",
    "email": "john.doe@example.com",
    "phone": "+1234567890",
    "department": "Engineering",
    "position": "Software Engineer"
  },
  "invalidEmployee": {
    "name": "",
    "email": "invalid-email",
    "phone": "123"
  }
}

// Usage in test
describe('Employee Tests with Fixtures', () => {
  it('should create employee using fixture data', () => {
    cy.fixture('employees').then((data) => {
      const employee = data.validEmployee;
      // Use employee data in test
    });
  });
});
```

---

## Test Cleanup

### Cypress Example

```javascript
describe('Employee Tests with Cleanup', () => {
  let createdEmployeeId;

  afterEach(() => {
    // Clean up created test data
    if (createdEmployeeId) {
      cy.request('DELETE', `http://localhost:3000/api/employees/${createdEmployeeId}`);
    }
  });

  it('should create employee', () => {
    // Create employee and store ID
    cy.request('POST', 'http://localhost:3000/api/employees', {
      name: 'Test Employee',
      email: 'test@example.com'
    }).then((response) => {
      createdEmployeeId = response.body.id;
    });
  });
});
```

---

## Deliverables

Submit the following for UI automation:

1. **Automated Test Code**
   - Complete test suite with all scenarios
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
   - Video of test execution
   - Demonstration of key test scenarios

---

## Best Practices

### Selectors
- Use `data-testid` attributes for stable selectors
- Avoid using CSS classes that might change
- Use semantic HTML elements when possible
- Create reusable selector constants

### Waits and Timing
- Use built-in waits (Cypress automatic waiting, Playwright auto-waiting)
- Avoid fixed waits (sleep/wait)
- Wait for specific conditions (visibility, text content)
- Set appropriate timeouts for slow operations

### Test Organization
- One test file per feature or page
- Use descriptive test names
- Group related tests with describe/test.describe
- Keep tests independent and idempotent

### Test Data
- Use fixtures for complex test data
- Generate unique data for each test run
- Clean up test data after execution
- Separate test data from test logic

### Error Handling
- Use proper assertions
- Add meaningful error messages
- Take screenshots on failure
- Log relevant information for debugging

---

## Tips for Effective UI Automation

1. **Start Small:** Begin with critical user journeys
2. **Keep Tests Fast:** Optimize test execution time
3. **Make Tests Reliable:** Eliminate flakiness
4. **Use Debugging Tools:** Leverage browser dev tools and framework debuggers
5. **Run Tests Locally:** Validate before committing
6. **CI/CD Integration:** Run tests in pipelines
7. **Maintain Tests:** Update tests when UI changes

---

## Evaluation Criteria

Your UI automation will be evaluated on:

- **Code Quality (30%):** Clean, maintainable, follows best practices
- **Test Coverage (25%):** Comprehensive scenario coverage
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
- [Playwright Examples](https://playwright.dev/docs/examples)

### General Resources
- [Page Object Model Pattern](https://martinfowler.com/bliki/PageObject.html)
- [Test Automation Patterns](https://testautomationpatterns.org/)
- [JavaScript Testing Best Practices](https://github.com/goldbergyoni/javascript-testing-best-practices)
