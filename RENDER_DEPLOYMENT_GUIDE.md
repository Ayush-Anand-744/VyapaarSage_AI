# Render Deployment Guide for VyapaarSage_AI

VyapaarSage_AI has a React/GitHub Pages frontend and a FastAPI backend. GitHub Pages can only host static files, so live dynamic data requires the backend to be deployed separately on Render or a similar Python hosting service.

## Render backend setup

Create a Render Web Service for the backend.

Recommended settings:

- Service type: Web Service
- Environment: Python or Docker
- Root directory: project root if using `Dockerfile.backend`, or `backend` if using Python directly
- Dockerfile path: `./Dockerfile.backend`
- Start command if using Python directly from `backend`: `uvicorn server:app --host 0.0.0.0 --port $PORT`

Required environment variables:

```env
MONGO_URL=your_mongodb_atlas_connection_string
DB_NAME=vyapaarsage_ai
JWT_SECRET=replace_with_a_secure_random_secret
```

Optional environment variables:

```env
SARVAM_API_KEY=your_sarvam_api_key_if_used
WHATSAPP_ACCESS_TOKEN=your_whatsapp_cloud_api_token_if_used
WHATSAPP_PHONE_NUMBER_ID=your_whatsapp_phone_number_id_if_used
WHATSAPP_VERIFY_TOKEN=your_custom_webhook_verify_token_if_used
BUSINESS_PHONE=your_business_phone_if_used
```

## Frontend backend URL

The static frontend is configured to try this backend first:

```text
https://vyapaarsage-ai-api.onrender.com
```

If your Render service URL is different, update the frontend backend URL in:

- `frontend/src/App.js`
- root `index.html` static fallback configuration, if you use the static GitHub Pages version

Then rebuild or re-upload the corrected root files.

## Why the page can look empty

If the backend URL is not deployed, sleeping, blocked by CORS, or connected to an empty MongoDB database, the original React build may show zeros or empty lists. The updated static root page includes demo fallback data so the GitHub Pages version still looks complete even before the backend is live.

## Backend sample data

The backend already contains sample seed logic. Once Render and MongoDB are correctly configured, startup will seed demo customers and inventory if the database is empty.
