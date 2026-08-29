# Apex_planet.task-2
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Intermediate Web Task</title>
  <style>
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      font-family: Arial, sans-serif;
    }

    body {
      background-color: #f4f7f6;
      color: #333;
    }

    /* Step 3: Flexbox Navigation */
    .navbar {
      display: flex;
      justify-content: space-between;
      align-items: center;
      background-color: #005a52;
      color: white;
      padding: 1rem 2rem;
    }

    .nav-links {
      display: flex;
      gap: 15px;
      list-style: none;
    }

    /* Step 3: CSS Grid for Main Content */
    .container {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 20px;
      padding: 20px;
      max-width: 1000px;
      margin: auto;
    }

    .card {
      background: white;
      padding: 20px;
      border-radius: 8px;
      box-shadow: 0 4px 6px rgba(0,0,0,0.1);
    }

    /* Step 1: Form Styling */
    .form-group {
      margin-bottom: 15px;
    }

    label {
      display: block;
      margin-bottom: 5px;
      font-weight: bold;
    }

    input, textarea {
      width: 100%;
      padding: 8px;
      border: 1px solid #ccc;
      border-radius: 4px;
    }

    button {
      background-color: #005a52;
      color: white;
      border: none;
      padding: 10px 15px;
      border-radius: 4px;
      cursor: pointer;
    }

    button:hover {
      background-color: #003d37;
    }

    .error {
      color: red;
      font-size: 0.85rem;
      display: none;
    }

    /* Step 4: Dynamic To-Do List Styling */
    ul {
      list-style: none;
      margin-top: 15px;
    }

    li {
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 8px;
      background: #e9ecef;
      margin-bottom: 5px;
      border-radius: 4px;
    }

    .delete-btn {
      background: red;
      padding: 4px 8px;
      font-size: 0.8rem;
    }

    /* Step 3: Media Query for Responsiveness */
    @media (max-width: 768px) {
      .container {
        grid-template-columns: 1fr;
      }
      .navbar {
        flex-direction: column;
        gap: 10px;
      }
    }
  </style>
</head>
<body>

  <!-- Flexbox Navigation Header -->
  <header class="navbar">
    <h2>ApexPlanet Dashboard</h2>
    <ul class="nav-links">
      <li>Home</li>
      <li>Form</li>
      <li>To-Do</li>
    </ul>
  </header>

  <!-- Responsive CSS Grid Layout -->
  <main class="container">
    
    <!-- Step 1 & 2: Contact Form with Validation -->
    <section class="card">
      <h3>Contact Us</h3>
      <form id="contactForm" onsubmit="validateForm(event)">
        <div class="form-group">
          <label for="name">Name:</label>
          <input type="text" id="name" placeholder="Enter name">
          <span class="error" id="nameError">Name is required.</span>
        </div>

        <div class="form-group">
          <label for="email">Email:</label>
          <input type="text" id="email" placeholder="Enter email">
          <span class="error" id="emailError">Please enter a valid email address.</span>
        </div>

        <button type="submit">Submit</button>
      </form>
    </section>

    <!-- Step 4: Dynamic To-Do List -->
    <section class="card">
      <h3>Dynamic To-Do List</h3>
      <div style="display: flex; gap: 5px;">
        <input type="text" id="taskInput" placeholder="Add a new task...">
        <button onclick="addTask()">Add Task</button>
      </div>
      <ul id="taskList"></ul>
    </section>

  </main>

  <script>
    // Step 2: Form Validation Logic
    function validateForm(event) {
      event.preventDefault();
      
      const name = document.getElementById('name').value.trim();
      const email = document.getElementById('email').value.trim();
      const nameError = document.getElementById('nameError');
      const emailError = document.getElementById('emailError');

      let isValid = true;

      if (name === '') {
        nameError.style.display = 'block';
        isValid = false;
      } else {
        nameError.style.display = 'none';
      }

      // Simple Email Regex check
      const emailPattern = /^[^ ]+@[^ ]+\.[a-z]{2,3}$/;
      if (!email.match(emailPattern)) {
        emailError.style.display = 'block';
        isValid = false;
      } else {
        emailError.style.display = 'none';
      }

      if (isValid) {
        alert('Form submitted successfully!');
        document.getElementById('contactForm').reset();
      }
    }

    // Step 4: DOM Manipulation To-Do List Logic
    function addTask() {
      const taskInput = document.getElementById('taskInput');
      const taskText = taskInput.value.trim();

      if (taskText === '') return;

      const li = document.createElement('li');
      li.innerHTML = `
        <span>${taskText}</span>
        <button class="delete-btn" onclick="removeTask(this)">Remove</button>
      `;

      document.getElementById('taskList').appendChild(li);
      taskInput.value = '';
    }

    function removeTask(button) {
      button.parentElement.remove();
    }
  </script>
</body>
</html>
