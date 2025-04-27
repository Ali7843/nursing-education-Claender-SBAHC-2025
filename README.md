<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta name="description" content="Interactive calendar of nursing educational activities for 2025">
    <title>Calendar of Educational Activities 2025</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
    <style>
        :root {
            --primary-color: #2563eb;
            --primary-dark: #1d4ed8;
            --secondary-color: #0ea5e9;
            --accent-color: #0284c7;
            --light-bg: #f0f9ff;
            --text-dark: #1e293b;
            --text-light: #64748b;
            --white: #ffffff;
            --success: #10b981;
            --warning: #f59e0b;
            --error: #ef4444;
        }
        
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }
        
        body {
            font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, sans-serif;
            background-color: var(--light-bg);
            color: var(--text-dark);
            line-height: 1.6;
        }
        
        .container {
            max-width: 1000px;
            margin: 2rem auto;
            background: var(--white);
            padding: 2rem;
            border-radius: 12px;
            box-shadow: 0 10px 25px rgba(0,0,0,0.05);
        }
        
        header {
            text-align: center;
            margin-bottom: 2rem;
            padding-bottom: 1.5rem;
            border-bottom: 1px solid #e2e8f0;
        }
        
        h1 {
            font-size: 2rem;
            font-weight: 700;
            color: var(--primary-color);
            margin-bottom: 0.5rem;
        }
        
        .subtitle {
            color: var(--text-light);
            font-size: 1rem;
        }
        
        .search-container {
            display: flex;
            margin-bottom: 2rem;
            position: relative;
        }
        
        .search-container i {
            position: absolute;
            left: 1rem;
            top: 50%;
            transform: translateY(-50%);
            color: var(--text-light);
        }
        
        input[type="text"] {
            flex-grow: 1;
            padding: 1rem 1rem 1rem 2.5rem;
            border: 1px solid #e2e8f0;
            border-radius: 8px;
            font-size: 1rem;
            transition: all 0.3s ease;
        }
        
        input[type="text"]:focus {
            outline: none;
            border-color: var(--primary-color);
            box-shadow: 0 0 0 3px rgba(37, 99, 235, 0.1);
        }
        
        button {
            padding: 0 1.5rem;
            margin-left: 0.75rem;
            background-color: var(--primary-color);
            color: white;
            border: none;
            border-radius: 8px;
            font-size: 1rem;
            font-weight: 500;
            cursor: pointer;
            transition: background-color 0.3s ease;
        }
        
        button:hover {
            background-color: var(--primary-dark);
        }
        
        .tabs {
            display: flex;
            margin-bottom: 1.5rem;
            border-bottom: 1px solid #e2e8f0;
        }
        
        .tab {
            padding: 0.75rem 1.5rem;
            margin-right: 0.5rem;
            cursor: pointer;
            border-bottom: 2px solid transparent;
            font-weight: 500;
            transition: all 0.3s ease;
        }
        
        .tab.active {
            border-bottom: 2px solid var(--primary-color);
            color: var(--primary-color);
        }
        
        #output {
            min-height: 200px;
        }
        
        .month-card {
            background-color: #f8fafc;
            border-radius: 8px;
            padding: 1.5rem;
            margin-bottom: 1.5rem;
            box-shadow: 0 2px 4px rgba(0,0,0,0.03);
            border-left: 4px solid var(--primary-color);
        }
        
        .month-title {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 1rem;
            cursor: pointer;
        }
        
        .month-title h3 {
            font-size: 1.25rem;
            color: var(--text-dark);
            font-weight: 600;
        }
        
        .event-list {
            list-style-type: none;
        }
        
        .event-item {
            display: flex;
            align-items: flex-start;
            padding: 0.75rem 0;
            border-bottom: 1px solid #e2e8f0;
        }
        
        .event-item:last-child {
            border-bottom: none;
        }
        
        .event-date {
            min-width: 50px;
            font-weight: 600;
            color: var(--accent-color);
        }
        
        .event-content {
            flex-grow: 1;
            margin-left: 1rem;
        }
        
        .event-title {
            font-weight: 500;
        }
        
        .event-link {
            display: inline-flex;
            align-items: center;
            margin-top: 0.5rem;
            color: var(--primary-color);
            text-decoration: none;
            font-size: 0.875rem;
            font-weight: 500;
        }
        
        .event-link i {
            margin-left: 0.25rem;
            font-size: 0.75rem;
        }
        
        .event-link:hover {
            text-decoration: underline;
        }
        
        .no-results {
            text-align: center;
            padding: 2rem;
            color: var(--text-light);
        }
        
        .calendar-view {
            display: none;
            margin-top: 1.5rem;
        }
        
        .calendar-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 1rem;
        }
        
        .calendar-nav {
            display: flex;
            align-items: center;
        }
        
        .calendar-nav button {
            background: none;
            border: none;
            color: var(--text-dark);
            font-size: 1rem;
            cursor: pointer;
            padding: 0.5rem;
        }
        
        .calendar-title {
            margin: 0 1rem;
            font-weight: 500;
        }
        
        .calendar-grid {
            display: grid;
            grid-template-columns: repeat(7, 1fr);
            gap: 0.5rem;
        }
        
        .calendar-day-header {
            text-align: center;
            font-weight: 600;
            font-size: 0.875rem;
            padding: 0.5rem;
            color: var(--text-light);
        }
        
        .calendar-day {
            position: relative;
            height: 5rem;
            border-radius: 6px;
            border: 1px solid #e2e8f0;
            padding: 0.5rem;
            background-color: var(--white);
            overflow: hidden;
        }
        
        .calendar-day.has-event {
            border-color: var(--primary-color);
            background-color: #eff6ff;
        }
        
        .calendar-day-number {
            font-size: 0.875rem;
            font-weight: 500;
        }
        
        .calendar-day-event {
            font-size: 0.75rem;
            color: var(--primary-color);
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
            margin-top: 0.25rem;
        }
        
        .loading {
            display: none;
            text-align: center;
            padding: 2rem;
        }
        
        .spinner {
            display: inline-block;
            width: 2rem;
            height: 2rem;
            border: 3px solid rgba(0,0,0,0.1);
            border-radius: 50%;
            border-top-color: var(--primary-color);
            animation: spin 1s ease-in-out infinite;
        }
        
        @keyframes spin {
            to { transform: rotate(360deg); }
        }
        
        .badge {
            display: inline-block;
            padding: 0.25rem 0.5rem;
            border-radius: 9999px;
            font-size: 0.75rem;
            font-weight: 500;
            margin-left: 0.5rem;
        }
        
        .badge-journal {
            background-color: #f0f9ff;
            color: var(--accent-color);
        }
        
        .badge-education {
            background-color: #ecfdf5;
            color: var(--success);
        }
        
        footer {
            text-align: center;
            margin-top: 2rem;
            padding-top: 1.5rem;
            border-top: 1px solid #e2e8f0;
            color: var(--text-light);
            font-size: 0.875rem;
        }
        
        @media (max-width: 768px) {
            .container {
                padding: 1.5rem;
                margin: 1rem;
                border-radius: 8px;
            }
            
            .search-container {
                flex-direction: column;
            }
            
            button {
                margin-left: 0;
                margin-top: 0.75rem;
                width: 100%;
                padding: 0.75rem;
            }
            
            .tabs {
                overflow-x: auto;
                white-space: nowrap;
                padding-bottom: 0.5rem;
            }
            
            .calendar-grid {
                grid-template-columns: repeat(7, minmax(2.5rem, 1fr));
                font-size: 0.75rem;
            }
            
            .calendar-day {
                height: 4rem;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>Calendar of Educational Activities 2025</h1>
            <p class="subtitle">Discover upcoming nursing education events and journal clubs</p>
        </header>
        
        <div class="search-container">
            <i class="fas fa-search"></i>
            <input type="text" id="userInput" placeholder="Search by month, topic, or keyword...">
            <button id="searchButton">
                <i class="fas fa-search"></i> Search
            </button>
        </div>
        
        <div class="tabs">
            <div class="tab active" data-view="list">List View</div>
            <div class="tab" data-view="calendar">Calendar View</div>
        </div>
        
        <div class="loading">
            <div class="spinner"></div>
        </div>
        
        <div id="output"></div>
        
        <div class="calendar-view" id="calendarView">
            <div class="calendar-header">
                <div class="calendar-nav">
                    <button id="prevMonth"><i class="fas fa-chevron-left"></i></button>
                    <div class="calendar-title">January 2025</div>
                    <button id="nextMonth"><i class="fas fa-chevron-right"></i></button>
                </div>
            </div>
            <div class="calendar-grid" id="calendarGrid">
                <!-- Calendar will be generated here -->
            </div>
        </div>
        
        <footer>
            <p>© 2025 Nursing Education Department. All rights reserved.</p>
        </footer>
    </div>

    <script>
        const educationLink = "https://teams.microsoft.com/l/channel/19%3Af84eb65317fe428cbd682e910d22f5b8%40thread.tacv2/Educational%20In-Service?groupId=9288c705-92ac-4ae2-ae2d-1620a3eee297&tenantId=ae8fab86-1b8a-48da-8035-7b59d3d42c89";
        const journalClubLink = "https://teams.microsoft.com/l/team/19%3A477da88b2534414ab2b819c72cc8252e%40thread.tacv2/conversations?groupId=5d12ee56-969e-4508-9a77-6e3368ff3d50&tenantId=ae8fab86-1b8a-48da-8035-7b59d3d42c89";

        const events = {
            "January 2025": ["29 January: Nursing Journal Club"],
            "February 2025": [
                "06 - Advances in the Management of Urinary Incontinence",
                "12 - Using Artificial Intelligence to Treat Diabetic Patients",
                "18 - Stroke: An Overview",
                "20 - In-Low's 60 Seconds: Diabetic Foot Screening",
                "26 - Nursing Journal Club"
            ],
            "March 2025": [
                "06 - Pharmacovigilance",
                "18 - Promoting Participation and Engagement thru Person-Centered Care",
                "26 - Nursing Journal Club"
            ],
            "April 2025": [
                "10 - Fecal Incontinence - Symptoms and Causes",
                "13 - Approach in Doing Quality Improvement Project",
                "16 - Workplace Wellness: Managing Pain in Healthcare Professionals",
                "24 - Skin Tear",
                "30 - Nursing Journal Club"
            ],
            "May 2025": [
                "07 - Intravenous Admixture",
                "08 - Drug-Induced Urinary Incontinence",
                "21 - Unveiling Chronic Pain Assessment Tools",
                "28 - Nursing Journal Club",
                "29 - Stoma Care and Management"
            ],
            "June 2025": [
                "05 - The Role of Botulinum Toxin A in Treating Neurogenic Bladder",
                "18 - The Role of Education in Managing Diabetic Patients",
                "25 - Nursing Journal Club",
                "26 - International Dysphagia Diet Standards Initiative IDDSI"
            ],
            "July 2025": [
                "03 - The process of nutritional screening and nutritional monitoring",
                "09 - Nursing Care for Complications of Diabetes",
                "13 - Coaching Nurses in Building Resilience",
                "23 - Placebo and Nocebo Effects: Practical Strategies for Pain Management",
                "30 - Nursing Journal Club"
            ],
            "August 2025": [
                "13 - Understanding Diabetic Patients",
                "17 - Approach in Doing Quality Improvement Project",
                "20 - Non-Pharmacological Pain Interventions: Practical Applications for Nurses",
                "27 - Nursing Journal Club",
                "28 - Wound Dressing Collection"
            ],
            "September 2025": [
                "04 - Antimicrobial Stewardship Program",
                "14 - Promoting Participation and Engagement thru Person-Centered Care",
                "17 - Engaging Nurses in Spinal Cord Stimulation",
                "24 - Nursing Journal Club",
                "25 - Pressure Injury Prevention & Management"
            ],
            "October 2025": [
                "02 - Clinical Practice Guidelines for the Management of Constipation",
                "08 - Nursing Care of Patients with Insulin Therapy",
                "19 - Cutting-Edge Tools: Unveiling Chronic Pain Assessment Approach",
                "29 - Nursing Journal Club",
                "30 - Stoma Care and Management"
            ],
            "November 2025": [
                "06 - Drug-Induced Urinary Incontinence",
                "12 - Using Artificial Intelligence to Treat Diabetic Patients",
                "16 - Coaching Nurses in Building Resilience",
                "26 - Nursing Journal Club",
                "27 - Dysphagia Interdisciplinary Assessment and Management"
            ],
            "December 2025": [
                "04 - Physical examination: mastering weight and height measurements",
                "10 - Medications Safety",
                "14 - Brain Injury: An Overview",
                "17 - Nursing Journal Club",
                "25 - Placebo and Nocebo Effects: Practical Strategies for Pain Management"
            ],
            "January 2026": [
                "- Fecal Incontinence - Symptoms and Causes",
                "07 - Using Artificial Intelligence to Treat Diabetic Patients",
                "14 - Pharmacology in pain management",
                "26 - Nursing Journal Club",
                "28 - Skin Tear"
            ],
            "February 2026": [
                "05 - Advances in the Management of Urinary Incontinence",
                "11 - Nursing Care of Patients with Insulin Therapy",
                "17 - Non-pharmacology pain intervention",
                "25 - Wound Dressing Collection",
                "27 - Nursing Journal Club"
            ]
        };

        // Parse events for calendar view
        const parsedEvents = [];
        for (const month in events) {
            const [monthName, year] = month.split(' ');
            const monthIndex = new Date(`${monthName} 1, ${year}`).getMonth();
            
            events[month].forEach(event => {
                let day, title;
                
                if (event.startsWith('-')) {
                    day = 1; // Default to day 1 if no date specified
                    title = event.substring(2);
                } else {
                    const parts = event.split(' - ');
                    day = parseInt(parts[0]);
                    title = parts[1] || parts[0];
                }
                
                parsedEvents.push({
                    date: new Date(parseInt(year), monthIndex, day),
                    title: title,
                    isJournalClub: title.includes("Journal Club")
                });
            });
        }

        // Current displayed month in calendar
        let currentMonth = new Date(2025, 0); // Start with January 2025

        // Search functionality
        function searchEvents() {
            const input = document.getElementById("userInput").value.toLowerCase();
            if (!input.trim()) {
                displayAllMonths();
                return;
            }
            
            showLoading();
            
            setTimeout(() => {
                let result = "";
                let hasResults = false;

                // Search by month
                for (const month in events) {
                    if (month.toLowerCase().includes(input)) {
                        result += createMonthCard(month, events[month]);
                        hasResults = true;
                        continue;
                    }
                    
                    // Search by event content
                    const matchingEvents = events[month].filter(event => 
                        event.toLowerCase().includes(input)
                    );
                    
                    if (matchingEvents.length > 0) {
                        result += createMonthCard(month, matchingEvents);
                        hasResults = true;
                    }
                }

                if (!hasResults) {
                    result = `
                        <div class="no-results">
                            <i class="fas fa-search" style="font-size: 2rem; color: #cbd5e1; margin-bottom: 1rem;"></i>
                            <h3>No matching events found</h3>
                            <p>Try different keywords or browse all events</p>
                        </div>
                    `;
                }

                document.getElementById("output").innerHTML = result;
                hideLoading();
            }, 300); // Small delay for loading animation
        }

        // Display all months
        function displayAllMonths() {
            showLoading();
            
            setTimeout(() => {
                let result = "";
                
                for (const month in events) {
                    result += createMonthCard(month, events[month]);
                }
                
                document.getElementById("output").innerHTML = result;
                hideLoading();
            }, 300);
        }

        // Create month card HTML
        function createMonthCard(month, eventList) {
            let html = `
                <div class="month-card">
                    <div class="month-title" onclick="toggleMonth(this)">
                        <h3>${month}</h3>
                        <i class="fas fa-chevron-down"></i>
                    </div>
                    <ul class="event-list">
            `;
            
            eventList.forEach(event => {
                let day, title;
                
                if (event.startsWith('-')) {
                    day = "";
                    title = event.substring(2);
                } else if (event.includes(':')) {
                    const parts = event.split(':');
                    day = parts[0];
                    title = parts[1].trim();
                } else {
                    const parts = event.split(' - ');
                    day = parts[0];
                    title = parts[1] || "";
                }
                
                const isJournalClub = event.includes("Journal Club");
                const link = isJournalClub ? journalClubLink : educationLink;
                const badgeClass = isJournalClub ? "badge-journal" : "badge-education";
                const badgeText = isJournalClub ? "Journal Club" : "Education";
                
                html += `
                    <li class="event-item">
                        <div class="event-date">${day}</div>
                        <div class="event-content">
                            <div class="event-title">
                                ${title}
                                <span class="badge ${badgeClass}">${badgeText}</span>
                            </div>
                            <a href="${link}" target="_blank" class="event-link">
                                Join Session <i class="fas fa-external-link-alt"></i>
                            </a>
                        </div>
                    </li>
                `;
            });
            
            html += `
                    </ul>
                </div>
            `;
            
            return html;
        }

        // Toggle month expansion
        function toggleMonth(element) {
            const eventList = element.nextElementSibling;
            const icon = element.querySelector("i");
            
            if (eventList.style.display === "none") {
                eventList.style.display = "block";
                icon.className = "fas fa-chevron-down";
            } else {
                eventList.style.display = "none";
                icon.className = "fas fa-chevron-right";
            }
        }

        // Show loading spinner
        function showLoading() {
            document.querySelector(".loading").style.display = "block";
            document.getElementById("output").style.display = "none";
        }

        // Hide loading spinner
        function hideLoading() {
            document.querySelector(".loading").style.display = "none";
            document.getElementById("output").style.display = "block";
        }

        // Generate calendar for given month
        function generateCalendar(date) {
            const year = date.getFullYear();
            const month = date.getMonth();
            
            // Update calendar title
            document.querySelector(".calendar-title").textContent = 
                new Date(year, month).toLocaleDateString('en-US', { month: 'long', year: 'numeric' });
            
            const firstDay = new Date(year, month, 1);
            const lastDay = new Date(year, month + 1, 0);
            const daysInMonth = lastDay.getDate();
            const startingDayOfWeek = firstDay.getDay(); // 0 = Sunday
            
            const calendarGrid = document.getElementById("calendarGrid");
            calendarGrid.innerHTML = "";
            
            // Add day headers
            const daysOfWeek = ["Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat"];
            daysOfWeek.forEach(day => {
                const dayHeader = document.createElement("div");
                dayHeader.className = "calendar-day-header";
                dayHeader.textContent = day;
                calendarGrid.appendChild(dayHeader);
            });
            
            // Add empty cells for days before first day of month
            for (let i = 0; i < startingDayOfWeek; i++) {
                const emptyDay = document.createElement("div");
                emptyDay.className = "calendar-day";
                calendarGrid.appendChild(emptyDay);
            }
            
            // Add cells for each day of the month
            for (let day = 1; day <= daysInMonth; day++) {
                const dayCell = document.createElement("div");
                dayCell.className = "calendar-day";
                
                const dayNumber = document.createElement("div");
                dayNumber.className = "calendar-day-number";
                dayNumber.textContent = day;
                dayCell.appendChild(dayNumber);
                
                // Find events for this day
                const currentDate = new Date(year, month, day);
                const dayEvents = parsedEvents.filter(event => {
                    return event.date.getDate() === day && 
                           event.date.getMonth() === month && 
                           event.date.getFullYear() === year;
                });
                
                if (dayEvents.length > 0) {
                    dayCell.classList.add("has-event");
                    
                    // Add first event (with indicator if there are more)
                    const eventElement = document.createElement("div");
                    eventElement.className = "calendar-day-event";
                    eventElement.textContent = dayEvents[0].title + (dayEvents.length > 1 ? ` (+${dayEvents.length - 1})` : "");
                    dayCell.appendChild(eventElement);
                    
                    // Make day clickable to show events
                    dayCell.style.cursor = "pointer";
                    dayCell.onclick = function() {
                        showDayEvents(currentDate, dayEvents);
                    };
                }
                
                calendarGrid.appendChild(dayCell);
            }
        }

        // Show events for selected day
        function showDayEvents(date, events) {
            const formattedDate = date.toLocaleDateString('en-US', {
                weekday: 'long',
                year: 'numeric',
                month: 'long',
                day: 'numeric'
            });
            
            let eventsHtml = `
                <div class="month-card">
                    <div class="month-title">
                        <h3>${formattedDate}</h3>
                    </div>
                    <ul class="event-list">
            `;
            
            events.forEach(event => {
                const isJournalClub = event.isJournalClub;
                const link = isJournalClub ? journalClubLink : educationLink;
                const badgeClass = isJournalClub ? "badge-journal" : "badge-education";
                const badgeText = isJournalClub ? "Journal Club" : "Education";
                
                eventsHtml += `
                    <li class="event-item">
                        <div class="event-content">
                            <div class="event-title">
                                ${event.title}
                                <span class="badge ${badgeClass}">${badgeText}</span>
                            </div>
                            <a href="${link}" target="_blank" class="event-link">
                                Join Session <i class="fas fa-external-link-alt"></i>
                            </a>
                        </div>
                    </li>
                `;
            });
            
            eventsHtml += `
                    </ul>
                </div>
            `;
            
            document.getElementById("output").innerHTML = eventsHtml;
            
            // Switch to list view to show the events
            document.querySelector('.tab[data-view="list"]').click();
        }

        // Initialize the page
        document.addEventListener("DOMContentLoaded", function() {
            // Set up search button
            document.getElementById("searchButton").addEventListener("click", searchEvents);
            document.getElementById("userInput").addEventListener("keyup", function(event) {
                if (event.key === "Enter") {
                    searchEvents();
                }
            });
            
            // Set up tab switching
            document.querySelectorAll(".tab").forEach(tab => {
                tab.addEventListener("click", function() {
                    // Update active tab
                    document.querySelectorAll(".tab").forEach(t => t.classList.remove("active"));
                    this.classList.add("active");
                    
                    // Show appropriate view
                    const view = this.getAttribute("data-view");
                    if (view === "list") {
                        document.getElementById("output").style.display = "block";
                        document.getElementById("calendarView").style.display = "none";
                    } else {
                        document.getElementById("output").style.display = "none";
                        document.getElementById("calendarView").style.display = "block";
                        generateCalendar(currentMonth);
                    }
                });
            });
            
            // Set up calendar navigation
            document.getElementById("prevMonth").addEventListener("click", function() {
                currentMonth = new Date(currentMonth.getFullYear(), currentMonth.getMonth() - 1);
                generateCalendar(currentMonth);
            });
            
            document.getElementById("nextMonth").addEventListener("click", function() {
                currentMonth = new Date(currentMonth.getFullYear(), currentMonth.getMonth() + 1);
                generateCalendar(currentMonth);
            });
            
            // Initial display
            displayAllMonths();
            
            // Add global function for month toggling
            window.toggleMonth = toggleMonth;
        });
    </script>
</body>
</html>
