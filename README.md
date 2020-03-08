# How to use flask-mail to send emails

Install the following dependencies:

    pip install flask
    pip install flask-mail

Then create a simple flask app that allows you to send messages as follows.
Create a new `app.py file`:

    from flask import Flask, make_response, jsonify
    from flask_mail import Mail, Message
    import os

    app = Flask(__name__)

    app.config['MAIL_SERVER'] = 'smtp.gmail.com'
    app.config['MAIL_PORT'] = 465
    app.config['MAIL_USE_TLS'] = False
    app.config['MAIL_USE_SSL'] = True
    app.config['MAIL_USERNAME'] = os.getenv('MAIL_USERNAME')
    app.config['MAIL_PASSWORD'] = os.getenv('MAIL_PASSWORD')
    mail = Mail(app)

    @app.route('/')
    def send_mail():
        with app.app_context():
            msg = Message(subject="Hello",
                        sender='arrotechtestmails@gmail.com',
                        recipients=["arrotechtestmails@gmail.com"],
                        body="This is a test email I sent with Gmail and Python!")
            mail.send(msg)
            return make_response(jsonify({
                "message": "Email sent successfully"
            }))

    if __name__ == '__main__':
        app.run(debug=True)

Note that the username and password are stored in a separate `.env` file and their values are called as show above.
Run the app by typing `python3 app.py`

