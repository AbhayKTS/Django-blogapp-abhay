# Django Blog App (MyBlog)

Frontend-focused Django blog application using **Django Templates** + **Bootstrap 5**.

## Features (UI)
- Base layout with navbar/footer
- Home page post cards (title, image, preview, Read More)
- Login / Signup pages
- Create Post page (multipart image upload)
- Blog detail page (full content + author + date)
- Conditional navbar (guest vs authenticated)

## Run locally (Windows / PowerShell)
From the project root (the folder that contains `manage.py`):

```powershell
# 1) Create venv (first time only)
py -m venv .venv

# 2) Activate
.\.venv\Scripts\Activate.ps1

# 3) Install dependencies
python -m pip install --upgrade pip
pip install -r requirements.txt

# 4) Migrate DB
python manage.py migrate

# 5) Start server
python manage.py runserver
```

Open: http://127.0.0.1:8000/

Optional (admin):
```powershell
python manage.py createsuperuser
```

## Deploy on Render
This repo includes `render.yaml` for a simple Render deployment.

### Steps
1. Push this repo to your GitHub.
2. In Render: **New +** → **Blueprint** → select the repo.
3. Render will use:
   - Build: `pip install -r requirements.txt && python manage.py collectstatic --noinput`
   - Start: `gunicorn myblog.wsgi:application --bind 0.0.0.0:$PORT`
4. Environment variables (already defined in `render.yaml`):
   - `DJANGO_SECRET_KEY` (auto-generated)
   - `DEBUG=False`
   - `ALLOWED_HOSTS=.onrender.com`

If you change your Render service domain, ensure `ALLOWED_HOSTS` matches it.
