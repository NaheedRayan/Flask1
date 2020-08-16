# Flask1



Visit this site for further details:
https://code.visualstudio.com/docs/python/tutorial-flask

## Prerequisites 
  1. Install the Python extension.
  2. Install a version of Python 3 (for which this tutorial is written). To install other Python packages you must run $sudo apt install python3-pip in the    	   	terminal.
       
## Create a project environment for the Flask tutorial 

1. On your file system, create a project folder for this tutorial, such as flask1.
	In that folder, use the following command (as appropriate to your computer) to create a virtual environment named env based on your current interpreter:
	```
	$  pip3 install virtualenv 
	$  virtualenv env   			
	```

2. For activating the environment:``` $ source env/bin/activate```

3. Now inside the env  terminal type:
	```$ pip3 install flask flask-sqlalchemy```
4. Create a app.py
	Then for running it type:
	```$ python3 -m flask run```
5. Go to browser and see your result in : http://127.0.0.1:5000/



## Creating database 
1.	from flask sqlalchemy import SQLAlchemy

2. 	app.config['SQLALCHEMY_DATABASE_URI'] = 'sqlite:///posts.db'
	db = SQLAlchemy(app)
	
	class BlogPost(db.Model):
		id = db.Column(db.Integer,primary_key=True)
   		title = db.Column(db.String(100) , nullable=False)
   		content = db.Column(db.Text, nullable=False)
   		author = db.Column(db.String(20) , nullable=False,default = 'N/A')
   		date_posted = db.Column(db.DateTime , nullable =False ,default = datetime.utcnow)
    		
   		def __repr__(self):
   			return 'Blog post '+str(self.id)
   			
   			
3. 	Now to build the file open the python environment
4.	$ from app import db
5. 	$ db.create_all()
	
	This will create a post.db file in the directory


## Adding some entries to database
for that in the python environment import the model
1. 	$ from app import BlogPost

## For querying BlogPost
 	$ BlogPost.query.all()

## For adding to BlogPost
1. 	$ db.session.add(BlogPost(title = 'Blog Post 1', content = 'Content of blog post 1',author ='aroon'))

## Example:

(env) naheed@naheed-s15-x530un:~/Desktop/Flask1$ python3
Python 3.8.2 (default, Jul 16 2020, 14:00:26) 
[GCC 9.3.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> from app import db
	/home/naheed/Desktop/Flask1/env/lib/python3.8/site-packages/flask_sqlalchemy/__init__.py:833: 
	FSADeprecationWarning: SQLALCHEMY_TRACK_MODIFICATIONS adds significant overhead and will be disabled 		
	by default in the future.  Set it to True or False to suppress this warning.
  	warnings.warn(FSADeprecationWarning(
>>> from app import BlogPost
>>> BlogPost.query.all()
[Blog post 1, Blog post 2, Blog post 3, Blog post 4, Blog post 5, Blog post 6]
>>> BlogPost.query.all()[1]
Blog post 2
>>> BlogPost.query.all()[1].author
'Naheed'
>>> BlogPost.query.all()[1].date_posted
datetime.datetime(2020, 8, 13, 6, 58, 57, 594283)
>>> 


## after adding something commit should be used
	$ db.session.commit()


## some functions

(env) naheed@naheed-s15-x530un:~/Desktop/Flask1$ python3
Python 3.8.2 (default, Jul 16 2020, 14:00:26) 
[GCC 9.3.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> from app import db ,BlogPost
/home/naheed/Desktop/Flask1/env/lib/python3.8/site-packages/flask_sqlalchemy/__init__.py:833: FSADeprecationWarning: SQLALCHEMY_TRACK_MODIFICATIONS adds significant overhead and will be disabled by default in the future.  Set it to True or False to suppress this warning.
  warnings.warn(FSADeprecationWarning(
>>> 
>>> BlogPost.query.all()
[Blog post 1, Blog post 2, Blog post 3, Blog post 4, Blog post 5, Blog post 6]
>>> BlogPost.query.first()
Blog post 1
>>> BlogPost.query[1]
Blog post 2
>>> BlogPost.query[2]
Blog post 3
>>> BlogPost.query[4]
Blog post 5
>>> 
>>> BlogPost.query.filter_by(author ='Naheed').all()
[Blog post 1, Blog post 2, Blog post 3, Blog post 4, Blog post 5]
>>> BlogPost.query.filter_by(author ='dodo').all()
[Blog post 6]
>>> BlogPost.query.filter_by(author ='Dodo').all()
[]
>>> 
>>> BlogPost.query.get(1)
Blog post 1
>>> BlogPost.query.get(2)
Blog post 2
>>> BlogPost.query.get(3)
Blog post 3
>>> BlogPost.query.get(6)
Blog post 6
>>> BlogPost.query.get(7)
>>> BlogPost.query.get(7)
[1]+  Stopped                 python3


## deleting and updating 

(env) naheed@naheed-s15-x530un:~/Desktop/Flask1$ python3
Python 3.8.2 (default, Jul 16 2020, 14:00:26) 
[GCC 9.3.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> from app import db ,BlogPost
/home/naheed/Desktop/Flask1/env/lib/python3.8/site-packages/flask_sqlalchemy/__init__.py:833: FSADeprecationWarning: SQLALCHEMY_TRACK_MODIFICATIONS adds significant overhead and will be disabled by default in the future.  Set it to True or False to suppress this warning.
  warnings.warn(FSADeprecationWarning(
>>> db.session.delete(BlogPost.query.get(4))   <--deleting post 4.It will delete it by primary key
>>> db.session.commit()
>>> 
>>> BlogPost.query.all()
[Blog post 1, Blog post 2, Blog post 3, Blog post 5, Blog post 6]
>>> BlogPost.query.get(1).author
'Naheed'
>>> 
>>> BlogPost.query.get(1).author = 'Qazi'   <--updating 
>>> db.session.commit()
>>> 
>>> BlogPost.query.get(1).author
'Qazi'
>>> 

BlogPost.query.get(4) returns an object.












 
