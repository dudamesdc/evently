# Evently – A Complete Django Event Management App

Evently is a production-ready Django project that serves as a complete **Event Management Platform**. Organizers can create events, manage sessions and venues, while attendees can register, receive notifications, and keep track of their participation.

---

##  Project Goals
- Provide a realistic, multi-app Django project.
- Demonstrate use of the **MVT** pattern.
- Offer both **Django Admin** back-office and user-facing pages with templates & forms.
- Persist data in **MySQL** (or **SQLite** for quick starts).
- Include optional **REST API** with Django REST Framework.

---

##  Features
### Public
- Browse events by category/date/location  
- Event detail with sessions/speakers/venue map  
- Ticket types (free/paid), availability, and checkout stub  
- User signup/login, profile & registrations history  
- Search & filters  

### Organizer
- Create/manage events, venues, sessions, speakers  
- Manage ticket inventory & discount codes  
 

### Attendee
- Register for events, receive confirmation email  

### Admin / Back-office
- Moderate events & speaker bios  
- Custom list filters, actions, and read-only fields  
---

##  Tech Stack
- **Python 3.12+**, **Django 5.x**  
- **MySQL 8** (or SQLite for dev), **Redis** (Celery broker)  
- **Django Admin**, **Django Forms**, **Messages framework**  
- **Django REST Framework** (optional API)  
- **Celery + Celery Beat** for background tasks  
- **Whitenoise** for static files in simple deployments  
- **pytest** + **pytest-django** for tests  
- **pre-commit** (black, isort, flake8) for code quality  
- **Docker Compose** for reproducible environments  

---

## Architecture Overview
- Monolith with multiple Django apps:
  - `accounts/` – user registration, login, profiles  
  - `events/` – events, sessions, venues, speakers, tickets  
  - `orders/` – registrations, payments, coupons  
  - `core/` – settings, utilities, email, home pages  
  - `api/` (optional) – DRF viewsets & serializers  

---

## Data Model
- **Event**: title, slug, description, category, start/end, status, banner  
- **Venue**: name, address, city, state, lat/lng, capacity  
- **Session**: event FK, title, speaker FK, start/end, room  
- **Speaker**: name, bio, photo, socials  
- **TicketType**: event FK, name, price, currency, quantity, sales window  
- **Registration**: user FK, event FK, ticket FK, qty, status  
- **Coupon** (optional): code, discount %, valid window, max uses  

---

##  Screens & Flows
- Home (featured events, search)  
- Event list (filters by date/location/category)  
- Event detail (sessions, speakers, venue map)  
- Checkout (select ticket → confirm → success)  
- Account (profile, registrations)  
- Organizer dashboard (CRUD for events/sessions/tickets)  

---

---

##  Getting Started
### Prerequisites
- Python 3.12+  
- MySQL 8 (if not using SQLite)  

### Quickstart (SQLite)
```bash
git clone https://github.com/dudamesdc/evently-django.git
cd evently-django
python -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
cp .env.example .env  # edit as needed
python manage.py migrate
python manage.py createsuperuser
python manage.py loaddata seed
python manage.py runserver
