# Link.ly

A minimal **URL shortener / link tracker** built with **Django**. Save a link under a short, readable slug, share `/<slug>/`, and see how many times it has been clicked.

> Early learning project (Django 5.1, early 2025).

## Features

- Create a link with a name, a destination URL and an optional custom slug
- Slug auto-generated from the name when left empty
- Short URL `/<slug>/` redirects to the destination
- Click counter incremented on every redirect
- Home page listing all saved links with their click counts
- Forms rendered with `django-crispy-forms` + `crispy-tailwind`

## Tech stack

- Python 3, Django 5.1
- SQLite
- Tailwind CSS through `django-tailwind`
- `django-crispy-forms` and `crispy-tailwind`
- `django-browser-reload` for auto-reload in development

## Data model

`Link`: `name` (unique), `url`, `slug` (unique, auto-filled from `name`), `clicks` (counter).

## Routes

| URL              | Description                                   |
| ---------------- | --------------------------------------------- |
| `/`              | List of all links and their click counts      |
| `/link/create`   | Form to add a new link                        |
| `/<slug>/`       | Increments the counter and redirects to the URL |
| `/admin/`        | Django admin                                  |

## Getting started

```bash
git clone https://github.com/kaminokyoi/linkly.git
cd linkly

python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install -r requirements.txt

python manage.py migrate
python manage.py runserver
```

Open <http://127.0.0.1:8000/> and add your first link from the create page.

### Tailwind CSS

The compiled stylesheet is committed (`theme/static/css/dist/styles.css`), so the app is styled out of the box. To modify the styles you need Node.js / npm:

```bash
python manage.py tailwind install
python manage.py tailwind start     # rebuilds the CSS on change (second terminal)
```

> `NPM_BIN_PATH` in `config/settings.py` currently points to a Windows install of npm. Update it to match your machine (for example `/usr/bin/npm`).

## Possible improvements

- Restrict slugs that clash with existing routes (e.g. `admin`, `link`)
- User accounts so each person manages their own links
- Click analytics (date, referrer)
- Environment-based settings (secret key, `DEBUG`, allowed hosts)
- Automated tests
