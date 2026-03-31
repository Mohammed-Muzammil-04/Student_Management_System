# Student Management App — Deployment Guide

This repository contains a Flask app prepared for deployment.

Quick checklist before deploy
- Ensure `.gitignore` excludes `myenv/` and sensitive files (already present).
- Ensure `requirements.txt` contains `gunicorn` (already present).
- Ensure `Procfile` exists with `web: gunicorn main:app` (already present).
- Set environment variables on the host: `DATABASE_URL` and `SECRET_KEY`.
- Create a remote database and import `students.sql`.

Render deployment (recommended)
1. Push this repo to GitHub/GitLab.
2. On Render: New → Web Service → Connect repo → Branch `main`.
3. Set the start command to `gunicorn main:app` (or rely on `Procfile`).
4. Add environment variables:
   - `DATABASE_URL` (example MySQL): `mysql://USER:PASSWORD@HOST:PORT/DBNAME`
   - `SECRET_KEY`: a long random string
5. Deploy and check logs. Visit `/test` to confirm DB connectivity.

Local testing (optional)
- Create a virtual environment:
  ```powershell
  python -m venv venv
  Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope Process -Force
  .\venv\Scripts\Activate.ps1
  pip install -r requirements.txt
  ```
- Set local env vars (PowerShell):
  ```powershell
  $env:DATABASE_URL = "mysql://user:pass@host/dbname"
  $env:SECRET_KEY = "some_secret"
  python main.py
  ```

Security notes
- Do NOT commit `.env` or any secrets.
- Rotate DB credentials if they were ever committed.

If you want, I can push this repo to a remote if you provide the Git URL.
