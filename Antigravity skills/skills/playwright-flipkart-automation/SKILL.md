---
name: playwright-flipkart-automation
description: Expert skill for building robust, clean, and scalable Playwright automation frameworks specifically for E-commerce platforms like Flipkart. Includes Page Object Model (POM) patterns, dynamic wait strategies, and anti-bot bypass techniques.
---

# Playwright Flipkart Automation

Master the art of high-performance web automation for Flipkart using Playwright. This skill focuses on creating modular, maintainable, and resilient test suites that handle dynamic content and complex user flows.

## Use this skill when

- Scaffolding a new Playwright project for Flipkart.com.
- Implementing Page Object Model (POM) for e-commerce workflows.
- Handling dynamic popups, login hurdles, and search interactions.
- Optimizing test execution speed and reliability.
- Mentoring team members on Playwright best practices.

## Do not use this skill when

- Performing manual exploratory testing.
- Automating non-web platforms (e.g., native mobile apps without WebView).
- The task is purely UI/UX design without implementation.

## Instructions

- **Use Page Object Model (POM)**: Segregate locators and actions from test logic.
- **Prefer Locators over Selectors**: Use `page.getByRole()`, `page.getByText()`, and `page.getByPlaceholder()` for stability.
- **Handle Interstitials**: Always account for the login/location popups that appear on Flipkart's landing page.
- **Smart Waiting**: Rely on Playwright's auto-waiting; use `waitForSelector` or `waitForLoadState` only when necessary for hydration.
- **Environment Isolation**: Use `playwright.config.ts` for browser configurations and environment variables.

## Output Format

- **Framework Structure**: Clear directory layout recommendations.
- **Code Snippets**: TypeScript examples for POM and Tests.
- **Best Practices**: Actionable tips for stability and speed.

## Resources

- `resources/implementation-playbook.md` for detailed code templates and advanced patterns.
