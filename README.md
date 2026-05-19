<!DOCTYPE html>
<html>
<head>
    <title>Email Validation</title>

    <style>

        body {
            background-color: #f2f2f2;
            font-family: Arial, sans-serif;
            text-align: center;
            padding-top: 100px;
        }

        h2 {
            color: #333;
        }

        input {
            width: 250px;
            padding: 10px;
            font-size: 16px;
            border: 2px solid #007BFF;
            border-radius: 5px;
        }

        button {
            padding: 10px 20px;
            font-size: 16px;
            background-color: #007BFF;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            margin-left: 10px;
        }

        button:hover {
            background-color: #0056b3;
        }

        #result {
            margin-top: 20px;
            font-size: 18px;
            font-weight: bold;
        }

    </style>

</head>

<body>

    <h2>Email Validation Form</h2>

    <input type="text" id="email" placeholder="Enter Email">
    
    <button onclick="validateEmail()">Check</button>

    <p id="result"></p>

    <script>

        function validateEmail() {

            let email = document.getElementById("email").value;

            let regex = /^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$/;

            if (regex.test(email)) {

                document.getElementById("result").innerHTML =
                "Valid Email Address";

                document.getElementById("result").style.color = "green";
            }

            else {

                document.getElementById("result").innerHTML =
                "Invalid Email Address";

                document.getElementById("result").style.color = "red";
            }
        }

    </script>

</body>
</html>
