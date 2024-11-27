


<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <link rel="stylesheet" href="style.css" />
    <title>Registration Form</title>
    <style>
      
        body {
            font-family: Arial, sans-serif;
            background: #f4f4f9;
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }

        form {
            background: #fff;
            padding: 20px 40px;
            border-radius: 10px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
            width: 100%;
            max-width: 400px;
        }

        h1 {
            text-align: center;
            color: #333;
            margin-bottom: 20px;
        }

        fieldset {
            border: none;
            margin: 15px 0;
        }

        legend {
            font-size: 18px;
            color: #333;
            margin-bottom: 10px;
        }

        label {
            display: block;
            margin: 10px 0 5px;
            color: #555;
        }

        input,
        select,
        textarea {
            width: 100%;
            padding: 10px;
            margin-bottom: 15px;
            border: 1px solid #ddd;
            border-radius: 5px;
            font-size: 14px;
            color: #333;
            background: #f9f9f9;
        }

        input:focus,
        select:focus,
        textarea:focus {
            border-color: #6c63ff;
            outline: none;
            background: #fff;
        }

        button {
            width: 100%;
            padding: 10px;
            background: #6c63ff;
            color: #fff;
            font-size: 16px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            transition: background 0.3s ease;
        }

        button:hover {
            background: #574bff;
        }

        .alert {
            display: none;
            background: #d4edda;
            color: #155724;
            padding: 10px;
            margin-bottom: 20px;
            border-left: 5px solid #28a745;
            border-radius: 5px;
            font-size: 14px;
        }

        .section {
            background: #6c63ff;
            color: #fff;
            padding: 5px 10px;
            border-radius: 50%;
            font-size: 12px;
            margin-right: 5px;
        }
    </style>
</head>

<body>
    <form id="registrationform">
        <h1>Register</h1>
        <div class="alert">Form Submitted Successfully</div>

        <fieldset>
            <legend><span class="section">1</span>Your Basic Info</legend>
            <label for="name">Name:</label>
            <input type="text" name="name" id="name" required />

            <label for="email">Email:</label>
            <input type="email" name="email" id="email" required />

            <label for="password">Password:</label>
            <input type="password" name="password" id="password" required />
        </fieldset>

        <!-- Section 2 -->
        <fieldset>
            <legend><span class="section">2</span>Profile</legend>
            <label for="bio">Bio:</label>
            <textarea name="bio" id="bio" rows="4" required></textarea>

            <label for="job">Job Role:</label>
            <select name="job" id="job" required>
                <optgroup label="Web">
                    <option value="front_end_developer">Frontend Developer</option>
                    <option value="back_end_developer">Backend Developer</option>
                    <option value="fullstack_developer">Fullstack Developer</option>
                </optgroup>
                <optgroup label="Mobile">
                    <option value="android">Android</option>
                    <option value="ionic">Ionic</option>
                    <option value="phonegap">PhoneGap</option>
                </optgroup>
            </select>

            <label for="interest">Interest:</label>
            <select id="interest" required>
                <option value="development">Development</option>
                <option value="design">Design</option>
                <option value="business">Business</option>
            </select>
        </fieldset>

        <button type="submit">Register</button>
    </form>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/9.15.0/firebase-app.js";
        import { getDatabase, ref, set } from "https://www.gstatic.com/firebasejs/9.15.0/firebase-database.js";

        // Firebase Configuration
        const firebaseConfig = {
            apiKey: "AIzaSyDGta-gMTgZETyGK7QmvuOouglowIVlwAw",
            authDomain: "my-app-3a3b4.firebaseapp.com",
            databaseURL: "https://my-app-3a3b4-default-rtdb.firebaseio.com",
            projectId: "my-app-3a3b4",
            storageBucket: "my-app-3a3b4.appspot.com",
            messagingSenderId: "73920339349",
            appId: "1:73920339349:web:535b303950123b731cea9c",
            measurementId: "G-LGG1VD0JLX"
        };

        // Initialize Firebase
        const app = initializeApp(firebaseConfig);
        const database = getDatabase(app);

        // Handle form submission
        const form = document.getElementById('registrationform');
        const alertBox = document.querySelector('.alert');

        form.addEventListener('submit', function (e) {
            e.preventDefault();

            // Retrieve form data
            const name = document.getElementById('name').value;
            const email = document.getElementById('email').value;
            const password = document.getElementById('password').value;
            const bio = document.getElementById('bio').value;
            const job = document.getElementById('job').value;
            const interest = document.getElementById('interest').value;

            // Save data to Firebase
            set(ref(database, 'users/' + Math.floor(Math.random() * 10000000)), {
                name,
                email,
                password,
                bio,
                job,
                interest
            }).then(() => {
                // Display success alert
                alertBox.style.display = 'block';
                setTimeout(() => alertBox.style.display = 'none', 7000);

                // Reset the form
                form.reset();
            }).catch((error) => {
                alert(`Error: ${error.message}`);
            });
        });
    </script>
</body>

</html>
