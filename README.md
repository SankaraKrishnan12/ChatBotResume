# Resume Analyzer Chatbot

[Chat With Me..!](https://chat-bot-resume.vercel.app/)

An Resume Analyzer built using Next.js, AI SDK, and Google Gemini (`gemini-2.5-flash`).
This application evaluates resumes using ATS-style analysis and provides structured, professional feedback with scoring and improvement suggestions.

---

## Features

* ATS-style resume evaluation
* Structured professional feedback
* Skill categorization and gap analysis
* Experience and project impact assessment
* ATS compatibility score (out of 100)
* Star rating (out of 5)
* Role-match analysis (if job description provided)
* Streaming AI responses
* Markdown-rendered output
* Modular system prompt architecture (Context + Task separation)

---

## Architecture

### Tech Stack

* Frontend: Next.js (App Router)
* AI Integration: `ai` SDK
* Model: Google Gemini (`gemini-2.5-flash`)
* Streaming: `streamText()`
* UI Rendering: Markdown Preview
* Language: TypeScript

---

## Project Structure

```
/app
  /api/chat/route.ts
  /components
      ChatInput.tsx
      ChatMessage.tsx
      MessageList.tsx
/README.md
```

---

## How It Works

### 1. Prompt Architecture

The chatbot uses a layered prompting system:

**Context Layer**

* Defines evaluator identity (Placement Officer / Technical Recruiter)
* Enforces objective and critical evaluation

**System Prompt Layer**

* Defines structured evaluation framework
* Defines scoring logic
* Defines output formatting rules

This ensures:

* Consistent analysis
* Structured responses
* Reduced hallucination
* Recruiter-aligned evaluation

---

### 2. Evaluation Framework

The AI performs:

1. Candidate Profile Assessment
2. Skill Categorization
3. Experience Quality Review
4. Project Depth Analysis
5. ATS Optimization Review
6. Strength and Weakness Identification
7. Improvement Action Plan
8. Role Match (if job description provided)

---

### 3. Streaming Response

The backend uses:

```ts
streamText({
  model: google('gemini-2.5-flash'),
  system: `${context}\n\n${systemPrompt}`,
  messages: await convertToModelMessages(messages),
});
```

This enables real-time streaming output to the UI.

---

## Environment Setup

### 1. Install Dependencies

```bash
npm install
```

### 2. Add Environment Variable

Create a `.env.local` file:

```
GOOGLE_GENERATIVE_AI_API_KEY=your_api_key_here
```

### 3. Run Development Server

```bash
npm run dev
```

Application runs at:

```
http://localhost:3000
```

---

## Example Use Case

1. User pastes resume content into the chat.
2. AI analyzes the resume.
3. AI returns structured output including:

   * Summary Evaluation
   * Skill Breakdown
   * Experience Analysis
   * ATS Score
   * Star Rating
   * Improvement Suggestions

---

## Scoring System

| Score Range | Interpretation                |
| ----------- | ----------------------------- |
| 90–100      | Industry-ready                |
| 75–89       | Strong but improvable         |
| 60–74       | Average                       |
| Below 60    | Needs significant improvement |

Star Rating is derived from:

* Technical strength
* Measurable impact
* Clarity
* ATS readiness

---

## Design Principles

* Does not invent missing experience
* Penalizes vague statements
* Avoids generic praise
* Structured and recruiter-aligned feedback
* Designed for campus placement workflows

---

## Future Improvements

* JSON schema structured output
* Resume file upload (PDF parsing)
* Job-description-based scoring
* Dashboard analytics
* Persistent user session memory
* Resume comparison feature

---

## Example Output Sections

```
SUMMARY EVALUATION
SKILLS ANALYSIS
EXPERIENCE REVIEW
PROJECT EVALUATION
ATS COMPATIBILITY SCORE
STAR RATING
STRENGTHS
WEAKNESSES
IMPROVEMENT ACTION PLAN
ROLE MATCH
```

