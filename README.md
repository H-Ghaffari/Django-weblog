# Django Blog

A multi-user blog built with **Django 5.2**. Registered users can write, edit and delete their own posts, upload images, and comment on posts. The front end uses the *Moderna* Bootstrap 5 template from BootstrapMade, and forms are rendered with `django-crispy-forms`.

## Features

- **Custom user model** (`accounts.CustomUser`) extending `AbstractUser` with `age`, `photo` (profile picture) and `about` fields
- **Authentication**: sign up, log in / log out, password change and password reset (reset emails are printed to the console in development)
- **Posts**: create, read, update and delete, each with a title, excerpt, body, date, author and cover image
- **Owner-only controls**: the *Update* and *Delete* links appear only for the post's author
- **Comments**: logged-in users can comment on any post; comments are shown on the post page
- **Pagination** on the home page (currently 1 post per page)
- **Sidebar** listing the 5 most recent posts on every page, provided by a context processor
- **Django admin** with a customized user admin and registered `Post` and `Comment` models
- **Media uploads** for post images and profile photos, served by Django in development

## Tech Stack

| Layer | Technology |
|---|---|
| Backend | Python 3, Django 5.2 |
| Database | SQLite (default) |
| Forms | django-crispy-forms, crispy-bootstrap4 |
| Images | Pillow |
| Front end | Django templates, Bootstrap 5 (BootstrapMade *Moderna* template) |

## Project Structure

```
Django_Blog/
├── manage.py
├── config/            # Project settings, root URLs, WSGI/ASGI
├── accounts/          # CustomUser model, signup view, user forms and admin
├── blog/              # Post and Comment models, views, forms, context processor
├── templates/         # base, home, post_*, sidebar and registration/* templates
├── static/            # Template assets (CSS, JS, images)
├── media/             # User uploads (created automatically)
└── db.sqlite3         # Development database
```

## Getting Started

### 1. Create a virtual environment

```bash
cd Django_Blog
python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate
```

### 2. Install dependencies

```bash
pip install -r requirements.txt
```

### 3. Set up the database

```bash
python manage.py migrate
python manage.py createsuperuser
```

### 4. Run the development server

```bash
python manage.py runserver
```

Open <http://127.0.0.1:8000/> for the blog and <http://127.0.0.1:8000/admin/> for the admin panel.

## URL Overview

| URL | Name | Description |
|---|---|---|
| `/` | `home` | Paginated list of posts |
| `/post/new` | `post_new` | Create a post |
| `/post/<id>` | `post_detail` | Read a post and add comments |
| `/post/update/<id>` | `update` | Edit a post |
| `/post/delete/<id>` | `delete` | Delete a post |
| `/accounts/signup/` | `signup` | Register a new account |
| `/accounts/login/`, `/accounts/logout/` | `login`, `logout` | Authentication |
| `/accounts/password_change/`, `/accounts/password_reset/` | | Password management |
| `/admin/` | | Django admin |

## Configuration Notes

- `EMAIL_BACKEND` is the console backend, so password-reset emails appear in the terminal.
- Uploaded files go to `media/` (`MEDIA_ROOT`) and are served via `MEDIA_URL = /media/`.
- Pagination is set by `paginate_by` in `HomeView` (`blog/views.py`); raise it to show more posts per page.
