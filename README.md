# Period-Tracker-App
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Period Tracker</title>

<style>
    body {
    font-family: Arial, sans-serif;
    text-align: center;
    margin: 20px;
    background-color: #d86aa7;
    color: white;
}


    h1 {
        color: #d63384;
    }

    .controls {
        margin-bottom: 20px;
    }

    input, button {
        padding: 8px;
        margin: 5px;
    }

    button {
        background-color: #d63384;
        color: white;
        border: none;
        cursor: pointer;
        border-radius: 5px;
    }

    button:hover {
        background-color: #b8256d;
    }

    .calendar-container {
        max-width: 700px;
        margin: auto;
    }

    .month-header {
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin-bottom: 10px;
    }

    .calendar {
        display: grid;
        grid-template-columns: repeat(7, 1fr);
        gap: 5px;
    }

    .day-name,
    .day {
        padding: 12px;
        border: 1px solid #ddd;
        background: white;
    }

.day {
    padding: 12px;
    border: 1px solid #ddd;
    background: #ffffff;
    color: #333;
}

.day-name {
    font-weight: bold;
    background: #ffb6d9;
    color: #333;
}

.period-day {
    background-color: #ff1493;
    color: white;
    font-weight: bold;
}


    .empty {
        background: transparent;
        border: none;
    }
</style>
</head>
<body>

<h1>Period Tracker</h1>

<div class="controls">
    <label>Start Date:</label>
    <input type="date" id="startDate">

    <label>End Date:</label>
    <input type="date" id="endDate">

    <button onclick="addPeriod()">Add Period</button>
</div>

<div class="calendar-container">
    <div class="month-header">
        <button onclick="changeMonth(-1)">◀</button>
        <h2 id="monthYear"></h2>
        <button onclick="changeMonth(1)">▶</button>
    </div>

    <div class="calendar" id="calendar"></div>
</div>

<script>
let currentDate = new Date();
let periodDates = []; // Stored only while page is open

const monthYear = document.getElementById("monthYear");
const calendar = document.getElementById("calendar");

function formatDate(date) {
    return date.toISOString().split("T")[0];
}

function addPeriod() {
    const start = document.getElementById("startDate").value;
    const end = document.getElementById("endDate").value;

    if (!start || !end) {
        alert("Please select both dates.");
        return;
    }

    let startDate = new Date(start);
    let endDate = new Date(end);

    if (startDate > endDate) {
        alert("End date must be after start date.");
        return;
    }

    while (startDate <= endDate) {
        const dateString = formatDate(startDate);

        if (!periodDates.includes(dateString)) {
            periodDates.push(dateString);
        }

        startDate.setDate(startDate.getDate() + 1);
    }

    renderCalendar();
}

function renderCalendar() {
    calendar.innerHTML = "";

    const monthNames = [
        "January", "February", "March", "April",
        "May", "June", "July", "August",
        "September", "October", "November", "December"
    ];

    const dayNames = ["Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat"];

    monthYear.textContent =
        `${monthNames[currentDate.getMonth()]} ${currentDate.getFullYear()}`;

    dayNames.forEach(day => {
        const div = document.createElement("div");
        div.className = "day-name";
        div.textContent = day;
        calendar.appendChild(div);
    });

    const firstDay = new Date(
        currentDate.getFullYear(),
        currentDate.getMonth(),
        1
    );

    const lastDay = new Date(
        currentDate.getFullYear(),
        currentDate.getMonth() + 1,
        0
    );

    for (let i = 0; i < firstDay.getDay(); i++) {
        const empty = document.createElement("div");
        empty.className = "empty";
        calendar.appendChild(empty);
    }

    for (let day = 1; day <= lastDay.getDate(); day++) {
        const date = new Date(
            currentDate.getFullYear(),
            currentDate.getMonth(),
            day
        );

        const dateString = formatDate(date);

        const div = document.createElement("div");
        div.className = "day";
        div.textContent = day;

        if (periodDates.includes(dateString)) {
            div.classList.add("period-day");
        }

        calendar.appendChild(div);
    }
}

function changeMonth(direction) {
    currentDate.setMonth(currentDate.getMonth() + direction);
    renderCalendar();
}

renderCalendar();
</script>

</body>
</html>
Can you please make the background a darker pink so the text is more clearly noticabale 
Absolutely. The easiest way is to change the page background from the very light pink (#fff5f8) to a darker pink and make the text darker/white for contrast.
Replace this section:
CSS
body {
font-family: Arial, sans-serif;
text-align: center;
margin: 20px;
background-color: #fff5f8;
}
with:
CSS
body {
font-family: Arial, sans-serif;
text-align: center;
margin: 20px;
background-color: #d86aa7;
color: white;
}
You may also want to make the calendar cells easier to read against the darker background:
CSS
.day {
padding: 12px;
border: 1px solid #ddd;
background: #ffffff;
color: #333;
}
 
.day-name {
font-weight: bold;
background: #ffb6d9;
color: #333;
}
 
.period-day {
background-color: #ff1493;
color: white;
font-weight: bold;
}
If you'd like an even nicer look, try this darker pink:
CSS
background-color: #c2185b;
or this softer but still dark pink:
CSS
background-color: #ad1457;
These shades create much stronger contrast, making the text and calendar stand out clearly.
