# Braymell Website

![Braymells](/backend/core/static/images/logo.jpeg)

A Django web application for Braymell's public site and admin-managed portfolio content..

## Features

### Public Website

- **Homepage** (`/`)

  - Route-to-market positioning
  - Service/capability summary
  - Featured testimonials
  - Client logo carousel linking to client pages

- **Clients** (`/clients/`)

  - Client logo and caption listing
  - Each client links to a dedicated client work page

- **Client Detail** (`/clients/<slug>/`)

  - Client logo and company context
  - Client objective
  - Activation footprint or stores activated
  - Team size
  - What Braymell did for the client
  - Achievement/results
  - Brand carousel for brands under that client

- **Brand Detail** (`/brands/<slug>/`)

  - Brand logo and parent client
  - Brand objective
  - Execution story
  - Outcome/results
  - Brand image gallery with lightbox
  - Related brands from the same client

- **Testimonials** (`/testimonials/`)

  - Client feedback
  - Ratings
  - Pagination

- **About** (`/about/`) and **Contact** (`/contact/`)

### Admin Content Management

- **Clients**

  - Name and slug
  - Client logo
  - Company caption
  - Company description
  - Objective
  - Stores activated / activation footprint
  - Team size
  - Work done by Braymell
  - Achievement
  - Active/inactive status
  - Inline brand management

- **Brands**

  - Parent client
  - Name and auto-generated slug
  - Brand logo
  - Brand caption
  - Objective
  - Execution
  - Outcome
  - Display order
  - Active/inactive status
  - Inline brand image gallery

- **Brand Images**

  - Image upload
  - Caption
  - Display order

- **Testimonials**

  - Client name, company, and position
  - Message
  - Rating
  - Optional image
  - Featured toggle

- **Projects**
  - Kept for compatibility/internal data
  - Can still store legacy project objective, mechanisms, achievement, and images
  - Brand detail pages can fall back to project content when new brand story fields are empty

## Technology Stack

- Django 4.2.11
- Django REST Framework 3.14.0
- drf-spectacular for OpenAPI/Swagger docs
- django-filter
- django-cors-headers
- Pillow for image uploads
- SQLite for local development

## Setup

From the repository root:

```bash
cd backend
```

Create and activate a virtual environment:

```bash
python3 -m venv venv
source venv/bin/activate
```

Install dependencies:

```bash
pip install -r requirements.txt
```

Run migrations:

```bash
python manage.py migrate
```

Create an admin user:

```bash
python manage.py createsuperuser
```

Start the development server:

```bash
python manage.py runserver
```

Open:

```text
Homepage: http://localhost:8000/
Admin:    http://localhost:8000/admin/
API Docs: http://localhost:8000/api/docs/
```

If port `8000` is already in use:

```bash
python manage.py runserver 8001
```

## Content Workflow

### Add a New Client

1. Open `/admin/`.
2. Go to **Clients**.
3. Add the client name, logo, caption, and description.
4. Fill in the client work story:
   - Objective
   - Stores activated / activation footprint
   - Team size
   - Work done
   - Achievement
5. Mark the client active.

### Add Brands Under a Client

1. Open the client in admin.
2. Add brands using the inline brand form, or go directly to **Brands**.
3. Upload the brand logo.
4. Add brand caption, objective, execution, and outcome.
5. Set the display order.
6. Mark the brand active.

### Add Brand Gallery Images

1. Open the brand in admin.
2. Use the inline **Brand Images** section.
3. Upload images, add captions, and set ordering.

The public flow will then be:

```text
Homepage client logo
  -> Client detail page
      -> Brand logo
          -> Brand detail page
```

## Project Structure

```text
backend/
├── config/
│   ├── settings.py
│   ├── urls.py
│   ├── wsgi.py
│   └── asgi.py
├── core/
│   ├── admin.py
│   ├── models.py
│   ├── serializers.py
│   ├── urls.py
│   ├── views.py
│   ├── migrations/
│   ├── static/
│   └── templates/
├── media/
├── staticfiles/
├── db.sqlite3
├── manage.py
└── requirements.txt
```

## Useful Commands

Run checks:

```bash
python manage.py check
```

Create migrations:

```bash
python manage.py makemigrations
```

Apply migrations:

```bash
python manage.py migrate
```

Run tests:

```bash
python manage.py test
```

Collect static files:

```bash
python manage.py collectstatic
```

**Last updated:** May 5, 2026
