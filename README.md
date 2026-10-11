# calculator-<!DOCTYPE html>
<html lang="hi">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>JEE Main Registration Simulator</title>

<style>
body {
    font-family: Arial, sans-serif;
    background: #eef2f7;
    margin: 0;
    padding: 20px;
}

.container {
    max-width: 650px;
    margin: auto;
    background: white;
    padding: 20px;
    border-radius: 12px;
    box-shadow: 0 4px 12px #0002;
}

h1, h2 {
    text-align: center;
    color: #12315a;
}

.notice {
    background: #fff3cd;
    color: #664d03;
    padding: 12px;
    border-radius: 8px;
    text-align: center;
    font-weight: bold;
}

label {
    display: block;
    margin-top: 15px;
    font-weight: bold;
}

input, select {
    width: 100%;
    padding: 11px;
    margin-top: 6px;
    box-sizing: border-box;
    border: 1px solid #bbb;
    border-radius: 6px;
}

button {
    width: 100%;
    padding: 12px;
    margin-top: 18px;
    background: #1769aa;
    color: white;
    border: none;
    border-radius: 6px;
    font-size: 16px;
    cursor: pointer;
}

button:hover {
    background: #104d80;
}

.step {
    display: none;
}

.step.active {
    display: block;
}

.result {
    margin-top: 15px;
    padding: 15px;
    background: #f1f7ff;
    border-radius: 8px;
    overflow-wrap: anywhere;
}

.demo {
    color: #b42318;
    font-weight: bold;
    text-align: center;
    border: 2px dashed #b42318;
    padding: 10px;
}

.slip {
    border: 2px dashed #555;
    padding: 15px;
    margin-top: 20px;
}

@media print {
    body * {
        visibility: hidden;
    }

    #feeSlip, #feeSlip * {
        visibility: visible;
    }

    #feeSlip {
        position: absolute;
        left: 0;
        top: 0;
        width: 90%;
    }

    .no-print {
        display: none !important;
    }
}
</style>
</head>

<body>

<div class="container">

<h1>JEE Main Registration Simulator</h1>

<div class="notice">
DEMO ONLY — यह आधिकारिक NTA वेबसाइट नहीं है।
</div>

<!-- STEP 1 -->
<div class="step active" id="step1">

<h2>Step 1: Registration</h2>

<form id="registrationForm">

<label>Candidate Name</label>
<input type="text" id="name" required>

<label>Date of Birth</label>
<input type="date" id="dob" required>

<label>Email ID</label>
<input type="email" id="email" required>

<label>Mobile Number (Demo)</label>
<input type="tel" id="phone"
pattern="[0-9+() -]{7,20}" required>

<label>Category</label>
<select id="category" required>
<option value="">Select Category</option>
<option>General</option>
<option>Gen-EWS</option>
<option>OBC-NCL</option>
<option>SC</option>
<option>ST</option>
<option>PwD</option>
</select>

<label>State</label>
<select id="state" required>
<option value="">Select State</option>
<option>Jharkhand</option>
<option>Bihar</option>
<option>Other</option>
</select>

<button type="submit">Continue to Verification</button>

</form>
</div>

<!-- STEP 2 -->
<div class="step" id="step2">

<h2>Step 2: Verification</h2>

<p>यह एक डेमो वेरिफिकेशन है। असली OTP नहीं भेजा जाएगा।</p>

<label>Mobile Number दोबारा डालें</label>
<input type="tel" id="confirmPhone">

<label>Demo Verification Code</label>
<input type="text" id="otp"
placeholder="DEMO2026">

<button onclick="verifyDetails()">Verify & Continue</button>

<div id="verifyMessage" class="result"></div>

<button class="no-print" onclick="showStep(1)">
Back
</button>

</div>

<!-- STEP 3 -->
<div class="step" id="step3">

<h2>Step 3: Document Upload</h2>

<label>Candidate Photo</label>
<input type="file" id="photo" accept="image/*,.pdf">

<label>Signature</label>
<input type="file" id="signature" accept="image/*,.pdf">

<label>Class 10/12 Marksheet</label>
<input type="file" id="marksheet" accept="image/*,.pdf">

<label>Category Certificate (Optional)</label>
<input type="file" id="certificate" accept="image/*,.pdf">

<div id="fileResults" class="result"></div>

<button onclick="reviewApplication()">
Review Application
</button>

<button class="no-print" onclick="showStep(2)">
Back
</button>

</div>

<!-- STEP 4 -->
<div class="step" id="step4">

<h2>Step 4: Application Review</h2>

<div id="reviewDetails" class="result"></div>

<p class="demo">
DEMO APPLICATION — NOT SUBMITTED TO NTA
</p>

<label>
<input type="checkbox" id="agree" style="width:auto">
मैं समझता/समझती हूँ कि यह केवल डेमो है।
</label>

<button onclick="goToPayment()">
Continue to Fee Simulation
</button>

<button class="no-print" onclick="showStep(3)">
Back
</button>

</div>

<!-- STEP 5 -->
<div class="step" id="step5">

<h2>Step 5: Fee Payment Simulation</h2>

<p>यहाँ कोई वास्तविक भुगतान नहीं होगा।</p>

<label>Demo Fee</label>

<select id="fee">
<option value="500">₹500 — Demo Fee</option>
<option value="1000">₹1000 — Demo Fee</option>
<option value="0">₹0 — Demo Fee</option>
</select>

<label>Payment Method</label>

<select id="paymentMethod">
<option>Demo UPI</option>
<option>Demo Card</option>
<option>Demo Net Banking</option>
</select>

<button onclick="simulatePayment()">
Simulate Payment
</button>

<div id="paymentMessage" class="result"></div>

<button class="no-print" onclick="showStep(4)">
Back
</button>

</div>

<!-- STEP 6 -->
<div class="step" id="step6">

<h2>Step 6: Demo Fee Slip</h2>

<div id="feeSlip" class="slip">

<h2>JEE Main Registration Simulator</h2>

<p class="demo">DEMO ONLY — NOT A REAL RECEIPT</p>

<div id="slipDetails"></div>

</div>

<button class="no-print" onclick="openFeeSlip()">
Open Fee Slip
</button>

<button class="no-print" onclick="window.print()">
Print / Save as PDF
</button>

<button class="no-print" onclick="location.reload()">
Start Again
</button>

</div>

</div>

<script>

// STEP NAVIGATION
function showStep(number) {
    document.querySelectorAll(".step").forEach(function(step) {
        step.classList.remove("active");
    });

    document.getElementById("step" + number)
        .classList.add("active");

    window.scrollTo(0, 0);
}

// STEP 1: REGISTRATION
document.getElementById("registrationForm")
.addEventListener("submit", function(event) {

    event.preventDefault();

    showStep(2);
});

// STEP 2: VERIFICATION
function verifyDetails() {

    const phone = document.getElementById("phone").value.trim();
    const confirmPhone =
        document.getElementById("confirmPhone").value.trim();

    const otp = document.getElementById("otp").value.trim();

    const message = document.getElementById("verifyMessage");

    if (phone !== confirmPhone) {
        message.textContent = "Demo phone numbers do not match.";
        return;
    }

    if (otp !== "DEMO2026") {
        message.textContent =
            "Incorrect demo code. Use DEMO2026.";
        return;
    }

    message.textContent =
        "Demo verification successful. This is not official verification.";

    showStep(3);
}

// STEP 3: DOCUMENT UPLOAD
function reviewApplication() {

    const files = [
        ["Photo", "photo"],
        ["Signature", "signature"],
        ["Marksheet", "marksheet"],
        ["Certificate", "certificate"]
    ];

    let output = "";

    files.forEach(function(item) {

        const input = document.getElementById(item[1]);

        if (input.files.length > 0) {
            output += "<p><b>" + item[0] + ":</b> "
                + escapeHTML(input.files[0].name)
                + "</p>";
        } else {
            output += "<p><b>" + item[0]
                + ":</b> Not attached</p>";
        }

    });

    document.getElementById("fileResults").innerHTML = output;

    const name = document.getElementById("name").value;
    const dob = document.getElementById("dob").value;
    const email = document.getElementById("email").value;
    const category = document.getElementById("category").value;
    const state = document.getElementById("state").value;

    document.getElementById("reviewDetails").innerHTML = `
        <p><b>Name:</b> ${escapeHTML(name)}</p>
        <p><b>Date of Birth:</b> ${escapeHTML(dob)}</p>
        <p><b>Email:</b> ${escapeHTML(email)}</p>
        <p><b>Category:</b> ${escapeHTML(category)}</p>
        <p><b>State:</b> ${escapeHTML(state)}</p>
        <p><b>Documents:</b> Selected files are listed above.</p>
    `;

    showStep(4);
}

// Escape user input before displaying it in HTML
function escapeHTML(value) {
    return String(value).replace(/[&<>"']/g, function(char) {
        return {
            "&": "&amp;",
            "<": "&lt;",
            ">": "&gt;",
            '"': "&quot;",
            "'": "&#39;"
        }[char];
    });
}

// STEP 4: REVIEW
function goToPayment() {

    if (!document.getElementById("agree").checked) {
        alert("Please confirm that this is a demo.");
        return;
    }

    showStep(5);
}

// STEP 5: PAYMENT SIMULATION
function simulatePayment() {

    const amount = document.getElementById("fee").value;
    const method = document.getElementById("paymentMethod").value;

    const demoReceiptID = "DEMO-" +
        Math.random().toString(36).substring(2, 8).toUpperCase();

    document.getElementById("paymentMessage").innerHTML =
        "<p>Demo payment simulated successfully.</p>" +
        "<p><b>Amount:</b> ₹" + escapeHTML(amount) + "</p>" +
        "<p><b>Method:</b> " + escapeHTML(method) + "</p>" +
        "<p><b>Demo Receipt ID:</b> " + demoReceiptID + "</p>" +
        "<p><b>Status:</b> No money deducted.</p>";

    document.getElementById("slipDetails").innerHTML =
        "<p><b>Candidate:</b> " +
        escapeHTML(document.getElementById("name").value) +
        "</p>" +

        "<p><b>Demo Phone:</b> " +
        escapeHTML(document.getElementById("phone").value) +
        "</p>" +

        "<p><b>Demo Receipt ID:</b> " +
        demoReceiptID + "</p>" +

        "<p><b>Practice Fee:</b> ₹" +
        escapeHTML(amount) + "</p>" +

        "<p><b>Payment Method:</b> " +
        escapeHTML(method) + "</p>" +

        "<p><b>Payment Status:</b> SIMULATED SUCCESS</p>" +

        "<p><b>Note:</b> No real payment occurred. " +
        "This is not an official NTA receipt.</p>";

    showStep(6);
}

// OPEN FEE SLIP IN NEW TAB
function openFeeSlip() {

    const slip = document.getElementById("feeSlip").innerHTML;

    const newWindow = window.open("", "_blank");

    if (!newWindow) {
        alert("Popup blocked. Use Print / Save as PDF.");
        return;
    }

    newWindow.document.write(`
        <!DOCTYPE html>
        <html>
        <head>
            <meta charset="UTF-8">
            <title>Demo Fee Slip</title>
            <style>
                body {
                    font-family: Arial, sans-serif;
                    max-width: 650px;
                    margin: 30px auto;
                    padding: 20px;
                }

                .slip {
                    border: 2px dashed #555;
                    padding: 20px;
                }

                .demo {
                    color: #b42318;
                    font-weight: bold;
                    text-align: center;
                }
            </style>
        </head>
        <body>
            <div class="slip">${slip}</div>
        </body>
        </html>
    `);

    newWindow.document.close();
}

</script>

</body>
</html>