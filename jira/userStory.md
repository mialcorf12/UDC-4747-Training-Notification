### **User Story: Add Training Notification Checkbox, Date Field & Email Automation on Support Case**

### **Description**

**As a** Client Services Representative (**uLab Client Services** profile),

**I want to** trigger an automated notification to the Training team directly from a Support Case and automatically track when the notification was sent,

**So that** I can seamlessly route case details to `training@ulabsystems.com` without manual email drafting and maintain an accurate audit trail of training requests.

---

### **Acceptance Criteria**

#### **1. Fields Creation & Page Layout**

* [ ] A new checkbox field **`Training Notification`** (`Training_Notification__c`) is created on the **Case** object (Default: `Unchecked` / `False`).
* [ ] A new date field **`Training Notification Date`** (`Training_Notification_Date__c`) is created on the **Case** object.
* [ ] Both fields are added to the Support Case page layout under the **Additional Information** section:
* **`Training Notification`** is placed adjacent to (above, below, or alongside) the existing **POD Notification** checkbox.
* **`Training Notification Date`** is placed directly next to the **`Training Notification`** checkbox (mirroring the **POD Notification Date** positioning).



#### **2. Email Automation & Field Update (Salesforce Flow)**

* [ ] When **`Training Notification`** is updated to `True`, an automated Flow executes to:
1. **Send Email Alert:** Send an immediate email to **`training@ulabsystems.com`** containing all relevant case details.
2. **Update Record Field:** Automatically populate **`Training_Notification_Date__c`** with the current date (`$Flow.CurrentDate` / `$Record.LastModifiedDate`).


* [ ] The email includes the following dynamic fields:
* **Company Name** (`{!Case.Account}`)
* **Acct #** (`{!Case.uLab_Acct_Number__c}`)
* **Contact Name** (`{!Case.Contact}`)
* **Subject** (`{!Case.Subject}`)
* **Description** (`{!Case.Description}`)
* **Action Taken** (`{!Case.Action_Taken__c}`)
* **Case Number** (`{!Case.CaseNumber}`)
* **Patient Name** (`{!Case.Patient_Name__c}`)
* **Order Number** (`{!Case.Related_uLab_Order__c}`)
* **Case Link** (`{!Case.Link}`)



#### **3. Security & Access Control (FLS)**

* [ ] Field-Level Security (FLS) for both `Training_Notification__c` and `Training_Notification_Date__c` grants Read/Write access to users with the **`uLab Client Services`** profile and **System Administrators**.
* [ ] Read-only or hidden access is applied to all other profiles.

---

### **Email Template Specification**

**Subject Line:**

`Training Request: Support Case {!Case.CaseNumber} - {!Case.Subject}`

**Body:**

> **Company Name:** {!Case.Account}
> **Acct #:** {!Case.uLab_Acct_Number__c}
> **Contact Name:** {!Case.Contact}
> **Case Number:** {!Case.CaseNumber}
> **Subject:** {!Case.Subject}
> **Description:** {!Case.Description}
> **Action Taken:** {!Case.Action_Taken__c}
> **Patient Name:** {!Case.Patient_Name__c}
> **Order Number:** {!Case.Related_uLab_Order__c}
> **Link to Case:** {!Case.Link}