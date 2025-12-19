<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Task Dashboard | Управление задачами</title>
    <style>
        :root {
            --primary-color: #12C1D9;
            --secondary-color: #2CC93C;
            --accent-color: #6C63FF;
            --vacation-color: #FF9F43;
            --sick-color: #FF6B6B;
            --light-color: #F8F9FA;
            --dark-color: #343A40;
            --gray-color: #6C757D;
            --light-gray: #E9ECEF;
            --border-radius: 12px;
            --box-shadow: 0 4px 12px rgba(0, 0, 0, 0.08);
            --transition: all 0.3s ease;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #f5f7fa 0%, #e4edf5 100%);
            color: var(--dark-color);
            line-height: 1.6;
            min-height: 100vh;
            padding: 20px;
        }

        .container {
            max-width: 1400px;
            margin: 0 auto;
        }

        header {
            text-align: center;
            margin-bottom: 30px;
            padding: 20px;
            background: white;
            border-radius: var(--border-radius);
            box-shadow: var(--box-shadow);
        }

        h1 {
            color: var(--dark-color);
            font-size: 2.5rem;
            margin-bottom: 10px;
            background: linear-gradient(45deg, var(--primary-color), var(--secondary-color));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .subtitle {
            color: var(--gray-color);
            font-size: 1.1rem;
        }

        .tab-button-container {
            display: flex;
            gap: 10px;
            margin-bottom: 30px;
            flex-wrap: wrap;
            background: white;
            padding: 15px;
            border-radius: var(--border-radius);
            box-shadow: var(--box-shadow);
        }

        .tab-button {
            padding: 14px 28px;
            background: white;
            border: 2px solid var(--light-gray);
            border-radius: var(--border-radius);
            cursor: pointer;
            font-weight: 600;
            font-size: 16px;
            color: var(--dark-color);
            transition: var(--transition);
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .tab-button:hover {
            border-color: var(--primary-color);
            color: var(--primary-color);
            transform: translateY(-2px);
        }

        .tab-button.active {
            background: linear-gradient(45deg, var(--primary-color), var(--secondary-color));
            color: white;
            border-color: transparent;
            box-shadow: 0 4px 15px rgba(18, 193, 217, 0.3);
        }

        .tab-content {
            display: none;
            background: white;
            padding: 30px;
            border-radius: var(--border-radius);
            box-shadow: var(--box-shadow);
            margin-bottom: 30px;
        }

        .tab-content h2 {
            margin-bottom: 25px;
            color: var(--dark-color);
            font-size: 1.8rem;
            padding-bottom: 15px;
            border-bottom: 2px solid var(--light-gray);
        }

        .form-group {
            margin-bottom: 20px;
        }

        label {
            display: block;
            margin-bottom: 8px;
            font-weight: 600;
            color: var(--dark-color);
        }

        input, select, textarea {
            width: 100%;
            padding: 14px;
            border: 2px solid var(--light-gray);
            border-radius: var(--border-radius);
            font-size: 16px;
            transition: var(--transition);
            background: white;
        }

        input:focus, select:focus, textarea:focus {
            outline: none;
            border-color: var(--primary-color);
            box-shadow: 0 0 0 3px rgba(18, 193, 217, 0.1);
        }

        textarea {
            min-height: 120px;
            resize: vertical;
        }

        .btn {
            padding: 14px 28px;
            background: linear-gradient(45deg, var(--primary-color), var(--secondary-color));
            color: white;
            border: none;
            border-radius: var(--border-radius);
            cursor: pointer;
            font-weight: 600;
            font-size: 16px;
            transition: var(--transition);
            display: inline-flex;
            align-items: center;
            gap: 8px;
        }

        .btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(18, 193, 217, 0.3);
        }

        .btn-secondary {
            background: var(--light-gray);
            color: var(--dark-color);
        }

        .btn-small {
            padding: 8px 16px;
            font-size: 14px;
        }

        ul {
            list-style: none;
            margin-top: 20px;
        }

        li {
            padding: 15px;
            background: var(--light-color);
            margin-bottom: 10px;
            border-radius: var(--border-radius);
            border-left: 4px solid var(--primary-color);
            display: flex;
            justify-content: space-between;
            align-items: center;
            transition: var(--transition);
        }

        li:hover {
            transform: translateX(5px);
            box-shadow: var(--box-shadow);
        }

        .view-toggle {
            display: flex;
            gap: 10px;
            margin-bottom: 20px;
        }

        .view-toggle-btn {
            padding: 10px 20px;
            background: white;
            border: 2px solid var(--light-gray);
            border-radius: var(--border-radius);
            cursor: pointer;
            font-weight: 600;
            transition: var(--transition);
        }

        .view-toggle-btn:hover {
            border-color: var(--primary-color);
            color: var(--primary-color);
        }

        .view-toggle-btn.active {
            background: linear-gradient(45deg, var(--primary-color), var(--secondary-color));
            color: white;
            border-color: transparent;
        }

        .calendar-container {
            background: white;
            padding: 25px;
            border-radius: var(--border-radius);
            box-shadow: var(--box-shadow);
        }

        .calendar-header {
            font-weight: bold;
            background: linear-gradient(45deg, var(--primary-color), var(--secondary-color));
            color: white;
            padding: 15px;
            text-align: center;
            border-radius: 8px;
        }

        .calendar {
            display: grid;
            grid-template-columns: repeat(7, 1fr);
            gap: 10px;
            margin-top: 20px;
        }

        .calendar-day {
            border: 2px solid var(--light-gray);
            padding: 15px;
            height: 120px;
            position: relative;
            border-radius: var(--border-radius);
            transition: var(--transition);
            background: white;
            overflow: hidden;
            cursor: pointer;
        }

        .calendar-day:hover {
            border-color: var(--primary-color);
            transform: scale(1.02);
            box-shadow: var(--box-shadow);
        }

        .calendar-day.selected {
            border-color: var(--accent-color);
            box-shadow: 0 0 0 3px rgba(108, 99, 255, 0.2);
        }

        .calendar-day span {
            display: block;
            font-weight: bold;
            font-size: 1.2rem;
            margin-bottom: 10px;
            z-index: 1;
            position: relative;
        }

        .calendar-day .hours {
            position: absolute;
            bottom: 15px;
            left: 15px;
            right: 15px;
            background: rgba(18, 193, 217, 0.1);
            padding: 8px;
            border-radius: 8px;
            text-align: center;
            font-weight: 600;
            color: var(--primary-color);
            z-index: 1;
        }

        .task-type-indicator {
            position: absolute;
            top: 5px;
            right: 5px;
            width: 8px;
            height: 8px;
            border-radius: 50%;
        }

        .task-type-indicator.project {
            background-color: var(--accent-color);
        }

        .task-type-indicator.routine {
            background-color: var(--primary-color);
        }

        .task-type-indicator.meeting {
            background-color: var(--secondary-color);
        }

        .task-type-indicator.vacation {
            background-color: var(--vacation-color);
        }

        .task-type-indicator.sick {
            background-color: var(--sick-color);
        }

        .hours-indicator {
            height: 4px;
            background: linear-gradient(90deg, var(--primary-color), var(--secondary-color));
            border-radius: 2px;
            margin-top: 5px;
            position: relative;
        }

        .hours-indicator::after {
            content: '';
            position: absolute;
            top: -2px;
            right: 0;
            width: 8px;
            height: 8px;
            background: var(--secondary-color);
            border-radius: 50%;
        }

        .day-details {
            background: white;
            padding: 25px;
            border-radius: var(--border-radius);
            box-shadow: var(--box-shadow);
            margin-top: 20px;
            display: none;
        }

        .day-details.active {
            display: block;
            animation: fadeIn 0.3s ease;
        }

        .day-details-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
            padding-bottom: 15px;
            border-bottom: 2px solid var(--light-gray);
        }

        .day-tasks-list {
            margin-top: 20px;
        }

        .day-task-item {
            padding: 15px;
            background: var(--light-color);
            margin-bottom: 10px;
            border-radius: var(--border-radius);
            border-left: 4px solid var(--primary-color);
            transition: var(--transition);
        }

        .day-task-item:hover {
            transform: translateX(5px);
            box-shadow: var(--box-shadow);
        }

        .day-task-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 10px;
        }

        .task-type-badge {
            padding: 4px 12px;
            border-radius: 20px;
            font-size: 12px;
            font-weight: 600;
            display: inline-flex;
            align-items: center;
            gap: 5px;
        }

        .badge-project {
            background-color: rgba(108, 99, 255, 0.1);
            color: var(--accent-color);
        }

        .badge-routine {
            background-color: rgba(18, 193, 217, 0.1);
            color: var(--primary-color);
        }

        .badge-meeting {
            background-color: rgba(44, 201, 60, 0.1);
            color: var(--secondary-color);
        }

        .badge-vacation {
            background-color: rgba(255, 159, 67, 0.1);
            color: var(--vacation-color);
        }

        .badge-sick {
            background-color: rgba(255, 107, 107, 0.1);
            color: var(--sick-color);
        }

        .table-container {
            overflow-x: auto;
            border-radius: var(--border-radius);
            box-shadow: var(--box-shadow);
        }

        table {
            width: 100%;
            border-collapse: separate;
            border-spacing: 0;
            background: white;
        }

        th {
            background: linear-gradient(45deg, var(--primary-color), var(--secondary-color));
            color: white;
            padding: 18px;
            text-align: left;
            font-weight: 600;
            position: sticky;
            top: 0;
        }

        td {
            padding: 16px;
            border-bottom: 1px solid var(--light-gray);
        }

        tr:hover {
            background: rgba(18, 193, 217, 0.05);
        }

        tr:last-child td {
            border-bottom: none;
        }

        .filters {
            display: flex;
            gap: 20px;
            margin-bottom: 25px;
            flex-wrap: wrap;
            background: white;
            padding: 20px;
            border-radius: var(--border-radius);
            box-shadow: var(--box-shadow);
        }

        .filter-group {
            flex: 1;
            min-width: 200px;
        }

        .stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            margin-top: 30px;
        }

        .stat-card {
            background: white;
            padding: 25px;
            border-radius: var(--border-radius);
            box-shadow: var(--box-shadow);
            text-align: center;
            transition: var(--transition);
        }

        .stat-card:hover {
            transform: translateY(-5px);
        }

        .stat-value {
            font-size: 2.5rem;
            font-weight: 700;
            margin: 10px 0;
        }

        .stat-label {
            color: var(--gray-color);
            font-size: 1rem;
            font-weight: 600;
        }

        .total-stats {
            display: flex;
            justify-content: space-between;
            align-items: center;
            background: linear-gradient(45deg, var(--primary-color), var(--secondary-color));
            color: white;
            padding: 25px;
            border-radius: var(--border-radius);
            margin-top: 20px;
            box-shadow: var(--box-shadow);
        }

        .total-item {
            text-align: center;
        }

        .total-value {
            font-size: 2.5rem;
            font-weight: 700;
            margin-bottom: 5px;
        }

        .total-label {
            font-size: 0.9rem;
            opacity: 0.9;
        }

        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.5);
            z-index: 1000;
            justify-content: center;
            align-items: center;
            animation: fadeIn 0.3s ease;
        }

        .modal.active {
            display: flex;
        }

        .modal-content {
            background: white;
            padding: 30px;
            border-radius: var(--border-radius);
            max-width: 600px;
            width: 90%;
            max-height: 80vh;
            overflow-y: auto;
            box-shadow: 0 10px 40px rgba(0, 0, 0, 0.2);
        }

        .modal-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
            padding-bottom: 15px;
            border-bottom: 2px solid var(--light-gray);
        }

        .modal-close {
            background: none;
            border: none;
            font-size: 24px;
            cursor: pointer;
            color: var(--gray-color);
            transition: var(--transition);
        }

        .modal-close:hover {
            color: var(--dark-color);
        }

        @media (max-width: 768px) {
            .tab-button-container {
                flex-direction: column;
            }
            
            .tab-button {
                width: 100%;
                justify-content: center;
            }
            
            .calendar {
                grid-template-columns: repeat(7, 1fr);
                gap: 5px;
            }
            
            .calendar-day {
                height: 80px;
                padding: 10px;
            }
            
            .filters {
                flex-direction: column;
            }
            
            .table-container {
                font-size: 14px;
            }
            
            th, td {
                padding: 10px;
            }
            
            .total-stats {
                flex-direction: column;
                gap: 20px;
            }
            
            .view-toggle {
                flex-direction: column;
            }
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .tab-content {
            animation: fadeIn 0.3s ease;
        }

        .notification {
            position: fixed;
            top: 20px;
            right: 20px;
            padding: 15px 25px;
            background: white;
            border-radius: var(--border-radius);
            box-shadow: 0 5px 20px rgba(0,0,0,0.15);
            border-left: 4px solid var(--secondary-color);
            transform: translateX(120%);
            transition: transform 0.3s ease;
            z-index: 1000;
        }

        .notification.show {
            transform: translateX(0);
        }
        
        .login-modal {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            z-index: 2000;
            display: flex;
            justify-content: center;
            align-items: center;
            animation: fadeIn 0.5s ease;
        }

        .login-container {
            background: white;
            padding: 40px;
            border-radius: var(--border-radius);
            box-shadow: 0 20px 60px rgba(0, 0, 0, 0.3);
            text-align: center;
            max-width: 400px;
            width: 90%;
        }

        .login-logo {
            margin-bottom: 30px;
        }

        .login-title {
            font-size: 1.8rem;
            margin-bottom: 10px;
            color: var(--dark-color);
        }

        .login-subtitle {
            color: var(--gray-color);
            margin-bottom: 30px;
            font-size: 1rem;
        }

        .login-form {
            margin-top: 20px;
        }

        .form-group {
            margin-bottom: 20px;
        }

        .form-group label {
            display: block;
            text-align: left;
            margin-bottom: 8px;
            font-weight: 600;
            color: var(--dark-color);
        }

        .password-container {
            position: relative;
        }

        .toggle-password {
            position: absolute;
            right: 10px;
            top: 50%;
            transform: translateY(-50%);
            background: none;
            border: none;
            cursor: pointer;
            color: var(--gray-color);
            font-size: 18px;
        }

        .login-error {
            color: #ff6b6b;
            margin-top: 10px;
            font-size: 0.9rem;
            display: none;
        }

        .login-error.show {
            display: block;
        }

        .remember-me {
            display: flex;
            align-items: center;
            margin-bottom: 20px;
        }

        .remember-me input {
            width: auto;
            margin-right: 10px;
        }

        .remember-me label {
            margin: 0;
            font-weight: normal;
        }

        .current-user {
            position: fixed;
            top: 20px;
            right: 20px;
            background: white;
            padding: 10px 20px;
            border-radius: 50px;
            box-shadow: var(--box-shadow);
            font-weight: 600;
            color: var(--primary-color);
            border: 2px solid var(--primary-color);
            z-index: 100;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .logout-btn {
            background: none;
            border: none;
            cursor: pointer;
            color: var(--gray-color);
            margin-left: 5px;
            font-size: 18px;
        }

        .logout-btn:hover {
            color: var(--dark-color);
        }

        .employee-view {
            display: none;
        }

        .employee-view.active {
            display: block;
        }

        .simplified-form {
            max-width: 600px;
            margin: 0 auto;
            padding: 30px;
            background: white;
            border-radius: var(--border-radius);
            box-shadow: var(--box-shadow);
        }
        
        .user-role-badge {
            background: var(--primary-color);
            color: white;
            padding: 2px 8px;
            border-radius: 12px;
            font-size: 0.8rem;
            margin-left: 8px;
        }

        .employee-card {
            background: white;
            padding: 20px;
            border-radius: var(--border-radius);
            box-shadow: var(--box-shadow);
            margin-bottom: 15px;
            border-left: 4px solid var(--primary-color);
        }

        .employee-info {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .employee-details {
            flex: 1;
        }

        .employee-name {
            font-weight: 600;
            font-size: 1.1rem;
            margin-bottom: 5px;
        }

        .employee-login {
            color: var(--gray-color);
            font-size: 0.9rem;
        }

        .employee-actions {
            display: flex;
            gap: 10px;
        }

        .form-row {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 20px;
            margin-bottom: 20px;
        }

        @media (max-width: 768px) {
            .form-row {
                grid-template-columns: 1fr;
            }
            
            .employee-info {
                flex-direction: column;
                align-items: flex-start;
                gap: 15px;
            }
            
            .employee-actions {
                align-self: flex-end;
            }
        }
    </style>
</head>
<body>
    <!-- Модальное окно авторизации -->
    <div id="loginModal" class="login-modal" style="display: block;">
        <div class="login-container">
            <div class="login-logo">
                <svg width="155" height="47" viewBox="0 0 155 47" fill="none" xmlns="http://www.w3.org/2000/svg">
                  <path d="M20.1671 47C20.1671 47 0 41.0173 0 11.3571V0H40.3342V11.3571C40.3342 39.9018 20.1671 47 20.1671 47Z" fill="#4FB84E"></path>
                  <path d="M31.8351 11.4585H15.5908V20.8889H31.8351V23.7282C31.8351 28.4941 30.4773 32.3474 23.3358 32.3474H15.5908V44.7692C18.2563 46.4423 20.1674 47 20.1674 47C20.1674 47 40.3345 39.9018 40.3345 11.3571V2.78857C40.3345 7.55449 38.2725 11.3571 31.8351 11.4585Z" fill="#055532"></path>
                  <path class="letter" d="M51.5488 27.9363H55.7231C57.9862 27.9363 59.5956 28.9503 59.5956 30.9276C59.5956 31.891 59.1429 32.8543 58.288 33.3613V33.412C59.5955 33.8176 60.0482 34.9837 60.0482 35.9978C60.0482 38.4821 57.9862 39.3947 55.7231 39.3947H51.5488V27.9363ZM55.7734 32.3473C56.4774 32.3473 56.7792 31.8403 56.7792 31.2826C56.7792 30.7755 56.4774 30.3192 55.7231 30.3192H54.3652V32.3473H55.7734ZM55.9745 36.9611C56.7792 36.9611 57.1815 36.4034 57.1815 35.7443C57.1815 35.0851 56.7792 34.5781 55.9745 34.5781H54.3149V36.9611H55.9745Z" fill="black"></path>
                  <path class="letter" d="M64.323 27.9363H67.2399L71.1124 39.344H68.2458L67.5417 36.9611H64.0212L63.3172 39.344H60.4505L64.323 27.9363ZM66.8879 34.7302L66.2341 32.4994C66.0329 31.7896 65.7815 30.522 65.7815 30.522H65.7312C65.7312 30.522 65.4797 31.7896 65.2786 32.4994L64.6248 34.7302H66.8879Z" fill="black"></path>
                  <path class="letter" d="M72.2188 27.9363H75.0352L78.1533 33.2599C78.6059 34.0204 79.1089 35.1865 79.1089 35.1865H79.1591C79.1591 35.1865 79.0083 33.9697 79.0083 33.2599V27.9363H81.7743V39.344H79.0083L75.8399 34.0204C75.3872 33.2599 74.8843 32.0938 74.8843 32.0938H74.834C74.834 32.0938 74.9849 33.3106 74.9849 34.0204V39.344H72.2188V27.9363Z" fill="black"></path>
                  <path class="letter" d="M86.9544 27.9363V32.3473H88.1111L90.4748 27.9363H93.4421L90.3743 33.412V33.4627L93.5929 39.3947H90.4748L88.0608 34.7809H86.9041V39.3947H84.1381V27.9363H86.9544Z" fill="black"></path>
                  <path class="letter" d="M51.5488 22.765V6.74344H61.3055V7.90957C61.3055 9.1264 60.3499 10.0897 59.1429 10.0897H55.4213V13.436H60.2493V14.5514C60.2493 15.7683 59.2435 16.7823 58.0365 16.7823H55.4213V22.7143H51.5488V22.765Z" fill="black"></path>
                  <path class="letter" d="M67.3905 13.9937H69.1004C69.7542 13.9937 70.2571 13.8416 70.6092 13.4867C70.9612 13.1318 71.1624 12.6755 71.1624 12.0164C71.1624 11.1544 70.8606 10.546 70.2068 10.2925C69.8548 10.1404 69.3519 10.0897 68.7484 10.0897H67.4408V13.9937H67.3905ZM63.4677 6.74344H68.9998C70.408 6.74344 71.4138 6.89555 72.0676 7.14905C72.9729 7.50396 73.7273 8.06167 74.2302 8.87289C74.7331 9.68411 74.9846 10.6474 74.9846 11.8136C74.9846 12.7262 74.7834 13.5881 74.3811 14.3993C73.9787 15.2105 73.3752 15.819 72.6208 16.2246V16.2753C72.7717 16.4781 72.9729 16.7823 73.2243 17.2386L76.2922 22.8664H72.0173L69.201 17.4414H67.3905V22.8664H63.4677V6.74344Z" fill="black"></path>
                  <path class="letter" d="M78.1027 22.765V6.74344H88.1108V10.0897H82.0254V13.0304H86.8535V16.3767H82.0254V19.4187H88.4125V22.765H78.1027Z" fill="black"></path>
                  <path class="letter" d="M90.8771 22.765V6.74344H100.835V10.0897H94.7999V13.0304H99.6279V16.3767H94.7999V19.4187H101.187V22.765H90.8771Z" fill="black"></path>
                  <path class="letter" d="M107.524 19.4187H109.133C110.491 19.4187 111.547 19.0131 112.301 18.2019C113.056 17.3907 113.458 16.2246 113.458 14.7035C113.458 13.2332 113.056 12.0671 112.301 11.2558C111.547 10.4446 110.491 10.0897 109.133 10.0897H107.524V19.4187ZM103.651 22.765V6.74344H109.284C111.798 6.74344 113.81 7.45326 115.269 8.87289C116.727 10.2925 117.481 12.2192 117.481 14.7542C117.481 17.2893 116.727 19.2159 115.269 20.6356C113.81 22.0552 111.798 22.765 109.284 22.765H103.651Z" fill="black"></path>
                  <path class="letter" d="M123.215 14.6531C123.215 16.0221 123.617 17.1882 124.422 18.1008C125.226 19.0134 126.283 19.4697 127.49 19.4697C128.747 19.4697 129.753 19.0134 130.557 18.1008C131.362 17.1882 131.764 16.0221 131.764 14.6531C131.764 13.3349 131.362 12.2195 130.557 11.3575C129.753 10.4956 128.747 10.0393 127.49 10.0393C126.232 10.0393 125.226 10.4956 124.422 11.3575C123.617 12.2195 123.215 13.3349 123.215 14.6531ZM119.191 14.6531C119.191 12.3209 119.946 10.3942 121.505 8.82249C123.064 7.25075 125.076 6.49023 127.49 6.49023C129.904 6.49023 131.915 7.25075 133.474 8.82249C135.033 10.3942 135.788 12.3209 135.788 14.6531C135.788 17.0361 135.033 19.0641 133.474 20.6359C131.915 22.2583 129.904 23.0188 127.49 23.0188C125.076 23.0188 123.064 22.2076 121.505 20.6359C119.946 19.0134 119.191 17.0361 119.191 14.6531Z" fill="black"></path>
                  <path class="letter" d="M137.648 22.765L138.956 6.74344H143.181L145.494 13.5374L146.299 16.1739H146.349C146.651 15.1091 146.902 14.1965 147.154 13.5374L149.467 6.74344H153.692L154.999 22.765H151.127L150.624 15.5654C150.573 15.2105 150.573 14.8049 150.573 14.3486C150.573 13.8923 150.573 13.5374 150.573 13.2839V12.8783H150.523C150.171 13.9937 149.869 14.9063 149.618 15.5654L147.958 20.23H144.639L142.979 15.5654L142.074 12.8783H142.024C142.074 13.8416 142.074 14.7542 142.024 15.5654L141.521 22.765H137.648Z" fill="black"></path>
                </svg>
            </div>
            
            <h2 class="login-title">Task Dashboard</h2>
            <p class="login-subtitle">Система управления задачами и временем</p>
            
            <div class="login-form">
                <div class="form-group">
                    <label for="login-username">Логин</label>
                    <input type="text" id="login-username" placeholder="Введите логин">
                </div>
                
                <div class="form-group">
                    <label for="login-password">Пароль</label>
                    <div class="password-container">
                        <input type="password" id="login-password" placeholder="Введите пароль">
                        <button type="button" class="toggle-password" onclick="togglePassword()">👁️</button>
                    </div>
                </div>
                
                <div class="remember-me">
                    <input type="checkbox" id="remember-me">
                    <label for="remember-me">Запомнить меня</label>
                </div>
                
                <div id="login-error" class="login-error">
                    Неверный логин или пароль
                </div>
                
                <button class="btn" onclick="login()" style="width: 100%;">
                    🔐 Войти в систему
                </button>
                
                <div style="margin-top: 20px; color: var(--gray-color); font-size: 0.9rem;">
                    <p><strong>Тестовые данные:</strong></p>
                    <p><strong>Администратор:</strong></p>
                    <p>Логин: admin | Пароль: admin123</p>
                    <p style="margin-top: 10px;"><strong>Сотрудники:</strong></p>
                    <p>Логин: ivanov | Пароль: ivanov123</p>
                    <p>Логин: petrov | Пароль: petrov123</p>
                </div>
            </div>
        </div>
    </div>

    <!-- Индикатор текущего пользователя -->
    <div id="currentUserIndicator" class="current-user" style="display: none;">
        <span id="currentUserName"></span>
        <span id="currentUserRole" class="user-role-badge"></span>
        <button onclick="logout()" class="logout-btn" title="Выйти">
            🚪
        </button>
    </div>

    <div class="container" id="mainContainer" style="display: none;">
        <header>
            <h1>Task Dashboard</h1>
            <p class="subtitle">Система управления задачами и временем</p>
        </header>

        <!-- Вкладки (только для администратора) -->
        <div id="adminTabs" class="tab-button-container" style="display: none;">
            <button class="tab-button active" onclick="showTab('task-themes')">
                <span>🎯</span> Темы задач
            </button>
            <button class="tab-button" onclick="showTab('employees-section')">
                <span>👥</span> Сотрудники
            </button>
            <button class="tab-button" onclick="showTab('add-task')">
                <span>➕</span> Добавить задачу
            </button>
            <button class="tab-button" onclick="showTab('task-list')">
                <span>📋</span> Список задач
            </button>
            <button class="tab-button" onclick="showTab('dashboard')">
                <span>📅</span> Дэшборд
            </button>
        </div>

        <!-- Упрощенный вид для сотрудника -->
        <div id="employeeView" class="employee-view" style="display: none;">
            <div class="simplified-form">
                <h2 style="text-align: center; margin-bottom: 30px;">📝 Добавление задачи</h2>
                
                <div class="form-group">
                    <label for="employee-task-name">Тема задачи:</label>
                    <select id="employee-task-name" name="employee-task-name">
                        <option value="">Выберите тему</option>
                    </select>
                </div>
                
                <div class="form-group">
                    <label for="employee-subtask-name">Подзадача:</label>
                    <input type="text" id="employee-subtask-name" name="employee-subtask-name" placeholder="Описание подзадачи...">
                </div>
                
                <div class="form-group">
                    <label for="employee-comment">Комментарий:</label>
                    <textarea id="employee-comment" name="employee-comment" placeholder="Добавьте комментарий..."></textarea>
                </div>
                
                <div class="form-group">
                    <label for="employee-task-type">Тип задачи:</label>
                    <select id="employee-task-type" name="employee-task-type">
                        <option value="проект">🚀 Проект</option>
                        <option value="рутина">🔄 Рутина</option>
                        <option value="созвон">📞 Созвон</option>
                        <option value="отпуск">🏖️ Отпуск</option>
                        <option value="больничный">🏥 Больничный</option>
                    </select>
                </div>
                
                <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 20px;">
                    <div class="form-group">
                        <label for="employee-start-time">Время начала:</label>
                        <input type="datetime-local" id="employee-start-time" name="employee-start-time">
                    </div>
                    <div class="form-group">
                        <label for="employee-end-time">Время окончания:</label>
                        <input type="datetime-local" id="employee-end-time" name="employee-end-time">
                    </div>
                </div>
                
                <div style="text-align: center;">
                    <button class="btn" onclick="addEmployeeTask()" style="width: 100%;">
                        <span>💾</span> Сохранить задачу
                    </button>
                </div>
                
                <div style="margin-top: 30px; padding-top: 20px; border-top: 2px solid var(--light-gray);">
                    <h3 style="margin-bottom: 15px;">📋 Мои последние задачи</h3>
                    <div id="employee-tasks-list" style="max-height: 300px; overflow-y: auto;">
                        <!-- Список задач сотрудника -->
                    </div>
                </div>
            </div>
        </div>

        <!-- Вкладка "Темы задач" (только для админа) -->
        <div id="task-themes" class="tab-content" style="display: none;">
            <h2>Темы задач</h2>
            <div class="form-group">
                <label for="new-task-theme">Название темы задачи:</label>
                <input type="text" id="new-task-theme" name="new-task-theme" placeholder="Введите название темы...">
            </div>
            <button class="btn" onclick="addTaskTheme()">
                <span>➕</span> Добавить тему
            </button>

            <h3 style="margin-top: 30px;">Доступные темы:</h3>
            <ul id="task-themes-list">
                <!-- Темы будут добавляться динамически -->
            </ul>
        </div>

        <!-- Вкладка "Сотрудники" (только для админа) -->
        <div id="employees-section" class="tab-content" style="display: none;">
            <h2>Управление сотрудниками</h2>
            
            <div style="background: var(--light-color); padding: 25px; border-radius: var(--border-radius); margin-bottom: 30px;">
                <h3 style="margin-bottom: 20px;">Добавить нового сотрудника</h3>
                
                <div class="form-row">
                    <div class="form-group">
                        <label for="new-employee-fio">ФИО сотрудника:</label>
                        <input type="text" id="new-employee-fio" name="new-employee-fio" placeholder="Иванов Иван Иванович">
                    </div>
                    
                    <div class="form-group">
                        <label for="new-employee-login">Логин:</label>
                        <input type="text" id="new-employee-login" name="new-employee-login" placeholder="ivanov">
                    </div>
                </div>
                
                <div class="form-group">
                    <label for="new-employee-password">Пароль:</label>
                    <input type="password" id="new-employee-password" name="new-employee-password" placeholder="Введите пароль">
                </div>
                
                <div class="form-group">
                    <label for="new-employee-role">Роль:</label>
                    <select id="new-employee-role" name="new-employee-role">
                        <option value="employee">Сотрудник</option>
                        <option value="admin">Администратор</option>
                    </select>
                </div>
                
                <button class="btn" onclick="addEmployee()">
                    <span>👥</span> Добавить сотрудника
                </button>
            </div>

            <h3 style="margin-top: 30px;">Список сотрудников:</h3>
            <div id="employees-list">
                <!-- Сотрудники будут добавляться динамически -->
            </div>
        </div>

        <!-- Вкладка "Добавить задачу" (для админа) -->
        <div id="add-task" class="tab-content" style="display: none;">
            <h2>Добавить задачу</h2>
            <div class="form-group">
                <label for="task-name">Тема задачи:</label>
                <select id="task-name" name="task-name">
                    <option value="">Выберите тему</option>
                </select>
            </div>
            
            <div class="form-group">
                <label for="responsible-select">Ответственный:</label>
                <select id="responsible-select" name="responsible-select">
                    <option value="">Выберите ответственного</option>
                </select>
            </div>
            
            <div class="form-group">
                <label for="subtask-name">Подзадача:</label>
                <input type="text" id="subtask-name" name="subtask-name" placeholder="Описание подзадачи...">
            </div>
            
            <div class="form-group">
                <label for="comment">Комментарий:</label>
                <textarea id="comment" name="comment" placeholder="Добавьте комментарий..."></textarea>
            </div>
            
            <div class="form-group">
                <label for="task-type">Тип задачи:</label>
                <select id="task-type" name="task-type">
                    <option value="проект">🚀 Проект</option>
                    <option value="рутина">🔄 Рутина</option>
                    <option value="созвон">📞 Созвон</option>
                    <option value="отпуск">🏖️ Отпуск</option>
                    <option value="больничный">🏥 Больничный</option>
                </select>
            </div>
            
            <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 20px;">
                <div class="form-group">
                    <label for="start-time">Время начала:</label>
                    <input type="datetime-local" id="start-time" name="start-time">
                </div>
                <div class="form-group">
                    <label for="end-time">Время окончания:</label>
                    <input type="datetime-local" id="end-time" name="end-time">
                </div>
            </div>
            
            <button class="btn" onclick="addTask()">
                <span>💾</span> Сохранить задачу
            </button>
        </div>

        <!-- Вкладка "Список задач" (только для админа) -->
        <div id="task-list" class="tab-content" style="display: none;">
            <h2>Список задач</h2>
            
            <!-- Фильтры для списка задач -->
            <div class="filters" style="margin-bottom: 25px;">
                <div class="filter-group">
                    <label for="list-task-theme-filter">Тема задачи:</label>
                    <select id="list-task-theme-filter" onchange="filterTaskList()">
                        <option value="">Все темы</option>
                    </select>
                </div>
                
                <div class="filter-group">
                    <label for="list-responsible-filter">Ответственный:</label>
                    <select id="list-responsible-filter" onchange="filterTaskList()">
                        <option value="">Все сотрудники</option>
                    </select>
                </div>
                
                <div class="filter-group">
                    <label for="list-task-type-filter">Тип задачи:</label>
                    <select id="list-task-type-filter" onchange="filterTaskList()">
                        <option value="">Все типы</option>
                        <option value="проект">🚀 Проект</option>
                        <option value="рутина">🔄 Рутина</option>
                        <option value="созвон">📞 Созвон</option>
                        <option value="отпуск">🏖️ Отпуск</option>
                        <option value="больничный">🏥 Больничный</option>
                    </select>
                </div>
                
                <div class="filter-group">
                    <label for="list-date-filter">Период:</label>
                    <select id="list-date-filter" onchange="filterTaskList()">
                        <option value="">Все время</option>
                        <option value="today">Сегодня</option>
                        <option value="yesterday">Вчера</option>
                        <option value="week">Текущая неделя</option>
                        <option value="month">Текущий месяц</option>
                        <option value="last_month">Прошлый месяц</option>
                    </select>
                </div>
                
                <div class="filter-group">
                    <label for="list-search">Поиск:</label>
                    <input type="text" id="list-search" placeholder="Введите текст..." oninput="filterTaskList()">
                </div>
                
                <div class="filter-group" style="align-self: flex-end;">
                    <button class="btn btn-secondary" onclick="resetTaskListFilters()" style="width: 100%;">
                        <span>🔄</span> Сбросить
                    </button>
                </div>
            </div>
            
            <!-- Счетчик отфильтрованных задач -->
            <div id="task-list-counter" style="margin-bottom: 15px; padding: 10px 15px; background: var(--light-color); border-radius: var(--border-radius); display: flex; justify-content: space-between; align-items: center;">
                <div>
                    <strong>Всего задач:</strong> <span id="total-tasks-count">0</span>
                    <span style="margin-left: 15px;">
                        <strong>Отфильтровано:</strong> <span id="filtered-tasks-count">0</span>
                    </span>
                </div>
                <div style="display: flex; gap: 10px; align-items: center;">
                    <label for="list-sort">Сортировка:</label>
                    <select id="list-sort" onchange="filterTaskList()" style="width: auto;">
                        <option value="newest">Сначала новые</option>
                        <option value="oldest">Сначала старые</option>
                        <option value="hours_desc">Больше часов</option>
                        <option value="hours_asc">Меньше часов</option>
                        <option value="name">По теме (А-Я)</option>
                    </select>
                </div>
            </div>
            
            <div class="table-container">
                <table id="task-table">
                    <thead>
                        <tr>
                            <th>Тема</th>
                            <th>Подзадача</th>
                            <th>Тип</th>
                            <th>Время</th>
                            <th>Затрачено</th>
                            <th>Ответственный</th>
                            <th>Действия</th>
                        </tr>
                    </thead>
                    <tbody>
                        <!-- Задачи будут добавляться динамически -->
                    </tbody>
                </table>
            </div>
            
            <!-- Если задач нет -->
            <div id="no-tasks-message" style="display: none; text-align: center; padding: 40px; color: var(--gray-color); background: var(--light-color); border-radius: var(--border-radius); margin-top: 20px;">
                <div style="font-size: 3rem; margin-bottom: 20px;">📋</div>
                <h3>Нет задач по выбранным фильтрам</h3>
                <p>Попробуйте изменить параметры фильтрации</p>
                <button class="btn" onclick="resetTaskListFilters()" style="margin-top: 15px;">
                    <span>🔄</span> Сбросить фильтры
                </button>
            </div>
        </div>

        <!-- Вкладка "Дэшборд" (только для админа) -->
        <div id="dashboard" class="tab-content" style="display: none;">
            <h2>Дэшборд по отработанным часам</h2>
            
            <div class="filters">
                <div class="filter-group">
                    <label for="responsible-filter">Ответственный:</label>
                    <select id="responsible-filter" onchange="updateDashboard()">
                        <option value="">Все сотрудники</option>
                    </select>
                </div>
                
                <div class="filter-group">
                    <label for="task-type-filter">Тип задачи:</label>
                    <select id="task-type-filter" onchange="updateDashboard()">
                        <option value="">Все типы</option>
                        <option value="проект">🚀 Проект</option>
                        <option value="рутина">🔄 Рутина</option>
                        <option value="созвон">📞 Созвон</option>
                        <option value="отпуск">🏖️ Отпуск</option>
                        <option value="больничный">🏥 Больничный</option>
                    </select>
                </div>
                
                <div class="filter-group">
                    <label for="period-filter">Период:</label>
                    <select id="period-filter" onchange="updateDashboard()">
                        <option value="current_month">Текущий месяц</option>
                        <option value="last_month">Прошлый месяц</option>
                        <option value="current_week">Текущая неделя</option>
                        <option value="all_time">За все время</option>
                    </select>
                </div>
            </div>

            <!-- Переключение вида -->
            <div class="view-toggle">
                <button class="view-toggle-btn active" onclick="setViewMode('calendar')">
                    📅 Календарь
                </button>
                <button class="view-toggle-btn" onclick="setViewMode('list')">
                    📋 Список по дням
                </button>
            </div>

            <!-- Итоговая статистика -->
            <div class="total-stats" id="total-stats">
                <!-- Итоги будут обновляться динамически -->
            </div>

            <!-- Календарь -->
            <div id="calendar-view" class="calendar-container">
                <div id="filter-indicator" style="margin-bottom: 15px; font-size: 14px; color: var(--gray-color);"></div>
                <div class="calendar" id="calendar"></div>
                
                <!-- Детали выбранного дня -->
                <div id="day-details" class="day-details">
                    <!-- Детали будут заполняться динамически -->
                </div>
            </div>

            <!-- Список по дням -->
            <div id="list-view" class="table-container" style="display: none;">
                <table id="days-table">
                    <thead>
                        <tr>
                            <th>Дата</th>
                            <th>Кол-во задач</th>
                            <th>Всего часов</th>
                            <th>Типы задач</th>
                            <th>Действия</th>
                        </tr>
                    </thead>
                    <tbody>
                        <!-- Дни будут добавляться динамически -->
                    </tbody>
                </table>
            </div>

            <div class="stats-grid" id="task-stats">
                <!-- Статистика по типам задач будет здесь -->
            </div>
        </div>
    </div>

    <!-- Модальное окно для детального просмотра дня -->
    <div id="day-modal" class="modal">
        <div class="modal-content">
            <div class="modal-header">
                <h3 id="modal-day-title">Детали дня</h3>
                <button class="modal-close" onclick="closeDayModal()">×</button>
            </div>
            <div id="modal-day-content">
                <!-- Контент будет заполняться динамически -->
            </div>
        </div>
    </div>

    <!-- Модальное окно для редактирования сотрудника -->
    <div id="edit-employee-modal" class="modal">
        <div class="modal-content">
            <div class="modal-header">
                <h3>Редактировать сотрудника</h3>
                <button class="modal-close" onclick="closeEditEmployeeModal()">×</button>
            </div>
            <div id="edit-employee-form">
                <!-- Форма будет заполняться динамически -->
            </div>
        </div>
    </div>

    <!-- Уведомление -->
    <div id="notification" class="notification"></div>

    <script>
        // Данные
        let taskThemes = ['Разработка', 'Тестирование', 'Документация', 'Встречи', 'Обучение'];
        let taskList = [];
        let selectedDate = null;
        let viewMode = 'calendar';
        let currentUser = null;
        let employees = [];

        // Изначальные пользователи
        const INITIAL_USERS = {
            'admin': {
                password: 'admin123',
                name: 'Администратор системы',
                role: 'admin',
                fio: 'Администратор системы'
            },
            'ivanov': {
                password: 'ivanov123',
                name: 'Иванов Иван Иванович',
                role: 'employee',
                fio: 'Иванов Иван Иванович'
            },
            'petrov': {
                password: 'petrov123',
                name: 'Петров Петр Петрович',
                role: 'employee',
                fio: 'Петров Петр Петрович'
            }
        };

        // Инициализация
        document.addEventListener('DOMContentLoaded', function() {
            checkSavedSession();
            loadData();
            
            // Инициализируем начальные данные, если их нет
            if (!localStorage.getItem('taskDashboard_tasks')) {
                // Создаем несколько тестовых задач
                const now = new Date();
                const yesterday = new Date(now);
                yesterday.setDate(yesterday.getDate() - 1);
                
                taskList = [
                    {
                        taskName: 'Разработка',
                        responsible: 'Иванов Иван Иванович',
                        subtaskName: 'Создание интерфейса',
                        comment: 'Работа над UI компонентами',
                        taskType: 'проект',
                        startTime: yesterday.toLocaleString('ru-RU'),
                        endTime: new Date(yesterday.getTime() + 4 * 60 * 60 * 1000).toLocaleString('ru-RU'),
                        timeSpent: 240,
                        hoursSpent: '4.00',
                        date: yesterday.toISOString().split('T')[0],
                        month: yesterday.getMonth(),
                        year: yesterday.getFullYear(),
                        week: getWeekNumber(yesterday),
                        timestamp: yesterday.getTime()
                    },
                    {
                        taskName: 'Тестирование',
                        responsible: 'Петров Петр Петрович',
                        subtaskName: 'Проверка функционала',
                        comment: 'Тестирование новых фич',
                        taskType: 'рутина',
                        startTime: now.toLocaleString('ru-RU'),
                        endTime: new Date(now.getTime() + 2 * 60 * 60 * 1000).toLocaleString('ru-RU'),
                        timeSpent: 120,
                        hoursSpent: '2.00',
                        date: now.toISOString().split('T')[0],
                        month: now.getMonth(),
                        year: now.getFullYear(),
                        week: getWeekNumber(now),
                        timestamp: now.getTime()
                    }
                ];
                
                saveData();
            }
        });

        // Функции для работы с авторизацией
        function checkSavedSession() {
            const savedSession = localStorage.getItem('taskDashboard_session');
            if (savedSession) {
                try {
                    const session = JSON.parse(savedSession);
                    if (session.username && session.role && session.name) {
                        if (session.expires && new Date(session.expires) > new Date()) {
                            currentUser = session;
                            showMainInterface();
                            return;
                        }
                    }
                } catch (e) {
                    console.error('Ошибка восстановления сессии:', e);
                }
            }
            showLoginModal();
        }

        function showLoginModal() {
            document.getElementById('loginModal').style.display = 'flex';
            document.getElementById('mainContainer').style.display = 'none';
            document.getElementById('currentUserIndicator').style.display = 'none';
        }

        function showMainInterface() {
            document.getElementById('loginModal').style.display = 'none';
            document.getElementById('mainContainer').style.display = 'block';
            document.getElementById('currentUserIndicator').style.display = 'flex';
            
            updateUserInfo();
            updateInterfaceForRole();
        }

        function togglePassword() {
            const passwordInput = document.getElementById('login-password');
            const toggleBtn = document.querySelector('.toggle-password');
            
            if (passwordInput.type === 'password') {
                passwordInput.type = 'text';
                toggleBtn.textContent = '🙈';
            } else {
                passwordInput.type = 'password';
                toggleBtn.textContent = '👁️';
            }
        }

        function login() {
            const username = document.getElementById('login-username').value.trim();
            const password = document.getElementById('login-password').value;
            const rememberMe = document.getElementById('remember-me').checked;
            const errorElement = document.getElementById('login-error');
            
            errorElement.classList.remove('show');
            
            if (!username || !password) {
                errorElement.textContent = 'Введите логин и пароль';
                errorElement.classList.add('show');
                return;
            }
            
            // Проверяем вначале инициальных пользователей
            if (INITIAL_USERS[username]) {
                if (INITIAL_USERS[username].password !== password) {
                    errorElement.textContent = 'Неверный пароль';
                    errorElement.classList.add('show');
                    return;
                }
                
                currentUser = {
                    username: username,
                    name: INITIAL_USERS[username].name,
                    fio: INITIAL_USERS[username].fio,
                    role: INITIAL_USERS[username].role
                };
            } else {
                // Проверяем в добавленных сотрудниках
                const employee = employees.find(emp => emp.login === username);
                if (!employee) {
                    errorElement.textContent = 'Пользователь не найден';
                    errorElement.classList.add('show');
                    return;
                }
                
                if (employee.password !== password) {
                    errorElement.textContent = 'Неверный пароль';
                    errorElement.classList.add('show');
                    return;
                }
                
                currentUser = {
                    username: employee.login,
                    name: employee.fio,
                    fio: employee.fio,
                    role: employee.role
                };
            }
            
            if (rememberMe) {
                const session = {
                    ...currentUser,
                    expires: new Date(Date.now() + 30 * 24 * 60 * 60 * 1000)
                };
                localStorage.setItem('taskDashboard_session', JSON.stringify(session));
            }
            
            showMainInterface();
            showNotification(`Добро пожаловать, ${currentUser.fio}!`);
        }

        function logout() {
            if (confirm('Вы уверены, что хотите выйти из системы?')) {
                localStorage.removeItem('taskDashboard_session');
                currentUser = null;
                showLoginModal();
                showNotification('Вы вышли из системы');
            }
        }

        function updateUserInfo() {
            if (!currentUser) return;
            
            const userNameElement = document.getElementById('currentUserName');
            const userRoleElement = document.getElementById('currentUserRole');
            
            userNameElement.textContent = currentUser.fio;
            
            let roleText = '';
            let roleColor = '';
            
            switch(currentUser.role) {
                case 'admin':
                    roleText = 'Администратор';
                    roleColor = '#6C63FF';
                    break;
                case 'employee':
                    roleText = 'Сотрудник';
                    roleColor = '#12C1D9';
                    break;
            }
            
            userRoleElement.textContent = roleText;
            userRoleElement.style.backgroundColor = roleColor;
        }

        function updateInterfaceForRole() {
            const adminTabs = document.getElementById('adminTabs');
            const employeeView = document.getElementById('employeeView');
            const tabContents = document.querySelectorAll('.tab-content');
            
            // Скрываем все
            adminTabs.style.display = 'none';
            employeeView.style.display = 'none';
            tabContents.forEach(tab => {
                tab.style.display = 'none';
            });
            
            if (currentUser.role === 'admin') {
                // Администратор видит все вкладки
                adminTabs.style.display = 'flex';
                showTab('task-themes');
                updateTaskTable(); // ОБНОВЛЯЕМ ТАБЛИЦУ ЗАДАЧ
            } else if (currentUser.role === 'employee') {
                // Сотрудник видит только форму добавления задач
                employeeView.style.display = 'block';
                updateEmployeeInterface();
            }
        }

        // Сохранение данных
        function saveData() {
            try {
                localStorage.setItem('taskDashboard_themes', JSON.stringify(taskThemes));
                localStorage.setItem('taskDashboard_tasks', JSON.stringify(taskList));
                localStorage.setItem('taskDashboard_employees', JSON.stringify(employees));
            } catch (e) {
                console.error('Ошибка сохранения данных:', e);
            }
        }

        // Загрузка данных
        function loadData() {
            try {
                const savedThemes = localStorage.getItem('taskDashboard_themes');
                const savedTasks = localStorage.getItem('taskDashboard_tasks');
                const savedEmployees = localStorage.getItem('taskDashboard_employees');
                
                if (savedThemes) taskThemes = JSON.parse(savedThemes);
                if (savedTasks) taskList = JSON.parse(savedTasks);
                if (savedEmployees) employees = JSON.parse(savedEmployees);
            } catch (e) {
                console.error('Ошибка загрузки данных:', e);
            }
        }

        // Функции для администратора
        function showTab(tabId) {
            if (currentUser.role !== 'admin') {
                showNotification('Доступ запрещен', 'error');
                return;
            }
            
            document.querySelectorAll('.tab-content').forEach(tab => {
                tab.style.display = 'none';
            });
            
            document.getElementById(tabId).style.display = 'block';
            
            document.querySelectorAll('.tab-button').forEach(button => {
                button.classList.remove('active');
            });
            
            const tabButtons = document.querySelectorAll('.tab-button');
            tabButtons.forEach(button => {
                if (button.textContent.includes(tabId === 'task-themes' ? 'Темы задач' :
                                               tabId === 'employees-section' ? 'Сотрудники' :
                                               tabId === 'add-task' ? 'Добавить задачу' :
                                               tabId === 'task-list' ? 'Список задач' : 'Дэшборд')) {
                    button.classList.add('active');
                }
            });
            
            if (tabId === 'dashboard') {
                updateDashboard();
            } else if (tabId === 'employees-section') {
                updateEmployeesList();
            } else if (tabId === 'task-list') {
                updateTaskTable(); // ОБНОВЛЯЕМ ТАБЛИЦУ ПРИ ПЕРЕКЛЮЧЕНИИ НА ВКЛАДКУ
            }
        }

        // Управление сотрудниками
        function addEmployee() {
            if (currentUser.role !== 'admin') {
                showNotification('Недостаточно прав', 'error');
                return;
            }
            
            const fio = document.getElementById('new-employee-fio').value.trim();
            const login = document.getElementById('new-employee-login').value.trim();
            const password = document.getElementById('new-employee-password').value;
            const role = document.getElementById('new-employee-role').value;
            
            if (!fio || !login || !password) {
                showNotification('Заполните все поля!', 'error');
                return;
            }
            
            // Проверяем уникальность логина
            if (INITIAL_USERS[login]) {
                showNotification('Такой логин уже существует!', 'error');
                return;
            }
            
            if (employees.some(emp => emp.login === login)) {
                showNotification('Такой логин уже существует!', 'error');
                return;
            }
            
            const newEmployee = {
                id: Date.now(),
                fio: fio,
                login: login,
                password: password,
                role: role,
                created: new Date().toISOString()
            };
            
            employees.push(newEmployee);
            saveData();
            
            // Очищаем форму
            document.getElementById('new-employee-fio').value = '';
            document.getElementById('new-employee-login').value = '';
            document.getElementById('new-employee-password').value = '';
            
            updateEmployeesList();
            updateResponsibleSelect();
            updateResponsibleFilter();
            updateTaskListFilters();
            
            showNotification('Сотрудник успешно добавлен!');
        }

        function updateEmployeesList() {
            const container = document.getElementById('employees-list');
            container.innerHTML = '';
            
            // Создаем массив всех пользователей (инициальные + добавленные)
            const allUsers = [...employees];
            
            // Добавляем инициальных пользователей (кроме текущего админа)
            Object.keys(INITIAL_USERS).forEach(key => {
                if (key !== 'admin') { // Не показываем системного админа в списке
                    const user = INITIAL_USERS[key];
                    allUsers.push({
                        id: key,
                        fio: user.fio,
                        login: key,
                        password: user.password,
                        role: user.role,
                        isInitial: true
                    });
                }
            });
            
            if (allUsers.length === 0) {
                container.innerHTML = '<p style="color: var(--gray-color); text-align: center;">Нет добавленных сотрудников</p>';
                return;
            }
            
            allUsers.sort((a, b) => a.fio.localeCompare(b.fio));
            
            allUsers.forEach(employee => {
                const employeeCard = document.createElement('div');
                employeeCard.className = 'employee-card';
                
                const roleText = employee.role === 'admin' ? 'Администратор' : 'Сотрудник';
                const roleColor = employee.role === 'admin' ? '#6C63FF' : '#12C1D9';
                
                employeeCard.innerHTML = `
                    <div class="employee-info">
                        <div class="employee-details">
                            <div class="employee-name">${employee.fio}</div>
                            <div class="employee-login">Логин: <strong>${employee.login}</strong></div>
                            <div style="margin-top: 5px;">
                                <span style="background: ${roleColor}; color: white; padding: 2px 8px; border-radius: 12px; font-size: 0.8rem;">
                                    ${roleText}
                                </span>
                                ${employee.isInitial ? '<span style="margin-left: 10px; color: var(--gray-color); font-size: 0.8rem;">(Системный)</span>' : ''}
                            </div>
                        </div>
                        <div class="employee-actions">
                            ${!employee.isInitial ? `
                                <button class="btn btn-small" onclick="editEmployee(${employee.id})">
                                    ✏️ Редактировать
                                </button>
                                <button class="btn btn-small" onclick="deleteEmployee(${employee.id})" style="background: #FF6B6B;">
                                    🗑️ Удалить
                                </button>
                            ` : ''}
                        </div>
                    </div>
                `;
                
                container.appendChild(employeeCard);
            });
        }

        function editEmployee(employeeId) {
            const employee = employees.find(emp => emp.id === employeeId);
            if (!employee) return;
            
            const modal = document.getElementById('edit-employee-modal');
            const form = document.getElementById('edit-employee-form');
            
            form.innerHTML = `
                <div class="form-group">
                    <label for="edit-employee-fio">ФИО сотрудника:</label>
                    <input type="text" id="edit-employee-fio" value="${employee.fio}" placeholder="Иванов Иван Иванович">
                </div>
                
                <div class="form-group">
                    <label for="edit-employee-login">Логин:</label>
                    <input type="text" id="edit-employee-login" value="${employee.login}" placeholder="ivanov" readonly>
                    <small style="color: var(--gray-color);">Логин нельзя изменить</small>
                </div>
                
                <div class="form-group">
                    <label for="edit-employee-password">Новый пароль (оставьте пустым, чтобы не менять):</label>
                    <input type="password" id="edit-employee-password" placeholder="Введите новый пароль">
                </div>
                
                <div class="form-group">
                    <label for="edit-employee-role">Роль:</label>
                    <select id="edit-employee-role">
                        <option value="employee" ${employee.role === 'employee' ? 'selected' : ''}>Сотрудник</option>
                        <option value="admin" ${employee.role === 'admin' ? 'selected' : ''}>Администратор</option>
                    </select>
                </div>
                
                <div style="display: flex; gap: 10px; margin-top: 20px;">
                    <button class="btn" onclick="saveEmployeeChanges(${employeeId})" style="flex: 1;">
                        💾 Сохранить изменения
                    </button>
                    <button class="btn btn-secondary" onclick="closeEditEmployeeModal()" style="flex: 1;">
                        ❌ Отмена
                    </button>
                </div>
            `;
            
            modal.classList.add('active');
        }

        function saveEmployeeChanges(employeeId) {
            const employeeIndex = employees.findIndex(emp => emp.id === employeeId);
            if (employeeIndex === -1) return;
            
            const fio = document.getElementById('edit-employee-fio').value.trim();
            const password = document.getElementById('edit-employee-password').value;
            const role = document.getElementById('edit-employee-role').value;
            
            if (!fio) {
                showNotification('Введите ФИО сотрудника!', 'error');
                return;
            }
            
            employees[employeeIndex].fio = fio;
            employees[employeeIndex].role = role;
            
            if (password) {
                employees[employeeIndex].password = password;
            }
            
            saveData();
            updateEmployeesList();
            updateResponsibleSelect();
            updateResponsibleFilter();
            updateTaskListFilters();
            
            closeEditEmployeeModal();
            showNotification('Изменения сохранены!');
        }

        function deleteEmployee(employeeId) {
            if (!confirm('Вы уверены, что хотите удалить этого сотрудника?')) return;
            
            const employeeIndex = employees.findIndex(emp => emp.id === employeeId);
            if (employeeIndex === -1) return;
            
            employees.splice(employeeIndex, 1);
            saveData();
            updateEmployeesList();
            updateResponsibleSelect();
            updateResponsibleFilter();
            updateTaskListFilters();
            
            showNotification('Сотрудник удален');
        }

        function closeEditEmployeeModal() {
            document.getElementById('edit-employee-modal').classList.remove('active');
        }

        // Обновленные функции для работы с ответственными
        function updateResponsibleSelect() {
            const select = document.getElementById('responsible-select');
            select.innerHTML = '<option value="">Выберите ответственного</option>';
            
            // Добавляем инициальных пользователей (кроме админа)
            Object.keys(INITIAL_USERS).forEach(key => {
                if (key !== 'admin') {
                    const user = INITIAL_USERS[key];
                    const option = document.createElement('option');
                    option.value = user.fio;
                    option.textContent = user.fio;
                    select.appendChild(option);
                }
            });
            
            // Добавляем сотрудников из базы
            employees.forEach(employee => {
                const option = document.createElement('option');
                option.value = employee.fio;
                option.textContent = employee.fio;
                select.appendChild(option);
            });
        }

        function updateResponsibleFilter() {
            const select = document.getElementById('responsible-filter');
            const currentValue = select.value;
            select.innerHTML = '<option value="">Все сотрудники</option>';
            
            // Добавляем инициальных пользователей (кроме админа)
            Object.keys(INITIAL_USERS).forEach(key => {
                if (key !== 'admin') {
                    const user = INITIAL_USERS[key];
                    const option = document.createElement('option');
                    option.value = user.fio;
                    option.textContent = user.fio;
                    select.appendChild(option);
                }
            });
            
            // Добавляем сотрудников из базы
            employees.forEach(employee => {
                const option = document.createElement('option');
                option.value = employee.fio;
                option.textContent = employee.fio;
                select.appendChild(option);
            });
            
            select.value = currentValue;
        }

        // Упрощенный интерфейс для сотрудника
        function updateEmployeeInterface() {
            const themeSelect = document.getElementById('employee-task-name');
            themeSelect.innerHTML = '<option value="">Выберите тему</option>';
            
            taskThemes.forEach(theme => {
                const option = document.createElement('option');
                option.value = theme;
                option.textContent = theme;
                themeSelect.appendChild(option);
            });
            
            updateEmployeeTasksList();
        }

        function updateEmployeeTasksList() {
            const container = document.getElementById('employee-tasks-list');
            container.innerHTML = '';
            
            const employeeTasks = taskList
                .filter(task => task.responsible === currentUser.fio)
                .sort((a, b) => new Date(b.startTime) - new Date(a.startTime))
                .slice(0, 10);
            
            if (employeeTasks.length === 0) {
                container.innerHTML = '<p style="text-align: center; color: var(--gray-color);">У вас пока нет задач</p>';
                return;
            }
            
            employeeTasks.forEach(task => {
                const taskEl = document.createElement('div');
                taskEl.className = 'day-task-item';
                taskEl.style.marginBottom = '10px';
                
                const badgeClass = getBadgeClass(task.taskType);
                const badgeIcon = getTypeIcon(task.taskType);
                const startDate = new Date(task.startTime);
                const formattedDate = startDate.toLocaleDateString('ru-RU');
                const formattedTime = startDate.toLocaleTimeString('ru-RU', { hour: '2-digit', minute: '2-digit' });
                
                taskEl.innerHTML = `
                    <div style="display: flex; justify-content: space-between; align-items: start;">
                        <div style="flex: 1;">
                            <div style="font-weight: 600; margin-bottom: 5px;">${task.taskName}</div>
                            <div style="font-size: 0.9em; color: var(--gray-color); margin-bottom: 5px;">
                                ${task.subtaskName}
                            </div>
                            <span class="task-type-badge ${badgeClass}" style="font-size: 0.8em;">
                                ${badgeIcon} ${task.taskType}
                            </span>
                        </div>
                        <div style="text-align: right;">
                            <div style="color: var(--primary-color); font-weight: 600; font-size: 1.1em;">
                                ${task.hoursSpent} ч
                            </div>
                            <div style="font-size: 0.8em; color: var(--gray-color);">
                                ${formattedDate}<br>
                                ${formattedTime}
                            </div>
                        </div>
                    </div>
                `;
                
                container.appendChild(taskEl);
            });
        }

        // ФУНКЦИЯ ДОБАВЛЕНИЯ ЗАДАЧИ СОТРУДНИКОМ (ИСПРАВЛЕННАЯ)
        function addEmployeeTask() {
            const taskName = document.getElementById('employee-task-name').value;
            const subtaskName = document.getElementById('employee-subtask-name').value;
            const comment = document.getElementById('employee-comment').value;
            const taskType = document.getElementById('employee-task-type').value;
            const startTime = document.getElementById('employee-start-time').value;
            const endTime = document.getElementById('employee-end-time').value;

            if (!taskName || !startTime || !endTime) {
                showNotification('Заполните все обязательные поля!', 'error');
                return;
            }

            const start = new Date(startTime);
            const end = new Date(endTime);
            
            if (end <= start) {
                showNotification('Время окончания должно быть позже времени начала!', 'error');
                return;
            }

            const timeSpent = Math.round((end - start) / 1000 / 60);

            const task = {
                taskName,
                responsible: currentUser.fio,
                subtaskName: subtaskName || '-',
                comment: comment || '-',
                taskType,
                startTime: start.toLocaleString('ru-RU'),
                endTime: end.toLocaleString('ru-RU'),
                timeSpent,
                hoursSpent: (timeSpent / 60).toFixed(2),
                date: start.toISOString().split('T')[0],
                month: start.getMonth(),
                year: start.getFullYear(),
                week: getWeekNumber(start),
                timestamp: Date.now() // УНИКАЛЬНЫЙ ИДЕНТИФИКАТОР
            };

            taskList.push(task);
            saveData();
            
            document.getElementById('employee-subtask-name').value = '';
            document.getElementById('employee-comment').value = '';
            document.getElementById('employee-start-time').value = '';
            document.getElementById('employee-end-time').value = '';
            
            updateEmployeeTasksList();
            
            showNotification('Задача успешно добавлена!');
        }

        // ФУНКЦИЯ ОБНОВЛЕНИЯ ТАБЛИЦЫ ЗАДАЧ (ИСПРАВЛЕННАЯ)
        function updateTaskTable() {
            if (currentUser.role !== 'admin') return;
            
            const tbody = document.querySelector('#task-table tbody');
            tbody.innerHTML = '';
            
            if (taskList.length === 0) {
                tbody.innerHTML = `
                    <tr>
                        <td colspan="7" style="text-align: center; padding: 40px; color: var(--gray-color);">
                            Нет добавленных задач
                        </td>
                    </tr>
                `;
                
                document.getElementById('task-list-counter').style.display = 'none';
                document.getElementById('no-tasks-message').style.display = 'none';
                
                return;
            }
            
            document.getElementById('task-list-counter').style.display = 'flex';
            
            updateTaskListFilters();
            
            // Сортируем задачи по дате (новые сверху)
            const tasksToShow = [...taskList].sort((a, b) => new Date(b.startTime) - new Date(a.startTime));
            
            tasksToShow.forEach(task => {
                const row = document.createElement('tr');
                
                let typeIcon = '🚀';
                let typeColor = '#6C63FF';
                if (task.taskType === 'рутина') {
                    typeIcon = '🔄';
                    typeColor = '#12C1D9';
                }
                if (task.taskType === 'созвон') {
                    typeIcon = '📞';
                    typeColor = '#2CC93C';
                }
                if (task.taskType === 'отпуск') {
                    typeIcon = '🏖️';
                    typeColor = '#FF9F43';
                }
                if (task.taskType === 'больничный') {
                    typeIcon = '🏥';
                    typeColor = '#FF6B6B';
                }
                
                const startDate = new Date(task.startTime);
                const formattedDate = startDate.toLocaleDateString('ru-RU');
                const formattedTime = startDate.toLocaleTimeString('ru-RU', { hour: '2-digit', minute: '2-digit' });
                const endTime = new Date(task.endTime).toLocaleTimeString('ru-RU', { hour: '2-digit', minute: '2-digit' });
                
                row.innerHTML = `
                    <td><strong>${task.taskName}</strong></td>
                    <td>${task.subtaskName}</td>
                    <td style="color: ${typeColor}; font-weight: 600;">${typeIcon} ${task.taskType}</td>
                    <td>
                        <div style="font-size: 0.9em; color: var(--gray-color);">
                            ${formattedDate}
                        </div>
                        <div style="font-weight: 500;">
                            ${formattedTime} - ${endTime}
                        </div>
                    </td>
                    <td><span style="color: var(--primary-color); font-weight: 600;">${task.hoursSpent} ч</span></td>
                    <td>👤 ${task.responsible}</td>
                    <td>
                        <button onclick="deleteTask('${task.timestamp}')" style="background: none; border: none; color: #FF6B6B; cursor: pointer; font-size: 18px; padding: 5px;" title="Удалить задачу">
                            🗑️
                        </button>
                    </td>
                `;
                tbody.appendChild(row);
            });
            
            // Обновляем счетчики
            document.getElementById('total-tasks-count').textContent = taskList.length;
            document.getElementById('filtered-tasks-count').textContent = taskList.length;
            
            // Скрываем сообщение "нет задач"
            document.getElementById('no-tasks-message').style.display = 'none';
        }

        // Функции для работы с темами задач
        function addTaskTheme() {
            if (currentUser.role !== 'admin') {
                showNotification('Недостаточно прав для добавления тем задач', 'error');
                return;
            }
            
            const input = document.getElementById('new-task-theme');
            const theme = input.value.trim();
            
            if (theme) {
                if (taskThemes.includes(theme)) {
                    showNotification('Такая тема уже существует!', 'error');
                    return;
                }
                
                taskThemes.push(theme);
                updateTaskThemesList();
                updateTaskSelect();
                updateTaskListFilters();
                input.value = '';
                saveData();
                showNotification('Тема успешно добавлена!');
            } else {
                showNotification('Введите название темы!', 'error');
            }
        }

        function removeTaskTheme(index) {
            if (currentUser.role !== 'admin') {
                showNotification('Недостаточно прав для удаления тем задач', 'error');
                return;
            }
            
            taskThemes.splice(index, 1);
            updateTaskThemesList();
            updateTaskSelect();
            updateTaskListFilters();
            saveData();
            showNotification('Тема удалена');
        }

        function updateTaskThemesList() {
            const list = document.getElementById('task-themes-list');
            list.innerHTML = '';
            
            if (taskThemes.length === 0) {
                list.innerHTML = '<li style="color: var(--gray-color); text-align: center;">Нет добавленных тем</li>';
                return;
            }
            
            taskThemes.forEach((theme, index) => {
                const li = document.createElement('li');
                li.innerHTML = `
                    ${theme}
                    <button onclick="removeTaskTheme(${index})" style="background: none; border: none; color: #FF6B6B; cursor: pointer; font-size: 18px;">
                        ×
                    </button>
                `;
                list.appendChild(li);
            });
        }

        function updateTaskSelect() {
            const select = document.getElementById('task-name');
            select.innerHTML = '<option value="">Выберите тему</option>';
            
            taskThemes.forEach(theme => {
                const option = document.createElement('option');
                option.value = theme;
                option.textContent = theme;
                select.appendChild(option);
            });
        }

        function updateTaskListFilters() {
            const themeFilter = document.getElementById('list-task-theme-filter');
            const currentTheme = themeFilter.value;
            themeFilter.innerHTML = '<option value="">Все темы</option>';
            
            taskThemes.forEach(theme => {
                const option = document.createElement('option');
                option.value = theme;
                option.textContent = theme;
                themeFilter.appendChild(option);
            });
            
            themeFilter.value = currentTheme || '';
            
            const responsibleFilter = document.getElementById('list-responsible-filter');
            const currentResponsible = responsibleFilter.value;
            responsibleFilter.innerHTML = '<option value="">Все сотрудники</option>';
            
            // Добавляем инициальных пользователей
            Object.keys(INITIAL_USERS).forEach(key => {
                if (key !== 'admin') {
                    const user = INITIAL_USERS[key];
                    const option = document.createElement('option');
                    option.value = user.fio;
                    option.textContent = user.fio;
                    responsibleFilter.appendChild(option);
                }
            });
            
            // Добавляем сотрудников из базы
            employees.forEach(employee => {
                const option = document.createElement('option');
                option.value = employee.fio;
                option.textContent = employee.fio;
                responsibleFilter.appendChild(option);
            });
            
            responsibleFilter.value = currentResponsible || '';
        }

        // Функция добавления задачи администратором
        function addTask() {
            if (currentUser.role !== 'admin') {
                showNotification('Недостаточно прав', 'error');
                return;
            }
            
            const taskName = document.getElementById('task-name').value;
            const responsible = document.getElementById('responsible-select').value;
            const subtaskName = document.getElementById('subtask-name').value;
            const comment = document.getElementById('comment').value;
            const taskType = document.getElementById('task-type').value;
            const startTime = document.getElementById('start-time').value;
            const endTime = document.getElementById('end-time').value;

            if (!taskName || !responsible || !startTime || !endTime) {
                showNotification('Заполните все обязательные поля!', 'error');
                return;
            }

            const start = new Date(startTime);
            const end = new Date(endTime);
            
            if (end <= start) {
                showNotification('Время окончания должно быть позже времени начала!', 'error');
                return;
            }

            const timeSpent = Math.round((end - start) / 1000 / 60);

            const task = {
                taskName,
                responsible,
                subtaskName: subtaskName || '-',
                comment: comment || '-',
                taskType,
                startTime: start.toLocaleString('ru-RU'),
                endTime: end.toLocaleString('ru-RU'),
                timeSpent,
                hoursSpent: (timeSpent / 60).toFixed(2),
                date: start.toISOString().split('T')[0],
                month: start.getMonth(),
                year: start.getFullYear(),
                week: getWeekNumber(start),
                timestamp: Date.now()
            };

            taskList.push(task);
            updateTaskTable();
            updateDashboard();
            saveData();
            
            document.getElementById('subtask-name').value = '';
            document.getElementById('comment').value = '';
            document.getElementById('start-time').value = '';
            document.getElementById('end-time').value = '';
            
            showNotification('Задача успешно добавлена!');
        }

        // Функция удаления задачи
        function deleteTask(timestamp) {
            if (currentUser.role !== 'admin') {
                showNotification('Недостаточно прав для удаления задач', 'error');
                return;
            }
            
            if (confirm('Вы уверены, что хотите удалить эту задачу?')) {
                const index = taskList.findIndex(task => task.timestamp == timestamp);
                if (index !== -1) {
                    taskList.splice(index, 1);
                    updateTaskTable();
                    updateDashboard();
                    saveData();
                    showNotification('Задача удалена');
                }
            }
        }

        // Функции фильтрации списка задач
        function filterTaskList() {
            const themeFilter = document.getElementById('list-task-theme-filter').value;
            const responsibleFilter = document.getElementById('list-responsible-filter').value;
            const taskTypeFilter = document.getElementById('list-task-type-filter').value;
            const dateFilter = document.getElementById('list-date-filter').value;
            const searchFilter = document.getElementById('list-search').value.toLowerCase();
            const sortFilter = document.getElementById('list-sort').value;
            
            const tbody = document.querySelector('#task-table tbody');
            const noTasksMessage = document.getElementById('no-tasks-message');
            const totalTasksCount = document.getElementById('total-tasks-count');
            const filteredTasksCount = document.getElementById('filtered-tasks-count');
            
            const rows = Array.from(tbody.querySelectorAll('tr'));
            let visibleCount = 0;
            
            rows.forEach(row => {
                const taskTheme = row.querySelector('td:nth-child(1) strong')?.textContent || '';
                const subtask = row.querySelector('td:nth-child(2)')?.textContent || '';
                const taskType = row.querySelector('td:nth-child(3)')?.textContent || '';
                const timeInfo = row.querySelector('td:nth-child(4)')?.textContent || '';
                const hoursSpent = parseFloat(row.querySelector('td:nth-child(5) span')?.textContent || 0);
                const responsible = row.querySelector('td:nth-child(6)')?.textContent || '';
                
                let shouldShow = true;
                
                if (themeFilter && taskTheme !== themeFilter) {
                    shouldShow = false;
                }
                
                if (responsibleFilter && !responsible.includes(responsibleFilter)) {
                    shouldShow = false;
                }
                
                if (taskTypeFilter) {
                    const typeText = taskType.toLowerCase();
                    if (!typeText.includes(taskTypeFilter.toLowerCase())) {
                        shouldShow = false;
                    }
                }
                
                if (dateFilter) {
                    const now = new Date();
                    const today = new Date(now.getFullYear(), now.getMonth(), now.getDate());
                    const taskDateText = timeInfo.split('\n')[0].trim();
                    const taskDate = new Date(taskDateText.split('.').reverse().join('-'));
                    
                    switch(dateFilter) {
                        case 'today':
                            if (taskDate.getDate() !== today.getDate() || 
                                taskDate.getMonth() !== today.getMonth() || 
                                taskDate.getFullYear() !== today.getFullYear()) {
                                shouldShow = false;
                            }
                            break;
                        case 'yesterday':
                            const yesterday = new Date(today);
                            yesterday.setDate(yesterday.getDate() - 1);
                            if (taskDate.getDate() !== yesterday.getDate() || 
                                taskDate.getMonth() !== yesterday.getMonth() || 
                                taskDate.getFullYear() !== yesterday.getFullYear()) {
                                shouldShow = false;
                            }
                            break;
                        case 'week':
                            const weekAgo = new Date(today);
                            weekAgo.setDate(weekAgo.getDate() - 7);
                            if (taskDate < weekAgo) {
                                shouldShow = false;
                            }
                            break;
                        case 'month':
                            if (taskDate.getMonth() !== today.getMonth() || 
                                taskDate.getFullYear() !== today.getFullYear()) {
                                shouldShow = false;
                            }
                            break;
                        case 'last_month':
                            const lastMonth = today.getMonth() - 1;
                            const lastMonthYear = lastMonth < 0 ? today.getFullYear() - 1 : today.getFullYear();
                            if (taskDate.getMonth() !== (lastMonth < 0 ? 11 : lastMonth) || 
                                taskDate.getFullYear() !== lastMonthYear) {
                                shouldShow = false;
                            }
                            break;
                    }
                }
                
                if (searchFilter) {
                    const searchText = (taskTheme + subtask + taskType + timeInfo + responsible).toLowerCase();
                    if (!searchText.includes(searchFilter)) {
                        shouldShow = false;
                    }
                }
                
                if (shouldShow) {
                    row.style.display = '';
                    visibleCount++;
                } else {
                    row.style.display = 'none';
                }
            });
            
            totalTasksCount.textContent = rows.length;
            filteredTasksCount.textContent = visibleCount;
            
            if (visibleCount === 0 && rows.length > 0) {
                noTasksMessage.style.display = 'block';
                tbody.style.display = 'none';
            } else {
                noTasksMessage.style.display = 'none';
                tbody.style.display = '';
            }
            
            if (visibleCount > 0) {
                sortTaskListRows(sortFilter);
            }
        }

        function sortTaskListRows(sortType) {
            const tbody = document.querySelector('#task-table tbody');
            const rows = Array.from(tbody.querySelectorAll('tr:not([style*="display: none"])'));
            
            rows.sort((a, b) => {
                const taskThemeA = a.querySelector('td:nth-child(1) strong')?.textContent || '';
                const taskThemeB = b.querySelector('td:nth-child(1) strong')?.textContent || '';
                const hoursA = parseFloat(a.querySelector('td:nth-child(5) span')?.textContent || 0);
                const hoursB = parseFloat(b.querySelector('td:nth-child(5) span')?.textContent || 0);
                const timeA = a.querySelector('td:nth-child(4) div:nth-child(1)')?.textContent || '';
                const timeB = b.querySelector('td:nth-child(4) div:nth-child(1)')?.textContent || '';
                
                switch(sortType) {
                    case 'newest':
                        const dateA = new Date(timeA.split('.').reverse().join('-'));
                        const dateB = new Date(timeB.split('.').reverse().join('-'));
                        return dateB - dateA;
                        
                    case 'oldest':
                        const dateA2 = new Date(timeA.split('.').reverse().join('-'));
                        const dateB2 = new Date(timeB.split('.').reverse().join('-'));
                        return dateA2 - dateB2;
                        
                    case 'hours_desc':
                        return hoursB - hoursA;
                        
                    case 'hours_asc':
                        return hoursA - hoursB;
                        
                    case 'name':
                        return taskThemeA.localeCompare(taskThemeB);
                        
                    default:
                        return 0;
                }
            });
            
            rows.forEach(row => tbody.appendChild(row));
        }

        function resetTaskListFilters() {
            document.getElementById('list-task-theme-filter').value = '';
            document.getElementById('list-responsible-filter').value = '';
            document.getElementById('list-task-type-filter').value = '';
            document.getElementById('list-date-filter').value = '';
            document.getElementById('list-search').value = '';
            document.getElementById('list-sort').value = 'newest';
            
            filterTaskList();
        }

        // Основная функция обновления дэшборда
        function updateDashboard() {
            if (currentUser.role !== 'admin') return;
            
            updateTotalStats();
            updateTaskStats();
            updateFilterIndicator();
            
            if (viewMode === 'calendar') {
                updateCalendar();
            } else {
                updateDaysList();
            }
        }

        function updateFilterIndicator() {
            const responsibleFilter = document.getElementById('responsible-filter').value;
            const taskTypeFilter = document.getElementById('task-type-filter').value;
            const periodFilter = document.getElementById('period-filter').value;
            const indicator = document.getElementById('filter-indicator');
            
            let indicators = [];
            
            if (responsibleFilter) {
                indicators.push(`Ответственный: ${responsibleFilter}`);
            }
            
            if (taskTypeFilter) {
                const typeNames = {
                    'проект': 'Проект',
                    'рутина': 'Рутина',
                    'созвон': 'Созвон',
                    'отпуск': 'Отпуск',
                    'больничный': 'Больничный'
                };
                indicators.push(`Тип: ${typeNames[taskTypeFilter]}`);
            }
            
            const periodNames = {
                'current_month': 'Текущий месяц',
                'last_month': 'Прошлый месяц',
                'current_week': 'Текущая неделя',
                'all_time': 'За все время'
            };
            indicators.push(`Период: ${periodNames[periodFilter]}`);
            
            indicator.innerHTML = `Активные фильтры: ${indicators.join(' • ')}`;
            indicator.style.color = 'var(--primary-color)';
            indicator.style.fontWeight = '600';
        }

        // Функции для календаря
        function updateCalendar() {
            const calendar = document.getElementById('calendar');
            const responsibleFilter = document.getElementById('responsible-filter').value;
            const taskTypeFilter = document.getElementById('task-type-filter').value;
            const periodFilter = document.getElementById('period-filter').value;
            
            calendar.innerHTML = '';
            
            const daysOfWeek = ['Пн', 'Вт', 'Ср', 'Чт', 'Пт', 'Сб', 'Вс'];
            daysOfWeek.forEach(day => {
                const header = document.createElement('div');
                header.className = 'calendar-header';
                header.textContent = day;
                calendar.appendChild(header);
            });
            
            const now = new Date();
            let year, month;
            
            switch(periodFilter) {
                case 'last_month':
                    year = now.getFullYear();
                    month = now.getMonth() - 1;
                    if (month < 0) {
                        month = 11;
                        year--;
                    }
                    break;
                case 'current_week':
                case 'all_time':
                case 'current_month':
                default:
                    year = now.getFullYear();
                    month = now.getMonth();
            }
            
            const firstDay = new Date(year, month, 1);
            const lastDay = new Date(year, month + 1, 0);
            
            const firstDayOfWeek = firstDay.getDay() === 0 ? 6 : firstDay.getDay() - 1;
            for (let i = 0; i < firstDayOfWeek; i++) {
                const empty = document.createElement('div');
                empty.className = 'calendar-day';
                empty.style.opacity = '0.3';
                calendar.appendChild(empty);
            }
            
            for (let day = 1; day <= lastDay.getDate(); day++) {
                const dateStr = `${year}-${String(month + 1).padStart(2, '0')}-${String(day).padStart(2, '0')}`;
                const dayCell = document.createElement('div');
                dayCell.className = 'calendar-day';
                dayCell.dataset.date = dateStr;
                
                if (selectedDate === dateStr) {
                    dayCell.classList.add('selected');
                }
                
                const dayTasks = getFilteredTasksForDate(dateStr, responsibleFilter, taskTypeFilter, periodFilter, now);
                
                let totalHours = dayTasks.reduce((sum, task) => sum + parseFloat(task.hoursSpent), 0);
                
                const taskTypes = {};
                dayTasks.forEach(task => {
                    taskTypes[task.taskType] = true;
                });
                
                let indicatorsHTML = '';
                Object.keys(taskTypes).forEach(type => {
                    indicatorsHTML += `<div class="task-type-indicator ${type}"></div>`;
                });
                
                dayCell.innerHTML = `
                    <span>${day}</span>
                    ${indicatorsHTML}
                    <div class="hours">
                        ${totalHours > 0 ? `${totalHours.toFixed(1)} ч` : '0 ч'}
                        ${dayTasks.length > 0 ? `<br><small>${dayTasks.length} задач</small>` : ''}
                    </div>
                    ${totalHours > 0 ? `<div class="hours-indicator" style="width: ${Math.min(totalHours * 10, 100)}%"></div>` : ''}
                `;
                
                dayCell.onclick = function() {
                    selectDate(dateStr);
                    showDayDetails(dateStr);
                };
                
                const currentDate = new Date();
                if (day === currentDate.getDate() && month === currentDate.getMonth() && year === currentDate.getFullYear()) {
                    dayCell.style.borderColor = 'var(--secondary-color)';
                    dayCell.style.boxShadow = '0 2px 8px rgba(44, 201, 60, 0.2)';
                }
                
                if (dayTasks.length > 0) {
                    dayCell.style.background = 'linear-gradient(135deg, #ffffff 0%, #f8fdff 100%)';
                    dayCell.style.borderColor = 'var(--primary-color)';
                }
                
                calendar.appendChild(dayCell);
            }
        }

        function getFilteredTasksForDate(dateStr, responsibleFilter, taskTypeFilter, periodFilter, now) {
            return taskList.filter(task => {
                if (task.date !== dateStr) return false;
                
                if (responsibleFilter && task.responsible !== responsibleFilter) return false;
                
                if (taskTypeFilter && task.taskType !== taskTypeFilter) return false;
                
                switch(periodFilter) {
                    case 'current_month':
                        return task.month === now.getMonth() && task.year === now.getFullYear();
                    case 'last_month':
                        const lastMonth = now.getMonth() - 1;
                        const lastYear = lastMonth < 0 ? now.getFullYear() - 1 : now.getFullYear();
                        return task.month === (lastMonth < 0 ? 11 : lastMonth) && task.year === lastYear;
                    case 'current_week':
                        return task.week === getWeekNumber(now) && task.year === now.getFullYear();
                    case 'all_time':
                        return true;
                    default:
                        return true;
                }
            });
        }

        function selectDate(dateStr) {
            selectedDate = dateStr;
            
            document.querySelectorAll('.calendar-day').forEach(day => {
                day.classList.remove('selected');
            });
            
            const selectedDay = document.querySelector(`.calendar-day[data-date="${dateStr}"]`);
            if (selectedDay) {
                selectedDay.classList.add('selected');
            }
        }

        function showDayDetails(dateStr) {
            const dayDetails = document.getElementById('day-details');
            const responsibleFilter = document.getElementById('responsible-filter').value;
            const taskTypeFilter = document.getElementById('task-type-filter').value;
            const periodFilter = document.getElementById('period-filter').value;
            const now = new Date();
            
            const dayTasks = getFilteredTasksForDate(dateStr, responsibleFilter, taskTypeFilter, periodFilter, now);
            
            if (dayTasks.length === 0) {
                dayDetails.innerHTML = `
                    <div class="day-details-header">
                        <h3>${formatDate(dateStr)}</h3>
                        <span style="color: var(--gray-color);">Нет задач на этот день</span>
                    </div>
                `;
            } else {
                const totalHours = dayTasks.reduce((sum, task) => sum + parseFloat(task.hoursSpent), 0);
                const taskTypes = [...new Set(dayTasks.map(task => task.taskType))];
                
                let tasksHTML = '';
                dayTasks.forEach(task => {
                    const badgeClass = getBadgeClass(task.taskType);
                    const badgeIcon = getTypeIcon(task.taskType);
                    
                    tasksHTML += `
                        <div class="day-task-item">
                            <div class="day-task-header">
                                <div>
                                    <strong>${task.taskName}</strong>
                                    <span class="task-type-badge ${badgeClass}">
                                        ${badgeIcon} ${task.taskType}
                                    </span>
                                </div>
                                <div style="color: var(--primary-color); font-weight: 600;">
                                    ${task.hoursSpent} ч
                                </div>
                            </div>
                            <div style="margin-bottom: 8px;">
                                <strong>Подзадача:</strong> ${task.subtaskName}
                            </div>
                            <div style="margin-bottom: 8px;">
                                <strong>Комментарий:</strong> ${task.comment}
                            </div>
                            <div style="display: flex; justify-content: space-between; color: var(--gray-color); font-size: 0.9em;">
                                <span>👤 ${task.responsible}</span>
                                <span>${task.startTime.split(',')[1]} - ${task.endTime.split(',')[1]}</span>
                            </div>
                        </div>
                    `;
                });
                
                dayDetails.innerHTML = `
                    <div class="day-details-header">
                        <h3>${formatDate(dateStr)}</h3>
                        <div>
                            <span style="color: var(--primary-color); font-weight: 600; margin-right: 15px;">
                                ${totalHours.toFixed(1)} ч всего
                            </span>
                            <span style="color: var(--gray-color);">
                                ${dayTasks.length} задач
                            </span>
                        </div>
                    </div>
                    <div class="day-tasks-list">
                        ${tasksHTML}
                    </div>
                `;
            }
            
            dayDetails.classList.add('active');
        }

        // Функция для обновления списка дней
        function updateDaysList() {
            const tableBody = document.querySelector('#days-table tbody');
            const responsibleFilter = document.getElementById('responsible-filter').value;
            const taskTypeFilter = document.getElementById('task-type-filter').value;
            const periodFilter = document.getElementById('period-filter').value;
            const now = new Date();
            
            const dateMap = {};
            
            taskList.forEach(task => {
                if (responsibleFilter && task.responsible !== responsibleFilter) return;
                if (taskTypeFilter && task.taskType !== taskTypeFilter) return;
                
                switch(periodFilter) {
                    case 'current_month':
                        if (!(task.month === now.getMonth() && task.year === now.getFullYear())) return;
                        break;
                    case 'last_month':
                        const lastMonth = now.getMonth() - 1;
                        const lastYear = lastMonth < 0 ? now.getFullYear() - 1 : now.getFullYear();
                        if (!(task.month === (lastMonth < 0 ? 11 : lastMonth) && task.year === lastYear)) return;
                        break;
                    case 'current_week':
                        if (!(task.week === getWeekNumber(now) && task.year === now.getFullYear())) return;
                        break;
                    case 'all_time':
                        break;
                }
                
                if (!dateMap[task.date]) {
                    dateMap[task.date] = {
                        tasks: [],
                        totalHours: 0,
                        types: new Set()
                    };
                }
                
                dateMap[task.date].tasks.push(task);
                dateMap[task.date].totalHours += parseFloat(task.hoursSpent);
                dateMap[task.date].types.add(task.taskType);
            });
            
            tableBody.innerHTML = '';
            
            if (Object.keys(dateMap).length === 0) {
                tableBody.innerHTML = `
                    <tr>
                        <td colspan="5" style="text-align: center; padding: 40px; color: var(--gray-color);">
                            Нет задач по выбранным фильтрам
                        </td>
                    </tr>
                `;
                return;
            }
            
            const sortedDates = Object.keys(dateMap).sort((a, b) => new Date(b) - new Date(a));
            
            sortedDates.forEach(date => {
                const data = dateMap[date];
                const row = document.createElement('tr');
                
                let typesHTML = '';
                data.types.forEach(type => {
                    const badgeClass = getBadgeClass(type);
                    const badgeIcon = getTypeIcon(type);
                    typesHTML += `<span class="task-type-badge ${badgeClass}" style="margin-right: 5px;">${badgeIcon}</span>`;
                });
                
                row.innerHTML = `
                    <td>
                        <strong>${formatDate(date)}</strong>
                        <div style="font-size: 0.9em; color: var(--gray-color);">
                            ${getDayOfWeek(date)}
                        </div>
                    </td>
                    <td>${data.tasks.length}</td>
                    <td><span style="color: var(--primary-color); font-weight: 600;">${data.totalHours.toFixed(1)} ч</span></td>
                    <td>${typesHTML}</td>
                    <td>
                        <button class="btn btn-small" onclick="showDayModal('${date}')">
                            📋 Подробнее
                        </button>
                    </td>
                `;
                
                tableBody.appendChild(row);
            });
        }

        // Показать модальное окно с деталями дня
        function showDayModal(dateStr) {
            const modal = document.getElementById('day-modal');
            const modalTitle = document.getElementById('modal-day-title');
            const modalContent = document.getElementById('modal-day-content');
            
            modalTitle.textContent = `Задачи за ${formatDate(dateStr)}`;
            
            const responsibleFilter = document.getElementById('responsible-filter').value;
            const taskTypeFilter = document.getElementById('task-type-filter').value;
            const periodFilter = document.getElementById('period-filter').value;
            const now = new Date();
            
            const dayTasks = getFilteredTasksForDate(dateStr, responsibleFilter, taskTypeFilter, periodFilter, now);
            
            if (dayTasks.length === 0) {
                modalContent.innerHTML = '<p style="text-align: center; color: var(--gray-color);">Нет задач на этот день</p>';
            } else {
                const totalHours = dayTasks.reduce((sum, task) => sum + parseFloat(task.hoursSpent), 0);
                
                let tasksHTML = '';
                dayTasks.forEach(task => {
                    const badgeClass = getBadgeClass(task.taskType);
                    const badgeIcon = getTypeIcon(task.taskType);
                    
                    tasksHTML += `
                        <div class="day-task-item" style="margin-bottom: 15px;">
                            <div class="day-task-header">
                                <div>
                                    <strong>${task.taskName}</strong>
                                    <span class="task-type-badge ${badgeClass}">
                                        ${badgeIcon} ${task.taskType}
                                    </span>
                                </div>
                                <div style="color: var(--primary-color); font-weight: 600;">
                                    ${task.hoursSpent} ч
                                </div>
                            </div>
                            <div style="margin-bottom: 8px;">
                                <strong>Подзадача:</strong> ${task.subtaskName}
                            </div>
                            <div style="margin-bottom: 8px;">
                                <strong>Комментарий:</strong> ${task.comment}
                            </div>
                            <div style="display: flex; justify-content: space-between; color: var(--gray-color); font-size: 0.9em;">
                                <span>👤 ${task.responsible}</span>
                                <span>${task.startTime.split(',')[1]} - ${task.endTime.split(',')[1]}</span>
                            </div>
                        </div>
                      `;
                });
                
                modalContent.innerHTML = `
                    <div style="margin-bottom: 20px; padding: 15px; background: var(--light-color); border-radius: var(--border-radius);">
                        <div style="display: flex; justify-content: space-between; align-items: center;">
                            <div>
                                <strong>Итого за день:</strong>
                                <div style="font-size: 1.5rem; color: var(--primary-color); font-weight: 600;">
                                    ${totalHours.toFixed(1)} часов
                                </div>
                            </div>
                            <div style="color: var(--gray-color);">
                                ${dayTasks.length} задач
                            </div>
                        </div>
                    </div>
                    <div class="day-tasks-list">
                        ${tasksHTML}
                    </div>
                `;
            }
            
            modal.classList.add('active');
        }

        // Закрыть модальное окно
        function closeDayModal() {
            document.getElementById('day-modal').classList.remove('active');
        }

        // Вспомогательные функции для форматирования
        function formatDate(dateStr) {
            const date = new Date(dateStr);
            return date.toLocaleDateString('ru-RU', {
                day: 'numeric',
                month: 'long',
                year: 'numeric'
            });
        }

        function getDayOfWeek(dateStr) {
            const date = new Date(dateStr);
            const days = ['Воскресенье', 'Понедельник', 'Вторник', 'Среда', 'Четверг', 'Пятница', 'Суббота'];
            return days[date.getDay()];
        }

        // Функция для обновления итоговой статистики
        function updateTotalStats() {
            const totalStats = document.getElementById('total-stats');
            const responsibleFilter = document.getElementById('responsible-filter').value;
            const taskTypeFilter = document.getElementById('task-type-filter').value;
            const periodFilter = document.getElementById('period-filter').value;
            
            const filteredTasks = taskList.filter(task => {
                if (responsibleFilter && task.responsible !== responsibleFilter) return false;
                
                if (taskTypeFilter && task.taskType !== taskTypeFilter) return false;
                
                const now = new Date();
                switch(periodFilter) {
                    case 'current_month':
                        return task.month === now.getMonth() && task.year === now.getFullYear();
                    case 'last_month':
                        const lastMonth = now.getMonth() - 1;
                        const lastYear = lastMonth < 0 ? now.getFullYear() - 1 : now.getFullYear();
                        return task.month === (lastMonth < 0 ? 11 : lastMonth) && task.year === lastYear;
                    case 'current_week':
                        return task.week === getWeekNumber(now) && task.year === now.getFullYear();
                    case 'all_time':
                        return true;
                    default:
                        return true;
                }
            });
            
            const totalHours = filteredTasks.reduce((sum, task) => sum + parseFloat(task.hoursSpent), 0);
            const totalTasks = filteredTasks.length;
            
            const avgTimePerTask = totalTasks > 0 ? (totalHours / totalTasks).toFixed(1) : 0;
            
            let mostProductiveDay = { date: '', hours: 0 };
            const dayStats = {};
            
            filteredTasks.forEach(task => {
                if (!dayStats[task.date]) {
                    dayStats[task.date] = 0;
                }
                dayStats[task.date] += parseFloat(task.hoursSpent);
                
                if (dayStats[task.date] > mostProductiveDay.hours) {
                    mostProductiveDay = { date: task.date, hours: dayStats[task.date] };
                }
            });
            
            const productiveDayStr = mostProductiveDay.date ? 
                new Date(mostProductiveDay.date).toLocaleDateString('ru-RU') : 'нет данных';
            
            totalStats.innerHTML = `
                <div class="total-item">
                    <div class="total-value">${totalTasks}</div>
                    <div class="total-label">Всего задач</div>
                </div>
                <div class="total-item">
                    <div class="total-value">${totalHours.toFixed(1)}</div>
                    <div class="total-label">Всего часов</div>
                </div>
                <div class="total-item">
                    <div class="total-value">${avgTimePerTask}</div>
                    <div class="total-label">Среднее время на задачу (ч)</div>
                </div>
                <div class="total-item">
                    <div class="total-value">${mostProductiveDay.hours.toFixed(1)}</div>
                    <div class="total-label">Лучший день: ${productiveDayStr}</div>
                </div>
            `;
        }

        // Функции для статистики по типам задач
        function updateTaskStats() {
            const statsContainer = document.getElementById('task-stats');
            const responsibleFilter = document.getElementById('responsible-filter').value;
            const taskTypeFilter = document.getElementById('task-type-filter').value;
            const periodFilter = document.getElementById('period-filter').value;
            
            const filteredTasks = taskList.filter(task => {
                if (responsibleFilter && task.responsible !== responsibleFilter) return false;
                
                if (taskTypeFilter && task.taskType !== taskTypeFilter) return false;
                
                const now = new Date();
                switch(periodFilter) {
                    case 'current_month':
                        return task.month === now.getMonth() && task.year === now.getFullYear();
                    case 'last_month':
                        const lastMonth = now.getMonth() - 1;
                        const lastYear = lastMonth < 0 ? now.getFullYear() - 1 : now.getFullYear();
                        return task.month === (lastMonth < 0 ? 11 : lastMonth) && task.year === lastYear;
                    case 'current_week':
                        return task.week === getWeekNumber(now) && task.year === now.getFullYear();
                    case 'all_time':
                        return true;
                    default:
                        return true;
                }
            });
            
            if (filteredTasks.length === 0) {
                statsContainer.innerHTML = `
                    <div class="stat-card">
                        <div class="stat-value" style="color: var(--gray-color);">0</div>
                        <div class="stat-label">Нет данных по выбранным фильтрам</div>
                    </div>
                `;
                return;
            }
            
            const types = {
                'проект': { count: 0, hours: 0, icon: '🚀', color: '#6C63FF' },
                'рутина': { count: 0, hours: 0, icon: '🔄', color: '#12C1D9' },
                'созвон': { count: 0, hours: 0, icon: '📞', color: '#2CC93C' },
                'отпуск': { count: 0, hours: 0, icon: '🏖️', color: '#FF9F43' },
                'больничный': { count: 0, hours: 0, icon: '🏥', color: '#FF6B6B' }
            };
            
            filteredTasks.forEach(task => {
                if (types[task.taskType]) {
                    types[task.taskType].count++;
                    types[task.taskType].hours += parseFloat(task.hoursSpent);
                }
            });
            
            let statsHTML = '';
            
            Object.entries(types).forEach(([type, data]) => {
                if (data.count > 0) {
                    const percentage = ((data.hours / filteredTasks.reduce((sum, t) => sum + parseFloat(t.hoursSpent), 0)) * 100).toFixed(1);
                    
                    statsHTML += `
                        <div class="stat-card">
                            <div class="stat-value" style="color: ${data.color};">${data.count}</div>
                            <div class="stat-label">${data.icon} ${type.charAt(0).toUpperCase() + type.slice(1)}</div>
                            <div style="font-size: 0.9rem; color: ${data.color}; font-weight: 600; margin-top: 5px;">
                                ${data.hours.toFixed(1)} ч (${percentage}%)
                            </div>
                        </div>
                    `;
                }
            });
            
            statsContainer.innerHTML = statsHTML;
        }

        // Установка режима просмотра
        function setViewMode(mode) {
            viewMode = mode;
            
            document.querySelectorAll('.view-toggle-btn').forEach(btn => {
                btn.classList.remove('active');
            });
            event.currentTarget.classList.add('active');
            
            document.getElementById('calendar-view').style.display = mode === 'calendar' ? 'block' : 'none';
            document.getElementById('list-view').style.display = mode === 'list' ? 'block' : 'none';
            
            if (mode === 'calendar') {
                updateCalendar();
            } else {
                updateDaysList();
            }
        }

        // Вспомогательные функции
        function showNotification(message, type = 'success') {
            const notification = document.getElementById('notification');
            notification.textContent = message;
            notification.style.borderLeftColor = type === 'success' ? '#2CC93C' : '#FF6B6B';
            notification.classList.add('show');
            
            setTimeout(() => {
                notification.classList.remove('show');
            }, 3000);
        }

        function getWeekNumber(date) {
            const firstDayOfYear = new Date(date.getFullYear(), 0, 1);
            const pastDaysOfYear = (date - firstDayOfYear) / 86400000;
            return Math.ceil((pastDaysOfYear + firstDayOfYear.getDay() + 1) / 7);
        }

        function getBadgeClass(taskType) {
            switch(taskType) {
                case 'проект': return 'badge-project';
                case 'рутина': return 'badge-routine';
                case 'созвон': return 'badge-meeting';
                case 'отпуск': return 'badge-vacation';
                case 'больничный': return 'badge-sick';
                default: return 'badge-project';
            }
        }

        function getTypeIcon(taskType) {
            switch(taskType) {
                case 'проект': return '🚀';
                case 'рутина': return '🔄';
                case 'созвон': return '📞';
                case 'отпуск': return '🏖️';
                case 'больничный': return '🏥';
                default: return '🚀';
            }
        }
    </script>
</body>
</html>
