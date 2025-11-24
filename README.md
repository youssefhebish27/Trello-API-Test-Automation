# Trello API Test Automation 📋

This repository contains a comprehensive Postman test collection for the [Trello REST API](https://developer.atlassian.com/cloud/trello/rest/). This project demonstrates an **End-to-End (E2E)** testing scenario simulating a complete user journey for managing Boards, Lists, Cards, and Checklists.

## 🛠️ Tools & Technologies
* **Postman:** For API request creation, execution, and automation.
* **JavaScript (Postman Sandbox):** For writing complex test scripts and logic.
* **Collection Runner:** For executing the full regression suite.

## 📑 Test Planning
Before automation, a detailed Test Execution Schedule was created to define dependencies and data flow based on the technical requirements.
* 📄 **[View the Test Execution Plan](Test_Execution_Plan.xlsx)**

## 🧪 Key Features & Skills Demonstrated

### 1. Advanced Request Chaining (Workflow)
* **Dynamic Data Handling:** The collection automatically captures IDs (Board, List, Card, Checklist) from responses and stores them in **Collection Variables** to be used in subsequent requests.
* **Full Hierarchy Testing:**
    * **Board:** Create -> Get -> Update -> Delete -> Verify Deletion.
    * **List:** Create -> Get -> Update -> Archive -> Verify Archive -> Unarchive.
    * **Card:** Create -> Get -> Update -> Delete.
    * **Checklist:** Create -> Get -> Update -> Delete.

### 2. Advanced Scripting & Validation
* **Dynamic Assertions:** Tests compare response data against stored variables (e.g., checking if the returned name matches the *updated* name stored in the previous step) rather than static hardcoded values.
* **Data Integrity Checks:** Verifying relationships between objects (e.g., ensuring a Card is created within the correct List and Board).
* **Decoding Parameters:** Handling URL encoding issues (e.g., `%20`) using `decodeURIComponent` to ensure accurate string comparison.
* **Negative Testing:** Verifying successful deletion by asserting `404 Not Found` on subsequent GET requests.
* **Performance Testing:** A collection-level script ensures acceptable response times (< 2000ms) for all requests.

### 3. Authentication Handling
* **Secure Variable Use:** API Key and Token are managed via Collection Variables (not hardcoded in URLs), demonstrating security best practices.
* **Pre-request Scripts:** Automatically appending authentication parameters to requests to keep the URLs clean and secure.

## 📂 Test Scenario Flow

The collection follows a logical execution order based on Trello's data hierarchy:

1.  **Setup:** Create a new Board (Clean slate with `defaultLists:false`).
2.  **Build Phase:**
    * Create a List on the Board.
    * Create a Card in the List.
    * Create a Checklist on the Card.
3.  **Verification Phase:** Verify all created entities via GET requests using stored IDs.
4.  **Update Phase:**
    * Update Board, List, Card, and Checklist details.
    * Verify updates reflect correctly on the server.
5.  **Logic Test Phase:** Test List Archiving logic (Archive -> Verify -> Unarchive).
6.  **Teardown Phase (Cleanup):**
    * Delete Checklist -> Verify Deletion.
    * Delete Card -> Verify Deletion.
    * Delete Board -> Verify Deletion.

## 🚀 How to Run

1.  **Clone** this repository.
2.  **Import** the `Trello Project.postman_collection.json` file into Postman.
3.  **Configure Variables:**
    * Select the collection and go to the **Variables** tab.
    * Set `base_url` to `https://api.trello.com/1`.
    * Add your Trello `key` and `token` in the **Current Value** column.
4.  **Run** using the Collection Runner to see the full E2E flow.

---
*This project serves as a proof of concept for advanced API automation skills.*
