<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Table Tennis Predictions - Lithuania</title>
  <style>
    /* Reset margins and paddings */
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    /* Styles for body */
    body {
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      background-color: #f0f0f0;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      color: #333;
    }

    /* Main container */
    .container {
      max-width: 800px;
      width: 100%;
      padding: 20px;
      background-color: #fff;
      border-radius: 8px;
      box-shadow: 0 0 20px rgba(0, 0, 0, 0.1);
    }

    /* Header */
    header {
      text-align: center;
      margin-bottom: 20px;
    }

    header h1 {
      color: #4CAF50;
      font-size: 2.5rem;
    }

    /* Warning */
    .warning {
      background-color: #f44336;
      color: white;
      text-align: center;
      padding: 10px;
      margin-bottom: 20px;
      border-radius: 4px;
      font-weight: bold;
    }

    /* Form */
    .form {
      margin-bottom: 20px;
    }

    .form h2 {
      margin-bottom: 10px;
      color: #555;
      text-align: center;
    }

    .form input[type="text"],
    .form input[type="password"],
    .form button {
      width: 100%;
      padding: 12px;
      margin-bottom: 10px;
      border: 1px solid #ccc;
      border-radius: 4px;
      font-size: 1rem;
      outline: none;
    }

    .form button {
      background-color: #4CAF50;
      color: white;
      cursor: pointer;
      transition: background-color 0.3s ease;
    }

    .form button:hover {
      background-color: #45a049;
    }

    .form p {
      text-align: center;
      margin-top: 10px;
    }

    .form p a {
      color: #007bff;
      text-decoration: none;
    }

    .form p a:hover {
      text-decoration: underline;
    }

    /* Predictions List */
    .predictions-list {
      margin-top: 20px;
    }

    .predictions-list div {
      background-color: #f9f9f9;
      border: 1px solid #ddd;
      padding: 12px;
      margin-bottom: 10px;
      border-radius: 4px;
      font-size: 1rem;
    }

    /* Ping Pong Image */
    .ping-pong-image {
      margin-top: 20px;
      max-width: 100%;
      height: auto;
      display: block;
      margin-left: auto;
      margin-right: auto;
    }

    /* Footer */
    footer {
      margin-top: 20px;
      text-align: center;
      color: #888;
    }
  </style>
</head>
<body>
  <div class="container">
    <header>
      <h1>Table Tennis Predictions - Lithuania</h1>
    </header>

    <div class="warning">
      WARNING: Do not communicate with others to avoid legal risks. Using VPN - Location: Unknown.
    </div>

    <div id="register-form" class="form" style="display: none;">
      <h2>Registration</h2>
      <input type="text" id="register-username" placeholder="Username">
      <input type="password" id="register-password" placeholder="Password">
      <button onclick="register()">Register</button>
      <p><a href="#" onclick="showLoginForm()">Already have an account? Login here.</a></p>
    </div>

    <div id="login-form" class="form">
      <h2>Administrator Login</h2>
      <input type="text" id="admin-username" placeholder="Username">
      <input type="password" id="admin-password" placeholder="Password">
      <button onclick="login()">Login</button>
      <p><a href="#" onclick="showRegisterForm()">Don't have an account? Register here.</a></p>
    </div>

    <div id="predictions-form" class="form" style="display: none;">
      <h2>Add Prediction</h2>
      <input type="text" id="match" placeholder="Match">
      <input type="text" id="prediction" placeholder="Prediction">
      <button onclick="addPrediction()">Add Prediction</button>
      <button onclick="logout()">Logout</button>
    </div>

    <div id="predictions-list" class="predictions-list"></div>
    
    <img src="ping-pong.jpg" alt="Ping Pong Image" class="ping-pong-image">

    <footer>
      <p>Website for table tennis predictions - Lithuania</p>
      <p>Current time: <span id="current-time"></span></p>
      <p>Time zones: Lithuania (EEST), New York (EDT), Tokyo (JST)</p>
    </footer>
  </div>

  <script>
    document.addEventListener('DOMContentLoaded', () => {
      const adminLoggedIn = localStorage.getItem('adminLoggedIn');
      const giancarloitaLoggedIn = localStorage.getItem('giancarloitaLoggedIn');

      if (adminLoggedIn === 'true') {
        showPredictionsForm();
      } else if (giancarloitaLoggedIn === 'true') {
        showPredictionsListOnly();
      }

      updateTime();
      setInterval(updateTime, 1000); // Update time every second
      fetchPredictions(); // Fetch predictions initially
    });

    function login() {
      const username = document.getElementById('admin-username').value;
      const password = document.getElementById('admin-password').value;

      // Check admin credentials
      if (username === 'admin' && password === 'gico1237') {
        localStorage.setItem('adminLoggedIn', 'true');
        localStorage.removeItem('giancarloitaLoggedIn'); // Remove giancarloita login if admin logs in
        showPredictionsForm();
      } else if (username === 'giancarloita' && password === 'itagianca16') {
        localStorage.setItem('giancarloitaLoggedIn', 'true');
        localStorage.removeItem('adminLoggedIn'); // Remove admin login if giancarloita logs in
        showPredictionsListOnly();
        alert('WELCOME TO THE TEAM. DO NOT DISCLOSE THIS INFORMATION TO AVOID PROBLEMS');
      } else {
        alert('Invalid username or password');
      }
    }

    function logout() {
      localStorage.removeItem('adminLoggedIn');
      localStorage.removeItem('giancarloitaLoggedIn');
      showLoginForm();
    }

    function showLoginForm() {
      document.getElementById('login-form').style.display = 'block';
      document.getElementById('predictions-form').style.display = 'none';
      document.getElementById('register-form').style.display = 'none';
    }

    function showPredictionsForm() {
      document.getElementById('login-form').style.display = 'none';
      document.getElementById('predictions-form').style.display = 'block';
      document.getElementById('register-form').style.display = 'none';
      fetchPredictions();
    }

    function showPredictionsListOnly() {
      document.getElementById('login-form').style.display = 'none';
      document.getElementById('predictions-form').style.display = 'none';
      document.getElementById('register-form').style.display = 'none';
      fetchPredictions();
    }

    function showRegisterForm() {
      document.getElementById('login-form').style.display = 'none';
      document.getElementById('predictions-form').style.display = 'none';
      document.getElementById('register-form').style.display = 'block';
    }

    function register() {
      const username = document.getElementById('register-username').value;
      const password = document.getElementById('register-password').value;

      // Allow registration only for the specific user
      if (username === 'giancarloita' && password === 'itagianca16') {
        alert('WELCOME TO THE TEAM. DO NOT DISCLOSE THIS INFORMATION TO AVOID PROBLEMS');
        showLoginForm();
      } else {
        alert('Registration is restricted to specific users.');
      }

      document.getElementById('register-username').value = '';
      document.getElementById('register-password').value = '';
    }

    function addPrediction() {
      const match = document.getElementById('match').value;
      const prediction = document.getElementById('prediction').value;

      if (match && prediction) {
        const predictions = JSON.parse(localStorage.getItem('predictions')) || [];
        predictions.push({ match, prediction });
        localStorage.setItem('predictions', JSON.stringify(predictions));
        fetchPredictions();
        document.getElementById('match').value = '';
        document.getElementById('prediction').value = '';
      } else {
        alert('Please fill in both fields');
      }
    }

    function fetchPredictions() {
      const predictionsList = document.getElementById('predictions-list');
      predictionsList.innerHTML = '';

      const predictions = JSON.parse(localStorage.getItem('predictions')) || [];
      predictions.forEach(prediction => {
        const div = document.createElement('div');
        div.textContent = `Match: ${prediction.match}, Prediction: ${prediction.prediction}`;
        predictionsList.appendChild(div);
      });
    }

    function updateTime() {
      const now = new Date();
      document.getElementById('current-time').textContent = now.toLocaleTimeString();

      // Update other time zones if necessary
    }
  </script>
</body>
</html>
