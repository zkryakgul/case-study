# Flask and PostgreSQL sample 

The sample is a simple Python Flask application that connects to a PostgreSQL database via SQLAlchemy.

The database connection information is specified via environment variables `DBHOST`, `DBPASS`, `DBUSER`, and `DBNAME`. This app always uses the default PostgreSQL port.

# Classic run command for app
```
export ENV FLASK_APP=app.py
flask db upgrade && flask run -h 0.0.0.0 -p 5000
```
