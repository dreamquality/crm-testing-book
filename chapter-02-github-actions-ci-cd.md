# Chapter 2: Setting Up GitHub Actions for Automated Testing

## 🧩 Assignment Overview

**Objective:** Learn how to set up Continuous Integration (CI) with GitHub Actions to automatically run API and UI tests on every code change.

**Difficulty Level:** Intermediate to Advanced

## 🎯 Goals

By completing this assignment, you will demonstrate your ability to:

1. **Set up GitHub Actions** workflows for automated testing
2. **Configure CI/CD pipelines** for API and UI test execution
3. **Integrate automated tests** into the development workflow
4. **Generate and publish** test reports automatically
5. **Implement best practices** for CI/CD in testing

## 🛠️ Required Tools

- **GitHub Account** with repository access
- **Git** for version control
- **Node.js and npm** (for running test frameworks)
- **Postman/Newman** (for API tests) or **Cypress/Playwright** (for UI tests)
- Basic understanding of YAML syntax
- Familiarity with GitHub Actions concepts

## 📋 Assignment Stages

### Stage 1: Understanding GitHub Actions

#### 1.1 GitHub Actions Basics

**Concepts to Learn:**

- **Workflows:** Automated processes defined in YAML files
- **Events:** Triggers that start workflows (push, pull_request, schedule, etc.)
- **Jobs:** Groups of steps that execute on the same runner
- **Steps:** Individual tasks within a job
- **Runners:** Servers that run your workflows (GitHub-hosted or self-hosted)
- **Actions:** Reusable units of code that can be shared across workflows

**Key Workflow Components:**
- Workflow file location: `.github/workflows/`
- Workflow triggers: when tests should run
- Environment setup: installing dependencies
- Test execution: running your test suite
- Artifact publishing: storing test results

---

### Stage 2: Setting Up API Test Automation with GitHub Actions

#### 2.1 Postman/Newman API Tests in CI

**Tasks:**

1. **Create Workflow File**
   - Create `.github/workflows/api-tests.yml` in your repository
   - Define workflow name and triggers (push, pull_request)

2. **Configure Workflow for API Tests**

   **Key Configuration Elements:**
   - Workflow name: "API Automated Tests"
   - Triggers: on push to main branch and pull requests
   - Runner: ubuntu-latest
   - Node.js setup: Use actions/setup-node
   - Newman installation: Install newman and reporters
   - Test execution: Run Postman collection with Newman
   - Report generation: Generate HTML/JUnit reports

3. **Environment Variables**
   - Set up API base URL
   - Configure authentication tokens (use GitHub Secrets)
   - Set test data variables

4. **Test Execution Steps**
   - Install dependencies
   - Start application (if needed)
   - Run Newman with collection and environment files
   - Generate test reports

5. **Report Publishing**
   - Upload test results as artifacts
   - Display test summary in workflow logs
   - Optionally publish to GitHub Pages or PR comments

**Deliverables:**
- Working GitHub Actions workflow file for API tests
- Newman test execution with proper configuration
- Test reports generated and accessible
- Screenshot of successful workflow run

---

### Stage 3: Setting Up UI Test Automation with GitHub Actions

#### 3.1 Cypress UI Tests in CI

**Tasks:**

1. **Create Workflow File**
   - Create `.github/workflows/ui-tests.yml` in your repository
   - Define workflow name and triggers

2. **Configure Workflow for Cypress Tests**

   **Key Configuration Elements:**
   - Workflow name: "UI Automated Tests"
   - Triggers: on push to main branch and pull requests
   - Runner: ubuntu-latest (with display server)
   - Cypress installation: Use cypress-io/github-action
   - Browser configuration: Chrome, Firefox, or Electron
   - Test execution: Run Cypress tests
   - Video/Screenshot capture: Record test execution

3. **Application Startup**
   - Start the application server before tests
   - Wait for application to be ready
   - Use `wait-on` to ensure server is running

4. **Test Execution Configuration**
   - Set base URL for tests
   - Configure browser selection
   - Set viewport sizes
   - Enable video recording
   - Configure screenshot on failure

5. **Artifacts Management**
   - Upload test videos on failure
   - Upload screenshots
   - Upload test reports (Mochawesome, JUnit)
   - Store artifacts with appropriate retention

**Deliverables:**
- Working GitHub Actions workflow file for UI tests
- Cypress tests running successfully in CI
- Test artifacts (videos, screenshots) available
- Screenshot of successful workflow run with reports

---

#### 3.2 Playwright UI Tests in CI

**Tasks:**

1. **Create Workflow File**
   - Create `.github/workflows/ui-tests-playwright.yml`
   - Define workflow configuration

2. **Configure Workflow for Playwright Tests**

   **Key Configuration Elements:**
   - Workflow name: "UI Automated Tests (Playwright)"
   - Multi-browser testing: Chrome, Firefox, Safari (WebKit)
   - Playwright installation: Use actions/setup-node + npx playwright install
   - Browser dependencies: Install system dependencies
   - Parallel test execution: Configure sharding if needed

3. **Test Execution**
   - Install Playwright browsers
   - Run tests across multiple browsers
   - Generate HTML report
   - Capture traces on failure

4. **Reporting and Artifacts**
   - Upload Playwright HTML report
   - Upload test traces for debugging
   - Upload screenshots and videos
   - Publish report to GitHub Pages (optional)

**Deliverables:**
- Working Playwright workflow file
- Tests running across multiple browsers
- HTML report with test results
- Traces and artifacts available for failed tests

---

### Stage 4: Advanced CI/CD Patterns

#### 4.1 Best Practices

**Workflow Optimization:**

1. **Caching Dependencies**
   - Cache npm packages for faster builds
   - Cache Playwright browsers
   - Use appropriate cache keys

2. **Parallel Execution**
   - Run API and UI tests in parallel
   - Use matrix strategy for multiple browsers
   - Shard large test suites

3. **Conditional Execution**
   - Run specific tests based on changed files
   - Skip tests for documentation-only changes
   - Use path filters for targeted testing

4. **Error Handling**
   - Continue on error for non-critical tests
   - Set appropriate timeout values
   - Retry flaky tests automatically

5. **Notifications**
   - Send notifications on test failures
   - Create GitHub Issues for failed runs
   - Post results to Slack or other channels

---

#### 4.2 Security Best Practices

**Protecting Sensitive Data:**

1. **Use GitHub Secrets**
   - Store API keys, tokens, and passwords
   - Never hardcode credentials in workflows
   - Use environment-specific secrets

2. **Limit Permissions**
   - Set minimal required permissions
   - Use GITHUB_TOKEN appropriately
   - Restrict workflow access

3. **Audit and Monitoring**
   - Review workflow runs regularly
   - Monitor for suspicious activities
   - Keep dependencies updated

---

### Stage 5: Monitoring and Reporting

#### 5.1 Test Result Visualization

**Tasks:**

1. **Status Badges**
   - Add workflow status badges to README
   - Display build status
   - Show test pass/fail status

2. **Test Reports**
   - Generate human-readable reports
   - Publish reports to GitHub Pages
   - Add test summaries to PR comments

3. **Metrics Tracking**
   - Track test execution time
   - Monitor test flakiness
   - Measure code coverage (if applicable)

4. **Dashboard Setup**
   - Use GitHub Actions dashboard
   - Set up custom dashboards (optional)
   - Monitor trends over time

**Deliverables:**
- Status badge in README
- Published test reports
- Test metrics documentation

---

## 📦 What to Submit

### Submission Process

**Step 1: Set Up Your Repository**

1. Use your forked Employee Management CRM repository
2. Ensure you have API or UI tests already created
3. Verify tests run successfully locally

**Step 2: Add GitHub Actions Workflows**

Add your workflow configuration to your forked repository:

- **For API Tests:**
  - Create `.github/workflows/api-tests.yml`
  - Configure Newman/Postman execution
  - Set up test reporting

- **For UI Tests:**
  - Create `.github/workflows/ui-tests.yml`
  - Configure Cypress or Playwright execution
  - Set up artifact collection

**Step 3: Verify and Document**

1. Push workflows to your repository
2. Verify workflows run successfully
3. Document your CI/CD setup in README
4. Include workflow badges

**Step 4: Create Pull Request**

Create a PR that includes:
- Workflow YAML files
- Updated README with badges and CI/CD documentation
- Screenshots of successful workflow runs
- Any configuration files needed
- Documentation on how to run workflows

### Submission Checklist:

- [ ] GitHub Actions workflow file(s) created
- [ ] Workflows run successfully on push/PR
- [ ] Test reports generated and accessible
- [ ] Workflow status badges added to README
- [ ] Documentation updated with CI/CD setup instructions
- [ ] Screenshots of successful workflow runs included
- [ ] Secrets properly configured (if needed)
- [ ] Pull Request created with all changes

---

## 💡 Additional Tips

### GitHub Actions Tips:
- Start with simple workflows and iterate
- Use GitHub's workflow editor for syntax validation
- Test workflows on a branch before merging
- Use `act` tool for local workflow testing
- Review GitHub Actions logs carefully

### Newman/API Testing Tips:
- Use reporters: cli, json, junit, html
- Store collections and environments in repository
- Use pre-request scripts for dynamic data
- Handle authentication properly
- Set appropriate timeouts

### Cypress Tips:
- Use official cypress-io/github-action
- Configure retry logic for flaky tests
- Record videos only on failure to save space
- Use parallel execution for faster runs
- Keep tests independent

### Playwright Tips:
- Install all browsers or specific ones
- Use sharding for parallel execution
- Enable trace on first retry
- Use HTML reporter for detailed results
- Configure multiple projects for different browsers

### Debugging Tips:
- Enable debug logging when needed
- Use `continue-on-error` for non-critical steps
- Add explicit wait times when necessary
- Check runner specifications match requirements
- Review workflow run logs thoroughly

---

## 📊 Evaluation Criteria

Your submission will be evaluated on:

1. **Workflow Configuration (30%):** Proper setup and configuration of GitHub Actions
2. **Test Integration (25%):** Successful integration of API/UI tests
3. **Reporting (20%):** Quality of test reports and artifacts
4. **Best Practices (15%):** Following CI/CD and security best practices
5. **Documentation (10%):** Clear documentation and instructions

---

## 🎓 Learning Resources

### GitHub Actions:
- [GitHub Actions Documentation](https://docs.github.com/en/actions)
- [GitHub Actions Marketplace](https://github.com/marketplace?type=actions)
- [Workflow Syntax](https://docs.github.com/en/actions/reference/workflow-syntax-for-github-actions)

### Newman/API Testing:
- [Newman GitHub Action](https://github.com/marketplace/actions/newman-action)
- [Newman CLI Documentation](https://learning.postman.com/docs/running-collections/using-newman-cli/command-line-integration-with-newman/)

### Cypress CI:
- [Cypress GitHub Action](https://github.com/cypress-io/github-action)
- [Cypress CI Documentation](https://docs.cypress.io/guides/continuous-integration/introduction)

### Playwright CI:
- [Playwright CI Documentation](https://playwright.dev/docs/ci)
- [Playwright GitHub Actions](https://playwright.dev/docs/ci-intro)

### CI/CD Best Practices:
- [GitHub Actions Best Practices](https://docs.github.com/en/actions/learn-github-actions/best-practices-for-github-actions)
- [Security Hardening](https://docs.github.com/en/actions/security-guides/security-hardening-for-github-actions)

---

## ❓ Frequently Asked Questions

**Q: Can I use other CI/CD tools instead of GitHub Actions?**  
A: This assignment focuses on GitHub Actions, but you can document alternative approaches (Jenkins, GitLab CI, CircleCI) as bonus work.

**Q: Do I need to run tests on multiple operating systems?**  
A: Not required, but using a matrix strategy to test on multiple OS is good practice and can be done as bonus work.

**Q: How do I handle secrets in GitHub Actions?**  
A: Use GitHub repository secrets under Settings > Secrets and variables > Actions. Reference them in workflows with `${{ secrets.SECRET_NAME }}`.

**Q: What if my tests fail in CI but pass locally?**  
A: Common issues include timing differences, missing dependencies, or environment configuration. Check workflow logs and ensure your CI environment matches local setup.

**Q: How can I reduce workflow execution time?**  
A: Use caching for dependencies, run jobs in parallel, use matrix strategies efficiently, and consider running only affected tests.

**Q: Should I commit my Postman collections?**  
A: Yes, commit collections and environment files (without sensitive data) to your repository so they can be used by workflows.

---

## 🏆 Bonus Challenges (Optional)

If you want to go beyond the basic requirements:

1. **Multi-Environment Testing:** Set up workflows for dev, staging, and production environments
2. **Scheduled Tests:** Run smoke tests on a schedule (e.g., nightly builds)
3. **Matrix Testing:** Test across multiple Node.js versions or browsers
4. **Custom Reporters:** Create custom test report formats
5. **Integration with Other Tools:** Integrate with Slack, JIRA, or test management tools
6. **Performance Monitoring:** Add performance testing to your CI/CD pipeline
7. **Code Coverage:** Integrate code coverage reporting
8. **Advanced Caching:** Implement sophisticated caching strategies

---

Good luck with your CI/CD automation assignment! Remember, the goal is to create reliable, maintainable workflows that improve your development process. 🚀
