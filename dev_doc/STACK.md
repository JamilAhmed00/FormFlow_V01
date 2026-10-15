# FormFlow — Technical Implementation & Scalable Architecture

For FormFlow, I recommend a TypeScript-first, local-first architecture with a browser extension, a secure encrypted vault, and a lightweight backend for accounts and encrypted synchronization.

The most important architectural decision is this: FormFlow should work without sending a user's personal profile or documents to your backend or an AI provider. The client should handle personal data and autofill locally wherever possible. That supports your privacy goal while keeping the backend easier to scale.

We should design for three concerns from the beginning:

1. Product functionality: reusable profiles, purpose-specific information, intelligent autofill, file preparation, and application tracking.
2. Security: client-side encryption, secure extension boundaries, recovery, device authorization, and minimal data collection.
3. Scalability: independent backend services, stateless APIs, background jobs when needed, and the ability to add users without redesigning the system.

## 1. Recommended technology stack

[TypeScript Logo Icons for Web and App Development](https://images.openai.com/static-rsc-4/Pbx8y0BkFx2FGL0rrQv12qhf7VCxQjJIxX5qzDbXfFc_2r0281FTrrhYxXs3oeHVXGVOioNH7bLrVixEVSASmJ_wcEhF77ZXSHxlzycjvcxjtXJBHHMnjUNYoQ5lFVUZW7gTZd7KpLmODFhOjJ9wCXSRFqfHbE7Oj1PItTwTFWk?purpose=inline)

TypeScript — primary language

Use it across the browser extension, frontend, backend, and shared schemas. This reduces context switching and lets you reuse validation rules and field definitions.

Shared types, validation, API contracts, browser logic

[React Logo Vector PNG | Modern JavaScript UI Library Emblem | Atomic-inspired Frontend Framework Symbol | Minimal Cyan Tech Icon - freepng](https://images.openai.com/static-rsc-4/v_YRxkVgaIO4SDeoNvs8wqFWCUPPpZZsL5kVx_ktDQiKtZgMAHiSkxHMJjDkyVuTICNI24RF-lwOIJxaeydWu09nWdyQFsirfUWfJani7GSpYOfLBE-LNBdDDc_8acLBouV10tSEh5cWrc3WFWUieGkP2unLzBMX37Q6Sq2WqGs?purpose=inline)

React + Next.js — application interface

Build account management, onboarding, profile editing, vault settings, application history, and the product dashboard. Use React for the extension interface as well, where useful.

Next.js, React, TypeScript

[Estensioni Chrome: come bloccare quelle troppo affamate di dati | IlSoftware.it](https://images.openai.com/static-rsc-4/SOzFcBKrHJ2YuanPxUbojQRIQZTTD0tsewV8LkDVpR6hCa0hPhZ06q3PuBO2-jNIaICoXv9WRUK1MnoP-eFdmcZ3Uwhmie49by-_QKAeZQFYNNAmQ_Q4HFuzTKqQvOAwSGQA3V55_wMIBdBp-nxyZt7wjdv_W9RFlEk_IIDCBT4?purpose=inline)

Chrome/Chromium extension — form automation

Use Manifest V3, a background service worker, content scripts, a popup, and an options/onboarding interface. Design the extension around least-privilege host access.

DOM inspection, field mapping, autofill, verification

[Fastify Logo PNG Vector (SVG) Free Download](https://images.openai.com/static-rsc-4/P_eNOOrzTBu7GVCyRISNC8y7virkrC7v1UwJz0MN_cOMUUUWbfDEKcpqBwXFv_okHXYTUwMDVUBGsU0E-Z6RwreNFIM3jn4Mv8BQkfmkpn8c3ygprgSZY1VNsxCd-D5ETUy82_y5j9dNN-58_3B2D3k7WPhRhJd37_TpemaL-2s?purpose=inline)

Node.js + Fastify — backend API

A lightweight API for account integration, device registration, encrypted sync, vault metadata, and subscription management. NestJS is an alternative if you prefer a more opinionated structure for a larger team.

REST APIs, authorization, rate limiting, OpenAPI

[Docker Hub Container Image Library | App Containerization](https://images.openai.com/static-rsc-4/Pole4xk5FkyhFJxxWDBh3yHjF1pQlxteoZyEQA0ykJQSPxLpLcdTrKWhkIQ2-SeCQp9ObINiyVMBFzoUkAM9P9RUAWW761nUuSEzxGOPsF9Keb0OX7HGw8IiQD84tSEoRfxnWrmYPSxGM1Bq9IBWZrT-EGb7Ta0uoZ1t6-qsVoY?purpose=inline)

PostgreSQL — application metadata

Store account references, registered devices, subscription records, sync versions, and operational metadata. Do not store plaintext profiles or documents.

Managed PostgreSQL, migrations, backups

[SubtleCrypto API 简明教程 | ShouChen's Blog](https://images.openai.com/static-rsc-4/vihas0ukVgYtx3EltxPaSXWztd6JLAAzsFIMGITSmWB7VcetCckH6QCBbPjJWmO5MRtbKf0n1fptdPsaLA-0Av-FARmkKKtC_z253Bf0EzTFiCx2esHOYQ-UVTd0fwZNU7sTWhXLRUiVouKJeZFJeyyLhz3vOEMBmwSpgD8Kkig?purpose=inline)

Client-side cryptography — encrypted vault

Use a vetted cryptographic implementation, versioned key envelopes, authenticated encryption, and a tested recovery flow. Keep encryption and decryption on the trusted client.

Web Crypto API or a carefully selected vetted library

Additional technologies I would use:

| Need                         | Recommendation                             |
| ---------------------------- | ------------------------------------------ |
| Frontend styling             | Tailwind CSS                               |
| Form validation              | Zod                                        |
| Database access              | Drizzle ORM or Prisma                      |
| API contracts                | OpenAPI + generated TypeScript types       |
| File processing              | Canvas / OffscreenCanvas + `pdf-lib`       |
| Unit and integration testing | Vitest                                     |
| Browser automation tests     | Playwright                                 |
| Extension-specific testing   | Playwright plus real-browser manual tests  |
| Error monitoring             | Privacy-configured Sentry or an equivalent |
| Deployment                   | Docker + managed cloud services            |
| CI/CD                        | GitHub Actions                             |

These are recommendations, not mandatory dependencies. In particular, do not build your own cryptographic primitives. Final cryptography and key-management choices need a focused security review.

## 2. High-level system architecture

I would divide FormFlow into six main components. They should have clear boundaries, but they do not need to be six separately deployed microservices initially.

\#chatgpt-mermaid-\_r_1e5\_{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:16px;fill:rgb(237, 237, 237);}@keyframes edge-animation-frame{from{stroke-dashoffset:0;}}@keyframes dash{to{stroke-dashoffset:0;}}#chatgpt-mermaid-\_r_1e5\_ .edge-animation-slow{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 50s linear infinite;stroke-linecap:round;}#chatgpt-mermaid-\_r_1e5\_ .edge-animation-fast{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 20s linear infinite;stroke-linecap:round;}#chatgpt-mermaid-\_r_1e5\_ .error-icon{fill:rgb(48, 48, 48);}#chatgpt-mermaid-\_r_1e5\_ .error-text{fill:rgb(237, 237, 237);stroke:rgb(237, 237, 237);}#chatgpt-mermaid-\_r_1e5\_ .edge-thickness-normal{stroke-width:1px;}#chatgpt-mermaid-\_r_1e5\_ .edge-thickness-thick{stroke-width:3.5px;}#chatgpt-mermaid-\_r_1e5\_ .edge-pattern-solid{stroke-dasharray:0;}#chatgpt-mermaid-\_r_1e5\_ .edge-thickness-invisible{stroke-width:0;fill:none;}#chatgpt-mermaid-\_r_1e5\_ .edge-pattern-dashed{stroke-dasharray:3;}#chatgpt-mermaid-\_r_1e5\_ .edge-pattern-dotted{stroke-dasharray:2;}#chatgpt-mermaid-\_r_1e5\_ .marker{fill:rgb(175, 175, 175);stroke:rgb(175, 175, 175);}#chatgpt-mermaid-\_r_1e5\_ .marker.cross{stroke:rgb(175, 175, 175);}#chatgpt-mermaid-\_r_1e5\_ svg{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:16px;}#chatgpt-mermaid-\_r_1e5\_ p{margin:0;}#chatgpt-mermaid-\_r_1e5\_ .label{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";color:rgb(237, 237, 237);}#chatgpt-mermaid-\_r_1e5\_ .cluster-label text{fill:rgb(237, 237, 237);}#chatgpt-mermaid-\_r_1e5\_ .cluster-label span{color:rgb(237, 237, 237);}#chatgpt-mermaid-\_r_1e5\_ .cluster-label span p{background-color:transparent;}#chatgpt-mermaid-\_r_1e5\_ .label text,#chatgpt-mermaid-\_r_1e5\_ span{fill:rgb(237, 237, 237);color:rgb(237, 237, 237);}#chatgpt-mermaid-\_r_1e5\_ .node rect,#chatgpt-mermaid-\_r_1e5\_ .node circle,#chatgpt-mermaid-\_r_1e5\_ .node ellipse,#chatgpt-mermaid-\_r_1e5\_ .node polygon,#chatgpt-mermaid-\_r_1e5\_ .node path{fill:rgb(9, 23, 44);stroke:rgb(31, 78, 148);stroke-width:1px;}#chatgpt-mermaid-\_r_1e5\_ .rough-node .label text,#chatgpt-mermaid-\_r_1e5\_ .node .label text,#chatgpt-mermaid-\_r_1e5\_ .image-shape .label,#chatgpt-mermaid-\_r_1e5\_ .icon-shape .label{text-anchor:middle;}#chatgpt-mermaid-\_r_1e5\_ .node .katex path{fill:#000;stroke:#000;stroke-width:1px;}#chatgpt-mermaid-\_r_1e5\_ .rough-node .label,#chatgpt-mermaid-\_r_1e5\_ .node .label,#chatgpt-mermaid-\_r_1e5\_ .image-shape .label,#chatgpt-mermaid-\_r_1e5\_ .icon-shape .label{text-align:center;}#chatgpt-mermaid-\_r_1e5\_ .node.clickable{cursor:pointer;}#chatgpt-mermaid-\_r_1e5\_ .root .anchor path{fill:rgb(175, 175, 175)!important;stroke-width:0;stroke:rgb(175, 175, 175);}#chatgpt-mermaid-\_r_1e5\_ .arrowheadPath{fill:rgb(175, 175, 175);}#chatgpt-mermaid-\_r_1e5\_ .edgePath .path{stroke:rgb(175, 175, 175);stroke-width:1px;}#chatgpt-mermaid-\_r_1e5\_ .flowchart-link{stroke:rgb(175, 175, 175);fill:none;}#chatgpt-mermaid-\_r_1e5\_ .edgeLabel{background-color:rgb(0, 0, 0);text-align:center;}#chatgpt-mermaid-\_r_1e5\_ .edgeLabel p{background-color:rgb(0, 0, 0);}#chatgpt-mermaid-\_r_1e5\_ .edgeLabel rect{opacity:0.5;background-color:rgb(0, 0, 0);fill:rgb(0, 0, 0);}#chatgpt-mermaid-\_r_1e5\_ .labelBkg{background-color:rgba(0, 0, 0, 0.5);}#chatgpt-mermaid-\_r_1e5\_ .cluster rect{fill:rgb(48, 48, 48);stroke:rgba(255, 255, 255, 0.15);stroke-width:1px;}#chatgpt-mermaid-\_r_1e5\_ .cluster text{fill:rgb(237, 237, 237);}#chatgpt-mermaid-\_r_1e5\_ .cluster span{color:rgb(237, 237, 237);}#chatgpt-mermaid-\_r_1e5\_ div.mermaidTooltip{position:absolute;text-align:center;max-width:200px;padding:2px;font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:12px;background:rgb(48, 48, 48);border:1px solid rgba(255, 255, 255, 0.15);border-radius:2px;pointer-events:none;z-index:100;}#chatgpt-mermaid-\_r_1e5\_ .flowchartTitleText{text-anchor:middle;font-size:18px;fill:rgb(237, 237, 237);}#chatgpt-mermaid-\_r_1e5\_ rect.text{fill:none;stroke-width:0;}#chatgpt-mermaid-\_r_1e5\_ .icon-shape,#chatgpt-mermaid-\_r_1e5\_ .image-shape{background-color:rgb(0, 0, 0);text-align:center;}#chatgpt-mermaid-\_r_1e5\_ .icon-shape p,#chatgpt-mermaid-\_r_1e5\_ .image-shape p{background-color:rgb(0, 0, 0);padding:2px;}#chatgpt-mermaid-\_r_1e5\_ .icon-shape .label rect,#chatgpt-mermaid-\_r_1e5\_ .image-shape .label rect{opacity:0.5;background-color:rgb(0, 0, 0);fill:rgb(0, 0, 0);}#chatgpt-mermaid-\_r_1e5\_ .label-icon{display:inline-block;height:1em;overflow:visible;vertical-align:-0.125em;}#chatgpt-mermaid-\_r_1e5\_ .node .label-icon path{fill:currentColor;stroke:revert;stroke-width:revert;}#chatgpt-mermaid-\_r_1e5\_ .node .neo-node{stroke:rgb(31, 78, 148);}#chatgpt-mermaid-\_r_1e5\_ [data-look="neo"].node rect,#chatgpt-mermaid-\_r_1e5\_ [data-look="neo"].cluster rect,#chatgpt-mermaid-\_r_1e5\_ [data-look="neo"].node polygon{stroke:url(#chatgpt-mermaid-\_r_1e5\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_1e5\_ [data-look="neo"].swimlane.cluster rect{filter:none;}#chatgpt-mermaid-\_r_1e5\_ [data-look="neo"].node path{stroke:url(#chatgpt-mermaid-\_r_1e5\_-gradient);stroke-width:1px;}#chatgpt-mermaid-\_r_1e5\_ [data-look="neo"].node .outer-path{filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_1e5\_ [data-look="neo"].node .neo-line path{stroke:rgb(31, 78, 148);filter:none;}#chatgpt-mermaid-\_r_1e5\_ [data-look="neo"].node circle{stroke:url(#chatgpt-mermaid-\_r_1e5\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_1e5\_ [data-look="neo"].node circle .state-start{fill:#000000;}#chatgpt-mermaid-\_r_1e5\_ [data-look="neo"].icon-shape .icon{fill:url(#chatgpt-mermaid-\_r_1e5\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_1e5\_ [data-look="neo"].icon-shape .icon-neo path{stroke:url(#chatgpt-mermaid-\_r_1e5\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_1e5\_ .node text{font-size:14px;font-weight:600;letter-spacing:normal;fill:rgb(153, 206, 255);}#chatgpt-mermaid-\_r_1e5\_ .edgeLabels text{font-size:13px;font-weight:600;letter-spacing:-0.08px;fill:rgb(153, 206, 255);}#chatgpt-mermaid-\_r_1e5\_ .node tspan[font-weight="normal"],#chatgpt-mermaid-\_r_1e5\_ .edgeLabels tspan[font-weight="normal"]{font-weight:600;}#chatgpt-mermaid-\_r_1e5\_ .edgeLabel .label rect{opacity:1;rx:13px;ry:13px;fill:rgb(0, 14, 26);stroke:rgb(26, 62, 95);stroke-width:1px;}#chatgpt-mermaid-\_r_1e5\_ .node rect,#chatgpt-mermaid-\_r_1e5\_ .node circle,#chatgpt-mermaid-\_r_1e5\_ .node ellipse,#chatgpt-mermaid-\_r_1e5\_ .node polygon,#chatgpt-mermaid-\_r_1e5\_ .node path{fill:rgb(0, 40, 77);stroke:rgba(255, 255, 255, 0.1);stroke-width:1px;}#chatgpt-mermaid-\_r_1e5\_ .node rect{rx:16px;ry:16px;}#chatgpt-mermaid-\_r_1e5\_ .node.mermaid-decision .label-container{fill:rgb(0, 14, 26);stroke:rgb(26, 62, 95);stroke-dasharray:2,2;}#chatgpt-mermaid-\_r_1e5\_ .edgePaths .flowchart-link{stroke:rgb(175, 175, 175);stroke-width:1px;stroke-linecap:round;stroke-linejoin:round;}#chatgpt-mermaid-\_r_1e5\_ .marker{fill:rgb(175, 175, 175);stroke:rgb(175, 175, 175);}#chatgpt-mermaid-\_r_1e5\_ :root{--mermaid-font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";}Backend ServicesTrusted Client EnvironmentNode.js APIAuthentication ProviderPostgreSQLEncrypted Blob StorageOptional Background WorkersNext.js AppBrowser ExtensionEncrypted Profile VaultForm Detection and FieldMappingSmart File PreparationApplication HistoryUserOptional AI Field ClassifierThird-Party ApplicationWebsiteSanitized field semantics only

The browser extension is responsible for interacting with third-party forms. The application interface is responsible for profile management and account settings. The encrypted vault holds personal information. The backend coordinates authentication, authorized devices, encrypted synchronization, and billing.

The diagram represents logical components. Initially, some can run in the same application deployment.

## 3. How I would implement each component

### A. Browser extension and form intelligence

Technology: TypeScript, Manifest V3, React, browser extension APIs.

Build this as an independent package in the repository.

The form-filling pipeline should work in this order:

### 1

Extract form fields

Read labels, input types, accessibility names, options, constraints and visible instructions.

### 2

Classify fields

Use deterministic rules and a shared field dictionary first.

### 3

Resolve ambiguous fields

Optionally use an AI classifier for sanitized field descriptions.

### 4

Match the local profile

Map semantic fields to locally stored values, respecting purpose and user permissions.

### 5

Fill and verify

Fill supported controls, trigger appropriate events and verify resulting values.

### 6

Review with the user

Highlight filled fields, missing values and sensitive fields; leave uncertain fields blank.

Use a shared semantic field dictionary, for example:

- `first_name`
- `last_name`
- `date_of_birth`
- `father_name`
- `mother_name`
- `present_address`
- `permanent_address`
- `education.degree`
- `education.institution`
- `employment.company`
- `employment.job_title`
- `document.resume`
- `document.profile_photo`
- `document.signature`

The field dictionary should be independent of any particular website. A website's field name might be `guardian_fullname`, while the matching profile field is `father_name` or `mother_name`. When the meaning is ambiguous, ask the user instead of guessing.

Important: Never give the AI model the user's actual profile values merely to classify a field. The classifier generally needs only the label, field type, limited options and relevant instructions. Even these should be minimized and sanitized.

### B. Encrypted profile vault

Technology: TypeScript, a vetted cryptographic library, browser-supported secure storage mechanisms.

The vault is one of the most important components because it determines whether your privacy promise is technically credible.

I recommend a structure like this:

```
Vault
├── Core Profile
│   ├── Identity
│   ├── Contact
│   └── Addresses
├── Education Records
├── Employment Records
├── Purpose Preferences
├── Documents and Assets
├── Application History
└── Vault Metadata
```

The logical organization is separate from the storage representation. Sensitive records and documents should be encrypted before being persisted or uploaded for synchronization.

Use the key hierarchy defined in the security specification:

- Vault Content Key (VCK): encrypts vault data.
- Vault passphrase: derives a key that protects the VCK.
- Recovery key: provides a separate recovery route to the VCK.
- Account credentials: authenticate the user but do not automatically decrypt the vault.

For implementation, use authenticated encryption and a vetted password-based key derivation function. Persist versioned encrypted records and wrapped keys, not raw vault keys in ordinary browser storage.

One architectural detail deserves special attention: a browser extension and a normal website are separate security contexts. Do not expose the vault key through page-global JavaScript or allow the website being filled to read the extension's decrypted profile. Establish an explicit, validated messaging boundary between the extension UI, its background worker, and its content scripts.

### C. Backend API and authentication

Technology: Node.js, Fastify, TypeScript, PostgreSQL.

Start with a modular monolith rather than microservices.

Suggested backend modules:

- `auth` — authentication integration and account linking
- `devices` — device registration, approval and revocation
- `sync` — encrypted vault synchronization and version tracking
- `assets` — encrypted document/blob upload coordination
- `billing` — plans and subscription status, if monetization is enabled
- `audit` — minimal security events without personal form contents

For authentication, support email verification, Google sign-in and mobile-number OTP through a provider that supports the required methods. Verify Bangladesh SMS delivery, pricing, rate limits and account recovery before selecting the provider.

The backend should enforce authorization on every account and device operation. A valid login alone should not automatically grant access to every device's sync operations.

### D. Database and encrypted cloud sync

Technology: PostgreSQL + managed object storage, such as Amazon S3.

Use PostgreSQL for structured operational data. Use object storage for larger encrypted vault snapshots or encrypted document blobs.

Example metadata tables:

| Table           | Purpose                                             |
| --------------- | --------------------------------------------------- |
| `users`         | Internal user reference and account status          |
| `devices`       | Authorized device metadata and revocation status    |
| `vaults`        | Vault identifier and cryptographic version metadata |
| `sync_records`  | Encrypted record references and version information |
| `blob_objects`  | References to encrypted document objects            |
| `subscriptions` | Billing and subscription metadata                   |

The server should not receive plaintext profile records or document contents. It may still see operational metadata such as object sizes, synchronization times and device activity, so the privacy policy must disclose that accurately.

For sync, plan for:

- Device authorization and revocation.
- Conflict resolution when multiple devices edit a profile.
- Version numbers and rollback detection.
- Encrypted backup and restore tests.
- Retry-safe uploads and interrupted sync recovery.
- Account deletion and backup-retention policies.

Do not assume encryption alone solves sync security. A malicious or compromised server might replay older ciphertext or replace encrypted objects. The client needs a way to detect invalid versions and unauthorized changes.

### E. Smart File Preparation

Technology: TypeScript, Canvas or OffscreenCanvas, `pdf-lib`.

This feature can run mostly on the client without introducing a separate backend service.

It should support:

- Converting images to PDF.
- Combining several images into one PDF.
- Resizing profile photos and signatures.
- Compressing files to meet upload limits.
- Preparing copies without modifying originals.
- Verifying file type, dimensions and size before attachment.

Use a deterministic pipeline for image resizing, conversion and validation. AI can help interpret ambiguous natural-language upload instructions, but it should not be responsible for calculating file dimensions or deciding whether a file passes technical validation.

Some websites use custom upload widgets, and some browser contexts prevent programmatic file attachment. For these cases, provide a guided manual-upload fallback instead of claiming universal compatibility.

### F. Application history

Technology: TypeScript and the encrypted vault.

Store application history in the user's vault by default, including the organization, application title, URL, status, notes and timeline events.

Keep history separate from a full copy of every completed form. That reduces the amount of sensitive information retained.

The status should not change to `Submitted` merely because the user clicked a button. Ask the user to confirm submission unless reliable evidence establishes that it succeeded.

## 4. Recommended repository structure

A monorepo is a good fit because the extension, web interface, backend and shared field definitions will evolve together.

```
formflow/
├── apps/
│   ├── web/                  # Next.js application
│   ├── extension/            # Browser extension
│   └── api/                  # Fastify backend
├── packages/
│   ├── shared-types/         # Shared domain types
│   ├── field-dictionary/     # Semantic field definitions
│   ├── validation/           # Zod schemas
│   ├── crypto-core/          # Reviewed vault crypto abstractions
│   ├── vault/                # Encrypted vault operations
│   ├── form-intelligence/    # Field classification and matching
│   └── file-processing/      # Image/PDF preparation
├── infrastructure/
│   ├── docker/
│   └── deployment/
├── docs/
│   ├── architecture.md
│   ├── threat-model.md
│   └── key-management.md
└── package.json
```

Use a workspace tool such as pnpm with Turborepo if its build caching and task orchestration are useful. Keep cryptography behind a small, well-tested interface so it can be audited independently of the UI.

Do not force every package to be shared. Browser-only functionality should remain browser-only, and the server should not import client-only code that could accidentally introduce vault data into backend processes.

## 5. What does scalability look like?

Start with a modular monolith, managed PostgreSQL and object storage. Add complexity only when measured traffic or operational requirements justify it.

Stage 1

Foundation and first users

One API deployment, managed PostgreSQL, encrypted object storage, one web app and one extension release. No distributed microservices required.

Stage 2

Growing usage

Add horizontal API scaling, connection pooling, rate limiting, background jobs for expensive tasks, monitoring and database indexes based on actual query patterns.

Stage 3

Large-scale operation

Separate independently scaling workloads, add queue-backed processing, tune storage and database capacity, and isolate costly or failure-prone integrations.

Good scalability decisions from day one:

- Keep API instances stateless where possible.
- Never require an AI request for every field.
- Process profile matching locally to reduce latency and server costs.
- Use object storage for large encrypted blobs rather than storing them directly in PostgreSQL.
- Add background workers only for work that actually needs asynchronous processing.
- Keep database migrations, backups and restore tests automated.
- Monitor performance using aggregate metrics without collecting profile values or form contents.

Do not introduce Kubernetes, Kafka, or a microservice for every feature at the beginning. They increase operational overhead before the product has demonstrated a need for them.

## 6. What about mobile browsers?

This is an important product constraint. A browser extension that works on desktop Chromium browsers will not automatically work in every mobile browser. Browser extension support and file-input automation vary substantially by browser and operating system.

I would therefore separate the implementation into two deliverables:

1. Initial extension: supported desktop Chromium browsers, with explicit compatibility tests.
2. Mobile experience: a responsive profile/vault interface first, followed by a dedicated mobile autofill integration or support for browsers that expose compatible extension APIs.

The encrypted vault and shared data model should be designed so that a later mobile client can reuse the same cryptographic and domain logic where the runtime supports it. Do not promise identical autofill behavior across every browser.

## 7. Implementation order I recommend

## Development checklist

0 of 18 complete

### Phase 1 — Foundation

Set up the TypeScript monorepo and CI pipeline

Define shared domain types and field dictionary

Write architecture decisions and threat-model acceptance criteria

### Phase 2 — Vault security

Implement vault creation, unlock, lock and recovery

Implement encrypted local persistence and key-envelope versioning

Test recovery, wrong-key handling, backup and restore

### Phase 3 — Profile and account

Implement email, Google and mobile authentication

Build core-profile onboarding and purpose selection

Implement reusable education, employment and asset records

### Phase 4 — Browser extension

Extract DOM and accessibility metadata

Implement deterministic field classification and matching

Add safe autofill, verification, missing-field prompts and review

### Phase 5 — Documents and history

Build local image/PDF preparation and validation

Implement application history and user-confirmed statuses

Test file-input compatibility and manual fallback paths

### Phase 6 — Sync and production

Implement encrypted sync, device authorization and conflict resolution

Deploy managed API, database and encrypted object storage

Complete security review, observability and deletion/restore tests

I would implement and security-test the vault before building broad autofill automation. Otherwise, the extension may become dependent on insecure storage choices that are difficult to replace later.

## 8. Final technology decision

| Layer                 | Final recommendation                                                     |
| --------------------- | ------------------------------------------------------------------------ |
| Primary language      | TypeScript                                                               |
| User interface        | React + Next.js                                                          |
| Browser automation    | Manifest V3 extension                                                    |
| Backend               | Node.js + Fastify                                                        |
| Data database         | Managed PostgreSQL                                                       |
| Large encrypted files | Managed object storage                                                   |
| Validation            | Zod                                                                      |
| Image/PDF handling    | Canvas + `pdf-lib`                                                       |
| Testing               | Vitest + Playwright                                                      |
| Deployment            | Docker + managed cloud infrastructure                                    |
| AI                    | Optional field-classification service with minimized inputs              |
| Vault                 | Client-side encryption, explicit key recovery, encrypted synchronization |

One last distinction: scalable technology does not automatically mean secure technology. The strongest FormFlow design is the one that minimizes the sensitive data the system needs to process in the first place. Before making public claims such as “zero-knowledge” or “end-to-end encrypted,” verify the actual key flows, client update model, sync behavior and recovery mechanism through an independent security review.

My recommendation is to start with the TypeScript monorepo, the cryptographic vault, and the shared field dictionary. Those are the three foundations that will shape almost every other implementation decision.