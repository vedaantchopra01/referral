<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Referral Program</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            margin: 20px;
        }
        form {
            max-width: 400px;
            margin: 0 auto;
            background-color: #f9f9f9;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }
        input, button {
            width: 100%;
            padding: 10px;
            margin: 10px 0;
            border: 1px solid #ccc;
            border-radius: 5px;
        }
        button {
            background-color: #4CAF50;
            color: white;
            border: none;
            cursor: pointer;
        }
        button:hover {
            background-color: #45a049;
        }
        .referral-card {
            display: none;
            margin-top: 20px;
        }
        .qr-code {
            margin-top: 10px;
        }
    </style>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/qrcodejs/1.0.0/qrcode.min.js"></script>
</head>
<body>
    <h1>Referral Program</h1>
    <form id="referralForm">
        <label for="name">Patient Name:</label>
        <input type="text" id="name" name="name" placeholder="Enter your name" required>
        
        <label for="phone">Phone Number:</label>
        <input type="tel" id="phone" name="phone" placeholder="Enter your phone number" required>
        
        <label for="photo">Upload Picture (Optional):</label>
        <input type="file" id="photo" name="photo" accept="image/*">

        <button type="submit">Generate Referral Card</button>
    </form>

    <div class="referral-card" id="referralCard">
        <h2>Referral Card</h2>
        <p>Patient Name: <span id="cardName"></span></p>
        <p>Referral Value: ₹1000</p>
        <div class="qr-code" id="qrcode"></div>
        <p>Share this card via WhatsApp or show the QR code at the clinic to avail the offer.</p>
        <p>Referred Friend Benefits: 2 Dry Cupping Sessions OR 1 Free Physiotherapy Session</p>
        <button onclick="shareReferral()">Share on WhatsApp</button>
    </div>

    <script>
        document.getElementById("referralForm").addEventListener("submit", function(event) {
            event.preventDefault();

            // Get patient details
            const name = document.getElementById("name").value;
            const phone = document.getElementById("phone").value;

            // Display referral card
            document.getElementById("referralCard").style.display = "block";
            document.getElementById("cardName").textContent = name;

            // Generate QR Code
            const qrCodeData = `Referral Card\nPatient Name: ${name}\nPhone: ${phone}\nValue: ₹1000\nReferred Benefits: 2 Dry Cupping Sessions OR 1 Physiotherapy Session`;
            const qrCodeContainer = document.getElementById("qrcode");
            qrCodeContainer.innerHTML = ""; // Clear any existing QR code
            new QRCode(qrCodeContainer, {
                text: qrCodeData,
                width: 128,
                height: 128
            });
        });

        function shareReferral() {
            const name = document.getElementById("name").value;
            const phone = document.getElementById("phone").value;
            const message = `Hi! This is my referral card from CnC Physiotherapy Center.\nPatient Name: ${name}\nReferral Value: ₹1000\nReferred Benefits: 2 Dry Cupping Sessions OR 1 Physiotherapy Session.\nShow this QR code to avail the benefits.`;
            const whatsappURL = `https://api.whatsapp.com/send?text=${encodeURIComponent(message)}`;
            window.open(whatsappURL, "_blank");
        }
    </script>
</body>
</html>
