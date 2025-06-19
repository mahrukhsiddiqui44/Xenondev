                                     Project Title 
                                    MOBILE BANKING APP
                                     **TEST PLAN**  
                                    <18th June, 2025>  

Version: 1.0.0  
Author: Mahrukh Siddiqui  


Version History:  

| Version | Date         | Author             | Comments          |
|---------|--------------|--------------------|-------------------|
| 1.0.0   | 18 June 2025 | Mahrukh Siddiqui   | Initial Draft     |

---

### TABLE OF CONTENTS:

1- Scope of Testing  
2- Test Scenarios & Cases  
3- Edge Case  
4- Validation Points  
5- Suggested Improvement  


### 1- Scope of Testing:

The goal is to test the **“Fund Transfer” flow in a mobile banking app** where one user logs in and transfers money to another.

### 2- Test Scenarios & Cases:

| # | Test Scenario                                               | Expected Result                          |
|---|-------------------------------------------------------------|------------------------------------------|
| 1 | Verify user can login with valid credentials                | User is redirected to dashboard          |
| 2 | Verify transfer screen opens after clicking "Transfer"      | Transfer screen loads with input fields  |
| 3 | Verify transfer with valid account number and amount        | Transaction is successful                |
| 4 | Verify error when account number is missing                 | Error message is shown                   |
| 5 | Verify balance reduces after successful transfer            | Updated balance is shown correctly       |

### 3- Edge Case:

- Transfer very small amount (e.g. 1 rupee)
- Transfer more than available balance (expect error)


### 4- Validation Points:

- Proper **error/success messages** should appear  
- **Balance should update** after transaction  
- UI should be responsive (loading, error highlights)  
- Transaction should follow **limits & rules**


### 5- Suggested Improvement:

Add a **confirmation screen** before final transfer (with “Back” and “Confirm” buttons) to avoid accidental money transfer.


