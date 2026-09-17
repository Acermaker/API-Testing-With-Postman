# Automated API Testing Suite: Branch Management Lifecycle

A comprehensive **Postman API testing collection** designed to validate the full CRUD (Create, Read, Update, Delete) workflow of an organizational Branch Management subsystem. This project demonstrates advanced QA capabilities including **end-to-end endpoint chaining, automated authentication tracking, runtime response validation, and performance benchmarking**.

---

## 🛠️ Key Testing Features Covered

* **Automated Session & Token Chaining:** Dynamically captures authentication JSON Web Tokens (JWT) upon login and binds them to collection variables, eliminating manual token copying.
* **State & Environment Persistence:** Automatically updates and sequences slug pathways (`{{slug}}`) between sequential POST, GET, PUT, PATCH, and DELETE operations to preserve workflow integrity.
* **Dynamic Test Data Generation:** Leverages Postman's native faker engines (`{{$randomFirstName}}`, `{{$randomStreetAddress}}`) to model realistic concurrent user payloads.
* **Rigorous Performance & Structure Benchmarking:** Implements strict validation assertions monitoring response latency thresholds (<600ms) and payload weight controls (<5KB).

---

## 📋 API Endpoint Coverage & Scenarios

| Request Name | Method | Endpoint Pathway | Core Validation & Test Assertions |
| :--- | :--- | :--- | :--- |
| **Branch Login** | `POST` | `/api/accounts/login/` | Validates `200 OK`, schema structure, token availability, latency limits (<600ms), and sizes (<5KB). |
| **Branches List** | `GET` | `/api/branch/branches/?limit=8` | Tests data pagination mechanics and authorization headers. |
| **Branch Create** | `POST` | `/api/branch/branches/` | Validates `201 Created` statuses, alphanumeric slug integrity regex, and tracks created resource identifiers. |
| **Branch Slug Read** | `GET` | `/api/branch/branches/{{slug}}/` | Confirms deep-linking validation mapping back to dynamically created resources. |
| **Branch Update** | `PUT` | `/api/branch/branches/{{slug}}/` | Complete replacement modification integrity validation. |
| **Branch Partial Update** | `PATCH`| `/api/branch/branches/{{slug}}/` | Micro-mutation payload adjustments with automatic tracking synchronization updates. |
| **Branch Delete** | `DELETE`| `/api/branch/branches/{{slug}}/` | Lifecycle conclusion scenario verifying total resource destruction. |

---

## 🚀 How to Import and Run This Suite

Recruiters or team engineers can run this collection locally using the following steps:

### Prerequisites
* Install the latest desktop version of [Postman](https://postman.com) or the **Postman CLI / Newman**.

### Running inside Postman GUI
1. Clone or download this repository to your desktop machine.
2. Launch your Postman application.
3. Click the **Import** button in the top left workspace corner.
4. Drag and drop the `Second wave.postman_collection.json` file from your directory.
5. Setup a collection variable or local environment block named `base URL` mapping to your intended target host environments (e.g., `https://chairlyo.com`).
6. Click on the collection context menu `...` and choose **Run Collection** to trigger the automated test runner.

---

## 📊 Sample Postman Assertion Snippet Showcase

This project includes JavaScript verification rules executed automatically on the context client layer after every transaction:

```javascript
// Verification framework snippet utilized on Login validation pipelines
pm.test("Verify status code is 200", function () {
    pm.response.to.have.status(200);
});

pm.test("Verify response time is below 600ms", function () {
    pm.expect(pm.response.responseTime).to.be.below(600); 
});

pm.test("Verify access token is present", function () {
    const responseData = pm.response.json();    
    pm.expect(responseData.access).to.exist; 
});
```
*Connect with me on LinkedIn or review my portfolio for deeper conversations around modern QA engineering paradigms!*
