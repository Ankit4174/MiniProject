'''
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Student Record Management System</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f4f4f9;
      margin: 0;
      padding: 0;
      text-align: center;
    }

    h1 {
      background: #007bff;
      color: white;
      padding: 15px 0;
      margin-bottom: 20px;
    }

    .form-container {
      background: white;
      padding: 20px;
      margin: auto;
      width: 400px;
      box-shadow: 0 0 10px rgba(0,0,0,0.2);
      border-radius: 10px;
    }

    input {
      display: block;
      width: 90%;
      margin: 10px auto;
      padding: 10px;
      font-size: 16px;
      border: 1px solid #ccc;
      border-radius: 5px;
    }

    button {
      background: #007bff;
      color: white;
      border: none;
      padding: 10px 20px;
      font-size: 16px;
      border-radius: 5px;
      cursor: pointer;
    }

    button:hover {
      background: #0056b3;
    }

    table {
      margin: 30px auto;
      width: 80%;
      border-collapse: collapse;
    }

    th, td {
      border: 1px solid #ccc;
      padding: 10px;
      font-size: 16px;
    }

    th {
      background: #007bff;
      color: white;
    }

    .no-data {
      color: gray;
      font-style: italic;
    }
  </style>
</head>
<body>
  <h1>Student Record Management System</h1>

  <div class="form-container">
    <h2>Add Student</h2>
    <input type="number" id="roll" placeholder="Enter Roll Number" required>
    <input type="text" id="name" placeholder="Enter Name" required>
    <input type="number" id="marks" placeholder="Enter Marks" required>
    <button onclick="addStudent()">Add Student</button>
  </div>

  <h2>Student Records</h2>
  <table>
    <thead>
      <tr>
        <th>Roll No</th>
        <th>Name</th>
        <th>Marks</th>
      </tr>
    </thead>
    <tbody id="studentTable"></tbody>
  </table>

  <script>
    // Load students from localStorage
    function loadStudents() {
      const students = JSON.parse(localStorage.getItem("students")) || [];
      const tableBody = document.getElementById("studentTable");
      tableBody.innerHTML = "";

      if (students.length === 0) {
        tableBody.innerHTML = '<tr><td colspan="3" class="no-data">No records found</td></tr>';
        return;
      }

      students.forEach(s => {
        const row = `<tr>
          <td>${s.roll}</td>
          <td>${s.name}</td>
          <td>${s.marks}</td>
        </tr>`;
        tableBody.innerHTML += row;
      });
    }

    // Add a student record
    function addStudent() {
      const roll = document.getElementById("roll").value;
      const name = document.getElementById("name").value;
      const marks = document.getElementById("marks").value;

      if (!roll || !name || !marks) {
        alert("Please fill all fields!");
        return;
      }

      const students = JSON.parse(localStorage.getItem("students")) || [];
      students.push({ roll, name, marks });
      localStorage.setItem("students", JSON.stringify(students));

      document.getElementById("roll").value = "";
      document.getElementById("name").value = "";
      document.getElementById("marks").value = "";

      loadStudents();
      alert("Student added successfully!");
    }

    // Initialize table on load
    loadStudents();
  </script>
</body>
</html>

'''
