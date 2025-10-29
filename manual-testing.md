# Manual Testing

## Overview

Manual testing is a crucial skill for QA engineers to identify usability issues, verify functionality, and explore the application from an end-user perspective. This section covers manual testing of the Employee Management CRM web application.

## Prerequisites

Before starting manual testing:
- The Employee Management CRM application should be running (see Project Launch section)
- Web browser (Chrome, Firefox, or Edge)
- Basic understanding of web application workflows
- Access to the application UI (typically at `http://localhost:3000`)

## Manual UI Testing

### Tasks

1. **Create a test plan covering:**
   - User registration/login (if applicable)
   - Employee creation workflow
   - Employee list viewing and filtering
   - Employee details viewing
   - Employee editing workflow
   - Employee deletion workflow
   - Form validation
   - Error handling
   - Navigation and usability

2. **Execute manual test cases and document:**
   - Test case ID
   - Test description
   - Prerequisites
   - Test steps
   - Expected results
   - Actual results
   - Status (Pass/Fail)
   - Screenshots of defects (if any)

### Test Scenarios

#### 1. Employee Creation Workflow
**Test Case ID:** TC-001  
**Objective:** Verify that a new employee can be successfully created

**Steps:**
1. Navigate to the employee creation page
2. Fill in all required fields (name, email, phone, department, etc.)
3. Click the "Save" or "Create" button
4. Verify success message is displayed
5. Navigate to the employee list
6. Verify the new employee appears in the list

**Expected Result:** Employee is created successfully and appears in the list

---

#### 2. Employee List Viewing
**Test Case ID:** TC-002  
**Objective:** Verify that the employee list displays correctly

**Steps:**
1. Navigate to the employees list page
2. Observe the displayed employee records
3. Check if pagination is available (if applicable)
4. Verify column headers are displayed
5. Check if sorting functionality is available

**Expected Result:** All employees are displayed with correct information

---

#### 3. Employee Details View
**Test Case ID:** TC-003  
**Objective:** Verify that employee details can be viewed

**Steps:**
1. Navigate to the employee list
2. Click on an employee record
3. Verify the details page loads
4. Check that all employee information is displayed correctly

**Expected Result:** Employee details are displayed accurately

---

#### 4. Employee Update Workflow
**Test Case ID:** TC-004  
**Objective:** Verify that an employee's information can be updated

**Steps:**
1. Navigate to an employee's details or edit page
2. Click the "Edit" button (if separate from details page)
3. Modify one or more fields (e.g., phone number, department)
4. Click "Save" or "Update"
5. Verify success message is displayed
6. Check that the changes are reflected in the employee details

**Expected Result:** Employee information is updated successfully

---

#### 5. Employee Deletion Workflow
**Test Case ID:** TC-005  
**Objective:** Verify that an employee can be deleted

**Steps:**
1. Navigate to the employee list
2. Select an employee to delete
3. Click the "Delete" button
4. Confirm the deletion in the confirmation dialog
5. Verify success message is displayed
6. Check that the employee is no longer in the list

**Expected Result:** Employee is deleted successfully

---

#### 6. Form Validation Tests
**Test Case ID:** TC-006  
**Objective:** Verify that form validation works correctly

**Scenario 6a: Empty Form Submission**
1. Navigate to employee creation page
2. Click "Save" without filling any fields
3. Verify validation error messages are displayed for required fields

**Scenario 6b: Invalid Email Format**
1. Navigate to employee creation page
2. Enter invalid email format (e.g., "notanemail")
3. Try to submit the form
4. Verify email validation error is displayed

**Scenario 6c: Invalid Phone Number**
1. Navigate to employee creation page
2. Enter invalid phone number format
3. Try to submit the form
4. Verify phone validation error is displayed

**Expected Result:** Appropriate validation messages are displayed for all invalid inputs

---

#### 7. Error Handling
**Test Case ID:** TC-007  
**Objective:** Verify that the application handles errors gracefully

**Steps:**
1. Try to access a non-existent employee (modify URL with invalid ID)
2. Verify appropriate error message is displayed
3. Try to submit duplicate data (if uniqueness constraints exist)
4. Verify error handling for network issues (stop backend temporarily)

**Expected Result:** User-friendly error messages are displayed

---

#### 8. Navigation and Usability
**Test Case ID:** TC-008  
**Objective:** Verify that navigation is intuitive and consistent

**Steps:**
1. Test all navigation links and buttons
2. Verify breadcrumbs (if available)
3. Test back button functionality
4. Check responsive design on different screen sizes
5. Verify loading indicators during operations
6. Check accessibility features (keyboard navigation, contrast, etc.)

**Expected Result:** Navigation is smooth and user-friendly

---

### Test Execution Template

Use this template to document your test execution:

| Test Case ID | Description | Priority | Status | Notes | Screenshot |
|--------------|-------------|----------|--------|-------|------------|
| TC-001 | Employee Creation | High | | | |
| TC-002 | Employee List View | High | | | |
| TC-003 | Employee Details | Medium | | | |
| TC-004 | Employee Update | High | | | |
| TC-005 | Employee Deletion | High | | | |
| TC-006 | Form Validation | High | | | |
| TC-007 | Error Handling | Medium | | | |
| TC-008 | Navigation | Low | | | |

### Bug Report Template

If you find defects during testing, document them using this template:

**Bug ID:** BUG-001  
**Severity:** High / Medium / Low  
**Priority:** High / Medium / Low  
**Status:** New / Open / Fixed / Retest / Closed  

**Summary:** Brief description of the bug

**Environment:**
- Browser: [e.g., Chrome 120]
- OS: [e.g., Windows 11, macOS 14]
- Application Version: [commit hash or version]

**Steps to Reproduce:**
1. Step 1
2. Step 2
3. Step 3

**Expected Result:** What should happen

**Actual Result:** What actually happened

**Screenshots/Video:** [Attach evidence]

**Additional Notes:** Any other relevant information

---

## Deliverables

Submit the following for manual testing:

1. **Manual Test Cases Document**
   - Format: Excel, Google Sheets, or Markdown table
   - Include all test case details
   - Cover all major workflows

2. **Test Execution Report**
   - Summary of tests executed
   - Pass/fail counts
   - Execution date and tester information
   - Overall assessment

3. **Bug Reports**
   - Detailed bug reports for any defects found
   - Severity and priority classification
   - Clear reproduction steps
   - Screenshots or videos as evidence

4. **Screenshots**
   - Key test execution screenshots
   - Evidence of successful tests
   - Screenshots of any defects found

---

## Tips for Effective Manual Testing

### Exploratory Testing
- Don't just follow the script - explore the application
- Try unexpected inputs and workflows
- Test boundary conditions
- Think like an end user

### Documentation
- Be detailed but concise
- Use clear, unambiguous language
- Include evidence (screenshots, videos)
- Document the testing environment

### Critical Thinking
- Question the expected behavior
- Consider edge cases
- Think about data integrity
- Consider security implications

### Efficiency
- Group similar tests together
- Use test data that covers multiple scenarios
- Take organized screenshots
- Keep notes as you test

---

## Best Practices

1. **Test in a Clean Environment:** Start with a known state of data
2. **Be Systematic:** Follow your test plan but remain flexible
3. **Document Everything:** Even minor observations can be valuable
4. **Think About Users:** Test from the end-user perspective
5. **Check Across Browsers:** Test on multiple browsers if possible
6. **Mobile Responsiveness:** Check how the app works on different screen sizes
7. **Accessibility:** Consider users with disabilities
8. **Performance:** Note any slow-loading pages or operations

---

## Evaluation Criteria

Your manual testing will be evaluated on:

- **Coverage (30%):** How thoroughly you tested the application
- **Quality of Test Cases (25%):** Clear, detailed, and well-structured
- **Defect Reporting (25%):** Quality and detail of bug reports
- **Documentation (20%):** Professionalism and completeness

---

## Resources

- [Test Case Writing Best Practices](https://www.softwaretestinghelp.com/how-to-write-test-cases-test-case-template/)
- [Bug Report Best Practices](https://www.browserstack.com/guide/how-to-write-a-bug-report)
- [Exploratory Testing Guide](https://www.ministryoftesting.com/dojo/lessons/what-is-exploratory-testing)
