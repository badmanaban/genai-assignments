# AI-Powered GitHub Code Review Web Application

## ICEPOT Master Prompt

**I** -- Instructions | **C** -- Context | **E** -- Example | **P** -- Persona | **O** -- Output | **T** -- Tone

Use this prompt with your coding agent in Agent Mode while your existing frontend project is open.

---

# I -- Instructions

Develop a complete frontend web application for my existing AI-powered GitHub Code Review system.

Users must be able to enter a GitHub repository URL, submit it to an existing n8n backend workflow, receive the AI-generated review, and view the results in a professional dashboard.

Implement the following six phases in order.

---

## Phase 1 -- Existing Project Analysis and Architecture Planning

Before making changes, analyze the complete existing project.

My existing n8n workflow contains:

- Webhook – Receives a GitHub repository URL.
- HTTP Request – Fetches the source code from GitHub.
- Basic LLM Chain – Sends retrieved source code to the LLM.
- Groq Chat Model – Analyzes the code and generates the review.
- Respond to Webhook – Returns the generated review.

### Tasks

- Inspect the project structure and identify existing frontend technologies and files.
- Identify where the new HTML UI should be created.
- Inspect how the n8n Webhook receives input.
- Identify the actual request payload and response structure.
- Identify CORS and API integration requirements.
- List all impacted files.

**Do not modify any files during this phase.**

---

## Phase 2 -- Develop the Frontend User Interface

Create a modern, professional, responsive web application aligned with the branding of Gupshup AI (https://www.gupshup.ai/).

### Branding & Visual Identity

- Display Gupshup AI branding throughout the application.
- Use organization name and logo in the header.
- Follow Gupshup-inspired color palette and styling.
- Use modern enterprise-grade typography.
- Maintain a clean AI-powered product experience.

### Layout Structure

#### Header

- Gupshup AI logo.
- Application title: AI Code Reviewer.
- Subtitle: AI-Powered GitHub Repository Analysis.

#### Repository Input Section

- GitHub Repository URL input.
- Placeholder: Enter GitHub repository URL.
- Analyze Code button.
- Reset button.
- URL validation with clear inline messages.
- Support public GitHub repository URLs.

#### Loading State

Display a branded loader with:

- Analyzing Repository...
- Fetching Code Review...
- Generating Insights...

Prevent duplicate submissions while processing.

#### Results Dashboard

Render the AI review inside structured enterprise dashboard cards.

Expected backend response:

```json
[
  {
    "text": "<AI Review Content>"
  }
]
```

Do not assume structured API fields such as:

- overallScore
- parameterScores
- improvementAreas
- recommendations
- summary

Instead dynamically parse the markdown review content.

Render sections such as:

- Overall Score
- Review Metrics Table
- Improvement Areas
- Recommendations
- Summary
- Detailed Feedback

### Rendering Requirements

- Proper markdown rendering.
- Render headings correctly.
- Render markdown tables.
- Render ordered and unordered lists.
- Render code blocks when present.
- Never display raw markdown.
- Gracefully handle missing sections.

Use clearly identified mock data only during this phase.

Do not connect n8n yet.

---

## Phase 3 -- Integrate the Frontend with the Existing n8n Backend

Connect the frontend to the existing n8n workflow.

### Webhook Inspection

- Inspect the Webhook node's actual HTTP method.
- Identify the exact input field and expected payload.
- Use the correct webhook URL.
- Do not invent request field names.
- Do not assume payload structures.
- Use the test webhook URL during testing and production URL for deployment.

### API Communication

When the user clicks Analyze Code:

1. Capture and validate the GitHub URL.
2. Send it to the n8n webhook using fetch().
3. Use the actual HTTP method and payload expected by n8n.
4. Wait for and parse the response.
5. Pass the response to the rendering layer.

### CORS

- Determine whether frontend and n8n are on different origins.
- Configure CORS only when necessary.
- Do not bypass browser security restrictions.

### Error Handling

Handle:

- Invalid URLs
- Empty URLs
- Missing repositories
- Private repositories
- Webhook failures
- Timeouts
- Invalid JSON
- Empty AI responses

Display clear user-friendly error messages.

Do not modify the existing code review prompt or Groq configuration.

---

## Phase 4 -- Dynamic AI Code Review Results Dashboard

Use the actual response returned by the n8n Respond to Webhook node.

Expected review response may be:

```json
[
  {
    "text": "<AI Review Content>"
  }
]
```

Do not assume a predefined JSON schema.

Extract and render information dynamically from the markdown content returned by the backend.

If structured fields are not provided:

- Derive sections from markdown headings.
- Derive score sections from markdown content.
- Render review information exactly as provided.

Do not hardcode:

- Scores
- Ratings
- Recommendations
- Summary sections

### Overall Score Detection

If an overall score is present in the markdown response:

- Highlight it prominently.
- Display score card or indicator.
- Display score out of 100 if available.

If no score exists:

- Do not generate one.
- Do not estimate one.

### Dynamic Response Handling

- Render actual backend response values only.
- Handle missing sections gracefully.
- Never display undefined values.
- Never expose raw objects.
- Sanitize all untrusted content before rendering.

Create a mapping layer only if necessary.

---

## Phase 5 -- UI Enhancement and User Experience

Customize the application UI based on Gupshup AI branding.

### Visual Design

Implement:

- Professional enterprise-grade dashboard.
- Gupshup-inspired color palette.
- Consistent spacing.
- Strong visual hierarchy.
- Professional typography.
- Modern buttons.
- Modern icons.
- Card-based sections.
- Clean layouts.

### Header & Footer

#### Header

Include:

- Gupshup AI logo.
- Application name.
- Brand styling.

#### Footer

Include:

- Gupshup branding.
- Copyright information.
- Application version.
- Responsive footer layout.

### Responsive Design

Support:

- Desktop
- Tablet
- Mobile

Requirements:

- Responsive grid layouts.
- Adaptive typography.
- Flexible cards.
- Touch-friendly controls.
- Mobile optimization.

### User Feedback States

#### Loading Messages

- Analyzing Repository...
- Fetching Code Review...
- Generating Insights...

#### Success Messages

- Code Review Generated Successfully.
- Review Copied Successfully.
- Report Downloaded Successfully.

#### Validation Messages

- GitHub repository URL is required.
- Please enter a valid GitHub repository URL.
- Repository URL format is invalid.

#### Error Messages

- Unable to reach review service.
- Repository could not be analyzed.
- Invalid response received from server.
- Review generation failed. Please try again.
- Something went wrong. Please retry.

### Dashboard Features

Implement:

- Copy Review button.
- Download Report button.
- Reset Review button.
- Scroll-to-top button.
- Sticky action toolbar.
- Expand/Collapse sections.
- Keyboard navigation.

### Markdown Rendering Support

Requirements:

- Render markdown headings.
- Render markdown tables.
- Render numbered lists.
- Render bullet lists.
- Render code blocks with syntax highlighting.
- Preserve markdown structure.
- Sanitize untrusted content.

### Accessibility

Implement:

- WCAG color compliance.
- Focus indicators.
- Keyboard accessibility.
- Screen-reader labels.
- Appropriate ARIA attributes.

### Performance

- Efficient markdown rendering.
- Optimized handling of large reviews.
- Prevent UI blocking.
- Lazy render large content where appropriate.

Keep the UI clean, professional, and focused on code-review analysis.

Avoid:

- Unnecessary animations.
- Decorative widgets.
- Unsupported charts.
- Hardcoded review values.
- UI components dependent on unavailable backend fields.

---

## Phase 6 -- End-to-End Testing and Final Validation

### Test 1 -- Valid Repository

- Submit valid repository URL.
- Verify request reaches n8n.
- Verify AI review is generated.
- Verify response is rendered correctly.

### Test 2 -- Invalid URL

- Verify validation appears.
- Verify no request is sent.

### Test 3 -- Empty Input

- Verify required validation message appears.

### Test 4 -- Backend Failure

- Simulate unavailable webhook.
- Verify friendly error appears.

### Test 5 -- Unexpected Response

Test:

- Empty response
- Invalid JSON
- Missing text field

Verify application remains stable.

### Test 6 -- Markdown Rendering

Verify:

- Headings
- Tables
- Lists
- Scores
- Recommendations
- Summary Sections

Render correctly.

### Test 7 -- Additional Features

Verify:

- Copy functionality
- Download functionality
- Reset functionality
- Responsive design
- Error notifications

### Final Validation

- Fix identified issues.
- Preserve existing functionality.
- Remove mock data.
- Verify complete end-to-end flow.
- Ensure n8n workflow remains unaffected.

---

# C -- Context

I already have a working n8n automation that performs AI-powered GitHub code reviews.

I want a separate HTML-based frontend so users do not interact directly with n8n.

### Existing Architecture

Frontend:
- HTML
- CSS
- JavaScript

Backend:
- n8n
- Webhook
- HTTP Request
- Basic LLM Chain
- Groq Chat Model
- Respond to Webhook

### Architecture Rules

- n8n handles all backend processing.
- Frontend handles UI and rendering.
- Do not duplicate AI processing in frontend.
- Do not hardcode review responses.
- Never expose credentials.
- Keep frontend loosely coupled.
- Preserve existing workflow.

---

# P -- Persona

You are a Senior Full-Stack Architect and UI/UX Developer with 10+ years of experience in:

- HTML5
- CSS3
- JavaScript
- Responsive Design
- REST APIs
- n8n Automation
- Webhook Architectures
- AI Applications
- Dashboard Development
- GitHub Integrations

You build production-ready applications following clean code principles, modular architecture, and maintainable design patterns.

---

# O -- Output

Provide:

### 1. Application Files

List all:

- Created files
- Modified files

### 2. Functional Frontend

Responsive AI Code Reviewer application.

### 3. Backend Integration

Working n8n integration.

### 4. Dynamic Results Dashboard

Displays markdown review dynamically from backend response.

### 5. Additional Features

- Validation
- Loading states
- Error handling
- Reset
- Copy review
- Download report

### 6. Testing Report

Include:

- Test scenarios
- Results
- Issues
- Fixes
- Limitations

### 7. Execution Instructions

Explain:

1. How to start frontend.
2. How to start n8n.
3. How to configure webhook.
4. How to test application.
5. How to access application.

### 8. Final Summary

Provide concise architecture and implementation summary.

---

# T -- Tone

Maintain a professional, technical, implementation-focused tone.

- Be technically accurate.
- Explain key decisions clearly.
- Avoid unnecessary complexity.
- Do not assume configurations.
- Ask questions only when required.
- Do not claim untested functionality.
- Prioritize maintainability and reliability.
- Preserve existing workflows.

---

# FINAL EXECUTION INSTRUCTION

Execute all six phases in the specified order.

Do not stop after providing plans or examples.

Implement the frontend, integrate with n8n, and validate functionality.

Before modifying protected backend components:

- Explain required change.
- Obtain approval.

After each phase:

- Summarize completed work.
- List modified files.
- Explain tests.
- Identify remaining issues.

Proceed automatically when backend approval is not required.

Final goal:

A fully functional AI-Powered GitHub Code Review Web Application with a Gupshup-branded responsive frontend and existing n8n-powered backend.

Important:

The actual n8n Webhook payload and response structure must always be inspected and used.

Never assume API fields. Render only the data returned by the backend.