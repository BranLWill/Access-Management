# Coffee Shop Backend

## Getting Started

### Installing Dependencies

#### Python 3.7

Follow instructions to install the latest version of python for your platform in the [python docs](https://docs.python.org/3/using/unix.html#getting-and-installing-the-latest-version-of-python)

#### Virtual Environment

We recommend working within a virtual environment whenever using Python for projects. This keeps your dependencies for each project separate and organized. Instructions for setting up a virtual environment for your platform can be found in the [python docs](https://packaging.python.org/guides/installing-using-pip-and-virtual-environments/)

#### PIP Dependencies

Once you have your virtual environment setup and running, install dependencies by naviging to the `/backend` directory and running:

```bash
pip install -r requirements.txt
```

This will install all of the required packages we selected within the `requirements.txt` file.

##### Key Dependencies

- [Flask](http://flask.pocoo.org/) is a lightweight backend microservices framework. Flask is required to handle requests and responses.

- [SQLAlchemy](https://www.sqlalchemy.org/) and [Flask-SQLAlchemy](https://flask-sqlalchemy.palletsprojects.com/en/2.x/) are libraries to handle the lightweight sqlite database. Since we want you to focus on auth, we handle the heavy lift for you in `./src/database/models.py`. We recommend skimming this code first so you know how to interface with the Drink model.

- [jose](https://python-jose.readthedocs.io/en/latest/) JavaScript Object Signing and Encryption for JWTs. Useful for encoding, decoding, and verifying JWTS.

## Running the server

From within the `./src` directory first ensure you are working using your created virtual environment.

Each time you open a new terminal session, run:

```bash
export FLASK_APP=api.py;
```

To run the server, execute:

```bash
flask run --reload
```

The `--reload` flag will detect file changes and restart the server automatically.

## Tasks

### Setup Auth0

1. Create a new Auth0 Account
2. Select a unique tenant domain
3. Create a new, single page web application
4. Create a new API
   - in API Settings:
     - Enable RBAC
     - Enable Add Permissions in the Access Token
5. Create new API permissions:
   - `get:drinks`
   - `get:drinks-detail`
   - `post:drinks`
   - `patch:drinks`
   - `delete:drinks`
6. Create new roles for:
   - Barista
     - can `get:drinks-detail`
     - can `get:drinks`
   - Manager
     - can perform all actions
7. Test your endpoints with [Postman](https://getpostman.com).
   - Register 2 users - assign the Barista role to one and Manager role to the other.
   - Sign into each account and make note of the JWT.
   - Import the postman collection `./starter_code/backend/udacity-fsnd-udaspicelatte.postman_collection.json`
   - Right-clicking the collection folder for barista and manager, navigate to the authorization tab, and including the JWT in the token field (you should have noted these JWTs).
   - Run the collection and correct any errors.
   - Export the collection overwriting the one we've included so that we have your proper JWTs during review!

### Implement The Server

There are `@TODO` comments throughout the `./backend/src`. We recommend tackling the files in order and from top to bottom:

1. `./src/auth/auth.py`
2. `./src/api.py`

### Valid JWT tokens

1. Manager:
   - eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCIsImtpZCI6IkJfOTR4TG45U0lVaTVVZTgxemFrZiJ9.eyJpc3MiOiJodHRwczovL2FjY2Vzcy1hdXRoLnVzLmF1dGgwLmNvbS8iLCJzdWIiOiJnb29nbGUtb2F1dGgyfDEwOTU2NDAyOTI0ODEwODg3NDUyMSIsImF1ZCI6IkNvZmZlZVNob3AiLCJpYXQiOjE2OTcxMzQ3MTksImV4cCI6MTY5NzE0MTkxOSwiYXpwIjoiYUFEZjBOejlOeTBGcnRFV3lEZUNFSEhVWlJjR1VxeGMiLCJzY29wZSI6IiIsInBlcm1pc3Npb25zIjpbImRlbGV0ZTpkcmlua3MiLCJnZXQ6ZHJpbmtzIiwiZ2V0OmRyaW5rcy1kZXRhaWwiLCJwYXRjaDpkcmlua3MiLCJwb3N0OmRyaW5rcyJdfQ.B10ziv1Xg_DYDmt-kmgKTqbO6osUSVM3sIGjSjZ4J-lIxubtQsAcJ1WlF7dlzdeo-Ttp3YrfOqYhVm5nGphxNzKhxq4ZaSIF3yJTU7A0ZPwo2mdFCfdd23bDN6-kmpH8utRKrJRUq606l3IVNyJOWvhg65etQEgI7OHtTPjFMwnAz0Z9P_dXSCr-i1wDZgVKrrKfVM5mFrzpPYPAvQVMLmVIlNteV8hyVsaRpV5M6VGOuVEjRN2o5GgjsNYr2Ogk8C_eTsXD9lvpubV_6hlTN5-gafXQ3JVaHYmJ-V8Rair6MNWPdyVvZzSkAO0m7CN2rxSP1SFKLXOxJWXbyCV12A
2. Barista:
   - eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCIsImtpZCI6IkJfOTR4TG45U0lVaTVVZTgxemFrZiJ9.eyJpc3MiOiJodHRwczovL2FjY2Vzcy1hdXRoLnVzLmF1dGgwLmNvbS8iLCJzdWIiOiJnb29nbGUtb2F1dGgyfDEwNTE0MzA3OTMwNTM5OTE3OTI0NiIsImF1ZCI6IkNvZmZlZVNob3AiLCJpYXQiOjE2OTcxMzUwNzQsImV4cCI6MTY5NzE0MjI3NCwiYXpwIjoiYUFEZjBOejlOeTBGcnRFV3lEZUNFSEhVWlJjR1VxeGMiLCJzY29wZSI6IiIsInBlcm1pc3Npb25zIjpbImdldDpkcmlua3MiLCJnZXQ6ZHJpbmtzLWRldGFpbCJdfQ.IIWbhIQiAGHjpgRpRYIxjr17y21jSIvn7dvJmK1_Z9Ucwgn2U4GGvToEiDxzkJw3\_\_WAdrPkCTM6jnX6mAcK5rX7fhqop8CeGhc2QEibIR7HIIdIVTRwfXRGlhAWmZHUfUAOc2SS1WrIoQ3l28Y7lIUcPIVibgXUGZJH4tigfFYT22VIgQftUcucGpKAbNyuEhmfLPhqbrV1gSuKj56e1ksm_J5mkRjr2evUgCuMd4QMAq8QzcJevb3t3N-\_9_r01_7yD1Jy9WvNtgsMKm6j2bQy-bRg8D8WhwOPNo85i0LN-bb9gpoDEgEV6wmAPZKPyqwxmsVcO_wxzAuEc65nGA
