# User-and-Activity-Period-model

Step One: Create a model to track login activity
We need to have our Django project setup with Django Rest Framework and django-rest-framework-jwt installed and configured. Now, we will create our UserLoginActivity model in our models.py file.


Step Two: Create a custom serializer
The JSONWebTokenSerializer of rest_framework_jwt.serializers is the serializer responsible for authenticating the user and returning the token. We will create a custom serializer which will inherit the JSONWebTokenSerializer and will override the validate() method to emit the user_logged_in signal on successful authentication. 


Step Three: Create a custom view
Create a custom view ObtainJWTView which will inherit from rest_framework_jwt.views.ObtainJSONWebToken and will set the serializer _class to the JWTSerializer which we have created.


Step Four: Create the route for login
We have our view and serializer ready to be used. Now, we have to create an URL to obtain jwt token in our url.py file.
Start the development server and hit the login endpoint http://127.0.0.1:8000/login/ . Enter the login credentials and send the post request. If everything works fine you will get a JSON Web Token in response:


Step Five: Create receiver for user_logged_in signal
As of now, we have our login endpoint working with the user_login_signal and user_login_failed signals being emitted properly. We will now write the code to handle these signals and keep our signal handling code in a separate signals.py file inside our app.


Step Six: Create receiver for user_login_failed signal
The user_login_failed signal receiver can be written in a similar manner as we have done for the user_logged_in signal receiver. The only difference is that now we would not get the user object as an argument, instead, we will get a dictionary containing the credentials used for login.


Final Step:
As a final step, we need to import signals in the ready() method of our AppConfig class in app.py file in order to make them discoverable and specify the app config file in the <app>/__init__.py file.
