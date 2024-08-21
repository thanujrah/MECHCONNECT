<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Mechanic Connect</title>
  <!-- Leaflet.js CSS -->
  <link rel="stylesheet" href="https://unpkg.com/leaflet/dist/leaflet.css" />
  <!-- Google Fonts -->
  <link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;600&display=swap">
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.4/css/all.min.css">
  <style>
    /* Your existing styles here */
    body {
        font-family: 'Poppins', sans-serif;
        margin: 0;
        padding: 0;
        display: flex;
        flex-direction: column;
        align-items: center;
        background: url('https://images.unsplash.com/photo-1506765515384-028b60a970df?ixlib=rb-4.0.3&auto=format&fit=crop&w=1950&q=80') no-repeat center center fixed;
        background-size: cover;
        color: #ffffff;
        overflow-x: hidden;
    }
    .hero {
        position: relative;
        width: 100%;
        height: 100vh;
        background: url('https://images.unsplash.com/photo-1506765515384-028b60a970df?ixlib=rb-4.0.3&auto=format&fit=crop&w=1950&q=80') no-repeat center center/cover;
        display: flex;
        align-items: center;
        justify-content: center;
        text-align: center;
        color: #ffffff;
        padding: 20px;
    }
    .hero-overlay {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background: rgba(0, 0, 0, 0.5);
    }
    .hero-content {
        position: relative;
        z-index: 1;
    }
    .hero h1 {
        font-size: 50px;
        font-weight: 700;
        margin: 0;
        animation: fadeIn 2s ease-out;
    }
    .hero h2 {
        font-size: 24px;
        font-weight: 300;
        margin: 10px 0;
        animation: fadeIn 2s ease-out 0.5s;
    }
    .hero-button {
        padding: 15px 30px;
        background: linear-gradient(135deg, #00c6ff, #0072ff);
        color: #ffffff;
        border: none;
        border-radius: 30px;
        font-size: 18px;
        cursor: pointer;
        box-shadow: 0 6px 15px rgba(0,0,0,0.4);
        transition: background 0.3s, transform 0.3s, box-shadow 0.3s;
        animation: fadeIn 2s ease-out 1s;
    }
    .hero-button:hover {
        background: linear-gradient(135deg, #0072ff, #00c6ff);
        transform: scale(1.05);
        box-shadow: 0 10px 30px rgba(0,0,0,0.6);
    }
    .container {
        background: rgba(255, 255, 255, 0.1);
        backdrop-filter: blur(15px);
        padding: 40px;
        border-radius: 20px;
        box-shadow: 0 15px 40px rgba(0,0,0,0.5);
        max-width: 800px;
        width: 90%;
        margin: 60px 0;
        transition: transform 0.5s ease, box-shadow 0.5s ease;
        animation: fadeIn 1s ease-out;
    }
    .container:hover {
        transform: scale(1.05);
        box-shadow: 0 20px 60px rgba(0, 0, 0, 0.7);
    }
    @keyframes fadeIn {
        from { opacity: 0; transform: translateY(10px); }
        to { opacity: 1; transform: translateY(0); }
    }
    h1, h2 {
        text-align: center;
        margin-bottom: 20px;
    }
    h1 {
        font-size: 50px;
        font-weight: 700;
        color: #ffffff;
        text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.7);
    }
    h2 {
        font-size: 26px;
        font-weight: 400;
        color: #e0f7fa;
        text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.6);
    }
    input, textarea {
        width: calc(100% - 60px);
        padding: 16px;
        margin-bottom: 20px;
        border-radius: 15px;
        border: none;
        font-size: 20px;
        color: #ffffff;
        background-color: rgba(255, 255, 255, 0.15);
        backdrop-filter: blur(5px);
        box-shadow: inset 0 0 10px rgba(0,0,0,0.3);
        transition: box-shadow 0.4s ease, transform 0.4s ease;
    }
    input:focus, textarea:focus {
        outline: none;
        box-shadow: inset 0 0 20px rgba(0,0,0,0.5);
        transform: translateY(-2px);
    }
    textarea {
        resize: vertical;
    }
    button {
        width: 100%;
        padding: 16px;
        background: linear-gradient(135deg, #00c6ff, #0072ff);
        color: #ffffff;
        border: none;
        border-radius: 15px;
        font-size: 20px;
        cursor: pointer;
        box-shadow: 0 6px 20px rgba(0, 114, 255, 0.4);
        transition: background 0.4s, transform 0.3s ease, box-shadow 0.3s ease;
    }
    button:hover {
        background: linear-gradient(135deg, #0072ff, #00c6ff);
        transform: translateY(-4px);
        box-shadow: 0 10px 30px rgba(0, 114, 255, 0.7);
    }
    .form-group {
        position: relative;
    }
    .form-group i {
        position: absolute;
        top: 50%;
        left: 18px;
        transform: translateY(-50%);
        color: #ffffff;
        pointer-events: none;
    }
    input, textarea {
        padding-left: 50px;
    }
    #map {
        width: 100%;
        height: 500px;
        margin-top: 30px;
        border-radius: 15px;
        overflow: hidden;
        box-shadow: 0 6px 20px rgba(0, 0, 0, 0.3);
        animation: slideIn 1s ease-out;
    }
    @keyframes slideIn {
        from { opacity: 0; transform: translateY(20px); }
        to { opacity: 1; transform: translateY(0); }
    }
    /* Custom Cursor */
    body {
        cursor: url('https://cdn-icons-png.flaticon.com/512/32/32441.png'), auto;
    }
    /* SVG Waves */
    .waves {
        position: absolute;
        bottom: 0;
        width: 100%;
        height: 150px;
        background: url('https://cdn.jsdelivr.net/gh/webdevpuneet/wave-animation@v1.0.1/wave.svg') repeat-x;
        background-size: 1000px 100px;
        animation: wave 10s linear infinite;
    }
    @keyframes wave {
        from { background-position-x: 0; }
        to { background-position-x: 1000px; }
    }
    .voice-btn {
        position: fixed;
        bottom: 20px;
        right: 20px;
        width: 60px;
        height: 60px;
        border-radius: 50%;
        background: linear-gradient(135deg, #00c6ff, #0072ff);
        color: #ffffff;
        border: none;
        font-size: 24px;
        cursor: pointer;
        box-shadow: 0 6px 15px rgba(0,0,0,0.4);
        transition: background 0.3s, transform 0.3s, box-shadow 0.3s;
    }
    .voice-btn:hover {
        background: linear-gradient(135deg, #0072ff, #00c6ff);
        transform: scale(1.1);
        box-shadow: 0 10px 30px rgba(0,0,0,0.6);
    }
  </style>
</head>
<body>
  <div class="hero">
    <div class="hero-overlay"></div>
    <div class="hero-content">
      <h1>Welcome to Mechanic Connect</h1>
      <h2>Your go-to place for finding nearby mechanics</h2>
      <button class="hero-button" onclick="document.getElementById('formSection').scrollIntoView({behavior: 'smooth'})">Get Started</button>
    </div>
  </div>

  <div class="container" id="formSection">
    <h1>Submit Your Vehicle Problem</h1>
    <form id="problemForm">
      <div class="form-group">
        <i class="fas fa-user"></i>
        <input type="text" id="name" name="name" placeholder="Name" required>
      </div>
      <div class="form-group">
        <i class="fas fa-envelope"></i>
        <input type="email" id="email" name="email" placeholder="Email" required>
      </div>
      <div class="form-group">
        <i class="fas fa-phone"></i>
        <input type="tel" id="phone" name="phone" placeholder="Phone Number" required>
      </div>
      <div class="form-group">
        <i class="fas fa-car"></i>
        <input type="text" id="vehicleModel" name="vehicleModel" placeholder="Vehicle Model" required>
      </div>



      <div class="form-group">
    <i class="fas fa-wrench"></i>
    <textarea id="problem" rows="4" placeholder="Describe your problem" required></textarea>
    <button type="button" class="voice-btn" onclick="toggleVoiceRecognition()">
        <i class="fas fa-microphone"></i>
    </button>
</div>


      <button type="submit"><a href="hello.html" style="color: inherit; text-decoration: none;">Submit</a></button>
    </form>
  </div>

  <div id="map"></div>
  <div class="waves"></div>

  <script>
    // Initialize Speech Recognition
    var recognition;
    var finalTranscript = ''; // To store the final text

    if ('webkitSpeechRecognition' in window) {
        recognition = new webkitSpeechRecognition();
        recognition.continuous = true;
        recognition.interimResults = true;

        recognition.onresult = function(event) {
            var transcript = '';
            for (var i = event.resultIndex; i < event.results.length; ++i) {
                transcript += event.results[i][0].transcript;
            }
            document.getElementById('problem').value = finalTranscript + transcript;
        };

        recognition.onend = function() {
            finalTranscript = document.getElementById('problem').value; // Save the transcript when speech recognition ends
        };

        recognition.onerror = function(event) {
            console.error('Speech recognition error detected: ' + event.error);
        };
    } else {
        console.warn('Speech recognition not supported');
    }

    function toggleVoiceRecognition() {
        if (recognition) {
            if (recognition.recognizing) {
                recognition.stop();
                recognition.recognizing = false;
            } else {
                recognition.start();
                recognition.recognizing = true;
            }
        }
    }

    // WebSocket code
    var ws = new WebSocket('ws://localhost:8765');

    ws.onopen = function() {
        console.log('WebSocket connection opened');
    };

    ws.onerror = function(error) {
        console.error('WebSocket error: ' + error.message);
    };

    ws.onclose = function() {
        console.log('WebSocket connection closed');
    };

    // Form submission handler
    document.getElementById('problemForm').onsubmit = function(event) {
        event.preventDefault(); // Prevent the default form submission

        var name = document.getElementById('name').value;
        var email = document.getElementById('email').value;
        var phone = document.getElementById('phone').value;
        var vehicleModel = document.getElementById('vehicleModel').value;
        var problem = document.getElementById('problem').value;

        // Log form data to console
        console.log('Name: ' + name);
        console.log('Email: ' + email);
        console.log('Phone: ' + phone);
        console.log('Vehicle Model: ' + vehicleModel);
        console.log('Problem: ' + problem);

        // Send form data via WebSocket
        if (ws.readyState === WebSocket.OPEN) {
            ws.send(JSON.stringify({
                name: name,
                email: email,
                phone: phone,
                vehicle: vehicleModel,
                problem: problem
            }));
        } else {
            console.error('WebSocket connection is not open.');
        }

        // Alert message
        alert('Your problem has been submitted successfully!');
    };
  </script>
</body>
</html>
