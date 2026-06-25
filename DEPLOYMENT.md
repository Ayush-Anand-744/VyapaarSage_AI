# Deployment

VyapaarSage_AI is prepared for local development and live hosting without changing the core application structure.

## Recommended runtime

FastAPI backend with MongoDB Atlas plus React frontend.

## Local run

`cd backend && pip install -r requirements.txt && uvicorn server:app --reload`

`cd frontend && npm install --legacy-peer-deps && npm start`

## Environment variables

Set MongoDB URL, JWT secret, and frontend backend URL.

## Production notes

- Keep secrets in the hosting provider's environment settings, not in source control.
- Use the included `.env.example` files as a checklist only.
- For AI/model projects, choose a plan with enough memory for model loading and inference.
- For frontend/backend projects, deploy the backend first, then point the frontend API base URL to the live backend URL if the frontend is not served by the same process.
