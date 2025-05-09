<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Isha Prayer Ending Time Calculator</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Inter', sans-serif;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            min-height: 100vh;
            background-color: #f0f9ff; /* Light blue background */
            color: #0f172a; /* Slate 900 */
            padding: 1rem;
            margin: 0; /* Ensure no default margin */
        }
        .container {
            background-color: white;
            padding: 2rem;
            border-radius: 0.75rem; /* Rounded corners */
            box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05);
            width: 100%;
            max-width: 500px;
            text-align: center;
        }
        .input-group {
            margin-bottom: 1rem;
            text-align: left;
        }
        .input-group label {
            display: block;
            margin-bottom: 0.5rem;
            font-weight: 500;
            color: #334155; /* Slate 700 */
        }
        .input-group input {
            width: 100%;
            padding: 0.75rem;
            border: 1px solid #cbd5e1; /* Slate 300 */
            border-radius: 0.375rem; /* Rounded corners */
            box-sizing: border-box;
        }
        .btn {
            background-color: #2563eb; /* Blue 600 */
            color: white;
            padding: 0.75rem 1.5rem;
            border: none;
            border-radius: 0.375rem;
            font-weight: 600;
            cursor: pointer;
            transition: background-color 0.3s ease;
            width: auto; /* Adjust button width */
            display: inline-block; /* Align buttons inline */
        }
        .btn:hover {
            background-color: #1d4ed8; /* Blue 700 */
        }
        .btn-secondary {
            background-color: #64748b; /* Slate 500 */
        }
        .btn-secondary:hover {
            background-color: #475569; /* Slate 600 */
        }
        .btn.w-full { /* Utility for full width button if needed */
            width: 100%;
        }
        .results-card {
            margin-top: 2rem;
            padding: 1.5rem;
            background-color: #f8fafc; /* Slate 50 */
            border: 1px solid #e2e8f0; /* Slate 200 */
            border-radius: 0.5rem;
            text-align: left;
        }
        .results-card h3 {
            font-size: 1.25rem;
            font-weight: 600;
            margin-bottom: 1rem;
            color: #1e293b; /* Slate 800 */
            text-align: center;
        }
        .results-card p {
            margin-bottom: 0.75rem;
            font-size: 1rem;
            color: #475569; /* Slate 600 */
        }
        .results-card p strong {
            color: #0f172a; /* Slate 900 */
        }
        .message-box {
            margin-top: 1rem;
            padding: 1rem;
            border-radius: 0.375rem;
            font-weight: 500;
            text-align: left;
        }
        .message-box.error {
            background-color: #fee2e2; /* Red 100 */
            color: #b91c1c; /* Red 700 */
            border: 1px solid #fecaca; /* Red 300 */
        }
        .message-box.info {
            background-color: #dbeafe; /* Blue 100 */
            color: #1e40af; /* Blue 700 */
            border: 1px solid #bfdbfe; /* Blue 300 */
        }
        .loader {
            border: 4px solid #f3f3f3; /* Light grey */
            border-top: 4px solid #2563eb; /* Blue */
            border-radius: 50%;
            width: 30px;
            height: 30px;
            animation: spin 1s linear infinite;
            margin: 1rem auto;
            display: none; /* Hidden by default */
        }
        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
        /* Responsive adjustments */
        @media (max-width: 640px) {
            .container {
                padding: 1.5rem;
            }
            .btn {
                padding: 0.6rem 1.2rem;
                font-size: 0.9rem;
            }
            #location-method-selector .btn {
                width: 100%;
                margin-bottom: 0.5rem;
            }
            #location-method-selector .btn:last-child {
                margin-bottom: 0;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <h1 class="text-3xl font-bold mb-6 text-blue-700">Islamic Night Divider</h1>

        <div id="location-method-selector" class="mb-4">
            <p class="mb-2 text-slate-600">Choose location method:</p>
            <button id="autoLocationBtn" class="btn mr-2 mb-2 sm:mb-0">Use My Location</button>
            <button id="manualLocationBtn" class="btn btn-secondary">Enter Manually</button>
        </div>

        <div id="manualLocationInput" class="hidden">
            <div class="input-group">
                <label for="city">City:</label>
                <input type="text" id="city" placeholder="e.g., London">
            </div>
            <div class="input-group">
                <label for="country">Country:</label>
                <input type="text" id="country" placeholder="e.g., UK">
            </div>
            <button id="getTimesBtn" class="btn w-full mt-2">Get Prayer Times</button>
        </div>

        <div id="loader" class="loader"></div>
        <div id="messageBox" class="message-box hidden"></div>

        <div id="results" class="results-card hidden">
            <h3 id="currentDateDisplay"></h3>
            <p>Location: <strong id="locationDisplay"></strong></p>
            <hr class="my-3 border-slate-300">
            <p>Maghrib (Sunset): <strong id="maghribTime"></strong></p>
            <p>Fajr (Dawn): <strong id="fajrTime"></strong></p>
            <hr class="my-3 border-slate-300">
            <p class="text-lg font-semibold text-blue-600">Middle of the Night: <strong id="midNightTime" class="text-xl"></strong></p>
        </div>
    </div>

    <script>
        // DOM Elements
        const autoLocationBtn = document.getElementById('autoLocationBtn');
        const manualLocationBtn = document.getElementById('manualLocationBtn');
        const manualLocationInputDiv = document.getElementById('manualLocationInput');
        const cityInput = document.getElementById('city');
        const countryInput = document.getElementById('country');
        const getTimesBtn = document.getElementById('getTimesBtn');
        const loader = document.getElementById('loader');
        const messageBox = document.getElementById('messageBox');
        const resultsDiv = document.getElementById('results');
        const currentDateDisplay = document.getElementById('currentDateDisplay');
        const locationDisplay = document.getElementById('locationDisplay');
        const maghribTimeDisplay = document.getElementById('maghribTime');
        const fajrTimeDisplay = document.getElementById('fajrTime');
        const midNightTimeDisplay = document.getElementById('midNightTime');

        // --- Helper Functions ---

        // Function to show/hide loader
        function showLoader(show) {
            loader.style.display = show ? 'block' : 'none';
        }

        // Function to display messages
        function showMessage(message, type = 'info') {
            messageBox.textContent = message;
            messageBox.className = `message-box ${type}`; // Reset classes and add new type
            messageBox.classList.remove('hidden');
            resultsDiv.classList.add('hidden'); // Hide results when a new message is shown
        }

        // Function to hide messages
        function hideMessage() {
            messageBox.classList.add('hidden');
        }
        
        // Function to format time to HH:MM AM/PM
        function formatTime(timeStr) {
            if (!timeStr || !timeStr.includes(':')) return "N/A"; // Basic validation
            const [hours, minutes] = timeStr.split(':');
            const date = new Date();
            date.setHours(parseInt(hours, 10));
            date.setMinutes(parseInt(minutes, 10));
            return date.toLocaleTimeString('en-US', { hour: '2-digit', minute: '2-digit', hour12: true });
        }

        // Function to parse time string (HH:MM) into minutes from midnight
        function timeToMinutes(timeStr) {
            const [hours, minutes] = timeStr.split(':').map(Number);
            return hours * 60 + minutes;
        }

        // Function to convert minutes from midnight back to HH:MM string (24-hour)
        function minutesToTime(totalMinutes) {
            const hours = Math.floor(totalMinutes / 60) % 24; // Handle midnight overflow
            const minutes = totalMinutes % 60;
            return `${String(hours).padStart(2, '0')}:${String(minutes).padStart(2, '0')}`;
        }


        // --- Event Listeners ---
        autoLocationBtn.addEventListener('click', () => {
            manualLocationInputDiv.classList.add('hidden');
            hideMessage();
            resultsDiv.classList.add('hidden');
            fetchPrayerTimesByGeolocation();
        });

        manualLocationBtn.addEventListener('click', () => {
            manualLocationInputDiv.classList.remove('hidden');
            hideMessage();
            resultsDiv.classList.add('hidden');
            cityInput.value = ''; // Clear previous input
            countryInput.value = ''; // Clear previous input
        });

        getTimesBtn.addEventListener('click', () => {
            const city = cityInput.value.trim();
            const country = countryInput.value.trim();
            if (city && country) {
                hideMessage();
                resultsDiv.classList.add('hidden');
                fetchPrayerTimesByCityCountry(city, country);
            } else {
                showMessage('Please enter both city and country.', 'error');
            }
        });

        // --- Core Logic ---

        // Fetch prayer times using Geolocation
        function fetchPrayerTimesByGeolocation() {
            if (navigator.geolocation) {
                showLoader(true);
                navigator.geolocation.getCurrentPosition(
                    (position) => {
                        const { latitude, longitude } = position.coords;
                        // Reverse geocode to get city and country for display (optional, but good for UX)
                        fetch(`https://nominatim.openstreetmap.org/reverse?format=json&lat=${latitude}&lon=${longitude}`)
                            .then(response => response.json())
                            .then(data => {
                                const city = data.address.city || data.address.town || data.address.village || 'Unknown City';
                                const country = data.address.country || 'Unknown Country';
                                locationDisplay.textContent = `${city}, ${country}`;
                                fetchPrayerTimesAPI(latitude, longitude, null, null);
                            })
                            .catch(() => {
                                locationDisplay.textContent = `Lat: ${latitude.toFixed(2)}, Lon: ${longitude.toFixed(2)}`;
                                fetchPrayerTimesAPI(latitude, longitude, null, null);
                            });
                    },
                    (error) => {
                        showLoader(false);
                        let errorMsg = "Geolocation failed. ";
                        switch(error.code) {
                            case error.PERMISSION_DENIED:
                                errorMsg += "User denied the request for Geolocation.";
                                break;
                            case error.POSITION_UNAVAILABLE:
                                errorMsg += "Location information is unavailable.";
                                break;
                            case error.TIMEOUT:
                                errorMsg += "The request to get user location timed out.";
                                break;
                            case error.UNKNOWN_ERROR:
                                errorMsg += "An unknown error occurred.";
                                break;
                        }
                        showMessage(errorMsg + " Please try entering location manually.", 'error');
                        manualLocationInputDiv.classList.remove('hidden'); // Show manual input as fallback
                    }
                );
            } else {
                showMessage('Geolocation is not supported by your browser. Please enter location manually.', 'error');
                manualLocationInputDiv.classList.remove('hidden');
            }
        }

        // Fetch prayer times using city and country
        function fetchPrayerTimesByCityCountry(city, country) {
            showLoader(true);
            locationDisplay.textContent = `${city}, ${country}`;
            fetchPrayerTimesAPI(null, null, city, country);
        }

        // Call Aladhan API
        async function fetchPrayerTimesAPI(latitude, longitude, city, country) {
            const method = 2; // ISNA (Islamic Society of North America) - common default. User can change if needed.
            const today = new Date();
            const dateString = `${String(today.getDate()).padStart(2, '0')}-${String(today.getMonth() + 1).padStart(2, '0')}-${today.getFullYear()}`;
            
            let apiUrl = `https://api.aladhan.com/v1/timings`;

            if (latitude && longitude) {
                apiUrl += `/${dateString}?latitude=${latitude}&longitude=${longitude}&method=${method}`;
            } else if (city && country) {
                apiUrl += `ByCity/${dateString}?city=${encodeURIComponent(city)}&country=${encodeURIComponent(country)}&method=${method}`;
            } else {
                showLoader(false);
                showMessage('Insufficient location information provided.', 'error');
                return;
            }
            
            try {
                const response = await fetch(apiUrl);
                if (!response.ok) {
                    const errorData = await response.json();
                    throw new Error(errorData.data || `HTTP error! status: ${response.status}`);
                }
                const data = await response.json();
                
                if (data.code === 200 && data.data.timings) {
                    processPrayerTimes(data.data.timings, data.data.date.readable);
                } else {
                    throw new Error(data.data || 'Could not fetch prayer times. Invalid response from API.');
                }
            } catch (error) {
                showLoader(false);
                console.error("API Error:", error);
                showMessage(`Error fetching prayer times: ${error.message}. Please check the location or try again.`, 'error');
                 // If city/country search fails, suggest auto-location or checking spelling
                if (city && country) {
                    showMessage(`Error fetching prayer times for ${city}, ${country}: ${error.message}. Please check spelling or try auto-location.`, 'error');
                } else {
                     showMessage(`Error fetching prayer times: ${error.message}. Please try entering location manually.`, 'error');
                }
            }
        }

        // Process and display prayer times
        function processPrayerTimes(timings, dateReadable) {
            showLoader(false);
            hideMessage();

            const maghribStr = timings.Maghrib; // e.g., "19:30"
            const fajrStr = timings.Fajr;     // e.g., "04:00"

            if (!maghribStr || !fajrStr) {
                showMessage('Maghrib or Fajr times are missing in the API response.', 'error');
                return;
            }

            const maghribMinutes = timeToMinutes(maghribStr);
            let fajrMinutes = timeToMinutes(fajrStr);

            // Fajr is on the next day if its time in minutes is less than Maghrib's
            // (e.g. Maghrib 19:00, Fajr 04:00 of next day)
            if (fajrMinutes < maghribMinutes) {
                fajrMinutes += 24 * 60; // Add 24 hours in minutes
            }

            const durationMinutes = fajrMinutes - maghribMinutes;
            const midPointOffsetMinutes = Math.floor(durationMinutes / 2);
            const midNightTotalMinutes = maghribMinutes + midPointOffsetMinutes;
            
            const midNightTimeStr = minutesToTime(midNightTotalMinutes);

            // Display results
            currentDateDisplay.textContent = `Timings for: ${dateReadable}`;
            maghribTimeDisplay.textContent = formatTime(maghribStr);
            fajrTimeDisplay.textContent = formatTime(fajrStr);
            midNightTimeDisplay.textContent = formatTime(midNightTimeStr);
            
            resultsDiv.classList.remove('hidden');
        }

        // Initial state: Prompt user to choose location method
        // No automatic fetching on load, user must interact first.
        showMessage('Please select a location method to get started.', 'info');

    </script>
</body>
</html>
