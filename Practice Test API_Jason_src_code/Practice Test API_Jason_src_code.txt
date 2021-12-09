from flask import Flask, jsonify

# Initializing the API app
app = Flask(__name__)

# Test employee list
employees = [{'Name': 'Jason Andrews', 'Age': 41, 'Employee_ID': 1234},
             {'Name': 'Sam Wiley', 'Age': 30, 'Employee_ID': 1024},
             {'Name': 'Sally Anne', 'Age': 50, 'Employee_ID': 1970}]


# Adding a test endpoint
@app.route('/')
def index():
    return "Hello World"


# Adding an endpoint to display all employees
@app.route("/employees", methods=["GET"])
def get_employees():
    return jsonify({"List of employees": employees})


# Adding an endpoint to display an employee's details by searching the ID
@app.route("/employees/<int:employee_id>", methods=["GET"])
def get_employee(employee_id):
    result = {}

    for employee in employees:
        if employee['Employee_ID'] == int(employee_id):
            result = jsonify({"Selected employee": employee})

    return result


# Running the application
if __name__ == "__main__":
    app.run(debug=True)
