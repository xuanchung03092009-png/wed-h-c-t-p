<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>StudyHub – Nền tảng hỗ trợ học tập cá nhân</title>
    <!-- Font Poppins (hoặc Inter/Roboto) -->
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <!-- Remix Icon CDN -->
    <link href="https://cdn.jsdelivr.net/npm/remixicon@4.2.0/fonts/remixicon.css" rel="stylesheet">
    <style>
        /* ---------------------------------------------------- */
        /* 1. VARIABLES & BASE STYLES */
        /* ---------------------------------------------------- */

        :root {
            /* Light Mode Colors */
            --color-primary: #4B6BFB;
            --color-primary-light: #F3F6FF;
            --color-background: #FFFFFF;
            --color-surface: #FFFFFF;
            --color-text: #1A1A1A;
            --color-text-secondary: #6B7280;
            --color-border: #E5E7EB;
            --color-shadow: rgba(0, 0, 0, 0.08);

            /* Note Tags Colors */
            --tag-red: #FECACA;
            --tag-blue: #BFDBFE;
            --tag-green: #D1FAE5;
            --tag-yellow: #FEF3C7;
            --tag-purple: #E9D5FF;

            /* Common styles */
            --radius: 12px;
            --shadow: 0 4px 14px var(--color-shadow);
            --transition: all 0.2s ease-in-out;
        }

        /* Dark Mode Overrides */
        .dark-mode {
            --color-primary: #6366F1; /* Slightly adjusted primary for dark theme contrast */
            --color-primary-light: #1E293B;
            --color-background: #0F172A;
            --color-surface: #1E293B;
            --color-text: #F8FAFC;
            --color-text-secondary: #94A3B8;
            --color-border: #334155;
            --color-shadow: rgba(0, 0, 0, 0.3);

            /* Note Tags Colors (Darker contrast) */
            --tag-red: #450A0A;
            --tag-blue: #1E3A8A;
            --tag-green: #065F46;
            --tag-yellow: #4C2B0B;
            --tag-purple: #4A1B57;
        }

        * {
            box-sizing: border-box;
        }

        body {
            font-family: 'Poppins', sans-serif;
            margin: 0;
            padding: 0;
            background-color: var(--color-background);
            color: var(--color-text);
            transition: background-color 0.3s, color 0.3s;
            line-height: 1.6;
        }

        /* Utility Classes */
        .card {
            background-color: var(--color-surface);
            border-radius: var(--radius);
            box-shadow: var(--shadow);
            padding: 20px;
            transition: var(--transition);
            border: 1px solid var(--color-border);
        }

        .card:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px var(--color-shadow);
        }

        .btn {
            padding: 10px 18px;
            border-radius: var(--radius);
            font-weight: 600;
            cursor: pointer;
            transition: var(--transition);
            border: none;
            display: inline-flex;
            align-items: center;
            gap: 8px;
            user-select: none;
        }

        .btn-primary {
            background-color: var(--color-primary);
            color: white;
        }

        .btn-primary:hover {
            opacity: 0.9;
            transform: scale(1.02);
        }

        .btn-secondary {
            background-color: var(--color-border);
            color: var(--color-text);
        }
        .btn-secondary:hover {
             opacity: 0.8;
             transform: scale(1.02);
        }
        
        .icon-btn {
            background: none;
            border: none;
            cursor: pointer;
            color: var(--color-text);
            padding: 8px;
            border-radius: 50%;
            transition: var(--transition);
        }
        .icon-btn:hover {
            background-color: var(--color-border);
            transform: scale(1.1);
        }

        /* Input Styles */
        input[type="text"], textarea, select {
            width: 100%;
            padding: 10px;
            border-radius: 8px;
            border: 1px solid var(--color-border);
            background-color: var(--color-background);
            color: var(--color-text);
            transition: var(--transition);
            outline: none;
        }
        input[type="text"]:focus, textarea:focus, select:focus {
            border-color: var(--color-primary);
            box-shadow: 0 0 0 2px var(--color-primary-light);
        }
        textarea {
            resize: vertical;
        }

        /* Scrollbar for better UX (optional, but good) */
        ::-webkit-scrollbar {
            width: 8px;
        }
        ::-webkit-scrollbar-thumb {
            background-color: var(--color-text-secondary);
            border-radius: 10px;
        }
        ::-webkit-scrollbar-track {
            background: var(--color-border);
        }

        /* ---------------------------------------------------- */
        /* 2. HEADER & LAYOUT */
        /* ---------------------------------------------------- */

        header {
            background-color: var(--color-surface);
            box-shadow: 0 2px 4px var(--color-shadow);
            position: sticky;
            top: 0;
            z-index: 1000;
            padding: 15px 30px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-bottom: 1px solid var(--color-border);
        }

        .logo {
            font-size: 1.8rem;
            font-weight: 700;
            color: var(--color-primary);
        }

        .nav-menu {
            display: flex;
            gap: 30px;
            align-items: center;
        }

        .nav-menu a {
            text-decoration: none;
            color: var(--color-text-secondary);
            font-weight: 500;
            padding: 5px 0;
            transition: color 0.2s;
            position: relative;
        }

        .nav-menu a:hover, .nav-menu a.active {
            color: var(--color-primary);
        }
        
        .nav-menu a.active::after {
            content: '';
            position: absolute;
            bottom: -5px;
            left: 0;
            width: 100%;
            height: 3px;
            background-color: var(--color-primary);
            border-radius: 2px;
        }

        .header-actions {
            display: flex;
            align-items: center;
            gap: 15px;
        }
        
        /* Search Box */
        .search-container {
            position: relative;
            width: 300px;
        }
        .search-container input {
            padding-left: 40px;
            background-color: var(--color-primary-light);
            border: 1px solid var(--color-border);
        }
        .search-container input:focus {
             background-color: var(--color-surface);
        }
        .search-container .ri-search-line {
            position: absolute;
            left: 10px;
            top: 50%;
            transform: translateY(-50%);
            color: var(--color-text-secondary);
            pointer-events: none;
        }
        .search-results {
            position: absolute;
            top: 100%;
            left: 0;
            width: 100%;
            max-height: 300px;
            overflow-y: auto;
            background-color: var(--color-surface);
            border-radius: var(--radius);
            box-shadow: var(--shadow);
            z-index: 100;
            padding: 10px 0;
            border: 1px solid var(--color-border);
            display: none; /* Controlled by JS */
        }
        .search-results div {
            padding: 8px 15px;
            cursor: pointer;
            transition: background-color 0.15s;
        }
        .search-results div:hover {
            background-color: var(--color-primary-light);
        }
        .search-results .source-tag {
            font-size: 0.75rem;
            color: var(--color-primary);
            margin-left: 10px;
            font-weight: 500;
        }

        /* Dark Mode Toggle Switch */
        #theme-toggle {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            background-color: var(--color-primary-light);
            color: var(--color-text);
            font-size: 1.2rem;
            transition: var(--transition);
        }

        #theme-toggle:hover {
            box-shadow: 0 0 0 4px var(--color-primary-light);
        }

        .main-content {
            padding: 30px;
        }

        .dashboard-grid {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 20px;
        }

        /* ---------------------------------------------------- */
        /* 3. DASHBOARD MODULES STYLING */
        /* ---------------------------------------------------- */
        
        h2 {
            font-size: 1.5rem;
            font-weight: 600;
            margin-top: 0;
            margin-bottom: 20px;
            color: var(--color-text);
        }

        /* Progress Tracker */
        .progress-tracker {
            grid-column: span 1;
            text-align: center;
        }
        .progress-tracker canvas {
            max-width: 100%;
            height: auto;
            margin: 10px 0;
        }
        .progress-tracker p {
            font-size: 0.9rem;
            color: var(--color-text-secondary);
        }
        .progress-stats {
            margin-top: 15px;
            text-align: left;
            display: flex;
            flex-direction: column;
            gap: 5px;
        }
        .progress-item {
            display: flex;
            justify-content: space-between;
            font-size: 0.95rem;
            font-weight: 500;
        }
        .progress-item span:first-child {
            color: var(--color-text-secondary);
        }
        .progress-bar-container {
            width: 100%;
            background-color: var(--color-border);
            border-radius: 10px;
            height: 6px;
            margin-top: 4px;
        }
        .progress-bar {
            height: 100%;
            background-color: var(--color-primary);
            border-radius: 10px;
            transition: width 0.5s ease-out;
        }
        
        /* Pomodoro Timer */
        .pomodoro-timer {
            grid-column: span 2;
            text-align: center;
            display: flex;
            flex-direction: column;
            align-items: center;
        }
        .timer-display {
            font-size: 4rem;
            font-weight: 700;
            color: var(--color-primary);
            margin: 10px 0;
        }
        .timer-mode {
            font-size: 1.2rem;
            font-weight: 500;
            color: var(--color-text-secondary);
            margin-bottom: 20px;
        }
        .timer-controls {
            display: flex;
            gap: 15px;
            margin-bottom: 15px;
        }
        .session-counter {
            font-size: 0.9rem;
            color: var(--color-text-secondary);
        }
        
        /* To-do List */
        .todo-list-module {
            grid-column: span 1;
            display: flex;
            flex-direction: column;
        }
        .task-input-group {
            display: flex;
            gap: 10px;
            margin-bottom: 20px;
        }
        .task-list {
            flex-grow: 1;
            overflow-y: auto;
            max-height: 300px; /* Limit height for dashboard view */
        }
        .task-item {
            display: flex;
            align-items: center;
            justify-content: space-between;
            padding: 10px 0;
            border-bottom: 1px solid var(--color-border);
            transition: background-color 0.15s;
        }
        .task-item:last-child {
            border-bottom: none;
        }
        .task-item.completed span {
            text-decoration: line-through;
            color: var(--color-text-secondary);
        }
        .task-item-content {
            display: flex;
            align-items: center;
            gap: 10px;
        }
        .task-item input[type="checkbox"] {
            width: 20px;
            height: 20px;
            cursor: pointer;
            accent-color: var(--color-primary);
        }
        .task-item .action-btns {
            display: flex;
            gap: 5px;
        }
        .task-item .action-btns button {
            background: none;
            border: none;
            cursor: pointer;
            color: var(--color-text-secondary);
            font-size: 1rem;
            padding: 5px;
            border-radius: 5px;
            transition: var(--transition);
        }
        .task-item .action-btns button:hover {
            color: var(--color-primary);
            background-color: var(--color-primary-light);
        }

        /* Schedule / Timetable */
        .schedule-module {
            grid-column: span 4;
            overflow-x: auto;
        }
        .schedule-table {
            width: 100%;
            min-width: 900px;
            border-collapse: collapse;
            table-layout: fixed;
        }
        .schedule-table th, .schedule-table td {
            border: 1px solid var(--color-border);
            padding: 10px;
            text-align: center;
            vertical-align: top;
            height: 100px;
        }
        .schedule-table th {
            background-color: var(--color-primary-light);
            color: var(--color-primary);
            font-weight: 600;
        }
        .schedule-entry {
            border-radius: 8px;
            padding: 5px;
            margin-bottom: 5px;
            cursor: pointer;
            font-size: 0.9rem;
            color: white;
            font-weight: 500;
            transition: var(--transition);
        }
        .schedule-entry:hover {
            opacity: 0.9;
        }
        .schedule-entry-empty {
            color: var(--color-text-secondary);
            font-style: italic;
            cursor: pointer;
        }

        /* ---------------------------------------------------- */
        /* 4. MODULE PAGES STYLING (Notes, Resources) */
        /* ---------------------------------------------------- */

        .page-content {
            display: none; /* Hidden by default, shown by JS */
            padding: 30px;
            animation: fadeIn 0.5s;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .page-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 25px;
        }
        .page-header h1 {
            font-size: 2rem;
            font-weight: 700;
            margin: 0;
        }

        /* Notes Module */
        .note-controls {
            display: flex;
            gap: 15px;
            align-items: center;
        }
        .note-view-toggle button {
            font-size: 1.2rem;
        }
        
        /* Note Grid View */
        #notes-list.grid-view {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
            gap: 20px;
        }
        
        .note-card {
            padding: 20px;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            height: 200px; /* Fixed height for grid view */
        }
        
        .note-card-header {
            display: flex;
            justify-content: space-between;
            align-items: flex-start;
            margin-bottom: 10px;
        }
        
        .note-card h3 {
            margin: 0;
            font-size: 1.1rem;
            font-weight: 600;
            overflow: hidden;
            text-overflow: ellipsis;
            white-space: nowrap;
            max-width: 80%;
        }

        .note-card p {
            font-size: 0.9rem;
            color: var(--color-text-secondary);
            overflow: hidden;
            display: -webkit-box;
            -webkit-line-clamp: 3;
            -webkit-box-orient: vertical;
            margin-bottom: 15px;
        }
        
        .note-meta {
            display: flex;
            justify-content: space-between;
            align-items: center;
            font-size: 0.75rem;
            color: var(--color-text-secondary);
            padding-top: 10px;
            border-top: 1px dashed var(--color-border);
        }
        
        .note-tag {
            padding: 4px 8px;
            border-radius: 6px;
            font-weight: 500;
            font-size: 0.7rem;
            color: var(--color-text); /* Fallback color */
        }

        /* Note List View */
        #notes-list.list-view {
            display: flex;
            flex-direction: column;
            gap: 10px;
        }
        .note-row {
            display: grid;
            grid-template-columns: 2fr 4fr 1fr 1fr 0.5fr;
            align-items: center;
            padding: 15px 20px;
            border-bottom: 1px solid var(--color-border);
            cursor: pointer;
        }
        .note-row:hover {
            background-color: var(--color-primary-light);
        }
        .note-row h3 {
            margin: 0;
        }
        .note-row p {
            margin: 0;
            overflow: hidden;
            white-space: nowrap;
            text-overflow: ellipsis;
        }
        .note-row .note-meta-date {
            color: var(--color-text-secondary);
            font-size: 0.9rem;
        }

        /* Resources Module */
        .resource-controls {
            display: flex;
            gap: 15px;
            margin-bottom: 20px;
            flex-wrap: wrap;
        }
        .resource-controls > div {
            flex-grow: 1;
        }
        .resource-controls select {
            width: auto;
            min-width: 150px;
        }
        
        .resource-table {
            width: 100%;
            border-collapse: collapse;
        }
        .resource-table th, .resource-table td {
            padding: 12px 15px;
            border-bottom: 1px solid var(--color-border);
            text-align: left;
        }
        .resource-table th {
            background-color: var(--color-primary-light);
            color: var(--color-primary);
            font-weight: 600;
        }
        .resource-table tbody tr:hover {
            background-color: var(--color-primary-light);
        }
        .resource-icon {
            font-size: 1.2rem;
            margin-right: 10px;
            color: var(--color-primary);
        }
        .resource-tag-list span {
            display: inline-block;
            background-color: var(--color-border);
            padding: 3px 8px;
            border-radius: 6px;
            font-size: 0.75rem;
            margin-right: 5px;
            color: var(--color-text-secondary);
        }
        .resource-link {
            color: var(--color-primary);
            text-decoration: none;
            font-weight: 500;
            transition: opacity 0.2s;
        }
        .resource-link:hover {
            opacity: 0.8;
        }

        /* Pagination */
        .pagination {
            display: flex;
            justify-content: center;
            gap: 10px;
            margin-top: 20px;
        }
        .pagination button {
            background-color: var(--color-surface);
            color: var(--color-text);
            border: 1px solid var(--color-border);
            padding: 8px 12px;
            border-radius: 8px;
            cursor: pointer;
            transition: var(--transition);
        }
        .pagination button:hover, .pagination button.active {
            background-color: var(--color-primary);
            color: white;
            border-color: var(--color-primary);
        }
        .pagination button:disabled {
            cursor: not-allowed;
            opacity: 0.5;
        }


        /* ---------------------------------------------------- */
        /* 5. MODAL STYLING */
        /* ---------------------------------------------------- */
        .modal-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.5);
            display: flex;
            justify-content: center;
            align-items: center;
            z-index: 2000;
            visibility: hidden;
            opacity: 0;
            transition: visibility 0.3s, opacity 0.3s;
        }
        .modal-overlay.open {
            visibility: visible;
            opacity: 1;
        }
        .modal-content {
            background-color: var(--color-surface);
            padding: 30px;
            border-radius: var(--radius);
            box-shadow: var(--shadow);
            max-width: 500px;
            width: 90%;
            transform: scale(0.9);
            transition: transform 0.3s ease-out;
        }
        .modal-overlay.open .modal-content {
            transform: scale(1);
        }
        .modal-content h3 {
            margin-top: 0;
            font-size: 1.5rem;
            border-bottom: 1px solid var(--color-border);
            padding-bottom: 10px;
            margin-bottom: 20px;
        }
        .modal-content label {
            display: block;
            margin-top: 15px;
            margin-bottom: 5px;
            font-weight: 500;
        }
        .modal-actions {
            margin-top: 30px;
            display: flex;
            justify-content: flex-end;
            gap: 10px;
        }
        .color-picker {
            display: flex;
            gap: 10px;
            margin-top: 10px;
        }
        .color-picker-item {
            width: 30px;
            height: 30px;
            border-radius: 50%;
            cursor: pointer;
            border: 2px solid transparent;
            transition: var(--transition);
        }
        .color-picker-item.selected {
            border-color: var(--color-primary);
            box-shadow: 0 0 0 2px var(--color-surface);
        }

        /* ---------------------------------------------------- */
        /* 6. RESPONSIVENESS (MOBILE & TABLET) */
        /* ---------------------------------------------------- */
        @media (max-width: 1200px) {
            .dashboard-grid {
                grid-template-columns: repeat(2, 1fr);
            }
            .schedule-module, .pomodoro-timer {
                grid-column: span 2;
            }
            .progress-tracker, .todo-list-module {
                grid-column: span 1;
            }
        }
        
        @media (max-width: 800px) {
            header {
                flex-wrap: wrap;
                padding: 10px 20px;
            }
            .logo {
                margin-bottom: 10px;
            }
            .nav-menu {
                display: none; /* Hide main menu on mobile */
                width: 100%;
                order: 3;
                flex-direction: column;
                gap: 10px;
                text-align: center;
                margin-top: 10px;
            }
            .nav-menu a {
                padding: 5px 10px;
                border-bottom: 1px solid var(--color-border);
            }
            .header-actions {
                margin-left: auto;
            }
            .search-container {
                width: 100%;
                order: 2;
                margin-bottom: 10px;
            }
            
            .dashboard-grid {
                grid-template-columns: 1fr;
            }
            .schedule-module, .pomodoro-timer, .progress-tracker, .todo-list-module {
                grid-column: span 1;
            }

            .main-content, .page-content {
                padding: 15px;
            }

            .note-row {
                grid-template-columns: 1fr 1fr 1fr;
                gap: 10px;
            }
            .note-row p {
                display: none; /* Hide content preview on small screens */
            }
            .note-row h3 {
                font-size: 1rem;
            }
            .resource-table th:nth-child(2), .resource-table td:nth-child(2) {
                display: none; /* Hide Description on mobile */
            }
        }
    </style>
</head>
<body>

    <!-- Header & Navigation -->
    <header>
        <div class="logo">StudyHub</div>
        
        <!-- Menu -->
        <nav class="nav-menu">
            <a href="#" data-page="dashboard" class="active"><i class="ri-dashboard-line"></i> Trang chủ</a>
            <a href="#" data-page="notes"><i class="ri-ball-pen-line"></i> Ghi chú</a>
            <a href="#" data-page="resources"><i class="ri-book-open-line"></i> Tài liệu</a>
            <a href="#" data-page="progress"><i class="ri-line-chart-line"></i> Tiến độ</a>
        </nav>

        <div class="header-actions">
            <!-- Search Global -->
            <div class="search-container">
                <i class="ri-search-line"></i>
                <input type="text" id="global-search-input" placeholder="Tìm kiếm Tài liệu, Ghi chú, Nhiệm vụ...">
                <div class="search-results" id="global-search-results">
                    <!-- Search results dynamically inserted here -->
                </div>
            </div>

            <!-- Dark/Light Mode Toggle -->
            <button id="theme-toggle" class="icon-btn" aria-label="Toggle Dark/Light Mode">
                <i class="ri-sun-line"></i>
            </button>
        </div>
    </header>

    <!-- Main Content Area -->
    <main>
        <!-- ---------------------------------------------------- -->
        <!-- 1. DASHBOARD PAGE (Default View) -->
        <!-- ---------------------------------------------------- -->
        <div id="dashboard" class="page-content main-content" style="display: block;">
            <h1>Dashboard Overview</h1>
            <div class="dashboard-grid">
                
                <!-- PROGRESS TRACKER (3.7) -->
                <div class="card progress-tracker">
                    <h2>Tiến Độ Tổng Quan</h2>
                    <canvas id="progress-chart" width="200" height="200"></canvas>
                    <div class="progress-stats">
                        <div class="progress-item">
                            <span>Nhiệm vụ Hoàn thành</span>
                            <span id="stat-tasks">0%</span>
                        </div>
                        <div class="progress-bar-container"><div id="bar-tasks" class="progress-bar" style="width: 0%;"></div></div>
                        
                        <div class="progress-item">
                            <span>Ghi chú Đã tạo</span>
                            <span id="stat-notes">0%</span>
                        </div>
                        <div class="progress-bar-container"><div id="bar-notes" class="progress-bar" style="width: 0%;"></div></div>
                        
                        <div class="progress-item">
                            <span>Phiên Pomodoro</span>
                            <span id="stat-pomodoro">0</span>
                        </div>
                    </div>
                </div>

                <!-- POMODORO TIMER (3.6) -->
                <div class="card pomodoro-timer">
                    <h2>Pomodoro Focus</h2>
                    <div class="timer-mode" id="pomodoro-mode">Học Tập (25:00)</div>
                    <div class="timer-display" id="pomodoro-display">25:00</div>
                    <canvas id="pomodoro-progress" width="250" height="250" style="display:none;"></canvas>
                    <div class="timer-controls">
                        <button id="pomodoro-start" class="btn btn-primary"><i class="ri-play-line"></i> Bắt đầu</button>
                        <button id="pomodoro-pause" class="btn btn-secondary" style="display: none;"><i class="ri-pause-line"></i> Tạm dừng</button>
                        <button id="pomodoro-reset" class="btn btn-secondary"><i class="ri-refresh-line"></i> Đặt lại</button>
                    </div>
                    <div class="session-counter">Số phiên hôm nay: <span id="session-count">0</span></div>
                    <audio id="timer-alarm" src="https://cdn.pixabay.com/download/audio/2021/08/04/audio_349d97a0e5.mp3?filename=bell-ring-39718.mp3" preload="auto"></audio>
                </div>

                <!-- TO-DO LIST (3.3) -->
                <div class="card todo-list-module">
                    <h2>Nhiệm Vụ Hàng Ngày</h2>
                    <div class="task-input-group">
                        <input type="text" id="task-input" placeholder="Thêm nhiệm vụ mới...">
                        <button id="add-task-btn" class="btn btn-primary"><i class="ri-add-line"></i></button>
                    </div>
                    <div class="task-list" id="active-tasks-list">
                        <!-- Active tasks dynamically inserted here -->
                        <p style="text-align:center; color: var(--color-text-secondary); margin-top: 10px;">Chưa có nhiệm vụ nào.</p>
                    </div>
                    <h3 style="font-size: 1.1rem; margin-top: 20px; border-top: 1px solid var(--color-border); padding-top: 15px;">Đã Hoàn Thành</h3>
                    <div class="task-list" id="completed-tasks-list">
                        <!-- Completed tasks dynamically inserted here -->
                        <p style="text-align:center; color: var(--color-text-secondary); margin-top: 10px;">Chưa hoàn thành nhiệm vụ nào.</p>
                    </div>
                </div>

                <!-- WEEKLY SCHEDULE (3.4) -->
                <div class="card schedule-module">
                    <h2>Thời Khóa Biểu Tuần</h2>
                    <div class="schedule-table-container">
                        <table class="schedule-table" id="weekly-schedule-table">
                            <thead>
                                <tr>
                                    <th>Thời Gian</th>
                                    <th>Thứ 2</th>
                                    <th>Thứ 3</th>
                                    <th>Thứ 4</th>
                                    <th>Thứ 5</th>
                                    <th>Thứ 6</th>
                                    <th>Thứ 7</th>
                                    <th>Chủ Nhật</th>
                                </tr>
                            </thead>
                            <tbody>
                                <!-- Rows will be generated by JS -->
                            </tbody>
                        </table>
                    </div>
                </div>

            </div>
        </div>
        
        <!-- ---------------------------------------------------- -->
        <!-- 2. NOTES PAGE (3.2) -->
        <!-- ---------------------------------------------------- -->
        <div id="notes" class="page-content">
            <div class="page-header">
                <h1>Ghi Chú Học Tập</h1>
                <div class="note-controls">
                    <div class="note-view-toggle">
                        <button id="list-view-btn" class="icon-btn active"><i class="ri-list-check"></i></button>
                        <button id="grid-view-btn" class="icon-btn"><i class="ri-grid-fill"></i></button>
                    </div>
                    <button id="add-note-btn" class="btn btn-primary"><i class="ri-add-line"></i> Thêm Ghi Chú</button>
                </div>
            </div>
            
            <div id="notes-list" class="list-view">
                <!-- Notes will be rendered here -->
                <p id="notes-placeholder" style="text-align:center; color: var(--color-text-secondary); margin-top: 50px;">Bấm "Thêm Ghi Chú" để bắt đầu.</p>
            </div>
        </div>

        <!-- ---------------------------------------------------- -->
        <!-- 3. RESOURCES PAGE (3.5) -->
        <!-- ---------------------------------------------------- -->
        <div id="resources" class="page-content">
            <div class="page-header">
                <h1>Kho Tài Liệu Học Tập</h1>
                <button id="add-resource-btn" class="btn btn-primary"><i class="ri-add-line"></i> Thêm Tài Liệu</button>
            </div>

            <div class="resource-controls card">
                <div>
                    <label for="resource-search">Tìm kiếm Tài liệu:</label>
                    <input type="text" id="resource-search" placeholder="Tên, mô tả, tag...">
                </div>
                <div>
                    <label for="resource-subject-filter">Lọc theo Môn học:</label>
                    <select id="resource-subject-filter">
                        <option value="">Tất cả Môn học</option>
                        <!-- Options generated by JS -->
                    </select>
                </div>
                <div>
                    <label for="resource-tag-filter">Lọc theo Tag:</label>
                    <input type="text" id="resource-tag-filter" placeholder="Nhập tag (vd: lý thuyết)">
                </div>
            </div>
            
            <table class="resource-table card" style="margin-top: 20px;">
                <thead>
                    <tr>
                        <th style="width: 25%;">Tên Tài Liệu</th>
                        <th style="width: 35%;">Mô tả</th>
                        <th style="width: 15%;">Môn học</th>
                        <th style="width: 15%;">Tags</th>
                        <th style="width: 10%;">Tác vụ</th>
                    </tr>
                </thead>
                <tbody id="resource-table-body">
                    <!-- Resources will be rendered here -->
                </tbody>
            </table>
            
            <div id="resource-pagination" class="pagination">
                <!-- Pagination buttons here -->
            </div>
            <p id="resources-placeholder" style="text-align:center; color: var(--color-text-secondary); margin-top: 50px; display:none;">Không tìm thấy tài liệu phù hợp.</p>
        </div>
        
        <!-- ---------------------------------------------------- -->
        <!-- 4. PROGRESS HISTORY PAGE (3.7) - Simple Text View for space -->
        <!-- ---------------------------------------------------- -->
        <div id="progress" class="page-content">
            <div class="page-header">
                <h1>Lịch Sử Tiến Độ Học Tập</h1>
            </div>
            <div class="card" id="progress-history-content">
                <p>Nội dung lịch sử tiến độ sẽ được hiển thị ở đây (chỉ ghi nhận Pomodoro và Nhiệm vụ).</p>
                <ul id="progress-log">
                    <li>2025-12-01: Hoàn thành 4/5 nhiệm vụ. 3 phiên Pomodoro.</li>
                    <li>2025-11-30: Hoàn thành 5/5 nhiệm vụ. 5 phiên Pomodoro.</li>
                </ul>
            </div>
        </div>
    </main>


    <!-- ---------------------------------------------------- -->
    <!-- MODALS (Hidden by default) -->
    <!-- ---------------------------------------------------- -->

    <!-- Modal for Notes (Add/Edit) -->
    <div id="note-modal" class="modal-overlay">
        <div class="modal-content">
            <h3 id="note-modal-title">Thêm Ghi Chú Mới</h3>
            <form id="note-form">
                <input type="hidden" id="note-id">
                <label for="note-title">Tiêu đề</label>
                <input type="text" id="note-title" required placeholder="Tóm tắt chương 1">
                
                <label for="note-content">Nội dung</label>
                <textarea id="note-content" rows="8" required placeholder="Các ý chính, công thức, định nghĩa..."></textarea>
                
                <label>Màu nhãn</label>
                <div class="color-picker" id="note-color-picker">
                    <!-- Color options dynamically inserted -->
                </div>

                <div class="modal-actions">
                    <button type="button" class="btn btn-secondary" onclick="closeModal('note-modal')">Hủy</button>
                    <button type="submit" class="btn btn-primary">Lưu Ghi Chú</button>
                </div>
            </form>
        </div>
    </div>

    <!-- Modal for Schedule (Add/Edit) -->
    <div id="schedule-modal" class="modal-overlay">
        <div class="modal-content">
            <h3 id="schedule-modal-title">Thêm Môn Học vào Lịch</h3>
            <form id="schedule-form">
                <input type="hidden" id="schedule-day">
                <input type="hidden" id="schedule-time">
                <input type="hidden" id="schedule-index">
                
                <label for="schedule-subject">Tên Môn học</label>
                <input type="text" id="schedule-subject" required placeholder="Toán Cao Cấp">
                
                <label for="schedule-time-input">Thời gian (VD: 08:00 - 10:00)</label>
                <input type="text" id="schedule-time-input" required>
                
                <label for="schedule-note">Ghi chú (Phòng học, Giáo viên...)</label>
                <input type="text" id="schedule-note" placeholder="Phòng A101">

                <label>Màu Môn học</label>
                <div class="color-picker" id="schedule-color-picker">
                    <!-- Color options dynamically inserted -->
                </div>

                <div class="modal-actions">
                    <button type="button" class="btn btn-secondary" onclick="closeModal('schedule-modal')">Hủy</button>
                    <button type="submit" class="btn btn-primary">Lưu Lịch</button>
                </div>
            </form>
        </div>
    </div>

    <!-- Modal for Resources (Add/Edit) -->
    <div id="resource-modal" class="modal-overlay">
        <div class="modal-content">
            <h3 id="resource-modal-title">Thêm Tài Liệu Mới</h3>
            <form id="resource-form">
                <input type="hidden" id="resource-id">
                <label for="resource-name">Tên Tài Liệu</label>
                <input type="text" id="resource-name" required placeholder="Ebook Vật Lý 11 Cơ bản">
                
                <label for="resource-description">Mô tả</label>
                <textarea id="resource-description" rows="3" placeholder="Tóm tắt lý thuyết và bài tập nâng cao."></textarea>
                
                <label for="resource-link">Link Tải / Xem</label>
                <input type="url" id="resource-link" required placeholder="https://link-to-file.com">

                <label for="resource-subject">Môn học</label>
                <select id="resource-subject" required>
                    <!-- Options generated by JS -->
                </select>

                <label for="resource-tags">Tags (phân cách bằng dấu phẩy)</label>
                <input type="text" id="resource-tags" placeholder="lớp 10, lý thuyết, bài tập">

                <div class="modal-actions">
                    <button type="button" class="btn btn-secondary" onclick="closeModal('resource-modal')">Hủy</button>
                    <button type="submit" class="btn btn-primary">Lưu Tài Liệu</button>
                </div>
            </form>
        </div>
    </div>

    <!-- Audio element for Pomodoro alarm -->
    <audio id="pomodoro-alarm" src="https://cdn.pixabay.com/download/audio/2021/08/04/audio_349d97a0e5.mp3?filename=bell-ring-39718.mp3" preload="auto"></audio>


    <script>
        // --- GLOBAL SETUP (Firestore variables are mandatory but overridden by localStorage for this specific request) ---
        // Note: The user explicitly requested localStorage, so we will not use the Firebase globals,
        // but they are included here as a requirement of the Canvas environment.
        const appId = typeof __app_id !== 'undefined' ? __app_id : 'default-app-id';
        const firebaseConfig = typeof __firebase_config !== 'undefined' ? JSON.parse(__firebase_config) : {};
        const initialAuthToken = typeof __initial_auth_token !== 'undefined' ? __initial_auth_token : null;
        
        // --- DATA KEYS & UTILITIES ---
        const LS_KEYS = {
            THEME: 'studyhub_theme',
            NOTES: 'studyhub_notes',
            TASKS: 'studyhub_tasks',
            SCHEDULE: 'studyhub_schedule',
            RESOURCES: 'studyhub_resources',
            POMODORO_COUNT: 'studyhub_pomodoro_count',
            PROGRESS_HISTORY: 'studyhub_progress_history'
        };

        const SUBJECTS = {
            'Toan': { name: 'Toán', icon: 'ri-calculator-line' },
            'VatLy': { name: 'Vật Lý', icon: 'ri-flashlight-line' },
            'Hoa': { name: 'Hóa', icon: 'ri-flask-line' },
            'Sinh': { name: 'Sinh', icon: 'ri-dna-line' },
            'Van': { name: 'Văn', icon: 'ri-quill-pen-line' },
            'TiengAnh': { name: 'Tiếng Anh', icon: 'ri-translate-2-line' },
            'TinHoc': { name: 'Tin học', icon: 'ri-code-s-slash-line' },
            'GDCD': { name: 'GDCD', icon: 'ri-compasses-2-line' }
        };

        const NOTE_COLORS = [
            { name: 'Red', hex: 'var(--tag-red)' },
            { name: 'Blue', hex: 'var(--tag-blue)' },
            { name: 'Green', hex: 'var(--tag-green)' },
            { name: 'Yellow', hex: 'var(--tag-yellow)' },
            { name: 'Purple', hex: 'var(--tag-purple)' }
        ];

        function saveData(key, data) {
            localStorage.setItem(key, JSON.stringify(data));
        }

        function loadData(key, defaultValue = []) {
            const data = localStorage.getItem(key);
            if (!data) return defaultValue;
            try {
                return JSON.parse(data);
            } catch (e) {
                console.error("Lỗi khi tải dữ liệu từ localStorage:", e);
                return defaultValue;
            }
        }

        function generateId() {
            return Date.now().toString(36) + Math.random().toString(36).substring(2);
        }

        // --- THEME MANAGEMENT (3.1 & 2.1) ---
        const themeToggleBtn = document.getElementById('theme-toggle');
        const themeIcon = themeToggleBtn.querySelector('i');

        function applyTheme(theme) {
            if (theme === 'dark') {
                document.body.classList.add('dark-mode');
                themeIcon.className = 'ri-moon-line';
            } else {
                document.body.classList.remove('dark-mode');
                themeIcon.className = 'ri-sun-line';
            }
            saveData(LS_KEYS.THEME, theme);
        }

        function toggleTheme() {
            const currentTheme = document.body.classList.contains('dark-mode') ? 'dark' : 'light';
            const newTheme = currentTheme === 'light' ? 'dark' : 'light';
            applyTheme(newTheme);
        }

        themeToggleBtn.addEventListener('click', toggleTheme);

        // Initialize theme from localStorage
        const savedTheme = loadData(LS_KEYS.THEME, 'light');
        applyTheme(savedTheme);


        // --- NAVIGATION & PAGE SWITCHING ---
        function showPage(pageId) {
            document.querySelectorAll('.page-content').forEach(page => {
                page.style.display = 'none';
            });
            document.getElementById(pageId).style.display = 'block';

            document.querySelectorAll('.nav-menu a').forEach(link => {
                link.classList.remove('active');
                if (link.getAttribute('data-page') === pageId) {
                    link.classList.add('active');
                }
            });
            
            // Re-render relevant modules when switching pages
            if (pageId === 'notes') NotesModule.renderNotes();
            if (pageId === 'resources') ResourcesModule.renderResources();
            if (pageId === 'dashboard') {
                TasksModule.renderTasks();
                ScheduleModule.renderSchedule();
                ProgressTrackerModule.updateDashboardStats();
            }
        }

        document.querySelectorAll('.nav-menu a').forEach(link => {
            link.addEventListener('click', (e) => {
                e.preventDefault();
                showPage(e.target.getAttribute('data-page'));
            });
        });

        // --- MODAL UTILITIES ---
        function openModal(id, ...args) {
            const modal = document.getElementById(id);
            if (!modal) return;
            modal.classList.add('open');
            
            // Custom modal logic based on ID
            if (id === 'note-modal') NotesModule.openNoteModal(...args);
            if (id === 'schedule-modal') ScheduleModule.openScheduleModal(...args);
            if (id === 'resource-modal') ResourcesModule.openResourceModal(...args);
        }

        function closeModal(id) {
            document.getElementById(id).classList.remove('open');
        }

        // Close modal on outside click (overlay)
        document.querySelectorAll('.modal-overlay').forEach(overlay => {
            overlay.addEventListener('click', (e) => {
                if (e.target === overlay) {
                    closeModal(overlay.id);
                }
            });
        });

        // --- 3.3 MODULE: TO-DO LIST / DAILY TASKS ---
        const TasksModule = {
            tasks: [],

            init() {
                this.tasks = loadData(LS_KEYS.TASKS, []);
                this.renderTasks();
                
                document.getElementById('add-task-btn').addEventListener('click', this.addTask.bind(this));
                document.getElementById('task-input').addEventListener('keypress', (e) => {
                    if (e.key === 'Enter') this.addTask();
                });
            },

            addTask() {
                const input = document.getElementById('task-input');
                const text = input.value.trim();
                if (text === '') return;

                const newTask = {
                    id: generateId(),
                    text: text,
                    completed: false,
                    date: new Date().toISOString().split('T')[0] // For potential future filtering
                };

                this.tasks.unshift(newTask);
                this.saveTasks();
                input.value = '';
                this.renderTasks();
            },

            toggleTask(id) {
                const task = this.tasks.find(t => t.id === id);
                if (task) {
                    task.completed = !task.completed;
                    this.saveTasks();
                    this.renderTasks();
                }
            },

            editTask(id) {
                const task = this.tasks.find(t => t.id === id);
                if (!task) return;

                const newText = prompt("Chỉnh sửa nhiệm vụ:", task.text);
                if (newText && newText.trim() !== '') {
                    task.text = newText.trim();
                    this.saveTasks();
                    this.renderTasks();
                }
            },

            deleteTask(id) {
                if (!confirm("Bạn có chắc chắn muốn xóa nhiệm vụ này?")) return;
                this.tasks = this.tasks.filter(t => t.id !== id);
                this.saveTasks();
                this.renderTasks();
            },

            saveTasks() {
                saveData(LS_KEYS.TASKS, this.tasks);
                ProgressTrackerModule.updateDashboardStats(); // Update progress every time tasks change
            },

            renderTasks() {
                const activeList = document.getElementById('active-tasks-list');
                const completedList = document.getElementById('completed-tasks-list');
                
                activeList.innerHTML = '';
                completedList.innerHTML = '';

                const activeTasks = this.tasks.filter(t => !t.completed);
                const completedTasks = this.tasks.filter(t => t.completed).sort((a, b) => new Date(b.date) - new Date(a.date));

                if (activeTasks.length === 0) {
                    activeList.innerHTML = '<p style="text-align:center; color: var(--color-text-secondary); margin-top: 10px;">Tuyệt vời! Bạn không còn nhiệm vụ nào đang chờ.</p>';
                } else {
                    activeTasks.forEach(task => activeList.appendChild(this.createTaskElement(task)));
                }

                if (completedTasks.length === 0) {
                    completedList.innerHTML = '<p style="text-align:center; color: var(--color-text-secondary); margin-top: 10px;">Chưa hoàn thành nhiệm vụ nào.</p>';
                } else {
                    completedTasks.forEach(task => completedList.appendChild(this.createTaskElement(task)));
                }
            },

            createTaskElement(task) {
                const div = document.createElement('div');
                div.className = `task-item ${task.completed ? 'completed' : ''}`;
                div.dataset.id = task.id;
                
                div.innerHTML = `
                    <div class="task-item-content">
                        <input type="checkbox" ${task.completed ? 'checked' : ''}>
                        <span>${task.text}</span>
                    </div>
                    <div class="action-btns">
                        <button class="edit-task-btn" title="Chỉnh sửa"><i class="ri-edit-line"></i></button>
                        <button class="delete-task-btn" title="Xóa"><i class="ri-delete-bin-line"></i></button>
                    </div>
                `;

                div.querySelector('input[type="checkbox"]').addEventListener('change', () => this.toggleTask(task.id));
                div.querySelector('.edit-task-btn').addEventListener('click', (e) => {
                    e.stopPropagation();
                    this.editTask(task.id);
                });
                div.querySelector('.delete-task-btn').addEventListener('click', (e) => {
                    e.stopPropagation();
                    this.deleteTask(task.id);
                });

                return div;
            }
        };

        // --- 3.2 MODULE: GHI CHÚ HỌC TẬP (Notes App) ---
        const NotesModule = {
            notes: [],
            viewMode: 'list',

            init() {
                this.notes = loadData(LS_KEYS.NOTES, []);
                this.renderNotes();

                document.getElementById('add-note-btn').addEventListener('click', () => openModal('note-modal', null));
                document.getElementById('note-form').addEventListener('submit', this.handleSaveNote.bind(this));
                document.getElementById('list-view-btn').addEventListener('click', () => this.setMode('list'));
                document.getElementById('grid-view-btn').addEventListener('click', () => this.setMode('grid'));
                
                this.renderColorPickers('note-color-picker', NOTE_COLORS, NOTE_COLORS[0].hex);
            },

            setMode(mode) {
                this.viewMode = mode;
                const list = document.getElementById('notes-list');
                list.classList.remove('list-view', 'grid-view');
                list.classList.add(`${mode}-view`);
                
                document.getElementById('list-view-btn').classList.toggle('active', mode === 'list');
                document.getElementById('grid-view-btn').classList.toggle('active', mode === 'grid');

                this.renderNotes();
            },

            renderColorPickers(containerId, colors, selectedColor) {
                const container = document.getElementById(containerId);
                container.innerHTML = colors.map((color, index) => `
                    <div 
                        class="color-picker-item ${color.hex === selectedColor ? 'selected' : ''}" 
                        style="background-color: ${color.hex};" 
                        data-color="${color.hex}"
                        data-index="${index}"
                        title="${color.name}"
                        onclick="this.parentElement.querySelector('.selected')?.classList.remove('selected'); this.classList.add('selected');"
                    ></div>
                `).join('');
            },

            openNoteModal(noteId) {
                const modalTitle = document.getElementById('note-modal-title');
                const form = document.getElementById('note-form');
                const noteIdInput = document.getElementById('note-id');
                const noteTitleInput = document.getElementById('note-title');
                const noteContentInput = document.getElementById('note-content');
                const defaultColor = NOTE_COLORS[0].hex;
                
                form.reset();
                noteIdInput.value = '';
                
                if (noteId) {
                    const note = this.notes.find(n => n.id === noteId);
                    if (note) {
                        modalTitle.textContent = 'Chỉnh Sửa Ghi Chú';
                        noteIdInput.value = note.id;
                        noteTitleInput.value = note.title;
                        noteContentInput.value = note.content;
                        this.renderColorPickers('note-color-picker', NOTE_COLORS, note.color || defaultColor);
                    }
                } else {
                    modalTitle.textContent = 'Thêm Ghi Chú Mới';
                    this.renderColorPickers('note-color-picker', NOTE_COLORS, defaultColor);
                }
            },

            handleSaveNote(e) {
                e.preventDefault();
                const noteId = document.getElementById('note-id').value;
                const title = document.getElementById('note-title').value.trim();
                const content = document.getElementById('note-content').value.trim();
                const color = document.querySelector('#note-color-picker .selected').getAttribute('data-color');

                if (noteId) {
                    // Update existing note
                    const note = this.notes.find(n => n.id === noteId);
                    if (note) {
                        note.title = title;
                        note.content = content;
                        note.color = color;
                    }
                } else {
                    // Add new note
                    const newNote = {
                        id: generateId(),
                        title: title,
                        content: content,
                        date: new Date().toLocaleDateString('vi-VN'),
                        color: color
                    };
                    this.notes.unshift(newNote);
                }

                this.saveNotes();
                closeModal('note-modal');
            },
            
            deleteNote(id) {
                if (!confirm("Bạn có chắc chắn muốn xóa ghi chú này?")) return;
                this.notes = this.notes.filter(n => n.id !== id);
                this.saveNotes();
            },

            saveNotes() {
                saveData(LS_KEYS.NOTES, this.notes);
                this.renderNotes();
                ProgressTrackerModule.updateDashboardStats();
            },

            renderNotes(filteredNotes = this.notes) {
                const container = document.getElementById('notes-list');
                container.innerHTML = '';
                document.getElementById('notes-placeholder').style.display = filteredNotes.length === 0 ? 'block' : 'none';

                filteredNotes.forEach(note => {
                    const element = this.viewMode === 'grid' ? this.createNoteCard(note) : this.createNoteRow(note);
                    container.appendChild(element);
                });
            },

            createNoteCard(note) {
                const card = document.createElement('div');
                card.className = 'card note-card';
                card.style.backgroundColor = note.color;
                
                card.innerHTML = `
                    <div style="flex-grow: 1;">
                        <div class="note-card-header">
                            <h3>${note.title}</h3>
                            <div class="note-actions" style="display:flex; gap:5px;">
                                <button class="icon-btn" title="Chỉnh sửa"><i class="ri-edit-line"></i></button>
                                <button class="icon-btn" title="Xóa"><i class="ri-delete-bin-line"></i></button>
                            </div>
                        </div>
                        <p>${note.content}</p>
                    </div>
                    <div class="note-meta">
                        <span>Ngày tạo: ${note.date}</span>
                    </div>
                `;

                card.querySelector('.note-card-header h3').addEventListener('click', () => openModal('note-modal', note.id));
                card.querySelector('.ri-edit-line').parentElement.addEventListener('click', (e) => {
                    e.stopPropagation();
                    openModal('note-modal', note.id);
                });
                card.querySelector('.ri-delete-bin-line').parentElement.addEventListener('click', (e) => {
                    e.stopPropagation();
                    this.deleteNote(note.id);
                });
                
                // Override default hover for colorful cards to be less distracting
                card.style.transition = 'none';
                card.onmouseover = () => card.style.boxShadow = '0 6px 20px var(--color-shadow)';
                card.onmouseout = () => card.style.boxShadow = 'var(--shadow)';


                return card;
            },
            
            createNoteRow(note) {
                const row = document.createElement('div');
                row.className = 'note-row card';
                row.dataset.id = note.id;
                
                row.innerHTML = `
                    <h3 class="note-title">${note.title}</h3>
                    <p class="note-content">${note.content}</p>
                    <span class="note-meta-date">${note.date}</span>
                    <span class="note-tag" style="background-color: ${note.color};">#GhiChú</span>
                    <div class="note-actions">
                        <button class="icon-btn" title="Chỉnh sửa"><i class="ri-edit-line"></i></button>
                        <button class="icon-btn" title="Xóa"><i class="ri-delete-bin-line"></i></button>
                    </div>
                `;

                row.addEventListener('click', () => openModal('note-modal', note.id));
                row.querySelector('.ri-edit-line').parentElement.addEventListener('click', (e) => {
                    e.stopPropagation();
                    openModal('note-modal', note.id);
                });
                row.querySelector('.ri-delete-bin-line').parentElement.addEventListener('click', (e) => {
                    e.stopPropagation();
                    this.deleteNote(note.id);
                });

                return row;
            }
        };

        // --- 3.4 MODULE: THỜI KHÓA BIỂU (Weekly Schedule) ---
        const ScheduleModule = {
            schedule: {}, // {Day: {TimeSlot: Entry}}
            days: ['Thứ 2', 'Thứ 3', 'Thứ 4', 'Thứ 5', 'Thứ 6', 'Thứ 7', 'Chủ Nhật'],
            defaultTimeSlots: ['Sáng (07:00-11:00)', 'Chiều (13:00-17:00)', 'Tối (18:00-21:00)'],
            colorMap: ['#4B6BFB', '#10B981', '#F59E0B', '#EF4444', '#8B5CF6'], // Subject colors

            init() {
                this.schedule = loadData(LS_KEYS.SCHEDULE, this.initializeDefaultSchedule());
                this.renderColorPickers('schedule-color-picker', this.colorMap.map(c => ({ hex: c })), this.colorMap[0]);
                document.getElementById('schedule-form').addEventListener('submit', this.handleSaveSchedule.bind(this));
                this.renderSchedule();
            },

            initializeDefaultSchedule() {
                const initial = {};
                this.days.forEach(day => {
                    initial[day] = {};
                    this.defaultTimeSlots.forEach(slot => initial[day][slot] = null);
                });
                // Add some mock data
                initial['Thứ 2']['Sáng (07:00-11:00)'] = {
                    subject: 'Toán Cao Cấp',
                    time: '7:30 - 9:00',
                    note: 'Phòng A101',
                    color: this.colorMap[0]
                };
                return initial;
            },

            renderSchedule() {
                const tbody = document.getElementById('weekly-schedule-table').querySelector('tbody');
                tbody.innerHTML = '';

                this.defaultTimeSlots.forEach((slot, timeIndex) => {
                    const row = document.createElement('tr');
                    
                    // Time Slot Header
                    const timeCell = document.createElement('th');
                    timeCell.textContent = slot;
                    row.appendChild(timeCell);

                    this.days.forEach((day, dayIndex) => {
                        const cell = document.createElement('td');
                        const entry = this.schedule[day][slot];
                        
                        if (entry) {
                            cell.innerHTML = `
                                <div class="schedule-entry" 
                                     style="background-color: ${entry.color};"
                                     data-day="${day}" data-slot="${slot}" data-index="${timeIndex}"
                                     title="${entry.note || ''}">
                                    <strong>${entry.subject}</strong><br>
                                    <small>${entry.time}</small>
                                </div>
                            `;
                        } else {
                            cell.innerHTML = `<span class="schedule-entry-empty">Thêm môn học</span>`;
                        }

                        // Add event listener to open modal
                        const entryElement = cell.querySelector('.schedule-entry') || cell.querySelector('.schedule-entry-empty');
                        entryElement.addEventListener('click', () => {
                            openModal('schedule-modal', day, slot, entry ? entry : null);
                        });

                        row.appendChild(cell);
                    });
                    
                    tbody.appendChild(row);
                });
            },

            openScheduleModal(day, slot, entry) {
                const modalTitle = document.getElementById('schedule-modal-title');
                const form = document.getElementById('schedule-form');
                
                document.getElementById('schedule-day').value = day;
                document.getElementById('schedule-time').value = slot;

                form.reset();

                if (entry && entry.subject) {
                    modalTitle.textContent = `Chỉnh Sửa: ${entry.subject}`;
                    document.getElementById('schedule-subject').value = entry.subject;
                    document.getElementById('schedule-time-input').value = entry.time;
                    document.getElementById('schedule-note').value = entry.note || '';
                    this.renderColorPickers('schedule-color-picker', this.colorMap.map(c => ({ hex: c })), entry.color);
                } else {
                    modalTitle.textContent = `Thêm Môn: ${day} (${slot})`;
                    this.renderColorPickers('schedule-color-picker', this.colorMap.map(c => ({ hex: c })), this.colorMap[0]);
                }

                // Add delete button only for existing entries
                let deleteBtn = document.querySelector('#schedule-modal .delete-btn');
                if (entry && entry.subject) {
                    if (!deleteBtn) {
                        deleteBtn = document.createElement('button');
                        deleteBtn.type = 'button';
                        deleteBtn.className = 'btn btn-secondary delete-btn';
                        deleteBtn.textContent = 'Xóa Môn Học';
                        deleteBtn.addEventListener('click', () => this.deleteScheduleEntry(day, slot));
                        document.querySelector('#schedule-modal .modal-actions').prepend(deleteBtn);
                    }
                } else {
                    if (deleteBtn) deleteBtn.remove();
                }
            },

            handleSaveSchedule(e) {
                e.preventDefault();
                const day = document.getElementById('schedule-day').value;
                const slot = document.getElementById('schedule-time').value;
                const subject = document.getElementById('schedule-subject').value.trim();
                const time = document.getElementById('schedule-time-input').value.trim();
                const note = document.getElementById('schedule-note').value.trim();
                const color = document.querySelector('#schedule-color-picker .selected').getAttribute('data-color');

                this.schedule[day][slot] = { subject, time, note, color };
                this.saveSchedule();
                closeModal('schedule-modal');
            },

            deleteScheduleEntry(day, slot) {
                if (!confirm("Bạn có chắc chắn muốn xóa môn học này khỏi lịch?")) return;
                this.schedule[day][slot] = null;
                this.saveSchedule();
                closeModal('schedule-modal');
            },

            saveSchedule() {
                saveData(LS_KEYS.SCHEDULE, this.schedule);
                this.renderSchedule();
            },
            
            renderColorPickers(containerId, colors, selectedColor) {
                const container = document.getElementById(containerId);
                container.innerHTML = colors.map((color) => {
                    const colorHex = color.hex || color; // Handle both object and string format
                    return `
                        <div 
                            class="color-picker-item ${colorHex === selectedColor ? 'selected' : ''}" 
                            style="background-color: ${colorHex};" 
                            data-color="${colorHex}"
                            onclick="this.parentElement.querySelector('.selected')?.classList.remove('selected'); this.classList.add('selected');"
                        ></div>
                    `;
                }).join('');
            }
        };


        // --- 3.5 MODULE: KHO TÀI LIỆU (Resource Library) ---
        const ResourcesModule = {
            resources: [],
            currentPage: 1,
            itemsPerPage: 10,
            
            init() {
                this.resources = loadData(LS_KEYS.RESOURCES, this.mockData());
                
                this.populateSubjectSelect();
                this.renderResources();
                
                document.getElementById('add-resource-btn').addEventListener('click', () => openModal('resource-modal', null));
                document.getElementById('resource-form').addEventListener('submit', this.handleSaveResource.bind(this));
                document.getElementById('resource-search').addEventListener('input', () => this.filterAndPaginate());
                document.getElementById('resource-subject-filter').addEventListener('change', () => this.filterAndPaginate());
                document.getElementById('resource-tag-filter').addEventListener('input', () => this.filterAndPaginate());
            },

            mockData() {
                return [
                    { id: generateId(), name: 'Bảng tuần hoàn Hóa học', description: 'Tóm tắt các nguyên tố cơ bản.', link: '#', subject: 'Hoa', tags: 'lớp 10, lý thuyết' },
                    { id: generateId(), name: 'Tài liệu ôn thi THPTQG Toán', description: 'Tập hợp đề thi thử các năm.', link: '#', subject: 'Toan', tags: 'lớp 12, bài tập, đề thi' },
                    { id: generateId(), name: 'Văn mẫu Tác phẩm Chiếc Thuyền Ngoài Xa', description: 'Phân tích nhân vật và tình huống.', link: '#', subject: 'Van', tags: 'lớp 12, văn mẫu' },
                    { id: generateId(), name: 'English Grammar Handbook', description: 'Comprehensive guide to English grammar.', link: '#', subject: 'TiengAnh', tags: 'grammar, reference' }
                ];
            },

            populateSubjectSelect() {
                const selectElement = document.getElementById('resource-subject');
                const filterElement = document.getElementById('resource-subject-filter');
                
                selectElement.innerHTML = Object.keys(SUBJECTS).map(key => 
                    `<option value="${key}">${SUBJECTS[key].name}</option>`
                ).join('');

                filterElement.innerHTML = `<option value="">Tất cả Môn học</option>` + Object.keys(SUBJECTS).map(key => 
                    `<option value="${key}">${SUBJECTS[key].name}</option>`
                ).join('');
            },

            openResourceModal(resourceId) {
                const modalTitle = document.getElementById('resource-modal-title');
                const form = document.getElementById('resource-form');
                
                form.reset();
                document.getElementById('resource-id').value = '';
                
                if (resourceId) {
                    const resource = this.resources.find(r => r.id === resourceId);
                    if (resource) {
                        modalTitle.textContent = 'Chỉnh Sửa Tài Liệu';
                        document.getElementById('resource-id').value = resource.id;
                        document.getElementById('resource-name').value = resource.name;
                        document.getElementById('resource-description').value = resource.description;
                        document.getElementById('resource-link').value = resource.link;
                        document.getElementById('resource-subject').value = resource.subject;
                        document.getElementById('resource-tags').value = resource.tags;
                    }
                } else {
                    modalTitle.textContent = 'Thêm Tài Liệu Mới';
                }
            },
            
            handleSaveResource(e) {
                e.preventDefault();
                const id = document.getElementById('resource-id').value;
                const name = document.getElementById('resource-name').value.trim();
                const description = document.getElementById('resource-description').value.trim();
                const link = document.getElementById('resource-link').value.trim();
                const subject = document.getElementById('resource-subject').value;
                const tags = document.getElementById('resource-tags').value.trim();

                const newResource = { id, name, description, link, subject, tags };

                if (id) {
                    // Update
                    const index = this.resources.findIndex(r => r.id === id);
                    if (index !== -1) this.resources[index] = newResource;
                } else {
                    // Add
                    newResource.id = generateId();
                    this.resources.unshift(newResource);
                }

                this.saveResources();
                closeModal('resource-modal');
            },

            deleteResource(id) {
                if (!confirm("Bạn có chắc chắn muốn xóa tài liệu này?")) return;
                this.resources = this.resources.filter(r => r.id !== id);
                this.saveResources();
            },

            saveResources() {
                saveData(LS_KEYS.RESOURCES, this.resources);
                this.filterAndPaginate();
            },

            filterResources() {
                const searchTerm = document.getElementById('resource-search').value.toLowerCase();
                const subjectFilter = document.getElementById('resource-subject-filter').value;
                const tagFilter = document.getElementById('resource-tag-filter').value.toLowerCase().split(',').map(t => t.trim()).filter(t => t.length > 0);

                return this.resources.filter(resource => {
                    const nameMatch = resource.name.toLowerCase().includes(searchTerm);
                    const descMatch = resource.description.toLowerCase().includes(searchTerm);
                    const tagStringMatch = resource.tags.toLowerCase().includes(searchTerm);
                    
                    const subjectMatch = subjectFilter === '' || resource.subject === subjectFilter;

                    const tagsMatch = tagFilter.every(tag => resource.tags.toLowerCase().includes(tag));
                    
                    return (nameMatch || descMatch || tagStringMatch) && subjectMatch && tagsMatch;
                });
            },

            filterAndPaginate(page = 1) {
                this.currentPage = page;
                const filtered = this.filterResources();
                const totalPages = Math.ceil(filtered.length / this.itemsPerPage);
                
                const start = (this.currentPage - 1) * this.itemsPerPage;
                const end = start + this.itemsPerPage;
                const paginated = filtered.slice(start, end);
                
                this.renderTable(paginated);
                this.renderPagination(totalPages);
                
                document.getElementById('resources-placeholder').style.display = (filtered.length === 0) ? 'block' : 'none';
            },

            renderTable(resources) {
                const tbody = document.getElementById('resource-table-body');
                tbody.innerHTML = resources.map(r => {
                    const subjectData = SUBJECTS[r.subject] || { name: 'Khác', icon: 'ri-file-line' };
                    const tagSpans = r.tags.split(',').map(tag => 
                        `<span>${tag.trim()}</span>`
                    ).join('');

                    return `
                        <tr data-id="${r.id}">
                            <td><i class="${subjectData.icon} resource-icon"></i> ${r.name}</td>
                            <td>${r.description}</td>
                            <td>${subjectData.name}</td>
                            <td class="resource-tag-list">${tagSpans}</td>
                            <td>
                                <a href="${r.link}" target="_blank" class="resource-link" title="Xem/Tải Tài Liệu"><i class="ri-external-link-line"></i></a>
                                <button class="icon-btn edit-resource-btn" title="Sửa"><i class="ri-edit-line"></i></button>
                                <button class="icon-btn delete-resource-btn" title="Xóa"><i class="ri-delete-bin-line"></i></button>
                            </td>
                        </tr>
                    `;
                }).join('');
                
                // Attach event listeners for edit/delete
                tbody.querySelectorAll('.edit-resource-btn').forEach(btn => {
                    const id = btn.closest('tr').getAttribute('data-id');
                    btn.addEventListener('click', () => openModal('resource-modal', id));
                });
                tbody.querySelectorAll('.delete-resource-btn').forEach(btn => {
                    const id = btn.closest('tr').getAttribute('data-id');
                    btn.addEventListener('click', () => this.deleteResource(id));
                });
            },

            renderPagination(totalPages) {
                const paginationContainer = document.getElementById('resource-pagination');
                paginationContainer.innerHTML = '';
                
                if (totalPages <= 1) return;

                const createButton = (text, page, isActive, isDisabled) => {
                    const btn = document.createElement('button');
                    btn.textContent = text;
                    btn.className = isActive ? 'active' : '';
                    btn.disabled = isDisabled;
                    btn.addEventListener('click', () => this.filterAndPaginate(page));
                    return btn;
                };

                // Previous Button
                paginationContainer.appendChild(createButton('Trước', this.currentPage - 1, false, this.currentPage === 1));

                // Page Numbers (simplified logic)
                for (let i = 1; i <= totalPages; i++) {
                    paginationContainer.appendChild(createButton(i, i, i === this.currentPage, false));
                }

                // Next Button
                paginationContainer.appendChild(createButton('Sau', this.currentPage + 1, false, this.currentPage === totalPages));
            },

            renderResources() {
                // Initial render defaults to page 1 without filtering
                this.filterAndPaginate(1);
            }
        };

        // --- 3.6 MODULE: POMODORO TIMER NÂNG CAO ---
        const PomodoroModule = {
            state: {
                running: false,
                mode: 'focus', // 'focus', 'short-break', 'long-break'
                focusTime: 25 * 60,
                shortBreakTime: 5 * 60,
                longBreakTime: 15 * 60,
                timeLeft: 25 * 60,
                interval: null,
                sessionCount: 0
            },

            init() {
                this.state.sessionCount = loadData(LS_KEYS.POMODORO_COUNT, 0);
                document.getElementById('session-count').textContent = this.state.sessionCount;

                document.getElementById('pomodoro-start').addEventListener('click', this.startTimer.bind(this));
                document.getElementById('pomodoro-pause').addEventListener('click', this.pauseTimer.bind(this));
                document.getElementById('pomodoro-reset').addEventListener('click', this.resetTimer.bind(this));
                
                this.updateDisplay();
                this.drawProgress(1, 'focus'); // Initial draw
            },

            startTimer() {
                if (this.state.running) return;
                this.state.running = true;
                this.state.interval = setInterval(this.tick.bind(this), 1000);
                document.getElementById('pomodoro-start').style.display = 'none';
                document.getElementById('pomodoro-pause').style.display = 'inline-flex';
            },

            pauseTimer() {
                if (!this.state.running) return;
                this.state.running = false;
                clearInterval(this.state.interval);
                document.getElementById('pomodoro-start').style.display = 'inline-flex';
                document.getElementById('pomodoro-pause').style.display = 'none';
            },

            resetTimer() {
                this.pauseTimer();
                this.state.mode = 'focus';
                this.state.timeLeft = this.state.focusTime;
                this.updateDisplay();
                this.drawProgress(1, 'focus');
            },

            tick() {
                this.state.timeLeft--;
                this.updateDisplay();
                this.drawProgress();

                if (this.state.timeLeft <= 0) {
                    this.pauseTimer();
                    this.alarm();
                    this.nextMode();
                }
            },

            alarm() {
                const alarm = document.getElementById('pomodoro-alarm');
                alarm.play().catch(e => console.log("Lỗi khi phát âm thanh:", e));
            },

            nextMode() {
                if (this.state.mode === 'focus') {
                    this.state.sessionCount++;
                    saveData(LS_KEYS.POMODORO_COUNT, this.state.sessionCount);
                    document.getElementById('session-count').textContent = this.state.sessionCount;
                    ProgressTrackerModule.logProgress('Pomodoro');

                    if (this.state.sessionCount % 4 === 0) {
                        this.state.mode = 'long-break';
                        this.state.timeLeft = this.state.longBreakTime;
                    } else {
                        this.state.mode = 'short-break';
                        this.state.timeLeft = this.state.shortBreakTime;
                    }
                } else {
                    this.state.mode = 'focus';
                    this.state.timeLeft = this.state.focusTime;
                }
                this.updateDisplay();
                this.startTimer();
            },

            updateDisplay() {
                const minutes = Math.floor(this.state.timeLeft / 60).toString().padStart(2, '0');
                const seconds = (this.state.timeLeft % 60).toString().padStart(2, '0');
                document.getElementById('pomodoro-display').textContent = `${minutes}:${seconds}`;
                
                let modeText;
                if (this.state.mode === 'focus') modeText = `Học Tập (${Math.floor(this.state.focusTime / 60)}:00)`;
                if (this.state.mode === 'short-break') modeText = `Nghỉ Ngắn (${Math.floor(this.state.shortBreakTime / 60)}:00)`;
                if (this.state.mode === 'long-break') modeText = `Nghỉ Dài (${Math.floor(this.state.longBreakTime / 60)}:00)`;

                document.getElementById('pomodoro-mode').textContent = modeText;
            },

            drawProgress(initialRatio = 0, initialMode = null) {
                const canvas = document.getElementById('pomodoro-progress');
                const ctx = canvas.getContext('2d');
                const size = canvas.width;
                const center = size / 2;
                const radius = center - 15;
                const totalTime = initialMode ? (initialMode === 'focus' ? this.state.focusTime : (initialMode === 'short-break' ? this.state.shortBreakTime : this.state.longBreakTime)) : 
                                    (this.state.mode === 'focus' ? this.state.focusTime : (this.state.mode === 'short-break' ? this.state.shortBreakTime : this.state.longBreakTime));

                const ratio = initialRatio === 0 ? this.state.timeLeft / totalTime : initialRatio;
                const endAngle = (2 * Math.PI) * ratio - (Math.PI / 2);

                const primaryColor = document.body.classList.contains('dark-mode') ? '#6366F1' : '#4B6BFB';
                const textColor = document.body.classList.contains('dark-mode') ? '#F8FAFC' : '#1A1A1A';
                
                // Clear canvas
                ctx.clearRect(0, 0, size, size);

                // Background ring
                ctx.beginPath();
                ctx.arc(center, center, radius, 0, 2 * Math.PI);
                ctx.strokeStyle = '#E5E7EB';
                ctx.lineWidth = 15;
                ctx.stroke();

                // Progress arc
                ctx.beginPath();
                ctx.arc(center, center, radius, -Math.PI / 2, endAngle, false);
                ctx.strokeStyle = primaryColor;
                ctx.lineWidth = 15;
                ctx.stroke();

                // Show the canvas and hide text display when running
                document.getElementById('pomodoro-display').style.display = 'none';
                canvas.style.display = 'block';

                if (initialRatio === 1) { // Hide canvas after full draw to show time text
                    document.getElementById('pomodoro-display').style.display = 'block';
                    canvas.style.display = 'none';
                }
            }
        };


        // --- 3.7 MODULE: PROGRESS TRACKER ---
        const ProgressTrackerModule = {
            history: [],

            init() {
                this.history = loadData(LS_KEYS.PROGRESS_HISTORY, []);
                this.updateDashboardStats();
            },

            updateDashboardStats() {
                const allTasks = loadData(LS_KEYS.TASKS, []);
                const completedTasks = allTasks.filter(t => t.completed).length;
                const totalTasks = allTasks.length;
                const taskPercent = totalTasks > 0 ? Math.round((completedTasks / totalTasks) * 100) : 0;
                
                const allNotes = loadData(LS_KEYS.NOTES, []).length;
                const targetNotes = 50; // Arbitrary goal
                const notePercent = Math.min(100, Math.round((allNotes / targetNotes) * 100));

                const sessionCount = loadData(LS_KEYS.POMODORO_COUNT, 0);

                // Update text stats
                document.getElementById('stat-tasks').textContent = `${taskPercent}%`;
                document.getElementById('bar-tasks').style.width = `${taskPercent}%`;

                document.getElementById('stat-notes').textContent = `${notePercent}% (${allNotes} / ${targetNotes})`;
                document.getElementById('bar-notes').style.width = `${notePercent}%`;

                document.getElementById('stat-pomodoro').textContent = `${sessionCount} phiên`;

                // Draw Chart
                this.drawProgressChart(taskPercent, notePercent, Math.min(100, sessionCount * 10)); // Map sessions to a visual metric
            },

            drawProgressChart(taskPercent, notePercent, pomoVisualPercent) {
                const canvas = document.getElementById('progress-chart');
                const ctx = canvas.getContext('2d');
                const size = canvas.width;
                const center = size / 2;
                const radius = center - 20;

                const total = 100;
                const taskAngle = (taskPercent / total) * 2 * Math.PI;
                const noteAngle = (notePercent / total) * 2 * Math.PI;
                const pomoAngle = (pomoVisualPercent / total) * 2 * Math.PI;
                
                const primaryColor = document.body.classList.contains('dark-mode') ? '#6366F1' : '#4B6BFB';
                const colorTask = primaryColor;
                const colorNote = '#10B981';
                const colorPomo = '#F59E0B';
                const colorBg = '#E5E7EB';

                ctx.clearRect(0, 0, size, size);

                let currentAngle = -Math.PI / 2; // Start from top

                // Draw Tasks Arc
                ctx.beginPath();
                ctx.arc(center, center, radius, currentAngle, currentAngle + taskAngle);
                ctx.strokeStyle = colorTask;
                ctx.lineWidth = 20;
                ctx.stroke();
                currentAngle += taskAngle;

                // Draw Notes Arc
                ctx.beginPath();
                ctx.arc(center, center, radius, currentAngle, currentAngle + noteAngle);
                ctx.strokeStyle = colorNote;
                ctx.lineWidth = 20;
                ctx.stroke();
                currentAngle += noteAngle;

                // Draw Pomodoro Arc
                ctx.beginPath();
                ctx.arc(center, center, radius, currentAngle, currentAngle + pomoAngle);
                ctx.strokeStyle = colorPomo;
                ctx.lineWidth = 20;
                ctx.stroke();
                currentAngle += pomoAngle;
                
                // Draw Remaining Background
                ctx.beginPath();
                ctx.arc(center, center, radius, currentAngle, 3 * Math.PI / 2);
                ctx.strokeStyle = colorBg;
                ctx.lineWidth = 20;
                ctx.stroke();

                // Center Text (Total Progress: simple average)
                const totalAvg = Math.round((taskPercent + notePercent + pomoVisualPercent) / 3);
                ctx.fillStyle = primaryColor;
                ctx.font = "700 30px Poppins";
                ctx.textAlign = "center";
                ctx.fillText(`${totalAvg}%`, center, center + 10);
            },

            logProgress(type) {
                const today = new Date().toLocaleDateString('vi-VN');
                
                // Find existing log for today
                let logEntry = this.history.find(h => h.date === today);

                // Always update stats before logging
                this.updateDashboardStats();

                const allTasks = loadData(LS_KEYS.TASKS, []);
                const completedTasks = allTasks.filter(t => t.completed).length;
                const totalTasks = allTasks.length;
                
                if (!logEntry) {
                    logEntry = {
                        date: today,
                        tasksCompleted: completedTasks,
                        tasksTotal: totalTasks,
                        pomodoroSessions: 0,
                        notesCount: loadData(LS_KEYS.NOTES, []).length
                    };
                    this.history.unshift(logEntry);
                }
                
                if (type === 'Task') {
                    logEntry.tasksCompleted = completedTasks;
                    logEntry.tasksTotal = totalTasks;
                }
                if (type === 'Pomodoro') {
                    logEntry.pomodoroSessions = loadData(LS_KEYS.POMODORO_COUNT, 0);
                }
                if (type === 'Note') {
                    logEntry.notesCount = loadData(LS_KEYS.NOTES, []).length;
                }

                this.saveHistory();
                this.renderHistoryLog();
            },
            
            saveHistory() {
                saveData(LS_KEYS.PROGRESS_HISTORY, this.history);
            },
            
            renderHistoryLog() {
                const logUl = document.getElementById('progress-log');
                if (!logUl) return;
                
                logUl.innerHTML = this.history.map(h => `
                    <li>
                        <strong>${h.date}:</strong> 
                        Hoàn thành ${h.tasksCompleted}/${h.tasksTotal} nhiệm vụ. 
                        ${h.pomodoroSessions} phiên Pomodoro. 
                        Tổng ${h.notesCount} ghi chú.
                    </li>
                `).join('');
            }
        };

        // --- 3.8 MODULE: GLOBAL SEARCH SYSTEM ---
        const SearchModule = {
            init() {
                document.getElementById('global-search-input').addEventListener('input', this.liveSearch.bind(this));
                document.addEventListener('click', (e) => {
                    const resultsBox = document.getElementById('global-search-results');
                    if (!resultsBox.contains(e.target) && e.target.id !== 'global-search-input') {
                        resultsBox.style.display = 'none';
                    }
                });
            },

            liveSearch(e) {
                const query = e.target.value.toLowerCase().trim();
                const resultsBox = document.getElementById('global-search-results');
                resultsBox.innerHTML = '';

                if (query.length < 2) {
                    resultsBox.style.display = 'none';
                    return;
                }
                
                const results = [];
                
                // 1. Search Notes
                NotesModule.notes.filter(n => 
                    n.title.toLowerCase().includes(query) || n.content.toLowerCase().includes(query)
                ).slice(0, 3).forEach(n => {
                    results.push({
                        title: n.title,
                        source: 'Ghi Chú',
                        id: n.id,
                        action: () => { showPage('notes'); openModal('note-modal', n.id); }
                    });
                });

                // 2. Search Tasks
                TasksModule.tasks.filter(t => 
                    t.text.toLowerCase().includes(query)
                ).slice(0, 3).forEach(t => {
                    results.push({
                        title: `[${t.completed ? 'Xong' : 'Chờ'}] ${t.text}`,
                        source: 'Nhiệm Vụ',
                        id: t.id,
                        action: () => { showPage('dashboard'); } // Tasks visible on dashboard
                    });
                });
                
                // 3. Search Resources
                ResourcesModule.resources.filter(r => 
                    r.name.toLowerCase().includes(query) || r.description.toLowerCase().includes(query) || r.tags.toLowerCase().includes(query)
                ).slice(0, 3).forEach(r => {
                    results.push({
                        title: r.name,
                        source: 'Tài Liệu',
                        id: r.id,
                        action: () => { showPage('resources'); }
                    });
                });
                
                if (results.length > 0) {
                    results.forEach(item => {
                        const div = document.createElement('div');
                        div.innerHTML = `${item.title} <span class="source-tag">(${item.source})</span>`;
                        div.addEventListener('click', () => {
                            item.action();
                            resultsBox.style.display = 'none';
                        });
                        resultsBox.appendChild(div);
                    });
                    resultsBox.style.display = 'block';
                } else {
                    resultsBox.innerHTML = '<div>Không tìm thấy kết quả.</div>';
                    resultsBox.style.display = 'block';
                }
            }
        };


        // --- APPLICATION INITIALIZATION ---
        document.addEventListener('DOMContentLoaded', () => {
            TasksModule.init();
            NotesModule.init();
            ScheduleModule.init();
            ResourcesModule.init();
            PomodoroModule.init();
            ProgressTrackerModule.init();
            SearchModule.init();
            
            // Set initial page view
            showPage('dashboard');
        });
    </script>
</body>
</html>