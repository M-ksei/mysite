# My site project

<p>This project just for learning github and git</p>

1. Home Page
2. Sign Up and Login (and account verification)
3. User Profile (dashboard)
4. Direct messages
5. Chat with others
6. Search users and pages
7. Users single page
8. Sharing new post and delete post
9. Followers and Following pages
10. Like and Comment on posts

# Getting Started

- [Project Structure](#Project-Structure)
- [Dependencies](#Dependencies)
- [Requirements](#Requirements)
- [Site Routes](#Site-Routes)
- [Project Modules](#BluePrints)
- [Data Base Diagram](#Database-Diagram)
- [About redis](#Redis)
- [About sqlalchemy](#SqlAlchemy)
- [About flask-migration](#Flask-Migration)
- [View site pages](#Site-Pages)


# Project-Structure
```bash
PyGram
├───app.py
├───requirements.txt
├───dependencies.txt
├───routes.txt
├───README.md
├───.env
├───.gitignore
├───Documentation
├───migrations
└───PyGram
    ├───__init__.py
    ├───controller.py
    ├───models.py
    ├───config.py
    ├───mod_direct_message
    │   ├───__init__.py
    │   └───controller.py
    ├───mod_follow
    │   ├───__init__.py
    │   └───controller.py
    ├───mod_post
    │   ├───__init__.py
    │   └───controller.py
    ├───mod_profile
    │   ├───__init__.py
    │   └───controller.py
    ├───mod_search
    │   ├───__init__.py
    │   └───controller.py
    ├───mod_setting
    │   ├───__init__.py
    │   └───controller.py
    ├───mod_user_page
    │   ├───__init__.py
    │   └───controller.py
    ├───static
    │   ├───Site-Screen
    │   ├───img
    │   ├───styles
    │   │    └───all of css files..
    │   └───upload
    │       ├───dir_of_user1
    │       ├───dir_of_user2
    │       └───dir_of_user3
    ├───Templates
    │   └───all of html files..
    └───utils
        ├───check_auth.py
        ├───registration.py
        └───upload.py
```

```python
class User(db.Model):
    __tablename__ = "users"

    name = Column(String(32), nullable = False)
    lastname = Column(String(32), nullable = False)
    email = Column(String(256), nullable = False)
    username = Column(String(64), primary_key = True)
    country = Column(String(32), nullable = False)
    password = Column(String(128), nullable = False)
    avatar = Column(String(256), nullable = False, default = "/static/upload/avatar.png")
    active = Column(Boolean, nullable = False, default = False)

    # One To Many:
    # list of posts for create a foreign key we use backreference to list of this mode(Parent) from another model 
    posts = relationship("Post", backref="user")
    
    # and other list for anothers classes
class Post(db.Model):
    __tablename__ = "posts"
    username = Column(String(64), ForeignKey('users.username'), primary_key = True) # Foreign Key is primary key of parent table
    caption = Column(Text(), nullable = True)
    picture = Column(String(256), nullable = False)
    post_date = Column(DateTime(), default = dt.datetime.utcnow, primary_key = True)
```