<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Expense Tracker Dashboard</title>
    <!-- Google Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <!-- Chart.js -->
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <!-- jsPDF for PDF Export -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf-autotable/3.5.31/jspdf.plugin.autotable.min.js"></script>
    <link rel="stylesheet" href="style.css">
</head>
<body>

    <!-- Login Screen View -->
    <div id="login-screen" class="login-container">
        <div class="login-card">
            <h2>Welcome</h2>
            <form id="login-form" onsubmit="handleLogin(event)" style="display: flex; flex-direction: column; gap: 18px; margin-top: 10px;">
                <input type="password" id="login-password" class="login-input" placeholder="Enter Password (1234)" required>
                <button type="submit" class="btn-login">LOGIN</button>
            </form>
            <div class="login-links">
                <a href="#">Forgot Password ?</a>
                <a href="#">Sign Up</a>
            </div>
            <div class="login-divider">
                <span>OR LOGIN WITH</span>
            </div>
            <div class="social-login">
                <!-- Google Icon -->
                <button class="btn-social google-btn" type="button">
                    <svg width="20" height="20" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path d="M22.56 12.25c0-.78-.07-1.53-.2-2.25H12v4.26h5.92c-.26 1.37-1.04 2.53-2.21 3.31v2.77h3.57c2.08-1.92 3.28-4.74 3.28-8.09z" fill="#4285F4"/><path d="M12 23c2.97 0 5.46-.98 7.28-2.66l-3.57-2.77c-.98.66-2.23 1.06-3.71 1.06-2.86 0-5.29-1.93-6.16-4.53H2.18v2.84C3.99 20.53 7.7 23 12 23z" fill="#34A853"/><path d="M5.84 14.09c-.22-.66-.35-1.36-.35-2.09s.13-1.43.35-2.09V7.07H2.18C1.43 8.55 1 10.22 1 12s.43 3.45 1.18 4.93l2.85-2.22.81-.62z" fill="#FBBC05"/><path d="M12 5.38c1.62 0 3.06.56 4.21 1.64l3.15-3.15C17.45 2.09 14.97 1 12 1 7.7 1 3.99 3.47 2.18 7.07l3.66 2.84c.87-2.6 3.3-4.53 6.16-4.53z" fill="#EA4335"/></svg>
                </button>
                <!-- Facebook Icon -->
                <button class="btn-social fb-btn" type="button">
                    <svg width="22" height="22" viewBox="0 0 24 24" fill="currentColor" xmlns="http://www.w3.org/2000/svg"><path d="M24 12.07C24 5.41 18.63 0 12 0S0 5.4 0 12.07C0 18.1 4.39 23.15 10.13 24v-8.44H7.08v-3.49h3.04V9.41c0-3.02 1.8-4.7 4.54-4.7 1.31 0 2.68.24 2.68.24v2.97h-1.5c-1.5 0-1.96.93-1.96 1.89v2.26h3.32l-.53 3.5h-2.8V24C19.62 23.15 24 18.1 24 12.07z"/></svg>
                </button>
            </div>
        </div>
    </div>

    <!-- Application Wrapper (Hidden initially) -->
    <div id="dashboard-screen" class="dashboard-container" style="display: none;">
        
        <!-- Sidebar Navigation -->
        <aside class="sidebar glass-panel">
            <div class="sidebar-top">
                <div class="profile-section">
                    <div class="avatar"></div>
                    <div class="profile-info">
                        <h2 id="sidebar-user-name">Personal Tracker</h2>
                        <p>Group 4 Project</p>
                    </div>
                </div>
                <nav>
                    <ul id="main-nav">
                        <li class="active" data-view="view-dashboard" data-title="Expense Overview">
                            <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><rect x="3" y="3" width="7" height="9"></rect><rect x="14" y="3" width="7" height="5"></rect><rect x="14" y="12" width="7" height="9"></rect><rect x="3" y="16" width="7" height="5"></rect></svg>
                            Dashboard
                        </li>
                        <li data-view="view-analytics" data-title="Analytics & Reports">
                            <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M21 16V8a2 2 0 0 0-1-1.73l-7-4a2 2 0 0 0-2 0l-7 4A2 2 0 0 0 3 8v8a2 2 0 0 0 1 1.73l7 4a2 2 0 0 0 2 0l7-4A2 2 0 0 0 21 16z"></path><polyline points="3.27 6.96 12 12.01 20.73 6.96"></polyline><line x1="12" y1="22.08" x2="12" y2="12"></line></svg>
                            Analytics
                        </li>
                        <li data-view="view-settings" data-title="Account Settings">
                            <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><circle cx="12" cy="12" r="3"></circle><path d="M19.4 15a1.65 1.65 0 0 0 .33 1.82l.06.06a2 2 0 0 1 0 2.83 2 2 0 0 1-2.83 0l-.06-.06a1.65 1.65 0 0 0-1.82-.33 1.65 1.65 0 0 0-1 1.51V21a2 2 0 0 1-2 2 2 2 0 0 1-2-2v-.09A1.65 1.65 0 0 0 9 19.4a1.65 1.65 0 0 0-1.82.33l-.06.06a2 2 0 0 1-2.83 0 2 2 0 0 1 0-2.83l.06-.06a1.65 1.65 0 0 0 .33-1.82 1.65 1.65 0 0 0-1.51-1H3a2 2 0 0 1-2-2 2 2 0 0 1 2-2h.09A1.65 1.65 0 0 0 4.6 9a1.65 1.65 0 0 0-.33-1.82l-.06-.06a2 2 0 0 1 0-2.83 2 2 0 0 1 2.83 0l.06.06a1.65 1.65 0 0 0 1.82.33H9a1.65 1.65 0 0 0 1-1.51V3a2 2 0 0 1 2-2 2 2 0 0 1 2 2v.09a1.65 1.65 0 0 0 1 1.51 1.65 1.65 0 0 0 1.82-.33l.06-.06a2 2 0 0 1 2.83 0 2 2 0 0 1 0 2.83l-.06.06a1.65 1.65 0 0 0-.33 1.82V9a1.65 1.65 0 0 0 1.51 1H21a2 2 0 0 1 2 2 2 2 0 0 1-2 2h-.09a1.65 1.65 0 0 0-1.51 1z"></path></svg>
                            Settings
                        </li>
                    </ul>
                </nav>
            </div>
            
            <!-- Requirement 7: Log out or exit -->
            <button class="btn-logout" id="btnLogout" onclick="logoutAndReset()">
                <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M9 21H5a2 2 0 0 1-2-2V5a2 2 0 0 1 2-2h4"></path><polyline points="16 17 21 12 16 7"></polyline><line x1="21" y1="12" x2="9" y2="12"></line></svg>
                Log Out / Exit
            </button>
        </aside>

        <!-- Main Content Area -->
        <main class="main-content">
            
            <header>
                <h1 id="page-title">Expense Overview</h1>
            </header>

            <!-- Dashboard View -->
            <div id="view-dashboard" class="view-section active">
                <!-- Metrics Grid (Requirements 4, 5, 6) -->
                <section class="metrics-grid">
                    <div class="glass-panel metric-card">
                        <h3>Total Budget</h3>
                        <p class="amount neon-blue-text" id="ui-budget">$0.00</p>
                    </div>
                    <div class="glass-panel metric-card">
                        <h3>Total Expenses</h3>
                        <p class="amount neon-red" id="ui-total-expense">$0.00</p>
                    </div>
                    <div class="glass-panel metric-card">
                        <h3>Remaining Budget</h3>
                        <p class="amount neon-green" id="ui-remaining">$0.00</p>
                    </div>
                    <div class="glass-panel metric-card">
                        <h3>Largest Expense</h3>
                        <p class="amount neon-orange-text" id="ui-largest" style="font-size: 1.3rem;">$0.00</p>
                    </div>
                </section>

                <!-- Forms Section (Requirements 1, 2) -->
                <section class="forms-section">
                    <div class="glass-panel form-card">
                        <h3>Set Monthly Budget</h3>
                        <form id="budget-form" onsubmit="handleSetBudget(event)" class="form-group">
                            <label>Budget Amount ($)</label>
                            <input type="number" id="budget-input" class="form-control" placeholder="e.g. 5000" min="1" step="0.01" required>
                            <button type="submit" class="btn-submit">Save Budget</button>
                        </form>
                    </div>
                    
                    <div class="glass-panel form-card">
                        <h3>Record New Expense</h3>
                        <form id="expense-form" onsubmit="handleAddExpense(event)" style="display: grid; grid-template-columns: 1fr 1fr; gap: 15px;">
                            <div class="form-group" style="grid-column: span 2;">
                                <label>Expense Name</label>
                                <input type="text" id="exp-name" class="form-control" placeholder="e.g. Weekly Groceries" required>
                            </div>
                            <div class="form-group">
                                <label>Amount ($)</label>
                                <input type="number" id="exp-amount" class="form-control" placeholder="0.00" min="0.01" step="0.01" required>
                            </div>
                            <div class="form-group">
                                <label>Category</label>
                                <select id="exp-category" class="form-control" required>
                                    <option value="" disabled selected>Select...</option>
                                    <option value="Housing">🏠 Housing & Rent</option>
                                    <option value="Food">🍔 Food & Dining</option>
                                    <option value="Transport">🚗 Transportation</option>
                                    <option value="Utilities">⚡ Utilities</option>
                                    <option value="Entertainment">🎮 Entertainment</option>
                                    <option value="Other">📦 Other</option>
                                </select>
                            </div>
                            <button type="submit" class="btn-submit" style="grid-column: span 2;">+ Add Expense</button>
                        </form>
                    </div>
                </section>

                <!-- Bottom Section Grid (Requirements 3) -->
                <section class="bottom-grid">
                    <div class="glass-panel transactions-list">
                        <h3 class="section-title">Recent Transactions</h3>
                        <div class="transactions-container" id="expense-list-container">
                            <!-- JS will populate expenses here -->
                        </div>
                    </div>
                    
                    <div class="glass-panel chart-card">
                        <h3 class="section-title">Spending Breakdown</h3>
                        <div class="canvas-wrapper">
                            <canvas id="expenseChart"></canvas>
                        </div>
                    </div>
                </section>
            </div>

            <!-- Analytics View Scaffold -->
            <div id="view-analytics" class="view-section">
                <section class="forms-section" style="grid-template-columns: 1fr 1fr;">
                    <div class="glass-panel form-card">
                        <h3>Budget vs Actual Projection</h3>
                        <p style="color: var(--text-muted); margin-bottom: 15px;">A detailed comparison of your set budget parameters against your actual recorded outflow.</p>
                        <div class="canvas-wrapper" style="min-height: 200px; background: rgba(0,0,0,0.2); border-radius: 10px; display:flex; align-items:center; justify-content:center;">
                            <span style="color: var(--text-muted);">[Analytics Chart Placeholder]</span>
                        </div>
                    </div>
                    
                    <div class="glass-panel form-card">
                        <h3>Export Reports</h3>
                        <p style="color: var(--text-muted); margin-bottom: 25px;">Download your transaction history and analytical summaries.</p>
                        <div style="display: flex; flex-direction: column; gap: 15px;">
                            <button class="btn-submit" onclick="exportToPDF()" style="display: flex; justify-content: center; gap: 10px;">
                                <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M21 15v4a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2v-4"></path><polyline points="7 10 12 15 17 10"></polyline><line x1="12" y1="15" x2="12" y2="3"></line></svg>
                                Export to PDF
                            </button>
                            <button class="btn-submit" onclick="exportToCSV()" style="background: transparent; display: flex; justify-content: center; gap: 10px;">
                                <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M14 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V8z"></path><polyline points="14 2 14 8 20 8"></polyline><line x1="8" y1="13" x2="16" y2="13"></line><line x1="8" y1="17" x2="16" y2="17"></line><polyline points="10 9 9 9 8 9"></polyline></svg>
                                Export CSV
                            </button>
                        </div>
                    </div>
                </section>
            </div>

            <!-- Settings / Profile View -->
            <div id="view-settings" class="view-section">
                <div class="settings-grid">
                    
                    <!-- Settings Left Sidebar -->
                    <div class="settings-menu">
                        <div class="glass-panel setting-nav-item active">
                            <h4>Account Setting</h4>
                            <p>Details about your Personal information</p>
                        </div>
                        <div class="glass-panel setting-nav-item">
                            <h4>Notification</h4>
                            <p>Details about your Personal information</p>
                        </div>
                        <div class="glass-panel setting-nav-item">
                            <h4>Membership Plan</h4>
                            <p>Details about your Personal information</p>
                        </div>
                        <div class="glass-panel setting-nav-item">
                            <h4>Password & Security</h4>
                            <p>Details about your Personal information</p>
                        </div>
                    </div>

                    <!-- Settings Right Content -->
                    <div class="settings-content">
                        
                        <div class="glass-panel photo-upload-card">
                            <div class="photo-left">
                                <div class="avatar-large"></div>
                                <div>
                                    <h3 style="font-size: 1.2rem; font-weight: 600; margin-bottom: 5px;">Upload a New Photo</h3>
                                    <p style="color: var(--text-muted); font-size: 0.9rem;">Profile-pic.jpg</p>
                                </div>
                            </div>
                            <button class="btn-submit" style="margin-top: 0; min-width: 120px;">Update</button>
                        </div>

                        <div class="glass-panel form-card">
                            <h3 style="font-size: 1.3rem; margin-bottom: 10px; border-bottom: none;">Change User Information here</h3>
                            <form id="profile-form" class="info-form-grid" onsubmit="handleProfileUpdate(event)">
                                <div class="form-group">
                                    <label>Full Name*</label>
                                    <input type="text" id="prof-fullname" class="form-control" value="Clarence Boquilla Agustin" required>
                                </div>
                                <div class="form-group">
                                    <label>Email Address*</label>
                                    <input type="email" class="form-control" value="clarence.agustin@nvsu.edu.ph" required>
                                </div>
                                <div class="form-group full-width">
                                    <label>Address*</label>
                                    <input type="text" class="form-control" value="Barangay Dumabato Norte" required>
                                </div>
                                <div class="form-group">
                                    <label>City</label>
                                    <input type="text" class="form-control" value="Maddela">
                                </div>
                                <div class="form-group">
                                    <label>State/Province</label>
                                    <input type="text" class="form-control" value="Quirino">
                                </div>
                                <div class="form-group">
                                    <label>Zip Code</label>
                                    <input type="text" class="form-control" value="3340">
                                </div>
                                <div class="form-group">
                                    <label>Country</label>
                                    <select class="form-control">
                                        <option value="Philippines" selected>🇵🇭 Philippines</option>
                                        <option value="US">🇺🇸 United States</option>
                                        <option value="UK">🇬🇧 United Kingdom</option>
                                    </select>
                                </div>
                                <button type="submit" class="btn-submit full-width" style="margin-top: 20px;">Update Information</button>
                            </form>
                        </div>
                        
                    </div>
                </div>
            </div>

        </main>
    </div>
    
    <!-- Toast Notification -->
    <div id="toast" class="toast">Profile Updated!</div>

    <script src="app.js"></script>
</body>
</html>