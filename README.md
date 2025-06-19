## Xenondev – API Test Automation Project (Postman)
This project demonstrates my hands-on API testing using Postman with the public Reqres API. I tested both valid and invalid cases, added assertions, and reused logic using scripts.

## Project Goal:
- Test public API like real app
- Cover both valid and invalid cases
- Use assertions to check response
- Reuse logic with Postman scripts
- Learn how to structure small API test project

## Tools Used
- Postman (for requests and tests)
- pm.test() (Postman test scripts)
- Pre-request Script (for dynamic login)

## Base URL
https://reqres.in

## Authorization
Some endpoints required an API key so i added this API key:

HEADER:
Key: x-api-key
Value: reqres-free-v1

## API Endpoints Covered
1. POST /api/login
Valid Login returns status 200 and a token

Invalid Login (e.g. missing password) returns 400 and error message

2. GET /api/users?page=2
Checks response code, data array, email format, pagination keys

3. DELETE /api/users/2
Valid: Returns 204 No Content

Edge Case: Deleting non-existent user still returns 204

## Reusable Logic
Used a helper function in Pre-request Script to dynamically generate login payload:


function generateLogin(email, password) {  

  return JSON.stringify({ email, password });  
  
}

## How to Run
Open Postman → Import the collection file
Add x-api-key in header for each request
Run all requests via Collection Runner

