![example workflow](https://github.com/Kirorus/yamdb_final/actions/workflows/yamdb_workflow.yml/badge.svg)

## What YaMDb is:

**YaMDb** collect user reviews on arts divided into categories (for example, "Books", "Movies", "Music"). A art can be assigned one or more genres. 
A user can leave one text review for an art in the YaMDb database and rate it on a scale from one to ten. From the average user rating of an art, formed rating of art.
You can leave comments on reviews.

## How to install:
You need install docker and docker-compose at first.
Instruction for different OS [here](https://docs.docker.com/engine/install/ubuntu/)

**1. Clone repository**
```
git clone git@github.com:Kirorus/infra_sp2.git
```
**2. Create .ENV**
go to infra folder
```
cd infra_sp2/infra
```

create .env file
```
nano .env
```

add this with yout data
```
SECRET_KEY=5UP3RS3CR3TK3Y
DEBUG=False
ALLOWED_HOSTS=*

DB_ENGINE=django.db.backends.postgresql
POSTGRES_DB=api_yamdb_db
POSTGRES_USER=postgres
POSTGRES_PASSWORD=5UP3RS3CR3TPA55W0RD
DB_HOST=db
DB_PORT=5432
```

**3. Run docker-compose up**
```
docker-compose up -d  --build
```
**4. Apply migrations**
```
docker-compose exec web python manage.py migrate
```
**5. Create SuperUser**
```
docker-compose exec web python manage.py createsuperuser
```
**6. Collect static**
```
docker-compose exec web python manage.py collectstatic --no-input 
```
**7. Load sample data in DB**
```
docker-compose exec web python manage.py loaddata fixtures.json 
```
&nbsp;

## Some examples of API requests:

&nbsp;

#### Registration and authorization of a new user:

> POST | http://127.0.0.1:8000/api/v1/auth/signup/

```
{
"email": "pochta@mylo.ru",
"username": "test_user"
}
```
> 200 OK

&nbsp;

> POST | http://127.0.0.1:8000/api/v1/auth/token/

```
{
"username": "test_user",
"confirmation_code": "61p-c0443f686f2ea7e2444f"
}
```
> 200 OK

&nbsp;

#### Getting a list of all categories:

> GET | http://127.0.0.1:8000/api/v1/categories/

> 200 OK

&nbsp;

#### Search by genre:

> GET | http://127.0.0.1:8000/api/v1/genres/?search=rock-n-roll

> 200 OK

&nbsp;

#### Getting a list of arts filtered by year and category:

> GET | http://127.0.0.1:8000/api/v1/titles/?year=1994&category=movie

> 200 OK

&nbsp;

#### Adding an art:

> POST | http://127.0.0.1:8000/api/v1/titles/

```
{
"name": "8 1/2",
"year": 1963,
"description": "Фантазия Феллини о месте художника в современном мире.",
"genre": [
"fantasy", "drama"
],
"category": "movie"
}

```

> 201 CREATED

&nbsp;

#### Getting review by id:

> GET | http://127.0.0.1:8000/api/v1/titles/1/reviews/2/

> 200 OK

&nbsp;

#### Partial review update:

> PATCH | http://127.0.0.1:8000/api/v1/titles/1/reviews/1/

```
{
  "text": "Класс! UPD: всем советую!",
  "score": 10
}
```
> 200 OK

&nbsp;

#### Deleting a comment:

> DELETE | http://127.0.0.1:8000/api/v1/titles/5/reviews/2/comments/1/

> 204 NO_CONTENT

&nbsp;

#### Getting and changing user data by username:

> GET | http://127.0.0.1:8000/api/v1/users/bingobongo/

> 200 OK

&nbsp;

> PATCH | http://127.0.0.1:8000/api/v1/users/bingobongo/

> 200 OK

&nbsp;

#### Getting and changing your account information:

> GET | http://127.0.0.1:8000/api/v1/users/me/

> 200 OK

&nbsp;

> PATCH | http://127.0.0.1:8000/api/v1/users/me/

> 200 OK


## About Authors
[Kirorus](https://github.com/Kirorus/)
Yandex Precticum Student
&nbsp;

[Gollum959](https://github.com/Gollum959)
Yandex Precticum Student
&nbsp;

[an-nastasiia](https://github.com/an-nastasiia)
Yandex Precticum Student
