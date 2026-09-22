# Best Cars Dealership — Full Stack Developer Capstone

**Project name:** Best Cars Dealership Review Portal
**Course:** IBM Full Stack Software Developer — Capstone Project
**Author:** Filippo Murillo

## About the project

Best Cars is a national car retailer with dealerships across the United States.
This web application lets visitors browse the dealership branches, filter them by
state, read customer reviews with automatic sentiment analysis, and — once
registered and logged in — post their own reviews.

## Architecture

| Component | Technology | Port |
|---|---|---|
| Web app, auth, admin, car makes/models | Django 6 + SQLite | 8000 |
| Frontend (Register, Login, Dealers, Dealer, Post Review) | React 18 | built into Django |
| Dealers & reviews API | Node.js + Express + MongoDB (Docker) | 3030 |
| Sentiment analyzer | Flask + NLTK VADER (Docker) | 5050 |

## Features

- Static pages: Home, About Us, Contact Us
- User registration, login and logout
- Django admin for `CarMake` and `CarModel`
- List all dealers, filter by state, view dealer details and reviews
- Sentiment (positive / neutral / negative) shown for every review
- Logged-in users can post a review
- CI with GitHub Actions (flake8 + JSHint)
- Containerised deployment (Docker + Kubernetes manifest)

## Running locally

```bash
# 1. Dealers/reviews API + MongoDB
cd server/database
docker build . -t nodeapp
docker compose up -d

# 2. Sentiment analyzer
cd ../djangoapp/microservices
docker build . -t us.icr.io/sn-labs/senti_analyzer
docker run -d -p 5050:5000 us.icr.io/sn-labs/senti_analyzer

# 3. React frontend
cd ../../frontend
npm install && npm run build

# 4. Django
cd ..
pip install -r requirements.txt
python manage.py makemigrations && python manage.py migrate
python manage.py runserver
```
