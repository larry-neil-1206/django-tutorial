## General django shells
#### Setup virtual environment
Virtual environment is for isolated Python environments, which are more practical than installing packages systemwide. It also allows installing packages without administrator privileges.
```
py -m venv venv
```

#### Activate virtual environment.
```
venv/Scripts/activate.bat
```

#### Install Django
```
python -m pip install Django
```
#### Check django version
```
py -m django --version
```
#### Creating a project
```
django-admin startproject mysite
```
#### Start development server
```
py manage.py runserver [PORT]
```
#### Migrate database
```
python manage.py migrate
```
#### Create app
```
py manage.py startapp polls
```
#### Make new migrations 
```
python manage.py makemigrations polls
```
#### Run migrations
The `sqlmigrate` command doesn't actually run the migration on your database - instead, it prints it to the screen so that you can see what SQL Django thinks is required. It’s useful for checking what Django is going to do or if you have database administrators who require SQL scripts for changes.
```
python manage.py sqlmigrate polls 0001
```
#### Create those model tables in your database
```
python manage.py migrate
```
## Database APIs
#### Playing with python shell
```
py manage.py shell
```
#### Shell examples
```
from polls.models import Choice, Question  # Import the model classes we just wrote.
from django.utils import timezone

Question.objects.all()
q = Question(question_text="What's new?", pub_date=timezone.now())
q.save()
q.id
q.question_text
q.pub_date
q.question_text = "What's up?"
q.save()
Question.objects.filter(id=1)
Question.objects.filter(question_text__startswith="What")
current_year = timezone.now().year
Question.objects.get(pub_date__year=current_year)
q = Question.objects.get(pk=1)
q.was_published_recently()

q.choice_set.all()
q.choice_set.create(choice_text="Not much", votes=0)
q.choice_set.create(choice_text="The sky", votes=0)
c = q.choice_set.create(choice_text="Just hacking again", votes=0)
c.question
q.choice_set.all()
q.choice_set.count()
Choice.objects.filter(question__pub_date__year=current_year)
c = q.choice_set.filter(choice_text__startswith="Just hacking")
c.delete()
```

## Django Admin
#### Creating an admin user
```
py manage.py createsuperuser
```

## Test 

```
py manage.py test polls
```

### References
https://docs.djangoproject.com/en/5.0/intro/tutorial01/
https://docs.djangoproject.com/en/5.0/intro/tutorial02/
https://docs.djangoproject.com/en/5.0/intro/tutorial03/
https://docs.djangoproject.com/en/5.0/intro/tutorial04/