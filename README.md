# GHL Auto Contact Sync + Team Notification - n8n


### **Goal:**

Automatically add or update contacts in GoHighLevel (GHL) based on outreach results, upload relevant files to Google Drive, and notify the internal team via Slack.

### **Problem:**

Manually managing contact updates in GHL after outreach campaigns was time-consuming and error-prone. There was no streamlined system to sync contacts, upload data, and keep the team in the loop.

### **Solution:**

An automated n8n workflow that:

- Detects whether a contact exists in GHL.
- Adds new contacts or updates existing ones.
- Uploads related outreach files to Google Drive.
- Sends Slack notifications to the internal team with relevant status updates.

---

### 🔹 Step 1:

**Webhook**

Entry point that triggers the automation upon receiving a new outreach request via HTTP.

### 🔹 Step 2:

**Check Website URL Exists**

Verifies if the input includes a valid website URL to proceed.

### 🔹 Step 3:

**Fetch Website HTML**

Retrieves the raw HTML content of the website for further parsing.

### 🔹 Step 4:

**HTML to JSON (HTML Extractor)**

Converts the HTML code into structured data format.

### 🔹  **Step 5:**

**Normalize Lead Data**

Cleans and formats the lead's data (e.g., removing unwanted characters, standardizing casing).

### 🔹 Step 6:

**Extract Root Domain**

Parses and extracts the root domain.

### 🔹 Step 7:

**Split Webpage Links**

Extracts all hyperlinks.

### 🔹 Step 8:

**Filter Internal Links**

Filters out only the internal links that belong to the same root domain.

### 🔹 Step 9:

**Remove Duplicated URLs**

Removes duplicate URLs from the internal link list.

### 🔹  **Step 10:**

**Check Valid URL**

Checks if each internal URL is reachable.

### 🔹 Step 11:

**Exclude Media File Extensions**

Filters out non-HTML resources.

### 🔹 Step 12:

**Request Valid Webpages**

Sends HTTP GET requests to the valid internal URLs to retrieve their content.

### 🔹 Step 13:

**Combine Page Contents**

Merges all retrieved webpage contents into a single text blob for AI input.

### 🔹 Step 14:

**Convert HTML to Markdown**

Converts the merged HTML content into readable Markdown for GPT prompt clarity.

### 🔹 Step 15:

**Generate Outreach Sequence (GPT)**

Uses OpenAI to generate a custom outreach sequence based on website content and business profile.

### 🔹 Step 16:

**Clean & Format Outreach**

Parses and structures the GPT output to prepare it for team notification or CRM sync.

### 🔹 Step 17:

**Switch: Add vs. Update in GHL**

Conditional logic to determine whether the contact should be added as new or updated in GoHighLevel.

### 🔹 Step 18:

**GHL – Add Contact**

Sends a POST request to add the contact to the GoHighLevel CRM.

### 🔹 Step 19:

**Upload File (Drive)**

Uploads GPT-generated outreach file or lead asset to Google Drive.

### 🔹 Step 20:

**Send Slack Message (New Contact)**

Notifies internal team via Slack about new contact creation and file upload.

### 🔹 Step 21:

**Edit GHL Contact**

Sends a request to update the contact in GHL if already present.

### 🔹 Step 22:

**Send Slack Message (Existing Contact)**

Notifies internal team that an existing contact was updated, not newly created.

---

### **Tools Used:**

- **n8n**
- **GoHighLevel API**
- **Google Drive API**
- **Slack API**
- **Open AI API**

### **Impact:**

- Eliminated manual updates in GHL.
- Saved internal team hours per week.
- Increased outreach data accuracy and visibility.
- Improved internal coordination with real-time Slack updates.

### **🧠Learnings:**

- Using switch nodes is ideal for branching logic based on contact status.
- GHL’s API requires careful handling of `contactId` to avoid duplication.
- Integrating Slack alerts ensures instant communication between ops and sales.

