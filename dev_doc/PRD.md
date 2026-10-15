# FormFlow — Product Requirements Document (PRD)

**Product:** FormFlow  
**Document type:** Product Requirements Document  
**Version:** 1.0  
**Status:** Proposed baseline for development  
**Primary release strategy:** Web application → Desktop browser extension → Mobile integrations  
**Primary users:** University admission applicants and job seekers  
**Product principle:** Privacy-first, user-controlled form completion

---

# 1. Executive Summary

## 1.1 Product overview

FormFlow is a privacy-focused application assistant that helps users manage reusable personal information, prepare application documents, complete repetitive online forms, and track their applications.

Users enter their personal information once and reuse it across supported admission portals, job applications, scholarship applications, and other repetitive forms.

FormFlow combines a secure profile vault, structured personal records, document preparation, browser-based form intelligence, and application history.

The product will not attempt to automate every website or submit applications without user involvement. Its purpose is to reduce repetitive work while keeping users in control of their information and final submissions.

## 1.2 Problem statement

Applicants repeatedly enter the same information across different websites. They may need to:

- Enter personal information, addresses, and family details.
- Re-enter academic and employment histories.
- Upload photographs, signatures, CVs, certificates, and transcripts.
- Resize images or convert them into PDFs.
- Understand unfamiliar fields on different application portals.
- Track application progress across multiple organizations.
- Protect sensitive personal documents from unnecessary exposure.

Traditional browser autofill does not reliably understand all application-specific fields or prepare documents according to individual portal requirements.

FormFlow aims to solve these problems through reusable structured data, semantic field matching, smart document preparation, and privacy-focused storage.

## 1.3 Product objectives

1. Reduce repetitive manual data entry.
2. Make personal and application information reusable across supported forms.
3. Prepare documents according to detected or explicitly provided requirements.
4. Improve the accuracy and reviewability of form completion.
5. Give users control over their personal information and documents.
6. Provide a reliable record of applications and their statuses.
7. Establish a shared architecture that supports desktop and future mobile integrations.

## 1.4 Success criteria

The product should demonstrate that users can:

- Complete onboarding without having to populate every possible profile field.
- Save, edit, and reuse personal, academic, and employment records.
- Fill supported online forms with fewer manual interactions.
- Prepare common image and PDF formats without external conversion tools.
- Identify uncertain or missing information before completing a form.
- Track applications without falsely claiming that a submission succeeded.
- Access their profile on authorized devices without exposing plaintext vault contents to the backend.

Quantitative targets will be established during usability testing and the initial implementation phase.

---

# 2. Product Scope and Release Strategy

## 2.1 Phase 1 — Web application

The web application establishes the user account, profile, encrypted vault, document management, file preparation, and application history.

Included:

- Account registration and authentication.
- Email, Google sign-in, and mobile-number authentication, subject to provider and security integration.
- Profile onboarding.
- Purpose-based profile setup.
- Education and employment records.
- Personal asset and document management.
- Smart file preparation.
- Application history.
- Vault security, recovery, and device management.
- Responsive interface for desktop and mobile screens.

The responsive interface is not equivalent to full mobile autofill. Native mobile autofill and mobile browser integrations are later phases.

## 2.2 Phase 2 — Desktop browser extension

The extension connects the saved profile to supported application forms.

Included:

- Detecting accessible form fields.
- Identifying field semantics.
- Matching fields to saved profile records.
- Requesting missing information.
- Filling supported controls.
- Handling repeated fields and conditional sections.
- Detecting file-upload requirements.
- Attaching supported prepared files when technically possible.
- Verifying filled values.
- Highlighting uncertain or sensitive matches.
- Letting the user review and submit manually.
- Offering to record the application in My Applications.

## 2.3 Phase 3 — Mobile integrations

Mobile support expands through platform-specific implementations.

Potential capabilities:

- Android Autofill Service.
- iOS Safari Web Extension.
- Guided form completion and copy/paste fallbacks.
- Mobile-friendly document preparation.
- Device enrollment and encrypted vault synchronization.

These capabilities require platform-specific feasibility and compatibility testing.

## 2.4 Out of scope

The following are not part of the initial releases:

- Automatically submitting applications.
- Bypassing CAPTCHA, authentication challenges, or website security controls.
- Automatically accepting legal declarations or consent.
- Guaranteeing compatibility with every website.
- Automatically inventing missing personal or academic information.
- Claiming a submission succeeded merely because the user clicked a button.
- Sending the complete personal profile to an AI model for routine matching.
- Building a universal mobile autofill engine in the first release.
- Automatically scraping private information from unrelated accounts.
- Making decisions about admission, hiring, or eligibility on behalf of users.

---

# 3. Target Users and Personas

## 3.1 University admission applicant

**Needs**

- Reuse personal and family information.
- Maintain SSC, HSC, and other academic records.
- Reuse profile photos and signatures.
- Prepare images or PDFs according to portal requirements.
- Track applications across multiple universities.

**Main success outcome:** Complete repetitive admission forms more quickly and accurately.

## 3.2 Job seeker

**Needs**

- Reuse personal and contact information.
- Maintain education and employment histories.
- Store a CV, cover letters, and certificates.
- Complete recurring job application forms.
- Track applications and their outcomes.

**Main success outcome:** Spend less time re-entering information and more time reviewing relevant opportunities.

## 3.3 Scholarship or official-form applicant

**Needs**

- Maintain verified records and supporting documents.
- Reuse common details across multiple forms.
- Prepare files with strict size and format requirements.
- Review sensitive declarations carefully.

**Main success outcome:** Complete supported forms with fewer formatting errors and less repeated work.

---

# 4. Information Architecture

The primary navigation for the web application should be simple and task-oriented.

| Navigation item | Purpose |
|---|---|
| Dashboard | Overview, setup progress, and quick actions |
| My Profile | Core identity and contact details |
| My Records | Education, employment, skills, and purpose-specific information |
| My Documents | Photos, signatures, CVs, certificates, and other assets |
| File Preparation | Convert, resize, combine, and compress supported files |
| My Applications | Application records, statuses, notes, and history |
| Security & Devices | Vault, recovery, authorized devices, and synchronization |
| Settings | Account details, preferences, and account deletion |

The browser extension should have a smaller interface focused on the current form:

- Connect or unlock vault.
- Detect form.
- Review field matches.
- Fill supported fields.
- Prepare or attach files.
- Review results.
- Save application record.

---

# 5. Screen Specifications

## 5.1 Screen inventory

| ID | Screen | Release |
|---|---|---|
| SCR-001 | Landing page | Web |
| SCR-002 | Sign up / Sign in | Web |
| SCR-003 | Account verification | Web |
| SCR-004 | Vault setup and recovery | Web |
| SCR-005 | Onboarding wizard | Web |
| SCR-006 | Dashboard | Web |
| SCR-007 | My Profile | Web |
| SCR-008 | Education records | Web |
| SCR-009 | Employment and skills | Web |
| SCR-010 | My Documents | Web |
| SCR-011 | Smart File Preparation | Web |
| SCR-012 | My Applications | Web |
| SCR-013 | Application details | Web |
| SCR-014 | Security and devices | Web |
| SCR-015 | Account settings | Web |
| EXT-001 | Extension connection and unlock | Extension |
| EXT-002 | Form detection and analysis | Extension |
| EXT-003 | Field matching and review | Extension |
| EXT-004 | File preparation and attachment | Extension |
| EXT-005 | Fill results and application tracking | Extension |

## 5.2 Detailed screen requirements

### SCR-001 — Landing page

**Purpose:** Explain FormFlow and help new users understand its value.

**Elements**

- Product description.
- Benefits and supported workflows.
- Privacy and security explanation.
- Sign-up and sign-in actions.
- Supported-use-case examples.
- Compatibility and limitations disclosure.

**Acceptance criteria**

- A user can navigate to account creation or sign-in.
- Product claims accurately reflect implemented capabilities.
- The page does not claim universal website compatibility or absolute security.
- The user can understand that FormFlow assists with filling and does not autonomously submit applications.

### SCR-002 — Sign up / Sign in

**Purpose:** Create and authenticate a user account.

**Elements**

- Email-based authentication.
- Google sign-in.
- Mobile-number authentication.
- Verification and error states.
- Privacy policy and terms links.

**Acceptance criteria**

- The user can register through a supported authentication method.
- The system verifies ownership of the relevant email address or phone number before treating it as verified.
- Duplicate account and conflicting identity states are handled safely.
- OTP attempts and resend requests are rate-limited.
- Authentication recovery does not silently decrypt a zero-knowledge vault.
- Verification codes and authentication secrets are never logged in plaintext.

### SCR-003 — Account verification

**Purpose:** Verify the selected authentication method.

**Elements**

- Verification instructions.
- OTP or email verification flow.
- Resend option with cooldown.
- Change email or phone option, where supported.
- Error and expiry states.

**Acceptance criteria**

- Expired or invalid verification codes are rejected.
- Repeated attempts are rate-limited.
- The user receives clear instructions without exposing whether another person's account exists.
- Successful verification updates the account's verified status.

### SCR-004 — Vault setup and recovery

**Purpose:** Establish encrypted storage for personal information and documents.

**Elements**

- Vault setup explanation.
- Vault unlock credential or key setup.
- Recovery key generation.
- Recovery key confirmation.
- Device enrollment information.
- Clear warning about losing access.

**Acceptance criteria**

- The user receives a clear explanation of the difference between account authentication and vault recovery.
- Recovery material is generated using an appropriate cryptographically secure mechanism.
- Recovery material is not stored as readable plaintext on the backend.
- The user is asked to confirm that recovery material has been saved.
- Recovery is tested before the user relies on it.
- If recovery material is lost and no alternate recovery method exists, the system clearly explains the possibility of permanent data loss.
- The interface never promises that email or SMS verification alone can decrypt an inaccessible vault.

**Design dependency:** Finalize the vault encryption, key derivation, recovery, and multi-device key-sharing model before implementing this screen.

### SCR-005 — Onboarding wizard

**Purpose:** Collect essential information without overwhelming the user.

**Recommended steps**

1. Basic identity.
2. Family details.
3. Present address.
4. Permanent address.
5. Photo and signature.
6. Intended application purposes.
7. Optional relevant records.
8. Review and finish.

**Core fields**

- First name.
- Last name.
- Email.
- Mobile number.
- Date of birth.
- Father's name.
- Mother's name.
- Present address details.
- Permanent address details.
- Profile photo.
- Signature.

The permanent address step should include a “Same as present address” option.

The user then selects one or more intended purposes, such as:

- University admission.
- Job applications.
- Scholarships.
- Government or official forms.
- Other applications.

**Acceptance criteria**

- Users can complete onboarding in multiple sessions.
- Optional fields can be skipped.
- Previously entered information is preserved when navigating backward.
- Address fields are structured rather than stored only as a single unparsed string.
- The user can choose multiple purposes.
- Purpose selection recommends relevant records without creating duplicate copies of universal profile information.
- The user can finish onboarding with incomplete optional information.
- The user can review the information before saving.
- No information is silently inferred or fabricated.

### SCR-006 — Dashboard

**Purpose:** Provide a clear starting point for recurring tasks.

**Elements**

- Profile completion summary.
- Quick links to profile and documents.
- Recent applications.
- Suggested next actions.
- File preparation shortcut.
- Security status and vault-lock action.

**Acceptance criteria**

- The dashboard reflects current saved information.
- Completion indicators distinguish missing optional data from required security setup.
- The user can navigate directly to any major module.
- Sensitive personal values and document contents are not exposed unnecessarily in summary cards.
- Empty states explain how to get started.

### SCR-007 — My Profile

**Purpose:** Manage universal personal information.

**Sections**

- Identity.
- Contact details.
- Family information.
- Present address.
- Permanent address.
- Photo.
- Signature.

**Acceptance criteria**

- Users can create, view, update, and delete editable profile values.
- Changes are encrypted before persistence.
- Address copying between present and permanent addresses works predictably.
- The interface distinguishes verified and unverified contact information.
- Conflicting changes are surfaced rather than silently overwritten.
- The system preserves an original asset when a prepared image variant is generated.

### SCR-008 — Education records

**Purpose:** Maintain reusable academic information.

**Suggested fields**

- Institution.
- Qualification.
- Examination or degree.
- Group, major, or discipline.
- Board or awarding body.
- Passing year.
- Roll number and registration number, where relevant.
- GPA, grade, or result.
- Academic documents.

**Acceptance criteria**

- Users can add multiple education records.
- Each record can be edited or removed independently.
- Records can be associated with supporting documents.
- The interface supports different educational structures without assuming every user follows the same pathway.
- Sensitive identifiers are not unnecessarily shown in summaries or logs.
- The user can mark a record as reviewed or verified.

### SCR-009 — Employment and skills

**Purpose:** Maintain reusable job-application information.

**Suggested fields**

- Employment history.
- Employer and job title.
- Employment dates.
- Skills.
- Professional summary.
- CV/resume.
- Portfolio links.
- Certifications and experience documents.

**Acceptance criteria**

- Users can maintain multiple employment records.
- Users can maintain a reusable skills list.
- Users can associate documents with specific records.
- Users can mark a CV as their preferred version.
- Updating a profile does not silently rewrite historical application records.
- Optional fields can remain empty until needed.

### SCR-010 — My Documents

**Purpose:** Manage personal assets and supporting documents.

**Asset categories**

- Profile photo.
- Signature.
- CV/resume.
- Academic certificates.
- Marksheets and transcripts.
- Experience certificates.
- Training certificates.
- Cover letters.
- Portfolio documents.
- Other supporting files.

**Acceptance criteria**

- Users can import supported files from their device.
- Each asset has a name, category, file type, size, and creation or update metadata.
- Users can rename, categorize, replace, and delete assets.
- Unsupported or invalid files are rejected with a clear explanation.
- Original assets are preserved when prepared variants are created.
- Document contents remain encrypted at rest.
- Temporary processing copies are removed according to the defined retention policy.
- The interface clearly identifies the currently preferred photo, signature, or CV where applicable.

### SCR-011 — Smart File Preparation

**Purpose:** Prepare documents for application requirements.

**Supported operations**

- JPG/JPEG/PNG image conversion to PDF.
- Combine multiple supported images into a single PDF.
- Resize and crop profile photos.
- Resize signatures without distorting their proportions.
- Compress supported images and PDFs.
- Convert supported image formats.
- Preview output and validate size and format.

**User journey**

1. Select an original asset or import a file.
2. Choose an operation or provide target requirements.
3. Review detected or entered requirements.
4. Preview the prepared result.
5. Save the result as a separate variant.
6. Use the prepared variant in an application.

**Acceptance criteria**

- The original file is never destructively replaced by default.
- Image conversion produces a valid output file.
- Combined PDFs preserve the selected image order.
- Compression does not silently exceed a user-specified quality threshold.
- Signature proportions are preserved.
- Known file-size and dimension constraints are validated before completion.
- Unknown requirements are clearly labelled as unknown.
- The user can cancel a preparation operation without losing the original.
- Processing failures leave the original asset available.
- Routine file processing does not require uploading the document to an AI service.
- The system does not claim that a file meets a portal's requirements when those requirements could not be established.

### SCR-012 — My Applications

**Purpose:** Maintain a useful record of application activity.

**List fields**

- Application title.
- Organization.
- Category.
- Application URL.
- Date started.
- Date submitted, if confirmed.
- Current status.
- Last updated.

**Filters**

- Category.
- Status.
- Organization.
- Date range.

**Acceptance criteria**

- Users can create application records manually.
- The system can offer to create a record from an extension workflow.
- Users can search and filter saved applications.
- A record is not automatically marked Submitted merely because a form was filled.
- Submission status is clearly distinguished from an unconfirmed submission.
- Users can edit or delete records.
- Empty states explain how to add an application.

### SCR-013 — Application details

**Purpose:** View and manage one application's history.

**Elements**

- Application metadata.
- Organization and URL.
- Status.
- Timeline.
- Notes.
- Relevant document references.
- Edit and delete actions.

**Acceptance criteria**

- The user can update status manually.
- Timeline events include timestamps and event descriptions.
- The system distinguishes user-confirmed events from automatically detected events.
- The system does not infer acceptance or rejection without reliable evidence.
- Sensitive form answers are not copied into application history by default.
- Deleting an application removes its associated metadata according to the retention policy.
- Application records remain accessible across authorized devices when encrypted synchronization is enabled.

### SCR-014 — Security and devices

**Purpose:** Give users visibility and control over vault access.

**Elements**

- Vault lock and unlock.
- Recovery status.
- Authorized devices.
- Device revocation.
- Synchronization status.
- Security notifications.
- Recovery instructions.

**Acceptance criteria**

- Users can review authorized devices.
- Users can revoke a device.
- Revocation prevents future access and synchronization after the revocation takes effect.
- The interface explains that revocation cannot guarantee deletion of plaintext already copied from a previously authorized or compromised device.
- Synchronization failures are visible and do not silently discard unsynchronized changes.
- The user can lock the vault.
- Recovery and device changes require appropriate reauthentication.
- The backend cannot retrieve a user's plaintext profile or documents under the intended zero-knowledge architecture.

### SCR-015 — Account settings

**Purpose:** Manage account preferences and lifecycle.

**Elements**

- Account email and phone.
- Verification status.
- Authentication methods.
- Preferences.
- Privacy information.
- Account deletion.

**Acceptance criteria**

- Users can update supported account details.
- Changes to email or phone require appropriate verification.
- Account deletion requires clear confirmation.
- The deletion flow explains the effects on account metadata, encrypted backups, and other devices.
- Backup-retention limitations are disclosed accurately.
- Account deletion does not falsely promise immediate removal from every backup if deletion is asynchronous.

---

# 6. Desktop Browser Extension Requirements

## 6.1 EXT-001 — Connection and unlock

**Purpose:** Connect the extension to the user's authorized FormFlow vault.

**Acceptance criteria**

- The extension clearly displays its connection and vault-lock status.
- The user must authorize access to the appropriate vault.
- The extension does not expose saved values while the vault is locked.
- Authentication or synchronization failures are shown clearly.
- The extension requests only the browser permissions necessary for its supported workflows.
- Sensitive information is not included in diagnostic logs.

## 6.2 EXT-002 — Form detection and analysis

**Purpose:** Identify accessible fields and understand their likely meanings.

The extension should extract available information from:

- Field labels.
- Associated labels.
- Accessible names.
- Input types.
- Placeholder text.
- Select options.
- Validation messages.
- Nearby instructions.
- File input attributes.
- Relevant page structure.

**Acceptance criteria**

- The extension identifies supported text, email, telephone, date, select, radio, checkbox, and file controls.
- Each field is assigned a detected control type and a candidate semantic type.
- Unknown fields remain unclassified rather than receiving invented mappings.
- Conditional fields are re-evaluated when the form changes.
- Dynamic forms can be rescanned.
- The extension does not bypass CAPTCHA or other access controls.
- The extension can stop analysis and explain unsupported page structures.

## 6.3 EXT-003 — Field matching and review

**Purpose:** Match detected form fields to saved profile values.

**Matching order**

1. Deterministic rules and known field labels.
2. Field dictionaries and contextual heuristics.
3. AI assistance for ambiguous semantics, where enabled.
4. Confidence and sensitivity checks.
5. User review where needed.

**Acceptance criteria**

- A field is not filled from an uncertain match merely because a value exists.
- Missing information is identified.
- Multiple plausible matches are presented for user selection.
- Conflicting values are surfaced.
- Sensitive fields receive additional review.
- Legal declarations and consent controls require explicit user action.
- Passwords, OTPs, and security challenges remain user-controlled.
- AI requests use minimal information and do not include personal profile values by default.
- The user can approve or reject proposed mappings.

## 6.4 EXT-004 — Fill fields and prepare files

**Purpose:** Complete supported fields and prepare required assets.

**Acceptance criteria**

- Only approved fields are filled.
- Supported controls receive values through appropriate browser interaction mechanisms.
- The extension verifies the resulting field values when possible.
- Invalid or rejected values are reported.
- File requirements are derived from accessible page information where possible.
- The user can select or generate a prepared asset.
- File attachment is attempted only when the browser and website allow it.
- The extension verifies attachment where possible and otherwise reports that manual verification is required.
- Unsupported custom upload controls receive a guided fallback.
- The extension never claims universal compatibility.

## 6.5 EXT-005 — Review results and record applications

**Purpose:** Let users review the completed form and optionally save application metadata.

**Acceptance criteria**

- The extension summarizes successfully filled, skipped, and failed fields.
- The user can return to any field requiring correction.
- The extension does not submit the application.
- The user can choose to create an application record.
- The application URL and title are captured only where available and permitted.
- A record is marked Submission Unconfirmed until the user confirms submission or reliable evidence establishes the outcome.
- The user can dismiss the workflow without creating an application record.

---

# 7. Core User Journeys

## Journey 1 — Registration and profile setup

**Goal:** Create a secure account and establish a reusable profile.

1. The user opens FormFlow.
2. The user selects email, Google, or mobile-number registration.
3. The authentication method is verified.
4. The user sets up the encrypted vault.
5. FormFlow explains recovery and generates recovery material.
6. The user confirms that recovery material has been saved.
7. The onboarding wizard collects core identity details.
8. The user adds family information and addresses.
9. The user uploads a photo and signature, if available.
10. The user selects admission, job applications, or other purposes.
11. FormFlow recommends relevant optional records.
12. The user skips or completes optional information.
13. The user reviews and saves the profile.
14. The dashboard displays the next recommended actions.

**Acceptance outcome:** The user has an authenticated account and an initialized vault with saved core information. Optional records can be completed later.

## Journey 2 — Complete an admission application

**Goal:** Reuse personal and academic information.

1. The user opens an admission website.
2. The user opens the FormFlow extension.
3. The extension detects supported form fields.
4. FormFlow matches identity, contact, family, and academic fields.
5. The extension presents ambiguous or missing information.
6. The user reviews and approves the proposed mappings.
7. FormFlow fills supported fields.
8. The user checks the results.
9. The website requests a photo and signature.
10. FormFlow identifies the relevant assets and prepares copies if needed.
11. The user reviews file requirements and attaches the files where supported.
12. The user completes unsupported fields manually.
13. The user reviews the entire application.
14. The user submits it manually.
15. The user confirms submission in FormFlow.
16. FormFlow records the application and timestamp.

**Acceptance outcome:** Supported fields are completed accurately, uncertain fields are reviewed, and the application is tracked without claiming an unverified submission.

## Journey 3 — Apply for a job

**Goal:** Reuse professional records and CVs.

1. The user opens a job application.
2. The extension detects personal and employment fields.
3. FormFlow matches the user's profile, employment records, skills, and preferred CV.
4. The extension asks about missing or ambiguous details.
5. The user reviews and approves the matches.
6. FormFlow fills supported fields.
7. The user selects a CV or other supporting document.
8. FormFlow prepares a compatible copy if required.
9. The user reviews all information.
10. The user submits manually and optionally confirms the submission.
11. FormFlow creates or updates the application record.

**Acceptance outcome:** Professional information is reused without silently inventing experience, skills, salary expectations, or other application-specific answers.

## Journey 4 — Prepare a profile photo or signature

**Goal:** Produce a file that matches a known application requirement.

1. The user opens Smart File Preparation.
2. The user selects the original photo or signature.
3. The user enters target dimensions, aspect ratio, format, or size limit—or chooses a known requirement.
4. FormFlow displays the transformation plan.
5. The user previews the result.
6. FormFlow validates known constraints.
7. The user saves the result as a separate asset variant.
8. The original remains unchanged.

**Acceptance outcome:** A prepared copy is available, and any unverified requirements are clearly identified.

## Journey 5 — Track applications

**Goal:** Maintain an accurate application history.

1. The user opens My Applications.
2. The user creates a record or accepts an extension suggestion.
3. FormFlow stores minimal metadata.
4. The user updates the status as progress occurs.
5. The user adds notes or timeline events.
6. The user filters applications by category, organization, or status.
7. The user edits or deletes records when necessary.

**Acceptance outcome:** The application history remains useful without requiring storage of every sensitive form answer.

## Journey 6 — Recover access to the vault

**Goal:** Regain access while protecting encrypted data.

1. The user signs in using an available authentication method.
2. FormFlow detects that the vault cannot currently be unlocked.
3. The user selects the supported recovery method.
4. FormFlow validates the recovery material or uses the configured recovery protocol.
5. The user restores access on the authorized device.
6. The system re-establishes synchronization where applicable.

**Acceptance outcome:** Recovery follows the implemented cryptographic model. If the required key material is permanently lost, FormFlow communicates the actual recovery limitation rather than promising an impossible restoration.

---

# 8. User Stories and Acceptance Criteria

The following stories are the baseline product backlog. Each story should be independently testable wherever practical.

## Epic A — Account and authentication

### AUTH-001 — Register an account

**User story:** As a new user, I want to create a FormFlow account so that I can access my saved profile.

**Acceptance criteria**

- Given a valid registration method, when I complete registration, then my account is created.
- Given an unverified email or phone number, when verification is required, then the system limits protected account operations until verification succeeds.
- Given invalid or expired verification information, then the system rejects it and explains how to retry.
- The backend stores authentication information separately from encrypted vault contents.

### AUTH-002 — Sign in

**User story:** As a returning user, I want to sign in securely so that I can access my account.

**Acceptance criteria**

- A supported authentication method allows a valid user to sign in.
- Invalid credentials produce a safe error.
- Repeated failures are rate-limited.
- Account authentication alone does not automatically expose vault plaintext.

### AUTH-003 — Set up vault recovery

**User story:** As a user, I want a recovery method so that I can restore my encrypted information if I lose access to a device.

**Acceptance criteria**

- Recovery setup explains its purpose and limitations.
- Recovery material is generated securely.
- The user confirms that the material has been saved.
- The server does not retain a readable copy of a zero-knowledge recovery secret.
- The implemented recovery flow is tested before release.

## Epic B — Onboarding and profile

### PROF-001 — Complete core onboarding

**User story:** As a new user, I want to enter essential personal information once so that I can reuse it later.

**Acceptance criteria**

- The wizard includes name, email, phone, date of birth, family details, and addresses.
- Present and permanent addresses are supported.
- The permanent address can be copied from the present address.
- The user can skip optional fields.
- Progress is saved securely.
- No field is populated with invented information.

### PROF-002 — Choose application purposes

**User story:** As a user, I want to select the types of applications I expect to complete so that FormFlow can recommend relevant profile records.

**Acceptance criteria**

- The user can select multiple purposes.
- Recommendations correspond to selected purposes.
- Changing a purpose does not delete existing profile information.
- The user can change their selections later.

### PROF-003 — Manage profile details

**User story:** As a user, I want to update my personal information so that FormFlow uses current values.

**Acceptance criteria**

- Profile values can be created, viewed, updated, and deleted.
- Changes are persisted securely.
- Conflicting values are surfaced.
- Verified information is not silently overwritten by unverified data.

### PROF-004 — Manage education records

**User story:** As an admission applicant, I want to store multiple education records so that I can reuse them in admission forms.

**Acceptance criteria**

- The user can create multiple records.
- Each record can be edited or removed.
- Records can be associated with documents.
- FormFlow can distinguish missing information from an explicitly entered zero or empty value.

### PROF-005 — Manage employment and skills

**User story:** As a job seeker, I want to maintain employment history and skills so that I can reuse them in job applications.

**Acceptance criteria**

- The user can manage multiple employment records.
- Skills can be added and removed.
- The user can select a preferred CV.
- FormFlow does not create unverified work experience or skills.

## Epic C — Documents and file preparation

### FILE-001 — Manage assets

**User story:** As a user, I want to organize my photos, signatures, and documents so that I can find them when an application requires them.

**Acceptance criteria**

- Supported assets can be imported and categorized.
- Metadata is displayed.
- Assets can be renamed, replaced, and deleted.
- Original files are preserved when variants are generated.
- Invalid files are rejected safely.

### FILE-002 — Convert images into PDFs

**User story:** As a user, I want to convert one or more images into a PDF so that I can upload them to portals that require PDF documents.

**Acceptance criteria**

- A supported image can be converted into a valid PDF.
- Multiple images can be combined in user-selected order.
- The output is previewable.
- Conversion errors are reported.
- The original images remain unchanged.

### FILE-003 — Resize and compress files

**User story:** As a user, I want to prepare images and documents to meet known upload limits.

**Acceptance criteria**

- The user can enter supported target constraints.
- The system previews the result before saving.
- The output is validated against known constraints.
- Image aspect ratio is preserved unless the user explicitly chooses a crop.
- The system does not claim compliance with unknown requirements.

### FILE-004 — Prepare files for extension upload

**User story:** As an applicant, I want FormFlow to prepare the right file for an upload field so that I do not need to use separate conversion tools.

**Acceptance criteria**

- The extension identifies available file requirements when accessible.
- The user reviews the selected asset and any generated variant.
- Attachment is attempted only when technically supported.
- The system verifies attachment when possible.
- Unsupported upload controls receive a manual fallback.

## Epic D — Browser extension and autofill

### FILL-001 — Detect supported fields

**User story:** As a user, I want FormFlow to identify fields on the current page so that it can suggest relevant saved information.

**Acceptance criteria**

- Supported accessible controls are detected.
- Each field receives a control type and candidate semantic type.
- Unknown fields are not assigned fabricated meanings.
- Dynamic form changes can trigger rescanning.
- Unsupported controls are reported where relevant.

### FILL-002 — Match fields to profile values

**User story:** As a user, I want FormFlow to match form fields with my saved records so that I do not have to enter the same information repeatedly.

**Acceptance criteria**

- High-confidence supported matches are proposed for filling.
- Ambiguous matches require review.
- Missing values are identified.
- Sensitive and legal fields follow stricter policies.
- AI assistance does not require sending plaintext profile values by default.

### FILL-003 — Review and fill

**User story:** As a user, I want to review proposed values before filling the form so that I remain in control of my information.

**Acceptance criteria**

- The user can approve or reject proposed values.
- Only approved values are filled.
- The extension verifies resulting values when possible.
- Failed fills are reported.
- The extension never submits the form automatically.

### FILL-004 — Handle unsupported forms

**User story:** As a user, I want a fallback when a website cannot be filled directly so that I can still complete the application.

**Acceptance criteria**

- The extension explains the limitation.
- It offers appropriate manual guidance or copy actions.
- It does not bypass website security controls.
- It does not claim success for actions that were not verified.

## Epic E — Application history

### APP-001 — Create an application record

**User story:** As an applicant, I want to record an application so that I can track it later.

**Acceptance criteria**

- The user can create a record manually.
- The user can accept a record suggestion from the extension.
- The record includes available title, organization, category, URL, and start date.
- Missing metadata can be completed manually.

### APP-002 — Track status

**User story:** As an applicant, I want to update an application's status so that I know where it stands.

**Acceptance criteria**

- Supported statuses include Draft, Ready to Submit, Submission Unconfirmed, Submitted, Under Review, Accepted, Rejected, and Withdrawn.
- The user can update the status.
- The submitted date is stored only when submission is confirmed.
- Status history includes timestamps.
- FormFlow does not infer acceptance or rejection.

### APP-003 — Search and filter applications

**User story:** As a user with multiple applications, I want to search and filter my records so that I can find an application quickly.

**Acceptance criteria**

- The user can search by application title or organization.
- The user can filter by category, status, and date.
- Results accurately reflect the current stored records.
- Empty results provide a clear message.

## Epic F — Security and privacy

### SEC-001 — Protect vault contents

**User story:** As a privacy-conscious user, I want my profile and documents encrypted so that the backend cannot read my personal information.

**Acceptance criteria**

- Vault content is encrypted before persistent storage or synchronization.
- Encryption keys are not exposed to the backend in plaintext.
- The implementation uses vetted cryptographic libraries and authenticated encryption.
- Plaintext personal information is excluded from application logs and analytics.
- The system documents any metadata that remains visible to the service.

### SEC-002 — Manage authorized devices

**User story:** As a user, I want to review and revoke devices so that I can control where my vault is accessible.

**Acceptance criteria**

- Authorized devices are listed.
- The user can revoke a device.
- Revocation blocks future access and sync according to the protocol.
- The system explains limitations concerning data already copied to a compromised device.

### SEC-003 — Delete profile and account data

**User story:** As a user, I want to delete my information so that I can stop using FormFlow without retaining unnecessary personal data.

**Acceptance criteria**

- Users can delete selected profile fields and assets.
- Users can delete application records.
- Account deletion has a clear confirmation flow.
- Deletion effects on backups and other devices are explained.
- The system reports completion only when the applicable deletion operation has succeeded.

### SEC-004 — Minimize AI data exposure

**User story:** As a user, I want FormFlow to minimize the personal information sent to AI services so that form understanding does not require sharing my entire profile.

**Acceptance criteria**

- Routine field classification can operate on field semantics without profile values.
- AI requests are minimized and reviewed against the data-handling policy.
- The system does not include entire profiles or documents by default.
- AI output is treated as a suggestion and validated before it affects the form.
- Provider retention and processing terms are reviewed before production use.

## Epic G — Reliability and usability

### UX-001 — Provide clear error states

**User story:** As a user, I want clear explanations when something fails so that I know how to recover.

**Acceptance criteria**

- Errors explain the failed action and a safe next step.
- Sensitive values are not included in error messages unnecessarily.
- Failed file preparation preserves the original asset.
- Failed synchronization does not silently discard changes.

### UX-002 — Support responsive screens

**User story:** As a user, I want to manage my profile from different screen sizes so that I can use FormFlow conveniently.

**Acceptance criteria**

- Core web screens remain usable at common desktop, tablet, and mobile viewport sizes.
- Forms, dialogs, file previews, and navigation adapt to smaller screens.
- Responsive web support does not imply native mobile autofill support.
- Keyboard navigation and accessible labels are provided for core interactions.

---

# 9. Data Model Requirements

The following entities are logical requirements, not a final database schema.

| Entity | Purpose | Key relationships |
|---|---|---|
| UserAccount | Account identity and authentication references | Has devices and vault metadata |
| VaultMetadata | Vault version, encryption parameters, recovery status metadata | Belongs to account |
| Device | Authorized device and synchronization state | Belongs to account |
| Profile | Universal personal information | Belongs to vault |
| ProfileFieldMetadata | Field provenance, verification, and update metadata | References profile fields |
| ApplicationPurpose | Selected application categories | Associated with profile |
| EducationRecord | Academic history | Belongs to profile |
| EmploymentRecord | Employment history | Belongs to profile |
| Skill | Reusable skills | Associated with profile |
| Asset | Original or prepared file metadata | Belongs to vault |
| AssetVariant | Prepared version of an asset | References original asset |
| Application | Application metadata and current status | Belongs to vault |
| ApplicationEvent | Status and activity timeline | Belongs to application |
| FormMapping | Candidate semantic mappings and outcomes | Used by extension workflow |
| SyncMetadata | Encrypted sync version and conflict metadata | Associated with device and vault |

## 9.1 Data ownership rules

- Universal personal information should have a single canonical record.
- Purpose-specific information should reference reusable records where possible.
- Application-specific answers must not automatically overwrite the permanent profile.
- Prepared files must reference their original assets.
- Application history should store minimal metadata by default.
- Sensitive records should remain inside the encrypted vault where practical.
- Backend metadata must be explicitly documented so a zero-knowledge claim remains accurate.

## 9.2 Field provenance

Where useful, each profile value should include provenance such as:

- User entered.
- Imported by the user.
- Extracted from a document.
- Suggested by FormFlow.
- Verified by the user.

Document extraction or AI suggestions must not silently replace verified information.

---

# 10. Non-Functional Requirements

## 10.1 Security

- Use established authentication providers or proven authentication libraries.
- Use vetted cryptographic libraries and authenticated encryption.
- Separate authentication secrets from vault encryption keys.
- Apply least-privilege permissions to the browser extension.
- Avoid collecting sensitive browser page data unnecessarily.
- Exclude plaintext profile values, documents, recovery secrets, and OTPs from logs.
- Implement secure device revocation and session management.
- Test account recovery, vault recovery, backup restoration, and deletion.
- Conduct security and privacy review before public launch.

## 10.2 Privacy

- Keep routine profile processing local where practical.
- Encrypt data before cloud backup or synchronization.
- Minimize AI input to the information required for the current operation.
- Clearly explain what metadata the backend can see.
- Provide deletion and export options according to the product's data policy.
- Do not claim zero-knowledge security unless the complete implementation supports that claim.

## 10.3 Performance

Initial targets to validate during testing:

- Standard profile screens should feel responsive under normal network conditions.
- Common local file preparation should provide visible progress and avoid freezing the interface.
- Form detection should handle ordinary supported pages without excessive repeated scans.
- Large file operations should be cancellable where technically practical.
- Vault synchronization should avoid unnecessary transfer of unchanged data.

## 10.4 Accessibility and usability

- Core workflows should support keyboard navigation.
- Controls should have meaningful accessible names.
- Errors should be readable and actionable.
- Important actions should not depend solely on color.
- Onboarding should permit optional information to be completed later.
- Security explanations should use clear language rather than unexplained cryptographic terminology.

## 10.5 Compatibility

- Define a supported desktop browser and operating-system matrix before extension development.
- Test common native and custom form controls.
- Maintain a documented list of known limitations.
- Test dynamic forms, validation errors, repeated fields, and file-upload widgets.
- Mobile browser and native autofill compatibility must be validated separately.

---

# 11. Release Acceptance Gates

A release should not be considered complete merely because its screens are implemented.

## Gate A — Web foundation

- [ ] Account registration and verification work.
- [ ] Vault initialization and recovery have passed tests.
- [ ] Core onboarding and profile management work.
- [ ] Education and employment records work.
- [ ] Assets can be imported and managed.
- [ ] Basic image-to-PDF and multi-image PDF creation work.
- [ ] My Applications supports CRUD, filtering, and status history.
- [ ] Data export, deletion, and backup-retention behavior are documented.
- [ ] Security review has addressed key management and plaintext exposure.

## Gate B — Desktop extension

- [ ] Supported controls are detected reliably in test fixtures.
- [ ] Semantic matching has measured precision and recall.
- [ ] Ambiguous mappings require user review.
- [ ] Dynamic forms and common validation states are tested.
- [ ] Fill operations are verified where possible.
- [ ] File attachment works on a documented set of supported websites.
- [ ] Unsupported forms provide a useful fallback.
- [ ] The extension never automatically submits forms.
- [ ] Browser permissions and data handling have been reviewed.

## Gate C — Mobile readiness

- [ ] Core web screens are responsive.
- [ ] Shared profile and field taxonomy interfaces are stable.
- [ ] Vault synchronization and device enrollment are tested.
- [ ] Android Autofill Service feasibility and behavior have been validated.
- [ ] iOS Safari extension feasibility and behavior have been validated.
- [ ] Mobile fallback flows have been tested on real devices.

---

# 12. Product Metrics

Metrics should measure usefulness and reliability without collecting unnecessary personal information.

| Metric | What it measures |
|---|---|
| Onboarding completion rate | Whether users can establish a usable profile |
| Time to first useful autofill | Time from setup to a successful form-filling experience |
| Field mapping precision | How often proposed matches are correct |
| Field mapping coverage | Proportion of supported fields with a usable mapping |
| Verified fill success rate | Proportion of attempted fills that are confirmed successful |
| Manual correction rate | How often users need to correct proposed values |
| File preparation success rate | Proportion of supported transformations completed successfully |
| Application tracking adoption | How often users maintain application records |
| Vault recovery success rate | Whether recovery works for supported recovery scenarios |
| Data-loss incidents | Failures that cause loss of profile or synchronization data |

Do not collect raw field values, documents, or complete application content merely to calculate these metrics. Prefer aggregate, privacy-preserving measurements.

---

# 13. Key Risks and Mitigations

| Risk | Mitigation |
|---|---|
| Websites use incompatible custom controls | Maintain a compatibility matrix and guided fallback |
| Incorrect semantic matching | Confidence thresholds, review, and measurable test datasets |
| Accidental overwriting of profile data | Provenance, conflict detection, and explicit approval |
| File preparation creates invalid output | Validate outputs and preserve originals |
| Browser extension permissions are too broad | Least-privilege design and security review |
| Recovery key loss causes permanent data loss | Clear recovery design, user education, and tested backup options |
| Cross-device sync causes conflicts | Versioned sync, conflict detection, and recovery testing |
| AI provider receives sensitive information | Minimize requests and exclude personal values by default |
| False submission status | Require confirmation or reliable evidence |
| Mobile support is assumed to be universal | Implement platform-specific integrations and test actual behavior |

---

# 14. Dependencies and Decisions Required Before Implementation

These decisions affect the architecture and should be resolved early.

1. **Vault and recovery model:** Define key generation, derivation, wrapping, recovery, and device enrollment.
2. **Synchronization model:** Decide how encrypted vault data is backed up, versioned, restored, and revoked across devices.
3. **Authentication providers:** Choose supported email, Google, and mobile-number authentication mechanisms.
4. **Initial browser support:** Select the desktop browsers and versions supported by the first extension release.
5. **Extension-to-vault integration:** Define how the extension obtains authorized access without exposing plaintext vault data unnecessarily.
6. **File preparation limits:** Establish supported input formats, file sizes, PDF operations, and quality constraints.
7. **AI routing and privacy:** Define when AI is necessary, which metadata may be sent, and which providers are permitted.
8. **Application history semantics:** Define exactly when statuses can change automatically and which require user confirmation.
9. **Data retention and deletion:** Define treatment of encrypted backups, device caches, temporary files, and account metadata.
10. **Testing strategy:** Select representative admission and job portals for controlled compatibility tests.

---

# 15. Recommended Implementation Order

The PRD should translate into development milestones in this order:

**Milestone 1 — Product foundation**
- Architecture and data model.
- Authentication.
- Vault security and recovery design.
- Shared profile schema.

**Milestone 2 — Core web experience**
- Onboarding.
- Profile and purpose management.
- Education and employment records.
- Dashboard and settings.

**Milestone 3 — Documents and applications**
- Asset management.
- Smart File Preparation.
- My Applications.
- Encryption, deletion, and recovery testing.

**Milestone 4 — Extension foundation**
- Shared semantic field taxonomy.
- DOM extraction and control classification.
- Vault integration.
- Mapping review interface.

**Milestone 5 — Reliable autofill**
- Fill operations.
- Dynamic form handling.
- File attachment.
- Verification, error handling, and compatibility tests.

**Milestone 6 — Production readiness**
- Security review.
- Usability testing.
- Performance and reliability testing.
- Privacy policy and limitations disclosure.
- Release acceptance review.

**Milestone 7 — Mobile integrations**
- Responsive web refinements.
- Android Autofill Service.
- iOS Safari extension.
- Mobile fallback workflows.
- Device synchronization and platform-specific security testing.

---

# 16. Definition of Done

A feature is complete only when:

- Its intended user journey works end to end.
- Acceptance criteria pass automated or documented manual tests.
- Loading, empty, success, failure, and recovery states are implemented.
- Sensitive data is handled according to the vault and privacy design.
- Accessibility and responsive behavior have been checked where applicable.
- Logs and analytics do not expose prohibited personal data.
- Known compatibility limitations are documented.
- Relevant security and regression tests pass.
- User-facing claims accurately describe actual behavior.

## Final product definition

FormFlow is a privacy-focused assistant that allows users to maintain a reusable personal profile, prepare application documents, fill supported online forms through a desktop browser extension, and track their application history.

The web application establishes the secure foundation. The desktop extension brings profile reuse into real application workflows. Mobile integrations follow after the shared architecture, vault security, and form intelligence have been validated.

The product should prioritize **correctness, transparency, and user control over maximum automation**. Its success depends not on claiming that every form can be completed automatically, but on reliably reducing repetitive work while keeping personal information protected and users in control of their applications.