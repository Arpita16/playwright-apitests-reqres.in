# playwright-apitests-reqres.in

***This project includes API testing of https://reqres.in/***

1.Use /api/login for successful and unsuccessful login

2.Validate /api/users/2 endpoint returns details of a specific user.

3.Verify /api/users endpoint by creating a user by sending a POST request with name and job fields.

4.Validate pagination handling and the integrity of data across pages using /api/users?page=2

5.Chained requests for user list and specific user

6.Validate pagination and user consistency across pages using /api/users?page=1 and /api/users?page=2


📦 playwrightautomationtests-ui-api
            ┣ 📂 tests
            ┃ ┣ 📂 api-testcases
            ┃ ┣ ┣📜 TS01-reqreslogin.spec.ts
            ┃ ┣ ┣📜 TS02-validateuserdata.spec.ts
            ┃ ┣ ┣📜 TS03-reqrescreateuser.spec.ts
            ┃ ┣ ┣📜 TS04-getuserdata.spec.ts
            ┃ ┣ ┣📜 TS05-validateuserid.spec.ts
            ┃ ┣ ┣📜 TS06-validateuniquelistusers.spec.ts


### 📌  API Test Scripts
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
