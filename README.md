# Phishing Email Analysis: Amazon Account Scam with PDF Attachment

## Project Overview

This project presents an in-depth analysis of a phishing email impersonating Amazon Customer Support. The email creates a false sense of urgency by claiming the recipient's account will be suspended unless immediate action is taken. It contains a malicious PDF attachment encouraging users to click a link and verify their credentials. The analysis uncovers attacker techniques such as spoofed sender details, psychological manipulation, and deceptive attachments, while demonstrating how to identify threats through header inspection, content analysis, and detection techniques like YARA rules. This report highlights the importance of phishing awareness and email security hygiene.

---

| **Attribute**           | **Details**                                                                                                                                                                 |
| ----------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Subject**             | `[Important] Unauthorized access; Your A̿m̿a̿z̿o̿n account has been locked`<br>— Crafted to induce panic and create urgency.                                                   |
| **From Address**        | `cs-noreplygrusakgrusuk0384911323@arulnotes.com`<br>— Spoofed to resemble official Amazon support but uses suspicious domain.                                              |
| **Sender Domain**       | `arulnotes.com`<br>— Not associated with Amazon; indicates domain impersonation or abuse of a compromised third-party domain.                                               |
| **Origin IP Address**   | `209.85.221.193`<br>— Belongs to Google infrastructure; possibly abused or hijacked email service.                                                                          |
| **Email Body**          | **Empty.** The email does not contain a written message — all content is hidden inside the PDF attachment.                                                                    |
| **Attachment**          | **PDF File** mimicking Amazon branding with a **“Verify Now”** button linked to a suspicious external redirect.                                                             |
| **Malicious Link**      | The button redirects first to a **LinkedIn URL**, likely as a redirection tactic to bypass security filters before leading to a phishing or credential harvesting site.       |
| **Observed Techniques** | - Impersonation & Spoofing<br>- Urgency Creation<br>- Use of Attachment to Avoid Detection<br>- Redirects via Reputable Sites (LinkedIn)                                    |
| **Phishing Indicators** | - Generic or no greeting<br>- Spoofed domain<br>- Urgent subject line<br>- Mismatched link destination<br>- No message body<br>- Attachment embeds phishing content          |


- Screenshot of the result:

 1. <br><img width="740" height="595" alt="Screenshot 2025-08-05 162040" src="https://github.com/user-attachments/assets/3bbb4308-a4e3-4caf-8e70-34ed2995565d" />
---

 2. <br> <img width="610" height="666" alt="Screenshot 2025-08-05 161526" src="https://github.com/user-attachments/assets/7342c1e8-2c0f-4ce2-98ac-2fd8edce850a" />

---

  3. after hovering over the button <br><img width="616" height="686" alt="image" src="https://github.com/user-attachments/assets/a100ca49-c5ad-4579-b61a-1f26cbdedce5" />

---

  4.  <br><img width="1610" height="619" alt="Screenshot 2025-08-05 162611" src="https://github.com/user-attachments/assets/6f710261-2c41-48cd-b553-6b88f8502a58" />

---
 5.  <br><img width="1362" height="731" alt="image" src="https://github.com/user-attachments/assets/71413f68-970d-4b3e-a725-7eacf4ad705b" />

---

## Detailed Explanation

- **Spoofed Identity:** Sender email uses a domain unrelated to Amazon, exposing lack of legitimacy.  
- **Urgency in Language:** Subject line prompts quick action by claiming unauthorized access and account lock.  
- **PDF-Based Attack Vector:** Attachment hides phishing content from text-based email scanners.  
- **Legitimate-Looking Redirects:** The PDF’s link initially goes to LinkedIn, a tactic to evade filters, before likely redirecting to a phishing site.  
- **Grammar Issues:** Example phrase “Your Amazon account where placed on hold” is incorrect and suspicious.it should be like "your Amazon account was placed on hold"

---

## Tools Used for Analysis

- **Thunderbird:** Email client used to open and inspect the phishing email and attachment safely.  
- **MxToolbox:** Online tool for checking email headers, SPF, DKIM, DMARC records, and blacklist status.  
- **AbuseIPDB:** Service used to check the reputation and blacklist status of the origin IP address.  
- **PDF Reader:** To safely examine the content of the PDF attachment.  
- **Controlled web environment:** To verify suspicious links without risk.


---

## Email Authentication & Relay Analysis

- **DMARC:** No DMARC record found for the sending domain, meaning no policy to prevent spoofing is implemented.  
- **SPF:** Passed authentication, confirming sending server IP is authorized.  
- **SPF Alignment Issue:** SPF domain does not align with the "From" domain, reducing trust.  
- **DKIM:** Passed verification, confirming message integrity.  
- **DKIM Alignment Issue:** Signing domain differs from "From" domain, lowering legitimacy.  
- **Blacklist Status:** One relay server involved is listed on a spam blacklist, increasing suspicion.  
- **Relay Path & Delay:** Email passed through Google and Microsoft servers with typical 3-second delivery delay.

---

## Attachment Behavior

The attached PDF mimics an Amazon alert and urges verification via a **“Verify Now”** button.

- The button’s link redirects first to LinkedIn, likely to exploit trusted domains for obfuscation.  
- This tactic helps attackers bypass security filters and hide phishing URLs.

---

## Phishing Indicators Summary

| Indicator                 | Details                                                       |
|---------------------------|---------------------------------------------------------------|
| Fake Display Name         | “Amazon Service” from non-Amazon domain                      |
| Obfuscated Subject       | Unicode characters used to evade filters                      |
| Suspicious Attachment    | PDF used instead of inline email content                      |
| Urgency & Threat         | Account lock threat within 24 hours                           |
| Redirect Behavior        | Link leads through LinkedIn redirector                        |
| Generic Greeting         | No personalized salutation                                    |

---

## User Recommendations
- Do not open attachments from unknown or suspicious senders.
- Verify sender domains before interacting.
- Inspect embedded links carefully, especially in attachments.
- Use multi-factor authentication on sensitive accounts.
- Report phishing attempts to relevant security teams or service providers.


## Conclusion
This phishing email employs PDF attachments and social engineering to lure victims. Despite passing SPF, DKIM, and DMARC checks technically, lack of alignment and absence of DMARC policy, combined with suspicious redirects and blacklisted relay involvement, clearly indicate malicious intent aiming at credential theft.
