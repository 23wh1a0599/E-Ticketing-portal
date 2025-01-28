# E-Ticketing-portal
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>TSRTC Bus Tickets</title>
  <!-- Bootstrap CSS -->
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/css/bootstrap.min.css" rel="stylesheet">

  <style>
    body {
      background-image: url("bus.png"); /* Replace with the actual path to your image */
      background-size: cover;
      background-position: center;
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 0;
    }
    .jumbotron {
      padding: 50px;
      background-color: rgba(255, 0, 0, 0.6); /* Semi-transparent red */
      color: white;
      text-align: center;
      border-radius: 8px;
    }
    .container {
      margin-top: 30px;
    }
    .col-sm-4 {
      padding: 20px;
      background-color: rgba(255, 255, 255, 0.7); /* Light transparent white */
      border-radius: 8px;
    }
    h3 {
      color: #333;
    }
    .bus-list {
      margin-top: 20px;
      padding: 20px;
      background-color: rgba(255, 255, 255, 0.8);
      border-radius: 8px;
    }
    .bus-item {
      margin-bottom: 15px;
      padding: 10px;
      border: 1px solid #ddd;
      border-radius: 5px;
      display: flex;
      justify-content: space-between;
      align-items: center;
    }
    .bus-item button {
      padding: 5px 10px;
      background-color: #007bff;
      color: white;
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }
    .bus-item button:hover {
      background-color: #0056b3;
    }
  </style>
</head>
<body>

  <div class="jumbotron">
    <h1>TSRTC Bus Tickets</h1>
    <p>Welcome to Telangana State Tour!</p>
  </div>

  <div class="container">
    <div class="row">
      <!-- Current Location Input -->
      <div class="col-md-4 mb-3">
        <h3>Current Location</h3>
        <textarea id="currentLocation" rows="2" class="form-control" placeholder="Enter current location"></textarea>
      </div>

      <!-- City Name Input -->
      <div class="col-md-4 mb-3">
        <h3>Name of the City</h3>
        <textarea id="cityName" rows="2" class="form-control" placeholder="Enter city name..."></textarea>
      </div>

      <!-- Travel Date Input -->
      <div class="col-md-4 mb-3">
        <h3>Travel Date</h3>
        <textarea id="travelDate" rows="2" class="form-control" placeholder="Enter date (DD/MM/YYYY)"></textarea>
      </div>
    </div>

    <div class="text-center mt-3">
      <button class="btn btn-primary" onclick="checkBuses()">Check Buses</button>
    </div>

    <div id="result" class="mt-3 text-center font-weight-bold"></div>

    <div id="busList" class="bus-list" style="display: none;">
      <h3>Available Buses</h3>
    </div>
  </div>

  <script>
    let ticketBooked = false; // Track if the user has already booked a ticket

    function checkBuses() {
      const currentLocation = document.getElementById('currentLocation').value.trim();
      const cityName = document.getElementById('cityName').value.trim();
      const travelDate = document.getElementById('travelDate').value.trim();

      if (!currentLocation || !cityName || !travelDate) {
        document.getElementById('result').innerText = "Please fill in all the details.";
        return;
      }

      // Simulate fetching bus data (this can be replaced with an API call)
      const buses = [
        { id: 1, time: "08:00 AM", seats: 20 },
        { id: 2, time: "10:30 AM", seats: 15 },
        { id: 3, time: "02:00 PM", seats: 30 },
        { id: 4, time: "06:00 PM", seats: 10 },
      ];

      document.getElementById('result').innerText = `Buses available on ${travelDate} from ${currentLocation} to ${cityName}:`;

      const busList = document.getElementById('busList');
      busList.innerHTML = '<h3>Available Buses</h3>';
      buses.forEach(bus => {
        const busItem = document.createElement('div');
        busItem.className = 'bus-item';
        busItem.innerHTML = ` 
          <span>Bus ID: ${bus.id}, Time: ${bus.time}, Seats Available: ${bus.seats}</span>
          <button class="btn btn-success" onclick="bookTicket(${bus.id})">Book Ticket</button>
        `;
        busList.appendChild(busItem);
      });
      busList.style.display = 'block';
    }

    function bookTicket(busId) {
      if (ticketBooked) {
        alert("You have already booked a ticket. You cannot book another ticket.");
        return;
      }

      ticketBooked = true; // Mark ticket as booked
      alert(`Ticket booked successfully for Bus ID: ${busId}`);
    }
  </script>

  <!-- Bootstrap JS and Popper.js (for responsiveness) -->
  <script src="https://cdn.jsdelivr.net/npm/@popperjs/core@2.11.6/dist/umd/popper.min.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/js/bootstrap.min.js"></script>

</body>
</html>
