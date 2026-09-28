### **User Story: Add Training Notification Checkbox & Email Automation on Support Case**
### **Description**

**As a** Client Services Representative (**uLab Client Services** profile),

**I want to** trigger an automated notification to the Training team directly from a Support Case,

**So that** I can seamlessly route case details to `training@ulabsystems.com` without manually copying and pasting information into an external email.

---

### **Acceptance Criteria**

#### **1. Field Creation & Page Layout**

* [ ] A new checkbox field **`Training Notification`** (`Training_Notification__c`) is created on the **Case** object.
* [ ] The **`Training Notification`** checkbox is added to the Support Case layout, placed adjacent to (above, below, or alongside) the existing **POD Notification** checkbox under the **Additional Information** section.
* [ ] Default value for the checkbox is set to `Unchecked` (`False`).

#### **2. Email Automation (Flow / Email Alert)**

* [ ] When **`Training Notification`** is set to `True`, an automated email is triggered immediately to **`training@ulabsystems.com`**.
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



#### **3. Security & Access Control**

* [ ] Field-Level Security (FLS) allows read/write access to users with the **`uLab Client Services`** profile (and System Administrators).
* [ ] Read-only or hidden access is applied to other profiles to prevent unauthorized triggering.

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