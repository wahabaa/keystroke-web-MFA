# Keystroke Dynamics MFA Website

This website demonstrates keystroke dynamics as an alternative MFA other than the popular OTP or push notification MFAs.

## House Keeping
1. Create a database called `Soteria` (you can use any name of your choice).
2. Modify the `settings.py` file with your newly created database name, user, host and password.
    ```python
    DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'soteria', # Set DB Name
        'HOST': 'localhost',
        'PORT': '3306',
        'USER': 'root',
        'PASSWORD': '*****', # Set DB password
    }}
    ```
3. Visit sendgrid.com to create an account for sending email.
4. Follow the guide here on how to set up a new api key https://app.sendgrid.com/guide/integrate/langs/smtp
5. Modify the code below in the `settings.py` file with your sendgrid account details such as email, api key and password.
    ```python
    # Email settings
    DEFAULT_FROM_EMAIL = 'tester@gmail.com'
    SERVER_EMAIL = 'tester@gmail.com'
    EMAIL_USE_TLS = True
    EMAIL_HOST = 'smtp.sendgrid.net'
    EMAIL_PORT = 587
    EMAIL_HOST_USER = 'apikey'
    EMAIL_HOST_PASSWORD = '***************************'
    ```
6. Visit `twilio.com` and create an account to get an assigned phone number for sending SMS. 
7. Modify the `view.py` file with your account_sid, auth_token, and assigned phone number (change from `+13233363926` to yours). You can find the information on your twilio dashboard.
   ```python
   def sendSMS(message, phone):
    if '+' not in str(phone):
        phone = '+1' + str(phone)
    account_sid = '*******************************'
    auth_token = '*******************************'
    client = Client(account_sid, auth_token)
    client.messages.create(to=phone, from_='+13233363926', body=message)
   ```
8. House is clean!

## Installation

Use the package manager [pip](https://pip.pypa.io/en/stable/) to install all required packages.

```bash
pip install -r requirements.txt
```

Allow django to automatically create the database tables using `manage.py`. This should run successfully if all the `House keeping` instructions above are followed.
```bash
python manage.py makemigrations
```

```bash
python manage.py migrate
```

Upon a successful migration, you can now run the server. The server should run on `http://127.0.0.1:8000`.
```bash
python manage.py runserver
```

![alt text](home screen.png)

## Usage
Steps to follow for a successful interaction with the website.
1. Complete Signup.
2. Login.
3. Attempt account recovery (forgot password)

#### NOTE: First 4 logins or account recoveries use OTP as MFA, after which keystroke dynamics is used.


## Contributing

Feel free to make changes to the code.

## Developer
<div style="display:flex;align-items:center;">
    <img src="img_1.png" align="left">
   <div style="margin-left:10px;margin-right:20px;">
   <h4> Ahmed Anu Wahab <br> </h4>

   [ahmedanuwahab@gmail.com](ahmedanuwahab@gmail.com) <br>
   [wahabaa@clarkson.edu](wahabaa@clarkson.edu)

   </div>
</div>



## License

[SERL Clarkson, CITER](https://choosealicense.com/licenses/mit/)