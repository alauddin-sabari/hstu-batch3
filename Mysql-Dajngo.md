# Connecting MySQL Database with Django

## Prerequisites
- Python installed (>=3.6)
- Django installed (`pip install django`)
- MySQL server installed
- MySQL client and connector (`pip install mysqlclient` or `pip install pymysql` for alternative)

## Step 1: Install MySQL Client
Run the following command based on your MySQL setup:
```bash
pip install mysqlclient  # Recommended
```
If you face installation issues, use:
```bash
pip install pymysql
```

## Step 2: Create a Django Project
If you haven’t already created a Django project, run:
```bash
django-admin startproject myproject
cd myproject
```

## Step 3: Configure `settings.py`
Open `settings.py` and update the `DATABASES` configuration:
```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'your_database_name',
        'USER': 'your_database_user',
        'PASSWORD': 'your_database_password',
        'HOST': 'localhost',  # or your MySQL server address
        'PORT': '3306',       # default MySQL port
    }
}
```
If using `pymysql`, add this in `myproject/__init__.py`:
```python
import pymysql
pymysql.install_as_MySQLdb()
```

## Step 4: Create MySQL Database
Log into MySQL and create a database:
```sql
CREATE DATABASE your_database_name;
GRANT ALL PRIVILEGES ON your_database_name.* TO 'your_database_user'@'localhost' IDENTIFIED BY 'your_database_password';
FLUSH PRIVILEGES;
EXIT;
```

## Step 5: Apply Migrations
Run the following commands:
```bash
python manage.py makemigrations
python manage.py migrate
```

## Step 6: Create a Superuser (Optional)
```bash
python manage.py createsuperuser
```
Follow the prompts to set up a Django admin user.

## Step 7: Run the Server
```bash
python manage.py runserver
```
Visit `http://127.0.0.1:8000/admin/` to check if the database connection works correctly.

## Troubleshooting
- **Access denied error**: Ensure MySQL user credentials are correct.
- **ModuleNotFoundError**: Ensure `mysqlclient` or `pymysql` is installed.
- **Database connection error**: Ensure MySQL server is running.

  
### You have successfully connected Django with a MySQL database!

# Interacting with MySQL Database in Django

After successfully connecting Django with MySQL, let's explore different ways to interact with the database.

## 1. Viewing Data in MySQL Workbench

### Steps:
1. Open **MySQL Workbench** and connect to your MySQL server.
2. Select your database from the left panel.
3. Run an SQL query to fetch data from a table:
```sql
SELECT * FROM your_table_name;
```
4. You should see your data displayed in the result set.

---

## 2. Viewing Data via `python manage.py shell`

### Steps:
1. Open the terminal and enter Django’s shell:
```bash
python manage.py shell
```
2. Import your model:
```python
from your_app.models import YourModel
```
3. Retrieve all objects:
```python
YourModel.objects.all()
```
4. Filter specific data:
```python
YourModel.objects.filter(field_name='value')
```
5. Exit the shell:
```python
exit()
```

---

## 3. Viewing Data in Django Admin Panel

### Steps:
1. Ensure your model is registered in `admin.py`:
```python
from django.contrib import admin
from .models import YourModel

admin.site.register(YourModel)
```
2. Restart the Django server:
```bash
python manage.py runserver
```
3. Log into Django admin (`http://127.0.0.1:8000/admin/`).
4. Navigate to your model’s section to view the database records.

---

## 4. Using Django QuerySet API
You can interact with the database using Django’s ORM in views or scripts:
```python
# Retrieve all records
records = YourModel.objects.all()

# Filter data
filtered_records = YourModel.objects.filter(field_name='value')

# Get a single object
single_record = YourModel.objects.get(id=1)
```

---

## 5. Using MySQL Command Line

### Steps:
1. Open a terminal and log into MySQL:
```bash
mysql -u your_database_user -p
```
2. Select your database:
```sql
USE your_database_name;
```
3. Retrieve all records:
```sql
SELECT * FROM your_table_name;
```

---

## 6. Using MySQL GUI Clients (e.g., phpMyAdmin)
1. Open **phpMyAdmin** or any MySQL GUI tool.
2. Connect to the database.
3. Browse tables and execute SQL queries.

---

 
#### Congratulations HSTU Database Administrator Team!
#### These methods allow you to interact with your MySQL database in Django efficiently, whether through MySQL Workbench, Django shell, the admin panel, or direct SQL commands.

#### Have an amazing journey with you all and 
