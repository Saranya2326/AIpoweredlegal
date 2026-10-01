# LegalEase

AI-powered legal document generator. Pick a template, answer a short guided questionnaire, and get a draft document you can review, edit, and export — with plain-English explanations of what each clause means.

> *Not legal advice.* LegalEase helps you draft documents faster, but it doesn't replace a licensed attorney. Review any generated document carefully, especially for anything with real financial, employment, or legal consequences.

## Features

- *Template library* — NDAs, leases, wills, employment agreements, freelance/vendor contracts, and power of attorney forms
- *Guided Q&A drafting* — fill in a short form instead of staring at a blank document
- *Clause explainer* — plain-English breakdown of what each clause does and why it's there
- *Risk flagging* — surfaces unusual, missing, or one-sided terms compared to standard language
- *Live preview* — see the document update as you fill in details
- *Export* — download as PDF or Word (.docx)    
- *Version history* — track edits to a document over time

## Tech stack

| Layer | Choice |
|---|---|
| Frontend | React |
| Backend | Node.js / Express |
| Drafting & explanations | LLM (Claude API) |
| Document structure | Rules-based template engine (LLM fills fields, doesn't freehand legal structure) |
| Database | PostgreSQL |
| Export | docx / pdf-lib |
| Auth | JWT-based sessions |

## Project structure


legalease/
├── client/                # React frontend
│   ├── src/
│   │   ├── components/    # UI components (wizard steps, preview, clause tooltips)
│   │   ├── templates/     # Template definitions (fields, clause structure)
│   │   └── pages/
├── server/                # Express backend
│   ├── routes/            # API endpoints (drafting, export, auth)
│   ├── services/          # LLM calls, risk-flagging logic
│   └── models/            # DB models (users, documents, versions)
├── templates/             # Legal document templates (jurisdiction-aware)
├── .env.example
└── README.md


## Getting started

### Prerequisites

- Node.js 18+
- PostgreSQL 14+
- An Anthropic API key

### Setup

bash
git clone <repo-url>
cd legalease

# Install dependencies
npm install --prefix client
npm install --prefix server

# Configure environment
cp .env.example .env
# then fill in DATABASE_URL, ANTHROPIC_API_KEY, JWT_SECRET

# Run database migrations
npm run migrate --prefix server

# Start dev servers
npm run dev --prefix server    # http://localhost:4000
npm run dev --prefix client    # http://localhost:5173


### Environment variables


DATABASE_URL=postgres://user:password@localhost:5432/legalease
ANTHROPIC_API_KEY=your_key_here
JWT_SECRET=your_secret_here
PORT=4000


## How it works

1. *Choose a template* — pick a document type and jurisdiction
2. *Answer questions* — a short wizard collects the details specific to that document (parties, dates, terms, amounts)
3. *Draft generated* — the template engine builds the document structure; the LLM fills in and phrases clauses based on your answers
4. *Review* — click any clause for a plain-English explanation; flagged clauses are highlighted
5. *Edit & export* — make changes directly, then export as PDF or Word

## Roadmap

- [ ] E-signature integration (DocuSign / HelloSign)
- [ ] "Negotiation mode" — suggest counter-clauses on documents someone else sent you
- [ ] Redline/version comparison view
- [ ] Attorney review handoff (partner network)
- [ ] Public API for embedding document generation in other products

## Disclaimer

LegalEase is a drafting tool, not a law firm. It does not provide legal advice, and using it does not create an attorney-client relationship. For anything with significant stakes, have a licensed attorney in your jurisdiction review the final document.

## License

MIT
