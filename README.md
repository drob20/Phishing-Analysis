# Phishing-Analysis# 

## 📘 Overview
While going through the **TCM SOC101** course, there’s a section on phishing analysis that uses various methodologies and tools to evaluate suspicious emails.  
For hands-on practice, I analyzed several potential phishing attempts found in my student email. One message in particular appeared to be a **phishing attempt** targeting financial aid information.

<img width="973" height="575" alt="image" src="https://github.com/user-attachments/assets/48ee6ccd-13fc-4a9b-ad8f-997870ff6648" />

---

## 📩 Email Indicators of Concern
1. **Urgency**  
   The email emphasizes a *24-hour timeframe* to resolve account issues for disbursing funds — a common tactic to pressure recipients into acting quickly.

2. **Improper Spelling**  
   The institution’s name, **“SAINTLEO”**, is written as one word instead of **“Saint Leo.”**

3. **Suspicious Links**
   - **Displayed Link:**  
     `www[.]vibeaccount[.]com/financialaid-management`
   - **Hover Redirect:**  
     `hxxps://8hs6rx18[.]forms[.]app/untitled-form`

4. **Unprofessional Sender Details**
   - The sender used a *Gmail address* within a subdomain of Saint Leo, rather than an official domain.
   - Signature included unusual formatting:  
     > `. FINANCIAL AID DEPARTMENT Manager, BankMobile Agency BankMobile Program (RSVP).`

---

## 🧾 Plain-Text View Analysis
Switching the message to **plain text** revealed further obfuscation techniques:

- The visible link  
  `www[.]vibeaccount[.]com/financialaid-management`  
  actually redirects to  
  `hxxps://8hs6rx18[.]forms[.]app/untitled-form`,  
  confirming possible phishing behavior.

---

## 🧱 Header Analysis
Using **Sublime Text** to review the raw email headers revealed:

- **Header of Concern:**  
  `X-MS-Exchange-Organization-AuthMechanism: 04`  
  → Indicates Exchange antispam flagged the message as potentially malicious.

---

## 🧩 DMARC, SPF, and DKIM Checks
Tools Used: **MXToolBox**

| Check | Result | Notes |
|--------|---------|-------|
| **DMARC** | ❌ Failed | No record for the subdomain |
| **SPF** | ❌ Missing | No SPF record found |
| **DKIM** | ❌ Missing | No DKIM signature |

**MXToolBox Output Summary:**
> No DMARC Record found for sub-domain.  
> Organization Domain of this sub-domain is: `saintleo.edu`  
> Inbox receivers will apply `saintleo.edu` DMARC record to mail sent from `email.saintleo.edu`.  
> SP Tag '' found: Inbox Receivers will treat all mail sent from `email.saintleo.edu` that fails DMARC as suspicious.  
> No SPF record was found, and no DKIM signature header was found.

---

## 🌐 URL and Domain Investigation
1. **Whois Lookup**  
   - `hxxps://8hs6rx18[.]forms[.]app/untitled-form`  
     → Registered via **GoDaddy**  
     → Hosted on a **Cloudflare** server

2. **VirusTotal Scan**  
   - One vendor **flagged the URL as malicious**  
   - HTML analysis revealed a form titled:  
     > “SAINTLEO UNIVERSITY | forms.app”  
     confirming **phishing intent**

---

## 🧪 Sandbox Analysis
The suspect URL was executed in a controlled sandbox environment.  
**Result:** The form was designed to **capture user credentials**, indicating a credential-harvesting campaign targeting students.
<img width="975" height="492" alt="image" src="https://github.com/user-attachments/assets/1f3a8fe2-9770-4722-995e-6f9860aaef7d" />
<img width="975" height="492" alt="image" src="https://github.com/user-attachments/assets/293a6aa1-7bd6-47af-a36b-5902402a60e8" />
<img width="975" height="492" alt="image" src="https://github.com/user-attachments/assets/81e16248-7e0c-4b8a-b988-f6514ab9999c" />

---

## ✅ Conclusion & Classification
This email is classified as a **phishing attempt** based on:

1. **Sense of Urgency** – Forces rapid action with a 24-hour threat.  
2. **Impersonation** – Mimics an official sender using fake domains and inconsistent branding.  
3. **Redirection Links** – Conceals malicious URLs behind legitimate-looking text.  
4. **Credential Harvesting** – Collects sensitive data via fraudulent forms.

> **Classification:** 🟥 *Phishing – Credential Harvesting*  
> **Impact Scope:** Student Accounts / Financial Credentials  
> **Confidence:** High

---

## 🧠 Lessons Learned
- Always verify sender domains and grammar inconsistencies.  
- Hover over links before clicking; check the redirect path.  
- Use **DMARC/SPF/DKIM** validation tools for legitimacy checks.  
- Report suspected phishing emails to the institution’s **IT Security** or **SOC team** immediately.

---

## 📎 Indicators of Compromise (IOCs)
| Type | Indicator |
|------|------------|
| URL | `hxxps://8hs6rx18[.]forms[.]app/untitled-form` |
| Displayed Link | `www[.]vibeaccount[.]com/financialaid-management` |
| Domain | `forms[.]app` |
| Email Subdomain | `email.saintleo[.]edu` |

---


### 🗂️ File Metadata
