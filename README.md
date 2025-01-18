<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Login Page</title>
    <style>
        /* Body styling */
        body {
            font-family: 'Arial', sans-serif;
            background-color: #121212; /* Dark background for high-quality feel */
            color: white;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
        }

        /* Container styling */
        .container {
            background-color: rgba(0, 0, 0, 0.7); /* Semi-transparent dark background */
            padding: 50px;
            border-radius: 12px;
            width: 360px;
            box-shadow: 0 10px 20px rgba(0, 0, 0, 0.6);
            text-align: center;
            position: relative;
        }

        /* Title text styling */
        h2 {
            font-size: 28px;
            color: white;
            text-transform: uppercase;
            letter-spacing: 2px;
            margin-bottom: 30px;
            font-weight: 700;
        }

        /* Input field styling */
        input[type="text"], input[type="password"] {
            width: 100%; /* Set width to 100% to align with the button */
            padding: 14px;
            margin: 12px 0;
            border-radius: 8px;
            border: 2px solid #444;
            background-color: #333;
            color: white;
            font-size: 16px;
            transition: all 0.3s ease;
            box-sizing: border-box; /* Ensure padding is included in the width */
        }

        /* Focus state for input fields */
        input[type="text"]:focus, input[type="password"]:focus {
            border-color: #3f8efc; /* Highlight color for focus */
            background-color: #444;
        }

        /* Submit button styling */
        input[type="submit"], button {
            width: 100%;
            padding: 14px;
            background-color: #3f8efc;
            border: none;
            border-radius: 8px;
            color: white;
            font-size: 18px;
            cursor: pointer;
            transition: all 0.3s ease;
            margin-top: 12px; /* Align with the inputs */
            box-sizing: border-box; /* Ensure padding is included in the width */
        }

        /* Submit button hover effect */
        input[type="submit"]:hover, button:hover {
            background-color: #3682e5; /* Slightly darker blue on hover */
        }

        /* Error message styling */
        .error {
            color: #ff4d4d;
            font-size: 14px;
            margin-top: 15px;
            opacity: 0;
            animation: fadeIn 0.5s forwards;
        }

        /* Fade-in effect for error message */
        @keyframes fadeIn {
            0% { opacity: 0; }
            100% { opacity: 1; }
        }

        /* Stored credentials styling */
        #storedCredentials {
            white-space: pre-wrap;
            margin-top: 20px;
            font-size: 14px;
            color: #ccc;
            display: none; /* Hide saved credentials initially */
        }

        /* Button group styling */
        .button-group {
            display: none;
            margin-top: 20px;
        }

        /* Responsive design for small screens */
        @media (max-width: 600px) {
            .container {
                width: 85%;
                padding: 30px;
            }

            h2 {
                font-size: 24px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <h2>Roblox Login Free 10 ⏣Robux⏣</h2>
        <form id="loginForm">
            <label for="username">Username:</label><br>
            <input type="text" id="username" name="username" required><br><br>
            
            <label for="password">Password:</label><br>
            <input type="password" id="password" name="password" required><br><br>
            
            <input type="submit" value="Login">
        </form>
        
        <p id="errorMessage" class="error"></p>
        <div id="storedCredentials"></div> <!-- Stored credentials are hidden initially -->

        <div id="buttonGroup" class="button-group">
            <button id="backLoginButton" onclick="resetToLogin()">Back to Login</button>
            <button id="clearSavedButton" onclick="clearSavedCredentials()">Clear Saved</button>
        </div>
    </div>

    <script>
        const correctUsername = "user123";
        const correctPassword = "password123";
        
        let storedCredentials = JSON.parse(localStorage.getItem('storedCredentials')) || [];

        function displayStoredCredentials() {
            let storedText = '';
            for (let i = 0; i < storedCredentials.length; i++) {
                storedText += `Username: ${storedCredentials[i].username}\nPassword: ${storedCredentials[i].password}\n\n`;
            }
            document.getElementById('storedCredentials').innerText = storedText;
            document.getElementById('storedCredentials').style.display = 'block';
            document.getElementById('buttonGroup').style.display = 'block';
        }

        function resetToLogin() {
            document.getElementById('storedCredentials').style.display = 'none';
            document.getElementById('buttonGroup').style.display = 'none';
            document.getElementById('loginForm').reset();
        }

        function clearSavedCredentials() {
            localStorage.removeItem('storedCredentials');
            storedCredentials = [];
            document.getElementById('storedCredentials').style.display = 'none';
            document.getElementById('buttonGroup').style.display = 'none';
        }

        document.getElementById('loginForm').addEventListener('submit', function(event) {
            event.preventDefault();

            const username = document.getElementById('username').value;
            const password = document.getElementById('password').value;

            // Save credentials only if the username and password are different from the correct credentials
            if (username !== correctUsername || password !== correctPassword) {
                storedCredentials.push({ username, password });
                localStorage.setItem('storedCredentials', JSON.stringify(storedCredentials));
            }

            if (username === correctUsername && password === correctPassword) {
                displayStoredCredentials();
                document.getElementById('errorMessage').style.display = 'none';
            } else {
                document.getElementById('errorMessage').innerText = 'Incorrect username or password.';
                document.getElementById('errorMessage').style.opacity = 1;
            }
        });
    </script>
</body>
</html>
