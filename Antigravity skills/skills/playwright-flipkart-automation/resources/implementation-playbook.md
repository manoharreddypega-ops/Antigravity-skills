# Playwright Flipkart Automation Implementation Playbook

This playbook provides a clean, clear roadmap and code templates for building a professional Playwright framework for Flipkart.

## 📂 Framework Structure (Best Practice)

```text
playwright-flipkart-framework/
├── tests/                  # Test scripts (.spec.ts)
├── pages/                  # Page Object Classes
├── utils/                  # Shared helper functions
├── playwright.config.ts    # Main configuration
├── .env                    # Environment variables
└── package.json
```

## 🏗️ 1. Page Object Model (POM) Template

### `pages/BasePage.ts`
```typescript
import { Page } from '@playwright/test';

export class BasePage {
    readonly page: Page;

    constructor(page: Page) {
        this.page = page;
    }

    async navigate(path: string = 'https://www.flipkart.com') {
        await this.page.goto(path);
    }
}
```

### `pages/HomePage.ts`
```typescript
import { Page, Locator } from '@playwright/test';
import { BasePage } from './BasePage';

export class HomePage extends BasePage {
    readonly searchBox: Locator;
    readonly closeLoginBtn: Locator;

    constructor(page: Page) {
        super(page);
        this.searchBox = page.getByPlaceholder('Search for Products, Brands and More');
        this.closeLoginBtn = page.locator('span:has-text("✕"), button._2doB4z');
    }

    async handlePopups() {
        try {
            if (await this.closeLoginBtn.isVisible({ timeout: 5000 })) {
                await this.closeLoginBtn.click();
            }
        } catch (e) {
            console.log('Login popup did not appear');
        }
    }

    async searchForProduct(product: string) {
        await this.searchBox.fill(product);
        await this.searchBox.press('Enter');
        await this.page.waitForLoadState('networkidle');
    }
}
```

## 🧪 2. Clean Test Script Template

### `tests/search.spec.ts`
```typescript
import { test, expect } from '@playwright/test';
import { HomePage } from '../pages/HomePage';

test.describe('Flipkart Search Workflow', () => {
    test('should search for a laptop and verify results', async ({ page }) => {
        const homePage = new HomePage(page);

        await homePage.navigate();
        await homePage.handlePopups();
        await homePage.searchForProduct('laptop');

        // Verify that products are visible
        const productList = page.locator('div._1AtVbE');
        await expect(productList.first()).toBeVisible();
        
        const productsCount = await productList.count();
        console.log(`Found ${productsCount} product items on page.`);
    });
});
```

## 🛠️ 3. Advanced Patterns

### Handling Dynamic Dynamic Selectors
Flipkart often hides classes behind obfuscation. Use **User-Facing Locators**:
- ❌ Avoid: `page.locator('._4rR01T')`
- ✅ Use: `page.locator('div[title="..."]')` or `page.getByText('Apple iPhone')`

### Anti-Bot Configuration
In `playwright.config.ts`, use realistic user agents:
```typescript
use: {
    userAgent: 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) ...',
    viewport: { width: 1280, height: 720 },
}
```

## 🚀 4. Execution Commands

- **Run all tests**: `npx playwright test`
- **Run in UI mode**: `npx playwright test --ui`
- **Debug specific test**: `npx playwright test tests/search.spec.ts --debug`

---
## 💡 Pro Tips for Flipkart
1. **Network Idle**: Flipkart is heavy on XHR. `waitForLoadState('networkidle')` is your friend after search.
2. **Cookies**: Use `context.storageState()` to save login state across sessions to avoid repetitive login hurdles.
3. **Responsive Testing**: Flipkart adapts significantly to mobile. Test both `Desktop Chrome` and `iPhone 13` projects.
