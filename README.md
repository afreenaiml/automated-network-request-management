# Automated Network Request Management in ServiceNow

## 📌 Project Overview

**Automated Network Request Management** is a ServiceNow application designed to automate the end-to-end lifecycle of network service requests.

The application allows users to submit network requests through the Service Catalog, automatically creates and tracks network request records, routes requests for approval, creates fulfillment tasks for the Network Team, and sends email notifications to the requester throughout the fulfillment process.

The project was developed as a **Scoped ServiceNow Application** using ServiceNow Studio and integrated with GitHub using ServiceNow Source Control.

---

## 🎯 Problem Statement

Manual network service request processes can involve multiple steps such as request submission, approval, assignment, fulfillment, and communication with the requester.

This project automates these activities to provide:

* Structured request submission
* Automated approval handling
* Automatic fulfillment task creation
* Role-based access
* Requester notifications
* Centralized request and fulfillment tracking
* Better auditability of network requests

---

## 🚀 Key Features

### 1. Network Request Catalog Item

Users can submit network requests through the Service Catalog.

The request form includes:

* Request Details
* Type of Connection

  * New
  * Existing
* Existing Connection ID
* Total Amount
* Mode of Payment

  * UPI
  * CARD
* Address
* Opened on behalf of
* Automatically populated user information

### 2. Dynamic Catalog Form

A Catalog UI Policy dynamically controls the **Existing ID** field.

* For a **New** connection → Existing ID remains hidden.
* For an **Existing** connection → Existing ID becomes visible and mandatory.

### 3. Automated Request Creation

Once a request is submitted, Flow Designer automatically:

1. Retrieves catalog variables.
2. Creates a Network Database record.
3. Stores the submitted request information.
4. Sets the initial approval status to **Requested**.
5. Sends a confirmation email to the requester.
6. Sends the request for approval.

### 4. Approval Automation

Requests are routed to the **Network Approvers** group.

Approvers can:

* Approve the request
* Reject the request

Based on the approval result, the Flow Designer automation follows the corresponding branch.

### 5. Fulfillment Task Automation

When a request is approved:

* The Network Database record is updated to **Approved**.
* The request is assigned to the Network Engineer.
* A **Network Fulfillment Task** is automatically created.

The fulfillment task contains:

* Fulfillment Task Number
* Network Request
* Assigned To
* Short Description
* State
* Work Notes
* Completion Notes

### 6. Fulfillment Lifecycle

Network engineers can update the fulfillment task through different states:

* Open
* Work in Progress
* Completed
* Cancelled

### 7. Email Notifications

The application sends notifications to the requester during important stages of fulfillment.

Notifications include:

* Request submitted
* Request in progress
* Request completed
* Request cancelled

### 8. Role-Based Security

Custom application roles were created for different responsibilities:

| Role      | Responsibility                     |
| --------- | ---------------------------------- |
| Requester | Submit and view network requests   |
| Approver  | Review and approve/reject requests |
| Engineer  | Work on fulfillment tasks          |
| Admin     | Application administration         |

ACLs are configured for the Network Database and Network Fulfillment Task tables.

---

## 🔄 Application Workflow

```text
Requester
   │
   ▼
Submit Network Request
   │
   ▼
Service Catalog
   │
   ▼
Get Catalog Variables
   │
   ▼
Create Network Database Record
   │
   ▼
Send Submission Notification
   │
   ▼
Approval
   │
   ├─────────────── Rejected
   │                    │
   │                    ▼
   │             Update Request
   │
   ▼
Approved
   │
   ▼
Assign Network Engineer
   │
   ▼
Create Fulfillment Task
   │
   ▼
Network Engineer
   │
   ├── Work in Progress
   │
   ├── Completed
   │
   └── Cancelled
          │
          ▼
Requester Notification
```

---

## 🛠️ ServiceNow Technologies Used

* ServiceNow Studio
* Scoped Application Development
* Service Catalog
* Catalog Items
* Catalog Variables
* Variable Sets
* Catalog UI Policies
* Flow Designer
* Service Catalog Trigger
* Get Catalog Variables
* Create Record
* Update Record
* Ask for Approval
* Send Email
* Conditional Flow Logic
* Custom Tables
* Reference Fields
* Choice Fields
* ACLs
* Custom Roles
* Groups
* Application Menu
* ServiceNow Source Control
* GitHub Integration

---

## 🗄️ Main Tables

### Network Database

Stores the submitted network request information.

Important fields include:

* Database Number
* Requested For
* Assignment to
* Mobile Number
* Type of Connection
* Customer Address
* Total Amount
* Mode of Payment
* Existing ID
* Request Details
* Approval Status

### Network Fulfillment Task

Stores the work that needs to be performed by the Network Team.

Important fields include:

* Fulfillment Task Number
* Network Request
* Assigned To
* Short Description
* State
* Work Notes
* Completion Notes

---

## 👥 User Groups

The application uses three functional groups:

### Network Requesters

Responsible for submitting network requests.

### Network Approvers

Responsible for reviewing and approving or rejecting requests.

### Network Team

Responsible for fulfilling approved network requests.

---

## 🔐 Security

The application implements role-based access control using ServiceNow ACLs.

Access is separated according to application responsibilities so that users do not receive unnecessary permissions.

The application contains custom roles for:

* Requesters
* Approvers
* Engineers
* Administrators

---

## ⚙️ Automation Flows

### Network Request Automation

Handles the main request lifecycle:

```text
Catalog Submission
       ↓
Get Catalog Variables
       ↓
Create Network Database Record
       ↓
Send Confirmation Email
       ↓
Ask for Approval
       ↓
Approved / Rejected
       ↓
Create Fulfillment Task
```

### Network Fulfillment Task Notifications

Monitors fulfillment task updates and sends requester notifications when the task moves into:

* Work in Progress
* Completed
* Cancelled

---

## 🧪 Testing

The application was tested using different application roles and scenarios.

### Requester Testing

* Submitted Network Request
* Verified catalog form behavior
* Verified automatic request creation
* Verified requester notification

### Approver Testing

* Received approval request
* Approved/rejected network request
* Verified approval result

### Engineer Testing

* Verified fulfillment task creation
* Verified assignment to Network Engineer
* Updated fulfillment task state
* Added work information

### Notification Testing

Requester notifications were tested for different fulfillment states.

### End-to-End Testing

The complete workflow was tested:

```text
Requester Submission
        ↓
Network Database Record
        ↓
Approval
        ↓
Fulfillment Task
        ↓
Engineer Update
        ↓
Requester Notification
```

---

## 🎥 Project Demo

A complete demonstration of the application is available here:

**Demo Video:**
https://drive.google.com/file/d/1-dFxkK_KNGUxj1idOT_5Af2uDDsc6MzK/view?usp=sharing

The demonstration covers:

1. Network request submission
2. Dynamic catalog behavior
3. Automatic request creation
4. Approval process
5. Automatic fulfillment task creation
6. Engineer fulfillment
7. Requester email notifications

---


## 📂 Project Structure

The ServiceNow application is maintained using ServiceNow Source Control and GitHub.

```text
automated-network-request-management/
│
├── dictionary/
├── update/
├── author_elective_update/
├── checksum.txt
└── README.md
```

ServiceNow application configuration is maintained through the source-controlled application files.

---

## 🔗 Source Control

This project uses **GitHub** for version control through ServiceNow Source Control.

Development workflow:

```text
ServiceNow Development
        ↓
Testing
        ↓
Commit Changes
        ↓
ServiceNow Source Control
        ↓
GitHub
```

---

## 📈 Future Enhancements

Possible future improvements include:

* SLA tracking
* Advanced reporting and dashboards
* Additional notification templates
* More detailed fulfillment tracking
* Integration with external network management systems

These enhancements are outside the current core implementation.

---

## 👨‍💻 Author

**Afreen Hasen Shaik**

ServiceNow Developer | Python & DSA Learner

---

## 📜 Project Status

**Completed**

The core Network Request → Approval → Fulfillment → Notification workflow has been implemented, secured with role-based access, tested with different application roles, and committed to GitHub.
