<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CAPTCHA Generator</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            background-color: #f4f4f4;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }

        .captcha-container {
            display: flex;
            flex-direction: column;
            align-items: center;
            background-color: #fff;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        }

        h1 {
            color: #333;
            margin-bottom: 20px;
        }

        #captcha {
            font-size: 24px;
            font-weight: bold;
            padding: 10px;
            background-color: #e2e2e2;
            border: 1px solid #ccc;
            border-radius: 5px;
            margin-bottom: 20px;
            letter-spacing: 3px;
        }

        input[type="text"] {
            padding: 10px;
            font-size: 16px;
            margin-bottom: 20px;
            width: 220px;
            border: 1px solid #ccc;
            border-radius: 5px;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
        }

        button {
            padding: 10px 20px;
            font-size: 16px;
            margin: 5px;
            cursor: pointer;
            border: none;
            background-color: #007bff;
            color: white;
            border-radius: 5px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
            transition: background-color 0.3s ease;
        }

        button:hover {
            background-color: #0056b3;
        }
    </style>
</head>
<body>
    <div class="captcha-container">
        <h1>CAPTCHA</h1>
        <div id="captcha"></div>
        <input type="text" id="userInput" placeholder="Enter CAPTCHA">
        <button onclick="validateCaptcha()">Submit</button>
        <button onclick="generateCaptcha()">New CAPTCHA</button>
        <div id="alert"></div>
    </div>

    <script>
        let attemptCount = 0;

        function generateCaptcha() {
            const characters = 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789';
            let captcha = '';
            for (let i = 0; i < 6; i++) {
                const randomIndex = Math.floor(Math.random() * characters.length);
                captcha += characters[randomIndex];
            }
            document.getElementById('captcha').textContent = captcha;
        }

        function validateCaptcha() {
            const userInput = document.getElementById('userInput').value;
            const captcha = document.getElementById('captcha').textContent;
            if (userInput === captcha) {
                alert('CAPTCHA validated successfully!');
                // You can proceed with form submission or other actions here
                attemptCount = 0;  // Reset attempt counter on success
            } else {
                attemptCount++;
                if (attemptCount >= 3) {
                    document.getElementById('alert').textContent = 'Too many failed attempts. Please wait 25 seconds.';
                    document.getElementById('alert').style.color = 'red';
                    setTimeout(() => {
                        generateCaptcha();
                        document.getElementById('alert').textContent = '';
                        attemptCount = 0; // Reset attempt counter after delay
                    }, 25000);
                } else {
                    alert('CAPTCHA validation failed. Please try again.');
                    generateCaptcha();
                }
            }
        }

        // Generate initial CAPTCHA
        generateCaptcha();
    </script>
</body>
</html>
 
 
 
