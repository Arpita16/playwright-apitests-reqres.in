# playwright-apitests-reqres.in

## 📌 Overview

***This project includes API testing of https://reqres.in/***

1.Use /api/login for successful and unsuccessful login

2.Validate /api/users/2 endpoint returns details of a specific user.

3.Verify /api/users endpoint by creating a user by sending a POST request with name and job fields.

4.Validate pagination handling and the integrity of data across pages using /api/users?page=2

5.Chained requests for user list and specific user

6.Validate pagination and user consistency across pages using /api/users?page=1 and /api/users?page=2

## 🛠️ Tech Stack

- Playwright 🕵️‍♂️ (End-to-end testing)

- TypeScript ⌨️ (Strongly typed JavaScript)

- Test Runner 🧪 (Test execution)

## 📂 Project Structure
           
     📦 playwrightautomationtests-ui-api
            ┣ 📂 tests
            ┃ ┣ 📂 api-testcases
            ┃ ┣ ┣📜 TS01-reqreslogin.spec.ts
            ┃ ┣ ┣📜 TS02-validateuserdata.spec.ts
            ┃ ┣ ┣📜 TS03-reqrescreateuser.spec.ts
            ┃ ┣ ┣📜 TS04-getuserdata.spec.ts
            ┃ ┣ ┣📜 TS05-validateuserid.spec.ts
            ┃ ┣ ┣📜 TS06-validateuniquelistusers.spec.ts


### 🚀 Installation & Setup

1.Clone the repository

              git clone https://github.com/Arpita16/playwright-apitests-reqres.in.git
              cd playwright-apitests-reqres.in

2.Install dependencies

              npx playwright install
              
3.Install Playwright browsers

              npx playwright install
              
4.Verify Playwright Installtion

            npx playwright doctor


🧪 Writing Tests

Tests are written using Playwright Test Runner.

  **Example** :tests/api-testcases/reqreslogin.spec.ts

               const validateResponse = async (response: APIResponse, expectedStatus: number, expectedBodyKeys: string[] = []) => {
               expect(response.status()).toBe(expectedStatus);
               expect(response.headers()['content-type']).toContain('application/json');
               const body = await response.json();
              for (const key of expectedBodyKeys) {
                   expect(body).toHaveProperty(key);
                }
              return body;
             };

                test(' Successful login with valid credentials', async () => {
                         const response = await apiContext.post(BASE_URL, {
                         data: { email: 'eve.holt@reqres.in', password: 'cityslicka' },
                      });

              const body = await validateResponse(response, 200, ['token']);
              console.log(' Login token:', body.token);
              expect(body).toHaveProperty('token');
              expect(typeof body.token).toBe('string');
              });


### 🛠 Running Tests

Run tests only in Chromium through CLI

      npx playwright test --project=chromium
      
Run tests in headed mode (with UI)

         npx playwright test --headed
         
Run tests with a specific file
             
             npx playwright test tests/api-testcases/TS01-reqreslogin.spec.ts
   
### 📊 Test Reporting

The framework generates an HTML report in ***playwright-report/***.

Run the following command to view reports:

         npx playwright show-report
         
### 🛡️ CI/CD Integration

You can integrate Playwright with GitHub Actions in adding ***.github/workflows/playwright.yml***.

***Example CI/CD workflow:***

       name: Playwright Tests
       on: [push, pull_request]
       jobs:
          test:
             runs-on: ubuntu-latest
             steps:
                  - name: Checkout Repository
                    uses: actions/checkout@v3
                  - name: Install Dependencies
                    run: npm install
                  - name: Install Playwright Browsers
                    run: npx playwright install
                  - name: Run Tests
                    run: npx playwright test
                    
### 📌 Additional Playwright Commands

Debug tests

     npx playwright test --debug
  
Run tests in different browsers

     npx playwright test --browser=firefox
