/* CSS Variables */
:root {
    --bg-gradient: linear-gradient(135deg, #0f0c29, #302b63, #24243e);
    --card-bg: rgba(30, 27, 46, 0.6);
    --card-border: rgba(255, 255, 255, 0.05);
    --neon-green: #00ff88;
    --neon-red: #ff4757;
    --neon-blue: #3742fa;
    --neon-orange: #ff9f43;
    --text-main: #f1f2f6;
    --text-muted: #a4b0be;
    --font-family: 'Inter', sans-serif;
}

/* Global Reset */
* { margin: 0; padding: 0; box-sizing: border-box; font-family: var(--font-family); }
body { background: var(--bg-gradient); background-attachment: fixed; color: var(--text-main); min-height: 100vh; overflow-x: hidden; display: flex; justify-content: center; }

/* Scrollbar */
::-webkit-scrollbar { width: 8px; }
::-webkit-scrollbar-track { background: rgba(0,0,0,0.2); }
::-webkit-scrollbar-thumb { background: rgba(255,255,255,0.2); border-radius: 4px; }
::-webkit-scrollbar-thumb:hover { background: rgba(255,255,255,0.4); }

/* Layout */
.dashboard-container { display: flex; width: 100%; max-width: 1600px; height: 100vh; padding: 20px; gap: 20px; }
.glass-panel { background: var(--card-bg); backdrop-filter: blur(12px); -webkit-backdrop-filter: blur(12px); border: 1px solid var(--card-border); border-radius: 20px; box-shadow: 0 8px 32px 0 rgba(0, 0, 0, 0.3); }

/* Sidebar */
.sidebar { width: 260px; padding: 30px 20px; display: flex; flex-direction: column; gap: 40px; flex-shrink: 0; overflow-y: auto; justify-content: space-between; }
.sidebar-top { display: flex; flex-direction: column; gap: 40px; }
.profile-section { display: flex; align-items: center; gap: 15px; }
.avatar { width: 50px; height: 50px; border-radius: 50%; background: linear-gradient(135deg, var(--neon-blue), var(--neon-green)); box-shadow: 0 4px 15px rgba(0, 255, 136, 0.3); flex-shrink: 0; }
.profile-info h2 { font-size: 1.1rem; font-weight: 600; }
.profile-info p { font-size: 0.8rem; color: var(--text-muted); }
nav ul { list-style: none; display: flex; flex-direction: column; gap: 10px; }
nav li { padding: 14px 20px; border-radius: 12px; cursor: pointer; transition: all 0.3s ease; color: var(--text-muted); font-weight: 500; display: flex; align-items: center; gap: 12px; }
nav li:hover, nav li.active { background: rgba(255, 255, 255, 0.1); color: var(--text-main); box-shadow: inset 3px 0 0 var(--neon-blue); }

.btn-logout { background: rgba(255, 71, 87, 0.1); color: var(--neon-red); border: 1px solid rgba(255, 71, 87, 0.3); padding: 14px 20px; border-radius: 12px; font-weight: 600; cursor: pointer; transition: all 0.3s ease; text-align: center; width: 100%; display: flex; justify-content: center; align-items: center; gap: 10px; }
.btn-logout:hover { background: rgba(255, 71, 87, 0.2); box-shadow: 0 0 15px rgba(255, 71, 87, 0.4); transform: translateY(-2px); }

/* Main Content */
.main-content { flex: 1; display: flex; flex-direction: column; gap: 25px; overflow-y: auto; padding-right: 10px; padding-bottom: 20px;}
header { display: flex; justify-content: space-between; align-items: center; padding: 10px 0; }
header h1 { font-size: 1.8rem; font-weight: 700; letter-spacing: -0.5px; }

/* Metrics Grid */
.metrics-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(220px, 1fr)); gap: 20px; }
.metric-card { padding: 25px; transition: transform 0.3s ease, box-shadow 0.3s ease; display: flex; flex-direction: column; gap: 10px; }
.metric-card:hover { transform: translateY(-5px); box-shadow: 0 12px 40px rgba(0, 0, 0, 0.5); }
.metric-card h3 { color: var(--text-muted); font-size: 0.95rem; font-weight: 500; text-transform: uppercase; letter-spacing: 1px; }
.amount { font-size: 2rem; font-weight: 700; word-break: break-word; }

/* Text Accents */
.neon-green { color: var(--neon-green); text-shadow: 0 0 15px rgba(0, 255, 136, 0.4); }
.neon-red { color: var(--neon-red); text-shadow: 0 0 15px rgba(255, 71, 87, 0.4); }
.neon-blue-text { color: #70a1ff; text-shadow: 0 0 15px rgba(112, 161, 255, 0.4); }
.neon-orange-text { color: var(--neon-orange); text-shadow: 0 0 15px rgba(255, 159, 67, 0.4); }

/* Forms Section */
.forms-section { display: grid; grid-template-columns: 1fr 2fr; gap: 20px; }
.form-card { padding: 25px; display: flex; flex-direction: column; gap: 15px; }
.form-card h3 { font-size: 1.2rem; font-weight: 600; margin-bottom: 5px; border-bottom: 1px solid rgba(255,255,255,0.1); padding-bottom: 10px;}

.form-group { display: flex; flex-direction: column; gap: 8px; }
.form-group label { font-size: 0.9rem; color: var(--text-muted); }
.form-control { background: rgba(0, 0, 0, 0.2); border: 1px solid rgba(255, 255, 255, 0.1); color: white; padding: 12px 15px; border-radius: 8px; outline: none; transition: 0.3s; font-size: 1rem; }
.form-control:focus { border-color: var(--neon-blue); box-shadow: 0 0 10px rgba(55, 66, 250, 0.3); background: rgba(0, 0, 0, 0.4); }
.form-control option { background: #1e1b2e; color: white; }

.btn-submit { background: rgba(55, 66, 250, 0.2); color: var(--text-main); border: 1px solid var(--neon-blue); padding: 12px 24px; border-radius: 8px; font-size: 1rem; font-weight: 600; cursor: pointer; transition: all 0.3s ease; margin-top: 10px;}
.btn-submit:hover { background: var(--neon-blue); box-shadow: 0 0 20px rgba(55, 66, 250, 0.6); transform: translateY(-2px); }

/* Bottom Section Grid */
.bottom-grid { display: grid; grid-template-columns: 2fr 1fr; gap: 20px; }

/* Transactions List */
.transactions-list, .chart-card { padding: 25px; display: flex; flex-direction: column;}
.section-title { margin-bottom: 20px; font-size: 1.2rem; font-weight: 600; border-bottom: 1px solid rgba(255,255,255,0.1); padding-bottom: 10px;}

.transactions-container { display: flex; flex-direction: column; gap: 10px; max-height: 350px; overflow-y: auto; padding-right: 5px; }
.transaction-item { display: flex; justify-content: space-between; align-items: center; padding: 16px; background: rgba(255, 255, 255, 0.02); border: 1px solid rgba(255, 255, 255, 0.03); border-radius: 12px; transition: all 0.3s ease; }
.transaction-item:hover { background: rgba(255, 255, 255, 0.08); transform: translateY(-2px); box-shadow: 0 5px 15px rgba(0,0,0,0.2); border-color: rgba(255, 255, 255, 0.1); }

.tx-left { display: flex; align-items: center; gap: 15px; }
.tx-icon { width: 42px; height: 42px; border-radius: 10px; background: rgba(255,255,255,0.05); display: flex; align-items: center; justify-content: center; font-size: 1.2rem; }
.tx-info { display: flex; flex-direction: column; gap: 4px; }
.tx-name { font-weight: 600; font-size: 1rem; }
.tx-category { font-size: 0.8rem; color: var(--text-muted); background: rgba(255,255,255,0.1); padding: 2px 8px; border-radius: 10px; width: fit-content;}
.tx-amount { font-weight: 700; font-size: 1.1rem; }

.empty-state { text-align: center; color: var(--text-muted); padding: 30px; font-style: italic; }

/* Chart */
.canvas-wrapper { position: relative; flex: 1; width: 100%; min-height: 250px; display: flex; justify-content: center; align-items: center;}

/* Views & Settings Layout Additions */
.view-section { display: none; flex-direction: column; gap: 25px; flex: 1; animation: fadeIn 0.4s ease; }
.view-section.active { display: flex; }
@keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }

.settings-grid { display: grid; grid-template-columns: 280px 1fr; gap: 20px; }
.settings-menu { display: flex; flex-direction: column; gap: 12px; }
.setting-nav-item { padding: 18px; cursor: pointer; border: 1px solid transparent; transition: 0.3s; }
.setting-nav-item:hover, .setting-nav-item.active { border-color: var(--neon-blue); background: rgba(55, 66, 250, 0.1); }
.setting-nav-item h4 { font-size: 1.05rem; margin-bottom: 5px; font-weight: 600; }
.setting-nav-item p { font-size: 0.8rem; color: var(--text-muted); }

.settings-content { display: flex; flex-direction: column; gap: 20px; }
.photo-upload-card { padding: 25px; display: flex; justify-content: space-between; align-items: center; }
.photo-left { display: flex; align-items: center; gap: 20px; }
.photo-left .avatar-large { width: 75px; height: 75px; border-radius: 50%; background: linear-gradient(135deg, var(--neon-blue), var(--neon-green)); box-shadow: 0 4px 15px rgba(0, 255, 136, 0.3); }

.info-form-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 20px; }
.full-width { grid-column: span 2; }

/* Toast Notification */
.toast { position: fixed; bottom: 30px; right: 30px; background: var(--neon-green); color: #000; padding: 14px 28px; border-radius: 10px; font-weight: 600; box-shadow: 0 5px 20px rgba(0, 255, 136, 0.4); transform: translateY(100px); opacity: 0; transition: all 0.4s cubic-bezier(0.68, -0.55, 0.265, 1.55); z-index: 3000; }
.toast.show { transform: translateY(0); opacity: 1; }

/* --- Login Screen Styles --- */
.login-container {
    position: fixed; top: 0; left: 0; width: 100vw; height: 100vh;
    background: url('https://images.unsplash.com/photo-1542224566-6e85f2e6772f?q=80&w=2000&auto=format&fit=crop') no-repeat center center/cover;
    display: flex; justify-content: center; align-items: center;
    z-index: 2000;
}
.login-container::before { 
    content: ''; position: absolute; top: 0; left: 0; right: 0; bottom: 0; 
    background: rgba(0,0,0,0.15); z-index: -1; 
}
.login-card {
    background: rgba(255, 255, 255, 0.1); backdrop-filter: blur(25px); -webkit-backdrop-filter: blur(25px);
    border: 1px solid rgba(255, 255, 255, 0.2); border-radius: 16px;
    padding: 40px; width: 100%; max-width: 420px;
    display: flex; flex-direction: column; gap: 20px; text-align: center;
    box-shadow: 0 15px 35px rgba(0,0,0,0.3);
}
.login-card h2 { font-weight: 500; font-size: 1.5rem; margin-bottom: 5px; }
.login-input { 
    background: rgba(255,255,255,0.15); border: 1px solid rgba(255,255,255,0.1); 
    color: white; padding: 14px 20px; border-radius: 30px; outline: none; 
    transition: 0.3s; font-size: 0.95rem; 
}
.login-input::placeholder { color: rgba(255,255,255,0.8); }
.login-input:focus { border-color: rgba(255,255,255,0.5); background: rgba(255,255,255,0.25); }

.btn-login { 
    background: #7c3a52; color: white; border: none; padding: 14px 20px; 
    border-radius: 30px; font-size: 0.95rem; font-weight: 500; letter-spacing: 0.5px;
    cursor: pointer; transition: all 0.3s ease; margin-top: 5px; 
}
.btn-login:hover { background: #964663; transform: translateY(-2px); box-shadow: 0 5px 15px rgba(124, 58, 82, 0.4); }

.login-links { display: flex; justify-content: space-between; font-size: 0.85rem; margin-top: -5px; }
.login-links a { color: rgba(255,255,255,0.9); text-decoration: none; transition: 0.3s; }
.login-links a:hover { color: white; text-shadow: 0 0 5px rgba(255,255,255,0.5); }

.login-divider { display: flex; align-items: center; justify-content: center; color: rgba(255,255,255,0.8); font-size: 0.75rem; font-weight: 500; margin: 10px 0;}
.login-divider::before, .login-divider::after { content: ''; flex: 1; border-bottom: 1px solid rgba(255,255,255,0.2); margin: 0 15px; }

.social-login { display: flex; justify-content: center; gap: 20px; }
.btn-social { width: 42px; height: 42px; border-radius: 50%; border: none; cursor: pointer; display: flex; align-items: center; justify-content: center; transition: 0.3s; }
.btn-social:hover { transform: translateY(-3px); box-shadow: 0 5px 15px rgba(0,0,0,0.3); }
.google-btn { background: white; }
.fb-btn { background: #1877f2; color: white; }

/* Animations */
.animate-out {
    animation: fadeOutScale 0.5s cubic-bezier(0.4, 0, 0.2, 1) forwards;
}
.animate-in {
    animation: fadeInScale 0.5s cubic-bezier(0.4, 0, 0.2, 1) forwards;
}

@keyframes fadeOutScale {
    from { opacity: 1; transform: scale(1); }
    to { opacity: 0; transform: scale(1.05); }
}

@keyframes fadeInScale {
    from { opacity: 0; transform: scale(0.95); }
    to { opacity: 1; transform: scale(1); }
}

/* Responsive */
@media (max-width: 1200px) {
    .forms-section, .bottom-grid { grid-template-columns: 1fr; }
    .settings-grid { grid-template-columns: 1fr; }
}
@media (max-width: 992px) {
    .dashboard-container { flex-direction: column; padding: 10px; height: auto; min-height: 100vh;}
    .sidebar { width: 100%; flex-direction: row; justify-content: space-between; align-items: center; padding: 15px 20px; gap: 20px; overflow-x: auto; }
    .sidebar-top { flex-direction: row; gap: 20px; align-items: center; width: auto; flex: 1; }
    nav ul { flex-direction: row; }
    .btn-logout { width: auto; padding: 10px 15px; }
}
@media (max-width: 600px) {
    .metrics-grid { grid-template-columns: 1fr; }
    .info-form-grid { grid-template-columns: 1fr; }
    .full-width { grid-column: span 1; }
    .photo-upload-card { flex-direction: column; gap: 15px; align-items: flex-start; }
    .login-card { padding: 30px 20px; width: 90%; }
}