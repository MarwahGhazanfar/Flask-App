from flask import Flask, render_template, request, redirect, url_for
from flask_sqlalchemy import SQLAlchemy

app = Flask(__name__)

# DATABASE CONFIG
app.config['SQLALCHEMY_DATABASE_URI'] = 'sqlite:///firstapp.db'
app.config['SQLALCHEMY_TRACK_MODIFICATIONS'] = False

# INITIALIZE DB
db = SQLAlchemy(app)

# SAMPLE MODEL
class Student(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    name = db.Column(db.String(100), nullable=False)
    email = db.Column(db.String(100), nullable=False)

    def __repr__(self):
        return f"{self.id} - {self.name}"

@app.route("/")
def home():
    # 1. Fetch all student records from the database
    all_students = Student.query.all()
    # 2. Send that list ('students') to your index.html file
    return render_template("index.html", students=all_students)

@app.route("/add", methods=["POST"])
def add_student():
    # 1. Get data from the form
    name = request.form.get("name")
    email = request.form.get("email")
    
    # 2. Create new Student object
    new_student = Student(name=name, email=email)
    
    # 3. Save to database
    db.session.add(new_student)
    db.session.commit()
    
    # 4. Go back to the home page to see the new data
    return redirect(url_for("home"))

if __name__ == "__main__":
    app.run(debug=True)
