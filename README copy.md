# Building a QRIS Extractor AI Agent on IBM watsonx Orchestrate

A step-by-step guide to creating a **BI Assistance Agent** that can extract and validate QRIS (QR Code Indonesian Standard) merchant data using IBM watsonx Orchestrate's Agent Builder, Document Extractor, and Agentic Workflow features.

---

## Table of Contents

1. [Landing Page](#1-landing-page)
2. [Navigate to Build Page](#2-navigate-to-build-page)
3. [Create Agent Page](#3-create-agent-page)
4. [Create a New Agent](#4-create-a-new-agent)
5. [Agent Profile Configuration](#5-agent-profile-configuration)
   - [5a. Knowledge & Toolset Sections](#5a-knowledge--toolset-sections)
   - [5b. Agents & Behavior Sections](#5b-agents--behavior-sections)
   - [5c. Guidelines & Channels Sections](#5c-guidelines--channels-sections)
6. [Customize the Welcome Message](#6-customize-the-welcome-message)
7. [Set Up Quick Start Prompts](#7-set-up-quick-start-prompts)
8. [Add Knowledge — Open the Knowledge Panel](#8-add-knowledge--open-the-knowledge-panel)
9. [Select Knowledge Source](#9-select-knowledge-source)
10. [Upload the Knowledge File](#10-upload-the-knowledge-file)
11. [Name the Knowledge Source](#11-name-the-knowledge-source)
12. [Add a Tool to the Agent](#12-add-a-tool-to-the-agent)
13. [Select Agentic Workflow Tool Type](#13-select-agentic-workflow-tool-type)
14. [Name the Agentic Workflow](#14-name-the-agentic-workflow)
15. [Agentic Workflow Canvas](#15-agentic-workflow-canvas)
16. [Add a File Upload User Activity](#16-add-a-file-upload-user-activity)
17. [Add a Document Extractor Step](#17-add-a-document-extractor-step)
18. [Select Document Format — Structured](#18-select-document-format--structured)
19. [Upload Sample Documents](#19-upload-sample-documents)
20. [Define the Schema](#20-define-the-schema)
21. [Create a Custom Schema](#21-create-a-custom-schema)
22. [Add Fields to the Schema](#22-add-fields-to-the-schema)
23. [Fix Incorrectly Extracted Values](#23-fix-incorrectly-extracted-values)
24. [Configure Field Extraction Settings](#24-configure-field-extraction-settings)
25. [Change the LLM Model](#25-change-the-llm-model)
26. [Add More Samples for Better Training](#26-add-more-samples-for-better-training)
27. [Verify the First Document](#27-verify-the-first-document)
28. [Verify All Sample Documents](#28-verify-all-sample-documents)
29. [Exit Workflow Builder](#29-exit-workflow-builder)
30. [Set Up Agent Behavior Instructions](#30-set-up-agent-behavior-instructions)
31. [Test the Agent](#31-test-the-agent)
32. [Copy the Embed Script](#32-copy-the-embed-script)
33. [Paste Script Into HTML File](#33-paste-script-into-html-file)
34. [Re-Test in Custom HTML Page](#34-re-test-in-custom-html-page)

---

## 1. Landing Page

Open **IBM watsonx Orchestrate**. You will land on the chat home screen with the active agent shown in the left panel. Quick start prompt cards are displayed in the center.

![Landing Page Watsonx Orchestrate](./Assets/MD/1.%20Landing%20Page%20Watsonx%20Orchestrate.png)

---

## 2. Navigate to Build Page

Click the hamburger menu (☰) at the top-left to expand the navigation sidebar. Select **Build** to go to the agent builder area.

![Go to Build Page](./Assets/MD/2.%20Go%20to%20Build%20Page.png)

---

## 3. Create Agent Page

The **Build agents and tools** page lists all existing agents (27), tools (333), and knowledge sources (24). Click the blue **Create agent +** button in the top-right to start building a new agent.

![Create Agent Page](./Assets/MD/3.%20Create%20Agent%20Page.png)

---

## 4. Create a New Agent

Choose **Create from scratch** (selected by default) to build a fully custom agent. Fill in:

- **Name**: `BI Assistance Agent` *(max 40 characters)*
- **Description**: `This agent extract information from QRIS through OCR`

Click the **Create** button to proceed.

![Create Agent](./Assets/MD/4.%20Create%20Agent.png)

---

## 5. Agent Profile Configuration

After creation, the agent configuration page opens. The left sidebar provides navigation tabs: **Profile**, **Knowledge**, **Toolset**, **Behavior**, and **Channels**.

### 5. Profile, Welcome Message & Quick Start Prompts

The **Profile** section holds the agent description. The **Welcome message** section lets you customize what users see on the home screen (max 100 characters). The **Quick start prompts** section pre-populates conversation starters. The **Agent style** selector lets you pick between `ReAct Core` (Recommended), `Default` (Deprecated), or `ReAct` (Deprecated).

![Agent Page – Profile](./Assets/MD/5.%20Agent%20Page.png)

---

### 5a. Knowledge & Toolset Sections

The **Knowledge** section is where you connect knowledge sources (files, databases, etc.). The **Toolset** section is where you attach tools and sub-agents. Both sections start empty — click **Add source** or **Add tool** to populate them.

![Agent Page – Knowledge & Toolset](./Assets/MD/5.a.%20Agent%20Page.png)

---

### 5b. Agents & Behavior Sections

The **Toolset → Agents** panel lets you delegate tasks to sub-agents. The **Behavior** section is where you write free-text instructions that define how the agent thinks and responds.

![Agent Page – Agents & Behavior](./Assets/MD/5.b.%20Agent%20Page.png)

---

### 5c. Guidelines & Channels Sections

The **Guidelines** section lets you add individual rules for the agent. The **Chat with documents** and **Scheduling** toggles control additional features. The **Channels** section (Preview) enables deployment to Home page, Embedded agent, Teams, WhatsApp with Twilio, Facebook Messenger, and more.

![Agent Page – Guidelines & Channels](./Assets/MD/5.c.%20Agent%20Page.png)

---

## 6. Customize the Welcome Message

In the **Profile** tab, scroll to the **Welcome message** field and replace the default text. Set it to:

> *Hail, Saya Bank Indonesia Virtual Assistant. Apa Yang Bisa Saya Bantu?*

This message is shown to every user when they open the chat (71/100 characters used).

![Change Welcome Message](./Assets/MD/6.%20Change%20Welcome%20Message.png)

---

## 7. Set Up Quick Start Prompts

In the **Quick start prompts** section, click **Add prompt +** and enter a relevant starter question. For the QRIS extractor use case, add:

> *Apakah QRIS ini valid?*

This prompt appears as a one-click suggestion on the agent's home screen.

![Change Quick Prompt Field](./Assets/MD/7.%20Change%20Quick%20Prompt%20Field.png)

---

## 8. Add Knowledge — Open the Knowledge Panel

In the **Knowledge** tab, locate the **Knowledge sources** section. Click **Add source +** to begin adding a knowledge file to the agent.

![Add Knowledge (panel)](./Assets/MD/8.%20Add%20Knowledge.png)

---

## 9. Select Knowledge Source

A wizard opens. On the **Select source** step, choose your knowledge backend. Available options are:

| Source | Notes |
|---|---|
| **Milvus** | Recommended — connect to an existing Milvus vector DB |
| Elasticsearch | Connect to an Elasticsearch instance |
| Custom service | External service via API |
| Astra DB | Connect to Astra DB |
| OpenSearch | Connect to OpenSearch |
| **Upload files** | ✅ Selected — create a local knowledge base (max 30 MB) |

Select **Upload files** and click **Next**.

![Select Source](./Assets/MD/9.%20Select%20Source.png)

---

## 10. Upload the Knowledge File

On the **Add knowledge** step, click the upload area or drag-and-drop your file. In the file picker that opens, navigate to **Downloads**, select **Data NNS** (the NNS code reference file), and click **Open**.

![Add Knowledge – Upload](./Assets/MD/10.%20Add%20Knowledge.png)

---

## 11. Name the Knowledge Source

On the **Knowledge details** step, fill in:

- **Name**: `NNS Code`
- **Description**: `This knowledge purpose is to make the agent know what banks release a QRIS by looking into the NNS code`

Click **Save** to finalize the knowledge source.

![Naming The Knowledge](./Assets/MD/11.%20Naming%20The%20Knowledge.png)

---

## 12. Add a Tool to the Agent

Back on the agent page, go to **Toolset** and click **Add tool +** in the **Tools** section.

![Add Tools](./Assets/MD/12.%20Add%20tools.png)

---

## 13. Select Agentic Workflow Tool Type

The **Add a tool** dialog appears. Under **Create new**, select **Agentic workflow** — this lets you automate repeatable business processes with low-code workflows that integrate document extraction and human input.

> Other options available: Catalog, Local instance, MCP server, OpenAPI.

![Select Agentic Workflow](./Assets/MD/13.%20Select%20Agentic%20Workflow.png)

---

## 14. Name the Agentic Workflow

A dialog prompts you to name the workflow. Enter:

- **Name**: `Agentic workflow 7`

Click **Start building** to open the workflow canvas.

![Naming The Workflow](./Assets/MD/14.%20Naming%20The%20Workflow.png)

---

## 15. Agentic Workflow Canvas

The workflow canvas opens showing an empty flow: **Start (0 inputs) → Add your first step → End (0 outputs)**. Use the left-side toolbar icons to add steps, variables, annotations, and navigate the canvas.

![Agentic Workflow Landing Page](./Assets/MD/15.%20Agentic%20Workflow%20Landing%20Page.png)

---

## 16. Add a File Upload User Activity

Click **Add your first step +** on the canvas. A context menu appears. Navigate to **User activities → Collect from user → File upload** to add a step that requests a file from the user.

![Add User Activity](./Assets/MD/16.%20Add%20User%20Activity.png)

---

## 17. Add a Document Extractor Step

With the **File upload 1** node on the canvas, click the **+** button below it to add the next step. Navigate to **Add a flow activity → Document extractor** to insert an AI-powered extraction node after the file upload.

![Add Document Extractor](./Assets/MD/17.%20Add%20Document%20Extractor.png)

---

## 18. Select Document Format — Structured

When the Document Extractor is added, choose the document format:

- **Structured** ✅ — For documents that look the same every time, like invoices, tax forms, or ID cards. *(Use this for QRIS images.)*
- Unstructured — For documents without a consistent layout, like contracts, reports, or emails.

Select **Structured**.

![Select Structured](./Assets/MD/18.%20Select%20Structured.png)

---

## 19. Upload Sample Documents

The Document Extractor needs training samples. Click **Drag and drop files here or upload**, then use the file picker to select sample QRIS images from the `Workshop > Sample` folder. Select **Sample1** first, then click **Open**.

Available samples: Sample1.png, Sample2.jpg, Sample3.jpeg, Sample4.jpeg, Test1, Test2, Test3.

![Upload File Into Document Extractor](./Assets/MD/19.%20Upload%20File%20Into%20Document%20Extractor.png)

---

## 20. Define the Schema

After uploading Sample1, the Document Extractor shows the sample on the right and prompts you to define a schema on the left. Click **Define schema** to open the schema builder.

![Define Schema](./Assets/MD/20.%20Define%20Schema.png)

---

## 21. Create a Custom Schema

The schema dialog offers **Custom schema** (User-defined) or a large library of **Predefined schemas** (ACORD insurance form, Bank statements, Bill of lading, Driver license, Invoice, National ID card, Passport, etc.).

Select **User-defined schema** under Custom schema, then click **Create** to build fields from scratch tailored to QRIS documents.

![Create Schema](./Assets/MD/21.%20Create%20Schema.png)

---

## 22. Add Fields to the Schema

The schema editor opens showing **Metrics Summary** on the left and **Define your schema** on the right. Click **Add field +** to define each data field you want the extractor to pull from the QRIS image.

Fields to add for QRIS extraction: `MerchantName`, `NMID`, `TID`, `NNS`.

![Add Field](./Assets/MD/22.%20Add%20Field.png)

---

## 23. Fix Incorrectly Extracted Values

After the first extraction run, review the **Extracted Value** vs **Correct Value** columns. If a field shows **No value** (e.g., the `NNS` field), click the three-dot menu (⋮) on that row and select **Edit** to manually enter the correct value. This corrected value becomes a training example.

![Edit False Value](./Assets/MD/23.%20Edit%20False%20Value.png)

---

## 24. Configure Field Extraction Settings

For each field (e.g., `NNS`), a configuration panel opens on the right. You can set:

- **Data type**: String, Number, Date, etc.
- **Description**: Describe what information to extract
- **Example**: Provide a sample value to guide the model
- **Available options**: Closed list of valid values (optional)

Enter an example value for the `NNS` field by using the **Select to copy** helper on the document preview, then click **Submit**.

![Block The Example](./Assets/MD/24.%20Block%20The%20Example.png)

---

## 25. Change the LLM Model

To improve extraction accuracy, switch the underlying foundation model. Click the **Models** dropdown at the top of the Document Extractor panel. Available options:

| Model | Status |
|---|---|
| mistral-small-3-1-24b-instruct-2503 | Recommended |
| mistral-medium-2505 | Recommended ⚠️ |
| **llama-4-maverick-17b-128e-instruct-fp8** | ✅ Selected — Recommended |

Select **llama-4-maverick-17b-128e-instruct-fp8** for best results with QRIS images.

![Change Document Extractor LLM Models](./Assets/MD/25.%20Change%20Document%20Extractor%20LLM%20Models.png)

---

## 26. Add More Samples for Better Training

Click **Add documents** at the bottom-left. In the file picker, select multiple samples at once (Sample2, Sample3, Sample4 — shown selected with red border). Click **Open** to upload all three.

More samples improve model accuracy and generalization across different QRIS designs.

![Add Another Sample For Better Train](./Assets/MD/26.%20Add%20Another%20Sample%20For%20Better%20Train.png)

---

## 27. Verify the First Document

With all fields defined and the model set, click **Verify document** for `Sample1.png`. Review the extracted fields:

| Field Name | Extracted Value |
|---|---|
| MerchantName | DINNCAFE |
| NMID | ID2021110182890 |
| TID | A01 |
| NNS | 93600815 |

If all values are correct, the document gets verified. Repeat for all other samples.

![Verify Document](./Assets/MD/27.%20Verify%20Document.png)

---

## 28. Verify All Sample Documents

Continue verifying each uploaded sample. Once `Sample1` reaches 100% accuracy, move to the remaining samples. The **Metrics Summary** panel tracks **Overall accuracy** across all documents. Here `Sample3.jpeg` shows 100% accuracy with all 4 fields correctly extracted from a different merchant (YAYASAN SERIBU CITA BANGSA).

![Verify All Sample](./Assets/MD/28.%20Verify%20All%20Sample.png)

---

## 29. Exit Workflow Builder

Once all samples are verified and the workflow is complete, the header bar shows **Saved** (green dot). Click the **Done** button (top-right) to exit the workflow builder and return to the agent configuration page.

![Exit Build Workflow By Click Done](./Assets/MD/29.%20Exit%20Build%20Workflow%20By%20Click%20Done.png)

---

## 30. Set Up Agent Behavior Instructions

Back on the agent page, go to the **Behavior** tab. In the **Instructions** text area, write the system prompt that governs how the agent behaves. For the BI QRIS Assistant, the instructions define two operating modes:

>You are a Bank Indonesia QRIS Assistant powered by watsonx Orchestrate.
>
>You operate in exactly two modes:
>
>━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
>MODE 1 — NORMAL CHATBOT
>━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
>
>If the user’s message is NOT requesting QRIS, QRIS image or QR code extraction, scanning, reading, analysis, or validation, respond as a normal helpful assistant.
>
>In this mode:
>- Answer questions naturally about Bank Indonesia, QRIS, payment systems, regulations, merchant onboarding, issuers, acquirers, and related topics.
>- Do NOT trigger any workflow.
>- Do NOT ask the user to upload an image.
>- Do NOT mention extraction unless the user explicitly asks for it.
>
>━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
>MODE 2 — QRIS EXTRACTION WORKFLOW
>━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
>
>Trigger this mode ONLY when the user explicitly asks to do any of the following on a QRIS, QRIS image or QR code:
>- scan
>- extract
>- read
>- analyze
>- validating
>- verify
>- decode
>- identify issuer
>- get merchant information
>- identify a bank or institution from the QRIS
>- inspect QRIS details from an image or QR code
>
>When Mode 2 is triggered:
>You are a Bank Indonesia QRIS Assistant powered by WatsonX Orchestrate. You have two distinct modes of operation:
>
>WORKFLOW STEPS (follow in order):
>
>STEP 1 — Ask the user to upload their QRIS image:
>  Say: "Please upload your QRIS image so I can extract the information for you. You can upload a PNG, JPG, or JPEG file."
>  Then invoke the image upload tool to receive the file.
>
>STEP 2 — After receiving the image, scan and extract the following fields from the QRIS QR code data:
>  - NNS   (National Numbering System — first 8 digits of tag 26 or 51 merchant account info, field ID "00" of the AID)
>  - TID   (Terminal ID — typically found in tag 26 sub-tag 02 or 51 sub-tag 02)
>  - NMID  (National Merchant ID — typically found in tag 26 sub-tag 03 or 51 sub-tag 03)
>  - Merchant Name (tag 59)
>
>  Do NOT alter, guess, or fabricate these values. Report them exactly as extracted from the QR code data.
>  Do NOT show any JSON or RAW format from document extractor to the user
>
>STEP 3 — After extracting the values, match the NNS against the knowledge base below and identify the Nama Penyelenggara (issuing institution). Report only the matching entry. If no match is found, state: "NNS [value] tidak ditemukan dalam daftar penyelenggara QRIS yang terdaftar."
>
>STEP 4 — Present the result in this exact format:
>
>---
>✅ QRIS Extraction Result
>
>🏷️ Merchant Name  : [value]
>🔢 NMID            : [value]
>🖥️ TID             : [value]
>📡 NNS             : [value]
>
>🏦 Issued by       : [Nama Penyelenggara matching the NNS not Nama Produk]
>
>— Give user a summary about:
>**1. NMID Validation**
>Check if the total character length of the NMID is between 15 and 18
>characters. State the actual length and whether it is valid or invalid.
>
>**2. Compliance Summary**
>Write 2–3 sentences summarizing the merchant identity, their
>GPN-affiliated institution, and the overall validity of this QRIS
>for a Bank Indonesia officer.
>
>**3. Anomalies & Warnings**
>Flag any of the following if present:
>- NMID length is outside 15–18 characters
>- NMID does not start with "ID"
>- TID is empty or missing
>- Merchant Name is empty or missing
>- NNS code not found in the knowledge source
>If no anomalies are found, state: "No anomalies detected."
>
>━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
>DECISION RULE
>━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
>
>Before responding, classify the user request:
>
>- If it is a general informational or conversational request, stay in Mode 1.
>- If it explicitly asks to process a QRIS, QRIS image or QR code, switch to Mode 2 and invoke "Agentic workflow 5".
>
>If there is no explicit request to process a QRIS, QRIS image or QR code, remain in Mode 1.

After editing, refresh the page to ensure the latest tool configuration is loaded.

![Setup Instruction & Refresh The Page](./Assets/MD/30.%20Setup%20Instruction%20%26%20Refresh%20The%20Page.png)

---

## 31. Test the Agent

Use the **Preview** panel on the right side of the agent page to test the agent. Type or click the quick start prompt **"Apakah QRIS ini valid?"**, then upload a QRIS image (e.g., `Test1.jpg`).

The agent:
1. Triggers **File upload 1** from the workflow
2. Runs the Document Extractor to extract `merchantname`, `nmid`, `tid`, and `nns`
3. Returns a structured **QRIS Extraction Result** including:
   - Merchant Name, NMID, TID, NNS, Issued by
   - **NMID Validation** (length, validity)
   - **Compliance Summary**
   - **Anomalies & Warnings**

![Agent Testing](./Assets/MD/31.%20Agent%20Testing.png)

---

## 32. Copy the Embed Script

To embed the agent on an external website, go to **Channels** (Preview) in the agent settings. Expand **Embedded agent**. Under **Embed on your website**, a JavaScript snippet is shown. Click the **copy** icon (📋) at the top-right of the code block to copy the script.

The script configures `window.wxOConfiguration` with your `orchestrationID`, `hostURL`, `rootElementID`, and `agentId`, then dynamically loads the `wxoLoader.js` file.

![Copy Script](./Assets/MD/32.%20Copy%20Script.png)

---

## 33. Paste Script Into HTML File

Open your website's HTML file in a code editor. Paste the copied `<script>` block just before the closing `</body>` tag. The script sets up the watsonx Orchestrate chat widget that will appear on the page.

```html
<script>
  window.wxOConfiguration = {
    orchestrationID: "20250606-0930-0376-6056-4e7376f1ae7b_...",
    hostURL: "https://dl.watson-orchestrate.ibm.com",
    rootElementID: "root",
    chatOptions: {
      agentId: "8c7d5793-3643-4812-babf-aafdc39923e6",
    }
  };
  setTimeout(function () {
    const script = document.createElement('script');
    script.src = `${window.wxOConfiguration.hostURL}/wxochat/wxoLoader.js?embed=true`;
    script.addEventListener('load', function () {
      wxoLoader.init();
    });
    document.head.appendChild(script);
  }, 0);
</script>
```

![Paste Script Into HTML File](./Assets/MD/33.%20Paste%20Script%20Into%20HTML%20file.png)

---

## 34. Re-Test in Custom HTML Page

Open the website in a browser. The **BI Assistance Agent** chat widget appears as a floating panel (bottom-right). Test the full flow again by asking **"Apakah QRIS ini valid?"** and uploading `Sample3.jpeg`.

The agent correctly extracts merchant data and the widget functions identically to the in-platform preview. The Bank Indonesia QRIS Intelligence Platform page shows stats: **130+ Registered NNS Codes**, **100+ Banks & E-Wallets**, **QRIS National Standard**.

![Re Test in Custom HTML](./Assets/MD/34.%20Re%20Test%20in%20Custom%20HTML.png)

---

## Summary

The following steps were completed to build and deploy the BI QRIS Extractor Agent:

| # | Step | Key Action |
|---|---|---|
| 1–2 | Access watsonx Orchestrate | Navigate to **Build** page |
| 3–4 | Create agent | Name: `BI Assistance Agent`, scratch build |
| 5–7 | Configure profile | Welcome message, quick prompts, agent style |
| 8–11 | Add knowledge | Upload NNS Code reference file |
| 12–13 | Add tool | Create new **Agentic workflow** |
| 14–15 | Name workflow | `Agentic workflow 7`, open canvas |
| 16 | Add user input | **Collect from user → File upload** |
| 17–18 | Add extractor | **Document extractor → Structured** |
| 19–22 | Train extractor | Upload samples, define schema (MerchantName, NMID, TID, NNS) |
| 23–26 | Improve accuracy | Fix values, add examples, change LLM to `llama-4-maverick`, add more samples |
| 27–28 | Verify samples | Reach 100% accuracy across all documents |
| 29–30 | Finalize agent | Click Done, write behavior instructions |
| 31 | Test | Preview panel validates QRIS extraction end-to-end |
| 32–34 | Deploy | Copy embed script → paste into HTML → verify on live website |
