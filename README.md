# Django Blog

A minimal Django blog: a landing page that shows the three most recent
posts, an "all posts" listing, and a slug-based post detail page. Built as a
starter project to practice Django templating, slug URLs, and many-to-many
relationships.

## Models

```text
Tag (caption)

Author (first_name, last_name, email_address)

Post
  ├─ title, excerpt, image_name
  ├─ date (auto-now), slug (unique)
  ├─ content (TextField, MinLengthValidator(10))
  ├─ author -> Author (SET_NULL)
  └─ tags  -> ManyToMany(Tag)
```

## URLs

| URL                  | View              | Template                  |
| -------------------- | ----------------- | ------------------------- |
| `/`                  | `starting_page`   | `blog/index.html`         |
| `/posts`             | `posts`           | `blog/all-posts.html`     |
| `/posts/<slug>`      | `post_detail`     | `blog/post-detail.html`   |

## Tech stack

- Python 3.10+
- Django 4.2
- SQLite (default)

## Setup

```bash
python -m venv venv
.\venv\Scripts\activate
pip install -r requirements.txt
cp .env.example .env             # set SECRET_KEY (optional in dev)
python manage.py migrate
python manage.py createsuperuser
python manage.py runserver
```

Visit <http://127.0.0.1:8000/> for the landing page or
<http://127.0.0.1:8000/admin/> to create posts.

## Project structure

```text
blog/
├── my_site/           # Django project (settings, urls)
├── blog/              # The blog app: models, views, urls
├── templates/         # base.html + blog/*.html
├── static/            # app.css
├── manage.py
└── requirements.txt
```

## Roadmap

- Replace `image_name: CharField` with a real `ImageField` + media handling.
- Add pagination on the "all posts" listing.
- Add comments and tag-based filtering.
- Add Markdown rendering for `Post.content`.
