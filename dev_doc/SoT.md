# FormFlow — Project Source of Truth (SoT)

**Document Type:** Product Requirements, System Architecture & Implementation Blueprint  
**Project Name:** FormFlow  
**Product Category:** Privacy-focused AI-powered form autofill and application management assistant  
**Document Status:** Proposed baseline for implementation  
**Version:** 1.0  
**Primary Audience:** Product owner, software engineers, AI engineers, QA engineers, security reviewers and future contributors

---

# 1. Executive Summary

## 1.1 What is FormFlow?

FormFlow is a privacy-focused, AI-powered form-filling assistant designed to help people complete repetitive online applications without repeatedly entering the same personal, educational, professional and other information.

The application helps users maintain a reusable personal profile, choose the purposes for which they want to use FormFlow, prepare documents and images according to application requirements, automatically fill supported website forms, and track the applications they have worked on or submitted.

FormFlow combines five major capabilities:

1. **Personal Profile Management** — Collect and organize reusable personal information.
2. **AI-Assisted Form Understanding** — Identify the meaning of fields on supported websites.
3. **Smart Autofill** — Match saved profile values to website fields and populate them.
4. **Smart File Preparation** — Convert images into PDFs, resize photos and signatures, compress files, and prepare assets according to application requirements.
5. **Application History** — Maintain a list of applications, their websites, dates and user-confirmed statuses.

The product should reduce repetitive work while keeping users in control of their personal information and final submissions.

## 1.2 Product vision

**Make repetitive online applications easier, faster and more private by allowing users to maintain their information once and reuse it whenever needed.**

## 1.3 Core product principles

- Enter reusable information once and reuse it across supported websites.
- Ask for information based on the user's chosen purposes rather than exposing hundreds of fields at once.
- Use AI to understand ambiguous fields, not to unnecessarily process sensitive personal values.
- Keep personal data under the user's control through an encrypted-vault architecture.
- Preserve original documents and images when preparing alternative versions.
- Automatically prepare compatible files whenever requirements can be determined reliably.
- Show users what FormFlow has filled or prepared.
- Never automatically submit an application without the user's explicit action.
- Never claim a form was successfully submitted without reliable evidence or user confirmation.
- Be transparent when a website or upload workflow cannot be automated.

---

# 2. Problem Statement

People applying for university admission, jobs, scholarships, government services and other opportunities often encounter repetitive forms.

The same information may be requested repeatedly:

- First name and last name
- Email and mobile number
- Date of birth
- Father's name and mother's name
- Present and permanent addresses
- Educational qualifications
- Employment history and skills
- Profile photo and signature
- CVs, transcripts, certificates and other documents

Applicants also face several additional difficulties.

### 2.1 Repetitive data entry

Applicants must manually enter the same information on multiple websites, increasing the time required to complete each application.

### 2.2 Inconsistent field labels

Different websites may ask for the same information using different labels.

Examples:

- `Mobile Number`
- `Phone`
- `Contact Number`
- `Applicant's Mobile`

### 2.3 File preparation difficulties

Applicants may need to:

- Convert JPG or PNG images into PDFs.
- Combine multiple images into one PDF.
- Resize passport photographs.
- Resize signatures.
- Reduce image or PDF file sizes.
- Understand accepted file formats and dimensions.
- Repeatedly prepare different versions of the same file.

### 2.4 Lack of application tracking

Applicants may forget:

- Which opportunities they applied for.
- Which website they used.
- When they started or submitted an application.
- Which applications remain drafts.
- Which applications are awaiting a response.

### 2.5 Privacy concerns

Personal profiles, identification documents, signatures and educational records are sensitive. Users should not have to upload all their information to a centralized database simply to receive autofill assistance.

FormFlow addresses these problems through a reusable profile, privacy-conscious field matching, client-side file preparation and a lightweight application tracker.

---

# 3. Target Users

## 3.1 Primary target users

### A. University and admission applicants

Students applying to universities, colleges, academic programs and entrance examinations.

Typical needs:

- Personal and family information
- Present and permanent addresses
- SSC/HSC or equivalent qualifications
- Roll and registration numbers
- GPA/CGPA and passing years
- University and degree information
- Academic transcripts and certificates
- Passport-style photos and signatures

### B. Job seekers

People applying to multiple companies or positions.

Typical needs:

- Personal and contact information
- Current position and employer
- Employment history
- Skills and certifications
- LinkedIn, GitHub and portfolio links
- CV and cover letter
- Photograph and supporting documents
- Application tracking

## 3.2 Secondary target users

- Scholarship applicants
- Government and official service applicants
- Professional certification candidates
- Visa and immigration applicants, subject to stricter review and compatibility limitations
- Users completing other repetitive online forms

## 3.3 User personas

| Persona | Main problem | Desired outcome |
|---|---|---|
| University applicant | Repeatedly entering academic and personal information | Complete admission forms faster |
| Job seeker | Repeatedly entering career information and uploading CVs | Apply to more positions with less repetitive work |
| Scholarship applicant | Managing personal and academic details across applications | Reuse verified information and supporting files |
| General user | Completing similar registration and application forms | Reduce repetitive typing |
| Privacy-conscious user | Avoiding unnecessary exposure of personal data | Use autofill with local encryption and controlled data sharing |

---

# 4. Product Scope

## 4.1 Included in the product

FormFlow should include:

1. Account registration and authentication.
2. Personal profile creation.
3. Purpose-based profile setup.
4. Profile editing and reusable structured information.
5. Browser extension for supported website forms.
6. DOM-based field discovery and semantic field matching.
7. AI-assisted interpretation of ambiguous fields.
8. Autofill, post-fill verification and review.
9. Secure personal asset management.
10. Image-to-PDF conversion.
11. Multi-image-to-PDF conversion.
12. Automatic photo resizing and preparation.
13. Automatic signature resizing and preparation.
14. File compression and validation.
15. Application history and status tracking.
16. Encrypted local storage and an appropriately designed cross-device synchronization mechanism.
17. Privacy settings, data deletion and recovery workflows.
18. Error handling and user feedback.

## 4.2 Outside the initial scope

The initial product should not attempt to:

- Automatically submit applications without user confirmation.
- Bypass CAPTCHA or other anti-bot protections.
- Bypass website access controls.
- Guarantee compatibility with every website.
- Automatically invent missing personal information.
- Make decisions about whether a user qualifies for an opportunity.
- Sign legal declarations or consent statements on behalf of the user.
- Handle passwords, OTPs or security challenges without explicit user control.
- Guarantee that an external website accepted a file or application merely because FormFlow attempted an action.
- Replace official document verification or government application systems.

---

# 5. Core Product Modules

The product is organized into eight main modules.

| Module | Responsibility |
|---|---|
| Authentication & Account | Registration, login, account recovery and device management |
| Personal Profile | Identity, family, contact and address information |
| Purpose-Based Profiles | Education, career and other user-selected categories |
| Form Intelligence | Field discovery, semantic interpretation and matching |
| Autofill Engine | Filling supported inputs and verifying results |
| Smart File Preparation | PDF conversion, photo/signature resizing and file validation |
| Application Tracker | Application history, statuses, notes and timeline |
| Security & Privacy | Encryption, key management, sync, deletion and access control |

These modules should have clearly defined interfaces so the file-processing system, browser extension and profile manager can evolve independently.

---

# 6. Account Creation and Authentication

## 6.1 Supported registration methods

FormFlow should support:

- Email and password
- Google sign-in
- Mobile number and OTP verification

Additional identity providers may be added later.

## 6.2 Registration flow

1. User opens FormFlow.
2. User selects email, Google or mobile registration.
3. FormFlow verifies the identity using the chosen authentication method.
4. User accepts the privacy policy and terms.
5. FormFlow initializes the user's account and secure vault.
6. User proceeds to profile setup.

Authentication data and personal profile data must be treated as separate concerns.

## 6.3 Account security

Requirements:

- Secure session management.
- Secure password handling by the authentication provider.
- Mobile-number verification before treating the number as verified.
- Rate limiting on login, OTP and recovery attempts.
- Session revocation and device management.
- Optional or recommended multifactor authentication where supported.
- Reauthentication for sensitive security changes.
- Notifications for important account security events where appropriate.

A verified email address or phone number establishes control of that communication channel; it does not automatically prove the user's legal identity.

---

# 7. Onboarding and Personal Profile

The onboarding flow follows the user's proposed approach: establish universal personal information first, then configure FormFlow according to the user's selected purposes.

## 7.1 Final onboarding flow

```text
Create Account
      |
      v
Personal Information
      |
      v
Choose FormFlow Purposes
      |
      v
Purpose-Specific Profile Setup
      |
      v
Optional Document and Asset Setup
      |
      v
Review Profile and Privacy Settings
      |
      v
FormFlow Dashboard
```

The onboarding process should be divided into short, understandable steps rather than one long page.

## 7.2 Step 1 — Basic identity

Fields:

- First name
- Last name
- Email
- Mobile number
- Date of birth

First name, last name and at least one usable account contact method are essential for initial setup. Date of birth and other fields should be collected according to the onboarding policy, with clear optionality where possible.

Email and mobile values should be associated with their verification status.

## 7.3 Step 2 — Family information

Fields:

- Father's name
- Mother's name

These are reusable personal-profile fields, particularly relevant to educational and official forms.

They should be stored as structured fields rather than as unstructured notes.

## 7.4 Step 3 — Present address

Recommended fields:

- Country
- Division/state/province
- District/county
- City or municipality
- Upazila/subdistrict or local area, where relevant
- Street, road or address line
- House/building and apartment, where relevant
- Postal code

The location model should be extensible to different countries instead of hardcoding Bangladesh-specific address rules throughout the application.

## 7.5 Step 4 — Permanent address

Provide the option:

**Permanent address is the same as present address.**

When enabled, reuse the address reference rather than asking the user to enter duplicate values.

If the addresses differ, collect the permanent address separately.

## 7.6 Step 5 — Profile photo and signature

Users may add:

- Profile photo
- Signature image

Both are reusable assets, not ordinary text fields.

Store metadata about each asset, such as its type, original format, dimensions and verification or preparation status. The actual binary files belong in the secure asset vault.

Uploading a photo or signature during initial onboarding should be encouraged when useful, but users should not be blocked from accessing the product if the asset is not immediately available.

---

# 8. Purpose-Based Profile Setup

## 8.1 Purpose selection

After collecting universal personal information, FormFlow asks:

**What would you mainly like to use FormFlow for?**

Suggested options:

- University and admission applications
- Job and career applications
- Scholarships
- Government and official forms
- Visa and immigration applications
- Professional certifications
- General online forms

Users may select multiple purposes.

The selection determines which profile sections FormFlow recommends during onboarding.

## 8.2 Education profile

For university and admission applicants, recommended fields include:

### Secondary education

- Institution
- Qualification level
- Group or stream
- Passing year
- Roll number
- Registration number
- GPA or equivalent result

### Higher secondary education

- Institution
- Qualification level
- Group or stream
- Passing year
- Roll number
- Registration number
- GPA or equivalent result

### Higher education

- University or institution
- Degree
- Department or major
- Session
- Student ID
- Enrollment date
- Graduation date or expected graduation date
- CGPA or equivalent result

Education records must support multiple qualifications and institutions.

For example, a user may have multiple degrees or academic records.

## 8.3 Career profile

For job seekers, recommended fields include:

### Professional information

- Current or most recent position
- Company
- Department
- Employment type
- Employment start and end dates
- Years of experience
- Current location
- Notice period or availability

### Skills and qualifications

- Technical skills
- Programming languages
- Tools and frameworks
- Soft skills
- Professional certifications
- Spoken and written languages

### Online profiles

- LinkedIn
- GitHub
- Portfolio
- Personal website

### Career preferences

- Preferred position
- Preferred location
- Preferred employment type
- Expected salary
- Availability

Sensitive or context-dependent information, such as salary expectations, should not be reused indiscriminately across unrelated applications.

## 8.4 Shared profile model

Selecting multiple purposes must not create duplicate personal records.

The data model should be:

```text
User
 ├── Personal Profile
 │    ├── Identity
 │    ├── Contact
 │    ├── Family
 │    └── Addresses
 │
 ├── Education Records[]
 │
 ├── Employment Records[]
 │
 ├── Skills[]
 │
 ├── Certifications[]
 │
 ├── Career Preferences
 │
 └── Personal Assets[]
```

The user's selected purposes control which sections are recommended and displayed; they do not create separate copies of shared identity information.

## 8.5 Profile completion policy

- Distinguish required, recommended and optional fields.
- Permit skipping nonessential profile sections.
- Allow users to edit information later.
- Show profile readiness in understandable terms.
- Do not require users to fill every possible field before using autofill.

The profile is intended to reduce repetitive work, not become another lengthy application.

---

# 9. Personal Data Model and Field Taxonomy

The master field taxonomy should support a broad range of forms without requiring every field to be exposed during onboarding.

## 9.1 Main semantic categories

1. Identity and personal details.
2. Contact information.
3. Present and permanent addresses.
4. Family and emergency contacts.
5. Education and academic results.
6. Employment and career history.
7. Skills and languages.
8. Certifications and achievements.
9. Career preferences.
10. Written responses and statements.
11. Date and time values.
12. Numeric values and amounts.
13. Documents and media.
14. Location selections.
15. Application-specific information.
16. Legal declarations and consent.
17. Authentication and security fields.
18. Unsupported or specialized interactive fields.

## 9.2 Semantic field representation

The implementation should distinguish three concepts:

- **DOM type:** The actual HTML control, such as `INPUT_TEXT`, `SELECT`, `CHECKBOX` or `FILE`.
- **Semantic type:** What the field means, such as `PHONE`, `DATE_OF_BIRTH`, `HSC_GPA` or `PROFILE_PHOTO`.
- **Automation policy:** What FormFlow is permitted to do with that field.

An internal field definition may resemble:

```json
{
  "semantic_type": "DATE_OF_BIRTH",
  "dom_type": "INPUT_DATE",
  "sensitivity": "HIGH",
  "automation_policy": "FILL_WITH_REVIEW",
  "source": "USER_PROFILE",
  "confidence": 0.99
}
```

This is an illustrative schema. Production confidence values should come from a defined and evaluated scoring process.

The taxonomy should be centrally versioned so the profile manager, AI field classifier and autofill engine interpret the same semantic types consistently.

---

# 10. Form Intelligence and AI Architecture

## 10.1 Objective

FormFlow must understand what information a website requests and map the request to an appropriate saved profile value or asset.

For example, these labels may all represent the same semantic field:

- Mobile number
- Phone number
- Contact number
- Applicant's mobile

The semantic classifier should map them to a common type such as `PHONE`.

## 10.2 Recommended processing pipeline

```text
Website Form
     |
     v
DOM and Accessibility Inspection
     |
     v
Label and Constraint Extraction
     |
     v
Deterministic Field Classification
     |
     v
AI Assistance for Ambiguous Fields
     |
     v
Semantic Field Mapping
     |
     v
Profile / Asset Lookup
     |
     v
Automation Policy Check
     |
     v
Fill and Verify
```

## 10.3 Deterministic-first approach

Use rules, accessible labels, HTML attributes, known field dictionaries and previously validated mappings before calling an AI model.

Use AI when:

- A field label is ambiguous.
- A custom control has unclear semantics.
- The page's visible instructions require interpretation.
- A complex field cannot be confidently classified by rules.

AI should not be required to interpret every ordinary text field.

## 10.4 Privacy-preserving AI

The preferred architecture is to send field descriptions rather than actual profile values.

Example request:

```json
{
  "label": "Applicant's mobile number",
  "input_type": "tel",
  "section": "Personal Information"
}
```

Possible interpretation:

```json
{
  "semantic_type": "PHONE",
  "confidence": 0.97
}
```

The actual phone number is retrieved from the authorized local profile and supplied to the matching field by the client.

The AI service should not receive the full profile or uploaded identity documents merely to determine a field's meaning.

If future functionality requires document OCR or cloud processing, it must use a separately defined consent, data-minimization and retention policy.

## 10.5 Model failure and uncertainty

When classification is uncertain:

- Ask the user to identify the field.
- Leave the field untouched.
- Explain why FormFlow could not determine the correct value.

Do not invent profile information or select an arbitrary value to make the form appear complete.

---

# 11. Browser Extension and Autofill Engine

## 11.1 Core responsibilities

The extension should:

- Detect supported forms.
- Extract field labels and constraints.
- Identify semantic field types.
- Access authorized profile data.
- Populate supported controls.
- Handle dynamically rendered forms.
- Verify values after filling.
- Highlight completed, uncertain and unsupported fields.
- Offer review before the user submits.

## 11.2 Supported controls

Initial support should prioritize:

- Text and email inputs
- Telephone inputs
- Number inputs
- Date inputs
- Text areas
- Standard dropdowns
- Radio buttons
- Nonlegal checkboxes
- Standard file inputs

Advanced support can include autocomplete widgets, custom dropdowns, rich-text editors and repeatable education or employment groups.

## 11.3 React, Vue and other dynamic applications

Modern frameworks may maintain internal state separate from the visible DOM value.

The autofill engine must use compatible input interactions and events, then verify that the website actually retained the value.

Simply assigning a string to an element's `value` property is not sufficient for reliable automation.

## 11.4 Dynamic forms

Some fields appear only after a previous selection.

The engine should:

1. Fill a supported field when permitted.
2. Detect relevant DOM changes.
3. Reinspect newly available fields.
4. Recompute the remaining mappings.
5. Continue within reasonable limits.

The extension should avoid uncontrolled repeated scanning that causes performance problems.

## 11.5 Autofill confidence and safety policy

| Category | Behavior |
|---|---|
| High-confidence ordinary field | Fill automatically and verify |
| Ambiguous field | Ask the user or leave unchanged |
| Sensitive field | Apply stricter confirmation policy |
| Legal declaration or consent | Require explicit user action |
| CAPTCHA or unsupported security challenge | Do not bypass |
| Unsupported custom upload widget | Provide guided manual assistance |
| Form submission | User remains responsible for final action |

## 11.6 Submission boundary

FormFlow is an assistant, not an autonomous application-submission bot.

The user reviews the filled form and submits it manually.

FormFlow should not automatically click buttons such as “Submit Application,” “Confirm Declaration” or “Pay Now.”

---

# 12. Smart Document and Image Preparation

This is a core product module designed to eliminate manual file-conversion and resizing work.

## 12.1 Supported inputs

The initial file preparation module should aim to support:

- JPEG and JPG
- PNG
- WebP
- PDF

Additional formats, such as HEIC or TIFF, may be introduced after compatibility, security and dependency support are validated.

DOCX and other document formats may require a separate conversion workflow and are not guaranteed to be supported by the initial implementation.

## 12.2 Image-to-PDF conversion

Requirements:

- Convert supported images into valid PDFs.
- Support combining multiple selected images into a single PDF.
- Preserve page ordering selected by the user.
- Correct image orientation.
- Maintain document readability.
- Allow file-size optimization when needed.
- Validate the resulting PDF.
- Preserve the original files.

## 12.3 Existing PDF handling

For PDFs:

- Keep the original unchanged.
- Inspect basic metadata and file size.
- Create an optimized copy only when needed.
- Avoid destructive transformations that damage readability.
- Report unsupported, corrupted or password-protected files clearly.

## 12.4 Automatic photo resizing

When a website requests a profile photo, FormFlow should:

1. Identify the relevant upload field.
2. Determine accepted file formats and known constraints.
3. Retrieve the user's authorized photo.
4. Correct orientation.
5. Crop and resize as needed.
6. Compress the image within the known limit.
7. Validate dimensions, format and file size.
8. Preview the prepared version when appropriate.
9. Attach it to the corresponding upload field.

If the required crop cannot be determined safely, the user should be offered a crop preview or guided adjustment.

## 12.5 Automatic signature resizing

The signature workflow should:

1. Retrieve the authorized signature image.
2. Correct orientation.
3. Trim excess whitespace where safe.
4. Preserve the original aspect ratio.
5. Resize to the required dimensions.
6. Convert to the required format.
7. Optimize the file size.
8. Validate the output.
9. Attach the prepared asset to the appropriate field.

FormFlow must preserve the original signature strokes and avoid stretching or visually altering the signature.

## 12.6 Requirements detection

The system should infer file requirements using:

1. HTML attributes, including `accept` and `multiple`.
2. Visible labels and upload instructions.
3. Nearby helper text and validation messages.
4. Deterministic parsing of dimensions, format and file-size instructions.
5. AI interpretation for ambiguous natural-language instructions.

HTML attributes alone do not guarantee that the server will accept a file.

If the actual requirements are unknown, FormFlow must not invent exact dimensions or claim complete validation.

## 12.7 Requirements-driven processing

The processor should receive a structured specification:

```json
{
  "asset_type": "PROFILE_PHOTO",
  "accepted_formats": ["image/jpeg"],
  "target_width": 300,
  "target_height": 300,
  "max_size_bytes": 102400,
  "constraints_source": "VISIBLE_FORM_INSTRUCTIONS"
}
```

This is an example specification, not a universal photo standard.

The processor should return:

- Prepared file or asset reference.
- Actual format.
- Actual dimensions.
- Actual size.
- Validation results.
- Any quality or compatibility warnings.

The validation engine determines whether the result meets all known requirements.

## 12.8 Browser integration

For supported file inputs, the extension may attach a generated `File` object through browser-supported mechanisms.

Some sites use custom upload widgets or restrictions that prevent programmatic assignment. In these cases, FormFlow must guide the user through the final upload step instead of claiming success.

## 12.9 File preparation service architecture

```text
Asset Vault
    |
    v
Asset Intake and Validation
    |
    +---------------------------+
    |                           |
    v                           v
Document Processor         Image Processor
    |                           |
    v                           v
PDF Conversion             Crop / Resize
Page Ordering              Compression
PDF Optimization           Format Conversion
    |                           |
    +-------------+-------------+
                  |
                  v
        Requirements Validator
                  |
                  v
          Prepared Asset
                  |
                  v
          Browser Autofill
                  |
                  v
           Result Verification
```

Routine conversions should preferably run locally in the browser or extension. Remote processing should only be introduced when necessary, with explicit privacy and retention controls.

---

# 13. Personal Asset Vault

The asset vault stores files that users may reuse across applications.

## 13.1 Asset categories

- Profile photo
- Signature
- CV or resume
- Academic transcripts
- Academic certificates
- Marksheets
- Training certificates
- Experience certificates
- Cover letters
- Portfolio files
- Other user-provided documents

The user should not be required to upload every document during onboarding.

## 13.2 Original and prepared asset separation

The system must maintain the original asset and its generated variants separately.

Example:

```text
Profile Photo
 ├── Original
 ├── University Photo Variant
 └── Job Portal Photo Variant
```

Prepared variants should record which requirements they satisfy and when those requirements were established.

If the target requirements change, FormFlow should be able to create a new variant without losing the original.

## 13.3 Document extraction

Document-to-profile extraction may be added as an optional capability.

If implemented, the workflow should be:

1. User selects a document.
2. FormFlow identifies the document type.
3. Text or structured data is extracted locally when practical.
4. Candidate fields are mapped to the semantic taxonomy.
5. The user reviews extracted values.
6. Approved values are saved to the profile.
7. Source information is retained where appropriate.

Unreviewed extracted data should not automatically overwrite existing verified profile values.

---

# 14. Application History and Tracker

## 14.1 Objective

Allow users to see where they have worked on or submitted applications.

The feature should be called **My Applications**.

## 14.2 Application list

Each record should display:

- Application title
- Organization
- Application category
- Website or application URL
- Date started
- Date submitted, if confirmed
- Current status
- Last updated date

The dashboard should provide search and filters for category, date and status.

## 14.3 Application statuses

Recommended statuses:

- Draft
- Ready to Submit
- Submission Unconfirmed
- Submitted
- Under Review
- Accepted
- Rejected
- Withdrawn

Status meanings must be explicit.

For example, `Under Review`, `Accepted` and `Rejected` should generally be based on a user update or a reliable external signal, not a guess from the fact that the user submitted the form.

## 14.4 Application tracking flow

```text
User Opens Application Website
            |
            v
FormFlow Detects Supported Form
            |
            v
User Starts Autofill
            |
            v
Offer to Create Application Record
            |
            v
Save Draft Metadata
            |
            v
User Reviews and Submits Externally
            |
            v
User Confirms Submission
            |
            v
Update Application History
```

FormFlow may detect submission-related events, but a button click alone does not prove the submission succeeded.

## 14.5 Application details

Each record should support:

- Application title and organization
- Original website link
- Category
- Dates and status
- Optional notes
- Timeline of important events
- Edit and delete actions
- Optional reminder information in a later release

## 14.6 Data minimization

Application history does not require a complete copy of every form.

By default, store only tracking metadata. Do not retain sensitive field values, uploaded documents or entire completed forms just to maintain an application list.

Where the encrypted-vault architecture permits, store application titles, notes, URLs and other sensitive metadata inside the user's encrypted data rather than as readable server records.

---

# 15. Security and Privacy Architecture

Security is a core product requirement because FormFlow handles identity, family information, addresses, educational records, photographs, signatures and official documents.

## 15.1 Recommended architecture

```text
                 User Devices
                      |
             FormFlow Client
                      |
          +-----------+-----------+
          |                       |
          v                       v
   Encrypted Local Vault    Browser Extension
          |                       |
          |                       v
          |                 Website Form
          |
          v
    Encrypted Sync
          |
          v
    Backend Services
    ├── Account Metadata
    ├── Device and Session Metadata
    ├── Sync Coordination
    └── Minimal Operational Data

Optional AI Service
    └── Field semantics and
        minimized context only
```

The preferred design keeps personal values and document contents outside the backend's readable data wherever technically practical.

## 15.2 Encrypted local vault

The vault should hold:

- Personal profile values
- Education and career records
- Photo and signature originals
- Documents
- Prepared asset metadata
- Application history
- User preferences

Sensitive data should be encrypted before persistence.

The exact storage technology and encryption-key hierarchy must be validated during the detailed security design.

## 15.3 Encryption model

A recommended design is envelope-style encryption:

1. Generate a random vault encryption key.
2. Encrypt user data with a vetted authenticated-encryption algorithm.
3. Protect the vault key with a separate key-encryption mechanism.
4. Keep the decryption capability on authorized devices where possible.
5. Synchronize ciphertext rather than plaintext.
6. Ensure the server cannot independently decrypt vault contents.

A cryptographic implementation should use established libraries and algorithms, not custom encryption.

The account password, authentication token and vault encryption key must not be treated as interchangeable values.

## 15.4 Password and recovery-key distinction

FormFlow should separate:

- Account authentication credentials.
- Vault encryption keys.
- Recovery mechanisms.
- Device authorization credentials.

Losing account access and losing the ability to decrypt the vault are different events.

If the product adopts a zero-knowledge vault, account recovery by email or SMS alone must not silently restore access to encrypted profile data.

The recovery strategy must be decided before production implementation. Options include a user-held recovery key, a separately protected recovery mechanism, or a clearly disclosed unrecoverable-vault policy.

Recovery keys should be generated securely, shown safely, and never stored in readable form on the server.

## 15.5 Cross-device synchronization

Users should be able to access their account from multiple authorized devices.

Synchronization should support:

- Encrypted data transfer.
- Device enrollment and revocation.
- Conflict detection and resolution.
- Versioning and recovery from accidental overwrites.
- Secure backup and restore.
- Clear handling of revoked or lost devices.

Google Drive or Apple-backed storage may be considered as an optional backup destination, but neither should be assumed to provide end-to-end encrypted vault semantics automatically. The application must encrypt data before sending it to the chosen storage provider.

## 15.6 Backend data minimization

The backend should retain only the information required for account operations, authentication integration, sync coordination, security and service reliability.

Potential metadata includes:

- Internal user identifier
- Authentication-provider references
- Account and device status
- Sync metadata
- Necessary security logs
- Subscription or billing metadata if later introduced

Avoid storing readable personal profiles, document contents or complete application answers when they are not necessary.

## 15.7 AI privacy

- Do not send the full personal profile to AI for routine field classification.
- Do not send identity documents for routine image conversion.
- Minimize page content sent for semantic interpretation.
- Avoid transmitting hidden page data or unrelated form values.
- Redact unnecessary personal data from logs.
- Establish retention and provider data-use policies before enabling external AI processing.
- Require explicit consent for any future feature that sends document contents or personal values to a remote service.

## 15.8 Browser extension security

- Request the minimum browser permissions needed.
- Avoid broad access to all websites unless required by a clearly explained feature.
- Process pages only within the intended autofill workflow.
- Do not transmit page contents or profile values to analytics systems.
- Do not inject personal data into unrelated websites.
- Never automatically fill passwords, OTPs or CAPTCHA responses.
- Apply strict message validation between the extension components.
- Protect the extension's local storage and communication channels.
- Keep dependencies updated and review permissions during releases.

## 15.9 Sensitive field policy

Fields such as national identification numbers, passports, legal declarations and financial information require stricter handling.

FormFlow should distinguish:

- Automatically fillable ordinary fields.
- Sensitive fields that require confirmation.
- Legal or consent fields requiring explicit user action.
- Unsupported security challenges that must remain under user control.

## 15.10 Data deletion

Users should be able to:

- Delete individual profile values.
- Delete documents and prepared variants.
- Delete application history records.
- Revoke authorized devices.
- Delete their account.
- Request deletion of applicable server-side data.

Deletion procedures must account for synchronized copies, backups and any applicable retention obligations. The product must not claim that all copies are instantly erased if backup retention or synchronization delays prevent that.

---

# 16. Functional Requirements

The following requirements can be used as implementation and QA references.

## 16.1 Authentication

- `AUTH-001`: Users can create an account through supported registration methods.
- `AUTH-002`: Users can sign in and sign out securely.
- `AUTH-003`: Users can verify their email or phone where required.
- `AUTH-004`: Users can manage authorized sessions and devices.
- `AUTH-005`: Vault recovery must follow the documented recovery policy.

## 16.2 Profile

- `PROF-001`: Users can create and update their personal information.
- `PROF-002`: Users can manage present and permanent addresses.
- `PROF-003`: Users can select multiple FormFlow purposes.
- `PROF-004`: Users can create multiple education and employment records.
- `PROF-005`: Users can mark fields as reusable or exclude them from autofill.
- `PROF-006`: Users can review the source and verification state of important values.

## 16.3 Autofill

- `FILL-001`: FormFlow identifies supported form controls.
- `FILL-002`: FormFlow maps recognized fields to semantic types.
- `FILL-003`: FormFlow uses deterministic classification before AI where practical.
- `FILL-004`: FormFlow fills supported fields according to the automation policy.
- `FILL-005`: FormFlow verifies that filled values were retained.
- `FILL-006`: FormFlow highlights filled, missing and uncertain fields.
- `FILL-007`: FormFlow does not automatically submit applications.
- `FILL-008`: FormFlow does not bypass CAPTCHA or access controls.

## 16.4 File preparation

- `FILE-001`: Users can import supported images and PDFs.
- `FILE-002`: FormFlow can convert supported images into PDFs.
- `FILE-003`: FormFlow can combine multiple images into one PDF.
- `FILE-004`: FormFlow can resize and compress photos.
- `FILE-005`: FormFlow can resize and compress signatures.
- `FILE-006`: FormFlow validates generated formats, dimensions and file sizes.
- `FILE-007`: FormFlow preserves original assets.
- `FILE-008`: FormFlow reports failures and unsupported constraints accurately.
- `FILE-009`: FormFlow can attach prepared files to supported upload fields.
- `FILE-010`: FormFlow verifies upload state where observable.

## 16.5 Application history

- `APP-001`: Users can create application history records.
- `APP-002`: FormFlow can offer to create a draft record during supported autofill workflows.
- `APP-003`: Users can confirm submission.
- `APP-004`: Users can update application statuses and notes.
- `APP-005`: Users can search and filter application records.
- `APP-006`: Users can edit and delete records.
- `APP-007`: FormFlow distinguishes confirmed submissions from unconfirmed attempts.

## 16.6 Security

- `SEC-001`: Sensitive profile data is encrypted at rest.
- `SEC-002`: Cross-device synchronization follows the approved encryption design.
- `SEC-003`: Server-side services cannot read zero-knowledge vault contents if the architecture promises that property.
- `SEC-004`: AI requests minimize exposure of personal information.
- `SEC-005`: The extension uses least-privilege permissions.
- `SEC-006`: Users can revoke devices and delete data.
- `SEC-007`: Security-sensitive actions are logged without unnecessarily logging personal content.

---

# 17. Non-Functional Requirements

## 17.1 Performance

Proposed initial targets, to be validated through testing:

- Routine field classification should normally complete within a few hundred milliseconds when no remote AI call is needed.
- Typical local photo resizing should complete within a few seconds for reasonable file sizes and supported devices.
- The dashboard should remain responsive while files are processed.
- Large file operations should run asynchronously where appropriate and provide progress feedback.

These are engineering targets, not guaranteed performance claims.

## 17.2 Reliability

- Failed processing must not corrupt the original asset.
- Autofill failures must be visible to the user.
- Network failure must not silently lose unsynchronized local data.
- Interrupted synchronization must be recoverable.
- Unsupported forms must degrade gracefully.

## 17.3 Compatibility

Target environments should be finalized during implementation planning.

The proposed baseline is:

- Chromium-based desktop browsers.
- Chrome extension support first.
- Responsive web interface.
- Mobile-browser usage for account and profile management where supported.
- Additional browser support after compatibility testing.

A desktop browser extension must not be assumed to work on every mobile browser. Mobile-browser autofill capabilities and extension support require separate validation.

## 17.4 Accessibility

- Clear labels and instructions.
- Keyboard navigation.
- Accessible error messages.
- Understandable progress indicators.
- Adequate color contrast.
- Status indicators that do not rely on color alone.

## 17.5 Maintainability

- Modular service boundaries.
- Typed field and asset schemas.
- Versioned semantic taxonomy.
- Automated unit, integration and end-to-end tests.
- Dependency and security scanning.
- Versioned data migrations.
- Documented browser compatibility behavior.

---

# 18. High-Level Technical Architecture

The exact framework and deployment choices remain implementation decisions, but the logical architecture should be established.

## 18.1 Client components

### FormFlow Web Application

Responsibilities:

- Account and profile management.
- Purpose-based profile configuration.
- Asset management.
- Application history.
- Privacy settings.
- Device management and recovery instructions.

### Browser Extension

Responsibilities:

- Form discovery.
- Field classification.
- Secure profile access.
- Autofill and verification.
- File preparation integration.
- Application history prompts.

### Local Vault and Processing Layer

Responsibilities:

- Encrypted local persistence.
- Profile retrieval.
- Asset preparation.
- Local field-to-profile matching.
- Synchronization queue.
- Temporary-file cleanup.

## 18.2 Backend components

Recommended logical services:

- Authentication integration.
- User/account metadata.
- Encrypted synchronization.
- Device/session management.
- Optional AI semantic interpretation.
- Operational monitoring.
- Optional subscription or billing integration in the future.

The backend should not become a centralized repository of all personal profiles and documents by default.

## 18.3 AI service

Responsibilities:

- Interpret ambiguous field labels.
- Interpret relevant visible form instructions.
- Classify field semantics.
- Return structured results.

Non-responsibilities:

- Holding the user's complete profile.
- Performing routine local image resizing.
- Automatically submitting applications.
- Inventing missing values.
- Making unapproved changes to the user's profile.

## 18.4 File processing service

Routine file processing should preferably run locally.

A remote processor may be considered for workloads that cannot reasonably be handled on the client, but this introduces additional data exposure, cost and retention obligations.

---

# 19. Suggested Data Entities

The following is a conceptual data model, not a finalized physical database schema.

| Entity | Purpose |
|---|---|
| UserAccount | Account identifier and authentication references |
| UserPreferences | User-selected purposes and application preferences |
| PersonalProfile | Identity, contact, family and address information |
| EducationRecord | One academic qualification or study record |
| EmploymentRecord | One employment experience |
| Skill | Reusable skill entry |
| Certification | Certification or professional qualification |
| AssetMetadata | Metadata for documents, photos and signatures |
| PreparedAsset | Derived file and its processing constraints |
| ApplicationRecord | Application tracking information |
| ApplicationEvent | Timeline events for an application |
| DeviceRecord | Authorized-device metadata |
| VaultSyncMetadata | Encrypted synchronization state |
| SecurityEvent | Minimal security and operational events |

## 19.1 Important modeling rules

- Support multiple education and employment records.
- Avoid duplicating identity information across purpose categories.
- Keep file metadata separate from binary asset storage.
- Keep original assets separate from prepared variants.
- Represent field sources and verification states.
- Avoid storing complete application form payloads by default.
- Store only the minimum backend metadata required for each service.

## 19.2 Profile field metadata

Reusable values may need metadata such as:

- Semantic field type
- Source: user-entered, imported or document-extracted
- Verification status
- Last updated timestamp
- Sensitivity classification
- Whether autofill is permitted
- Optional source reference

This supports accurate reuse and safer updates.

---

# 20. Main User Journeys

## Journey A — New user

1. Create a FormFlow account.
2. Verify the account's email or phone where required.
3. Enter core personal details.
4. Enter family and address information.
5. Add a photo and signature if available.
6. Choose application purposes.
7. Complete relevant education or career sections.
8. Configure privacy and recovery options.
9. Open the dashboard.

## Journey B — Filling a university application

1. User opens a university website.
2. FormFlow detects a supported form.
3. The extension identifies field semantics and requirements.
4. The engine matches fields with the local profile.
5. The user reviews sensitive or uncertain mappings.
6. FormFlow fills supported fields.
7. Missing fields remain clearly identified.
8. The user provides any remaining values.
9. FormFlow prepares required documents, photos or signatures.
10. The user reviews the completed form.
11. The user submits the application.
12. FormFlow offers to save the application to history.

## Journey C — Preparing a photo or signature

1. User has an original asset in the vault.
2. FormFlow detects an upload field.
3. The requirements detector determines known constraints.
4. The preparation engine generates a compatible copy.
5. The validator checks the copy.
6. The extension attaches the prepared file where supported.
7. The user reviews the visible preview or status.
8. The original asset remains unchanged.

## Journey D — Tracking applications

1. User opens My Applications.
2. User sees recent drafts and confirmed submissions.
3. User opens a record to review its URL, dates and notes.
4. User updates its status when new information arrives.
5. User deletes records they no longer want to retain.

## Journey E — New device

1. User authenticates on the new device.
2. The device is authorized.
3. Encrypted vault data is restored or synchronized.
4. The device obtains the necessary key material through the approved key-management design.
5. The user can access permitted profile information.
6. Lost or revoked devices can no longer obtain future access through the normal authorization path.

---

# 21. Error Handling and Edge Cases

FormFlow must account for situations in which normal automation cannot proceed.

## 21.1 Form handling

- Missing or ambiguous field labels.
- Multiple fields with similar names.
- Dynamic form updates.
- Custom controls.
- Cross-origin frames.
- Closed shadow roots or inaccessible controls.
- Unsupported browser behavior.
- Website validation errors.
- Network failures during submission.

## 21.2 File handling

- Unsupported formats.
- Corrupted or password-protected PDFs.
- Oversized images.
- Poor image quality.
- Incorrect photo cropping.
- Signature distortion risks.
- Unknown target requirements.
- Output still too large after reasonable compression.
- Custom uploaders that reject generated files.

## 21.3 Security handling

- Lost devices.
- Lost recovery keys.
- Unauthorized access attempts.
- Vault synchronization conflicts.
- Interrupted encryption or migration operations.
- Revoked sessions.
- Accidental deletion.
- External AI service failure.

In every case, preserve the original data where possible, report the issue accurately, and offer a clear recovery path.

---

# 22. Testing Strategy

## 22.1 Unit tests

Test:

- Field normalization and semantic mapping.
- Address and education schemas.
- Image resizing and compression.
- Image-to-PDF conversion.
- PDF output validation.
- File-size and dimension checks.
- Application status transitions.
- Encryption and key-management utilities.

## 22.2 Integration tests

Test:

- Authentication and account recovery.
- Vault encryption and restoration.
- Encrypted synchronization.
- Extension-to-vault communication.
- AI classification response validation.
- Profile-to-field mapping.
- Prepared asset delivery to the extension.
- Application history persistence.

## 22.3 End-to-end tests

Create controlled test websites with:

- Standard HTML inputs.
- Selects and radio buttons.
- Checkboxes.
- React-based controlled inputs.
- Dynamic fields.
- File upload controls.
- Required-field validation.
- Custom upload widgets.
- Simulated submission success and failure.

## 22.4 Security tests

Include:

- Threat modeling.
- Dependency scanning.
- Extension permission review.
- Local storage inspection.
- Network traffic inspection for unintended personal-data transmission.
- Authentication and authorization tests.
- Vault recovery testing.
- Backup and synchronization testing.
- Malformed file handling.
- Sensitive information leakage checks.

## 22.5 Acceptance criteria

A feature should not be considered complete merely because its interface works.

For example, photo resizing is complete only when the output meets the specified constraints, the original remains unchanged, errors are reported correctly and the generated file can be used in the supported upload workflow.

---

# 23. Development Roadmap

The phases below are a proposed delivery order, not a promise about duration.

## Phase 1 — Product foundation

- Finalize requirements and user journeys.
- Establish the field taxonomy.
- Define the security and threat model.
- Select the authentication and local vault architecture.
- Implement account creation.
- Implement personal profile setup.
- Implement purpose selection.
- Implement education and career profile sections.

**Deliverable:** A working account and reusable profile foundation.

## Phase 2 — Browser extension and autofill

- Implement form discovery.
- Implement deterministic field classification.
- Build profile matching.
- Add AI interpretation for ambiguous fields.
- Implement supported input filling.
- Add post-fill verification.
- Add review and confirmation UI.
- Test on controlled websites.

**Deliverable:** Users can fill supported forms using their saved profile.

## Phase 3 — Smart File Preparation

- Implement asset import.
- Implement image-to-PDF conversion.
- Implement multi-image PDF creation.
- Implement photo resizing.
- Implement signature resizing.
- Implement file compression and validation.
- Preserve originals and generate variants.
- Integrate prepared assets with supported upload controls.

**Deliverable:** Users can prepare and reuse application files without manually converting them.

## Phase 4 — Application History

- Implement application records.
- Add draft tracking.
- Add user-confirmed submission tracking.
- Add application details and event timeline.
- Add search and filters.
- Add manual status updates.
- Add editing and deletion.

**Deliverable:** Users can track where they applied and review their application history.

## Phase 5 — Production security and reliability

- Complete vault recovery.
- Complete encrypted synchronization.
- Implement device revocation.
- Complete data deletion.
- Add monitoring and operational controls.
- Perform security testing.
- Test recovery and backup scenarios.
- Review privacy claims and documentation.

**Deliverable:** A production-readiness candidate with documented security boundaries.

## Phase 6 — Advanced capabilities

Potential future work:

- More browsers and supported mobile environments.
- Advanced custom upload widgets.
- Optional document extraction.
- Better document quality detection.
- Reminders and deadline tracking.
- Additional application categories.
- More sophisticated compatibility rules.

These should follow evidence from user testing and compatibility testing rather than being prerequisites for the initial release.

---

# 24. Key Product Metrics

Track product performance without collecting unnecessary personal data.

## 24.1 Usability metrics

- Time required to fill a supported form.
- Number of fields populated successfully.
- Number of fields requiring manual correction.
- Onboarding completion rate.
- Repeat usage rate.
- Application history usage.

## 24.2 File preparation metrics

- Successful conversion rate.
- Percentage of generated files meeting known requirements.
- Image preparation failure rate.
- Average processing time.
- Percentage of upload attempts successfully verified.

## 24.3 Reliability metrics

- Autofill success rate by control type.
- Semantic classification accuracy.
- False-positive field matches.
- Recovery and synchronization success rate.
- Unsupported website rate.

## 24.4 Privacy metrics

- Number of unnecessary profile-value transmissions, with a target of zero.
- Number of sensitive values exposed in logs, with a target of zero.
- Security incidents.
- Data deletion completion rate.
- Unauthorized device access attempts.

Metrics should be aggregated and privacy-preserving. Avoid transmitting raw website form contents or personal values to analytics systems.

---

# 25. Key Risks and Mitigations

| Risk | Mitigation |
|---|---|
| Incorrect field matching | Confidence checks, review and verification |
| Wrong values reused | Field source metadata and editable profile |
| Photo crop is incorrect | Preview and guided adjustment |
| PDF compression damages readability | Quality checks and failure reporting |
| Website blocks programmatic upload | Guided manual fallback |
| Website reports false submission state | Explicit confirmation and conservative status transitions |
| AI receives personal data unnecessarily | Local matching and minimized semantic requests |
| Recovery key is lost | Clearly documented recovery options and early user education |
| Sync conflicts overwrite data | Versioning and conflict resolution |
| Browser extension permissions are too broad | Least-privilege design and permission review |
| Product promises universal compatibility | Publish clear support boundaries and measure compatibility |
| Application history reveals sensitive behavior | Data minimization, encryption and user-controlled deletion |

---

# 26. Product Decisions and Open Questions

The following decisions should be resolved before production implementation.

## 26.1 Security and storage

- Final encryption algorithms and key hierarchy.
- Whether the vault is fully zero-knowledge.
- Recovery key format and recovery policy.
- Local storage technology.
- Cross-device synchronization protocol.
- Backup retention and deletion behavior.
- Whether any remote document processing will be offered.

## 26.2 Authentication

- Exact authentication provider.
- Account linking between Google, email and mobile.
- Mobile OTP provider and cost.
- Session expiration and reauthentication rules.

## 26.3 Browser compatibility

- Initial supported browsers.
- Extension distribution strategy.
- Mobile browser support.
- Support boundaries for custom upload controls.
- Policy for sites that prohibit or restrict automated interaction.

## 26.4 File preparation

- Maximum supported file sizes.
- Initial accepted image formats.
- PDF library and dependency review.
- Whether generated files are retained or regenerated on demand.
- Image-quality thresholds and validation behavior.

## 26.5 Application tracking

- How much website metadata is retained.
- Which events may be inferred automatically.
- Whether reminders are included in the first release.
- How to handle multiple applications from the same website.

These questions should be resolved explicitly instead of being decided accidentally during implementation.

---

# 27. Final Architecture Principles

The following principles should guide future development.

1. **Profile-first design:** Personal information is organized before the user begins filling forms.
2. **Purpose-based onboarding:** The user's selected purposes determine which profile sections are recommended.
3. **Modular profile:** Identity, education, employment and assets remain separate but connected.
4. **Local-first privacy:** Personal values and routine file processing remain on the user's device wherever practical.
5. **Deterministic-first intelligence:** Rules handle clear cases; AI helps interpret ambiguous cases.
6. **Semantic consistency:** All components share a versioned field taxonomy.
7. **Requirements-driven preparation:** Files are transformed according to known constraints rather than arbitrary defaults.
8. **Original preservation:** Prepared files never silently replace the user's originals.
9. **Verified autofill:** FormFlow checks whether values were actually retained.
10. **User-controlled submission:** FormFlow never silently submits applications or makes legal declarations.
11. **Conservative tracking:** Drafts, attempted submissions and confirmed submissions remain distinct.
12. **Privacy by design:** The backend and AI service receive only the information they need.
13. **Graceful failure:** Unsupported fields and websites produce useful explanations and manual alternatives.
14. **Testable requirements:** Every major capability has acceptance criteria and automated tests.
15. **Incremental implementation:** Core profile, autofill, file preparation and application history are built as distinct modules.

---

# 28. Final Product Definition

**FormFlow is a privacy-focused, AI-powered application assistant that helps users maintain reusable personal information, fill supported online forms, prepare documents and images according to application requirements, and track their application history.**

The complete product consists of:

- A universal personal profile.
- Purpose-based education, career and other profile sections.
- A browser extension that understands and fills supported forms.
- An AI-assisted semantic interpretation service.
- A secure asset vault.
- A smart document and image preparation engine.
- An application history and tracking interface.
- A security architecture based on data minimization, encryption and controlled synchronization.

The central user journey is:

**Create an account → Build a reusable profile → Choose application purposes → Open a website → Match and fill information → Prepare required files → Review the completed form → Submit manually → Track the application.**

The long-term goal is to make repetitive applications substantially easier without requiring users to surrender control of their personal information.

This document should serve as the baseline for future product specifications, architecture decisions, implementation tasks, security reviews and acceptance tests. Any major deviation from these principles should be recorded as an explicit product or architecture decision before implementation.
