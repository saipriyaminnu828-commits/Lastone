<!DOCTYPE html>
<html>
<head>

<title>Email → IP → Location Flow</title>

<style>

body {
    font-family: Arial;
    text-align: center;
    background: #f2f2f2;
    padding-top: 40px;
}

input {
    padding: 10px;
    width: 250px;
    border: 2px solid #007BFF;
    border-radius: 5px;
}

button {
    padding: 10px 20px;
    margin-top: 10px;
    background: #007BFF;
    color: white;
    border: none;
    border-radius: 5px;
}

section {
    display: none;
    margin-top: 25px;
}

</style>

</head>

<body>

<!-- EMAIL -->
<h2>Email Validation</h2>

<input id="email" placeholder="Enter Email">

<br>

<button onclick="validateEmail()">Validate Email</button>
<button onclick="goIP()">Next</button>

<p id="msg1"></p>

<!-- IP -->
<section id="ipSection">

<h2>IP Address Verification</h2>

<button onclick="checkIP()">Check IP</button>
<button onclick="goLocation()">Next</button>

<p id="msg2"></p>

</section>

<!-- LOCATION -->
<section id="locSection">

<h2>Location traced using IP address</h2>

<button onclick="getLocation()">Click here</button>

<p id="msg3"></p>

<button onclick="closeAll()">Close ✖</button>

</section>

<script>

let emailOk = false;
let ipOk = false;

// EMAIL VALIDATION
function validateEmail() {

    let email = document.getElementById("email").value;

    let regex =
    /^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$/;

    if(regex.test(email)) {

        emailOk = true;

        document.getElementById("msg1").innerHTML =
        "Valid Email";

        document.getElementById("msg1").style.color =
        "green";

    } else {

        emailOk = false;

        document.getElementById("msg1").innerHTML =
        "Invalid Email - BLOCKED ❌";

        document.getElementById("msg1").style.color =
        "red";
    }
}

// NEXT AFTER EMAIL
function goIP() {

    if(emailOk) {

        document.getElementById("ipSection").style.display =
        "block";

    } else {

        alert("❌ Email invalid. Access blocked.");
    }
}

// IP CHECK
async function checkIP() {

    if(!emailOk) {
        alert("❌ Email not valid. IP blocked.");
        return;
    }

    let res =
    await fetch("https://api.ipify.org?format=json");

    let data = await res.json();

    let ip = data.ip;

    let regex =
    /^(25[0-5]|2[0-4][0-9]|1[0-9][0-9]|[1-9]?[0-9])(\.(25[0-5]|2[0-4][0-9]|1[0-9][0-9]|[1-9]?[0-9])){3}$/;

    if(regex.test(ip)) {

        ipOk = true;

        document.getElementById("msg2").innerHTML =
        "Valid IP: " + ip;

        document.getElementById("msg2").style.color =
        "green";

    } else {

        ipOk = false;

        document.getElementById("msg2").innerHTML =
        "Invalid IP - BLOCKED ❌";

        document.getElementById("msg2").style.color =
        "red";
    }
}

// NEXT TO LOCATION
function goLocation() {

    if(ipOk) {

        document.getElementById("locSection").style.display =
        "block";

    } else {

        alert("❌ IP invalid. Cannot proceed.");
    }
}

// LOCATION TRACE
function getLocation() {

    fetch("https://ipapi.co/json/")
    .then(res => res.json())
    .then(data => {

        document.getElementById("msg3").innerHTML =
        "City: " + data.city +
        "<br>Country: " + data.country_name +
        "<br>IP: " + data.ip;

    });

}

// CLOSE
function closeAll() {

    document.getElementById("ipSection").style.display = "none";
    document.getElementById("locSection").style.display = "none";

    document.getElementById("email").value = "";

    document.getElementById("msg1").innerHTML = "";
    document.getElementById("msg2").innerHTML = "";
    document.getElementById("msg3").innerHTML = "";

    emailOk = false;
    ipOk = false;
}

</script>

</body>
</html>
