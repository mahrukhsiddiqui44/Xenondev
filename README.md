# Xenondev – API Test Automation Project (Postman)

This project shows my hands-on understanding of **API testing** using **Postman**. I used the public API [Reqres](https://reqres.in) and wrote complete test coverage including **valid**, **invalid**, and **edge cases**, along with assertions and reusable logic.

## PROJECT GOAL:

- Test public API like real app
- Cover both valid and invalid cases
- Use assertions to check response
- Reuse logic with Postman scripts
- Learn how to structure small API test project

## TOOLS USED:

- **Postman** (for API request, response, assertions)
- **pm.test()** (Postman’s built-in test scripting)
- **Pre-request Script** (for reusable logic)

## 🔗 Base URL:

https://reqres.in


## Authorization:
Although Reqres is mostly public, in my case the API returned:

```json
{
  "error": "Missing API key"
}

So I added an API key to all requests using headers:

- Key: x-api-key
- Value: reqres-free-v1


##  API Endpoints Covered
I tested 3 main endpoints from the Reqres API:

1- POST /api/login – User Login (Valid and Non-valid Login)
2- GET /api/users?page=2 – Get List of Users
3- DELETE /api/users/2 – Delete a User(Existing and Non-existing)

## 1- POST /api/login – User Login (Valid and Non-valid Login)

# VALID LOGIN TEST:
METHOD: POST
REQUEST BODY:
{
  "email": "eve.holt@reqres.in",
  "password": "cityslicka"
}
EXPECTED: Status code: 200 OK
ASSERTION/SCRPTS IN POSTMAN:
pm.test("Status is 200", () => pm.response.to.have.status(200));
pm.test("Token is present", () => {
  let res = pm.response.json();
  pm.expect(res.token).to.be.a("string");
});

# IN-VALID LOGIN TEST:
METHOD: POST
REQUEST BODY:
{
  "email": "eve.holt@reqres.in"
}
EXPECTED: Status code: 400 Bad Request
          Message: "Missing password"

## 2- GET /api/users?page=2 – Get List of Users
Validations performed:
- Status code = 200
- data should be an array
- Pagination fields like page, per_page, etc. should exist
- All emails should contain @reqres.in
- Avatar URLs should start with https://

ASSERTION/SCRPTS IN POSTMAN:
let res = pm.response.json();

pm.test("Status is 200", () => pm.response.to.have.status(200));
pm.test("Data is array", () => pm.expect(res.data).to.be.an("array"));
pm.test("Emails look valid", () => {
  res.data.forEach(user => pm.expect(user.email).to.include("@reqres.in"));
});
pm.test("Pagination exists", () => {
  pm.expect(res).to.have.property("page");
  pm.expect(res).to.have.property("per_page");
  pm.expect(res).to.have.property("total");
  pm.expect(res).to.have.property("total_pages");
});

## 3- DELETE /api/users/2 – Delete a User(Existing and Non-existing)

# VALID CASE:

METHOD: DELETE
EXPECTED: 204 No Content
          No body returned

 # INVALID/EDGE CASE:

 - I also tried deleting a non-existent user /api/users/999
 - API returned 204     

 ASSERTION/SCRPTS IN POSTMAN:

 pm.test("Status is 204", () => pm.response.to.have.status(204));
 

## Reusable Helper Logic:

I added a helper function in Pre-request Script for the login body(ONLY IN VALID-LOGIN CASE):

function generateLogin(email, password) {
  return JSON.stringify({ email, password });
}
pm.environment.set("loginPayload", generateLogin("eve.holt@reqres.in", "cityslicka"));

Then in Body (raw JSON):

{{loginPayload}}


