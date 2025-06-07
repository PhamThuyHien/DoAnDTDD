<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Advanced Cloud Computing Platform</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            color: #333;
        }

        .sidebar {
            position: fixed;
            left: 0;
            top: 0;
            width: 250px;
            height: 100vh;
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(10px);
            border-right: 1px solid rgba(255, 255, 255, 0.2);
            z-index: 1000;
            transition: transform 0.3s ease;
        }

        .sidebar.collapsed {
            transform: translateX(-200px);
        }

        .sidebar-header {
            padding: 20px;
            border-bottom: 1px solid rgba(102, 126, 234, 0.2);
            text-align: center;
        }

        .sidebar-header h2 {
            color: #667eea;
            font-size: 1.2rem;
            margin-bottom: 5px;
        }

        .sidebar-header .version {
            font-size: 0.8rem;
            color: #666;
        }

        .nav-menu {
            padding: 20px 0;
        }

        .nav-item {
            display: block;
            padding: 12px 20px;
            color: #555;
            text-decoration: none;
            transition: all 0.3s ease;
            border-left: 3px solid transparent;
        }

        .nav-item:hover {
            background: rgba(102, 126, 234, 0.1);
            border-left-color: #667eea;
            color: #667eea;
        }

        .nav-item.active {
            background: rgba(102, 126, 234, 0.15);
            border-left-color: #667eea;
            color: #667eea;
            font-weight: bold;
        }

        .nav-item i {
            margin-right: 10px;
            width: 20px;
        }

        .main-content {
            margin-left: 250px;
            padding: 20px;
            transition: margin-left 0.3s ease;
        }

        .main-content.expanded {
            margin-left: 50px;
        }

        .top-bar {
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(10px);
            padding: 15px 20px;
            border-radius: 15px;
            margin-bottom: 20px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            box-shadow: 0 4px 20px rgba(0,0,0,0.1);
        }

        .top-bar-left {
            display: flex;
            align-items: center;
            gap: 15px;
        }

        .menu-toggle {
            background: none;
            border: none;
            font-size: 1.5rem;
            cursor: pointer;
            color: #667eea;
        }

        .breadcrumb {
            color: #666;
            font-size: 0.9rem;
        }

        .top-bar-right {
            display: flex;
            align-items: center;
            gap: 15px;
        }

        .notification-icon {
            position: relative;
            font-size: 1.2rem;
            color: #667eea;
            cursor: pointer;
        }

        .notification-badge {
            position: absolute;
            top: -5px;
            right: -5px;
            background: #f56565;
            color: white;
            border-radius: 50%;
            width: 18px;
            height: 18px;
            font-size: 0.7rem;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .user-profile {
            display: flex;
            align-items: center;
            gap: 10px;
            cursor: pointer;
        }

        .user-avatar {
            width: 35px;
            height: 35px;
            border-radius: 50%;
            background: linear-gradient(45deg, #667eea, #764ba2);
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-weight: bold;
        }

        .page-content {
            display: none;
        }

        .page-content.active {
            display: block;
        }

        .page-header {
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(10px);
            padding: 20px;
            border-radius: 15px;
            margin-bottom: 20px;
            box-shadow: 0 4px 20px rgba(0,0,0,0.1);
        }

        .page-header h1 {
            color: #667eea;
            margin-bottom: 10px;
            font-size: 1.8rem;
        }

        .page-header p {
            color: #666;
            margin-bottom: 15px;
        }

        .quick-stats {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 15px;
            margin-bottom: 20px;
        }

        .stat-card {
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(10px);
            padding: 20px;
            border-radius: 15px;
            text-align: center;
            box-shadow: 0 4px 20px rgba(0,0,0,0.1);
            transition: transform 0.3s ease;
        }

        .stat-card:hover {
            transform: translateY(-5px);
        }

        .stat-value {
            font-size: 2rem;
            font-weight: bold;
            color: #667eea;
            margin-bottom: 5px;
        }

        .stat-label {
            color: #666;
            font-size: 0.9rem;
        }

        .dashboard-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
            gap: 20px;
            margin-bottom: 20px;
        }

        .card {
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(10px);
            border-radius: 15px;
            padding: 25px;
            box-shadow: 0 8px 32px rgba(0,0,0,0.1);
            border: 1px solid rgba(255,255,255,0.2);
            transition: transform 0.3s ease, box-shadow 0.3s ease;
        }

        .card:hover {
            transform: translateY(-5px);
            box-shadow: 0 12px 40px rgba(0,0,0,0.15);
        }

        .card-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
        }

        .card-title {
            font-size: 1.2rem;
            color: #4a5568;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .card-actions {
            display: flex;
            gap: 10px;
        }

        .btn-icon {
            background: none;
            border: none;
            padding: 8px;
            border-radius: 8px;
            cursor: pointer;
            color: #667eea;
            transition: background 0.3s ease;
        }

        .btn-icon:hover {
            background: rgba(102, 126, 234, 0.1);
        }

        .progress-bar {
            width: 100%;
            height: 8px;
            background: #e2e8f0;
            border-radius: 4px;
            overflow: hidden;
            margin: 10px 0;
        }

        .progress-fill {
            height: 100%;
            background: linear-gradient(90deg, #667eea, #764ba2);
            border-radius: 4px;
            transition: width 0.5s ease;
        }

        .metric-row {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 10px 0;
            border-bottom: 1px solid rgba(0,0,0,0.05);
        }

        .metric-row:last-child {
            border-bottom: none;
        }

        .metric-label {
            color: #666;
        }

        .metric-value {
            font-weight: bold;
            color: #667eea;
        }

        .status-indicator {
            display: inline-flex;
            align-items: center;
            gap: 5px;
        }

        .status-dot {
            width: 8px;
            height: 8px;
            border-radius: 50%;
        }

        .status-dot.online {
            background: #48bb78;
        }

        .status-dot.warning {
            background: #ed8936;
        }

        .status-dot.offline {
            background: #f56565;
        }

        .table-container {
            overflow-x: auto;
            border-radius: 10px;
            box-shadow: 0 4px 20px rgba(0,0,0,0.1);
        }

        .data-table {
            width: 100%;
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(10px);
            border-collapse: collapse;
        }

        .data-table th,
        .data-table td {
            padding: 12px 15px;
            text-align: left;
            border-bottom: 1px solid rgba(0,0,0,0.05);
        }

        .data-table th {
            background: rgba(102, 126, 234, 0.1);
            color: #667eea;
            font-weight: bold;
        }

        .data-table tr:hover {
            background: rgba(102, 126, 234, 0.05);
        }

        .form-group {
            margin-bottom: 20px;
        }

        .form-label {
            display: block;
            margin-bottom: 5px;
            color: #4a5568;
            font-weight: 500;
        }

        .form-input {
            width: 100%;
            padding: 12px;
            border: 1px solid rgba(102, 126, 234, 0.3);
            border-radius: 8px;
            font-size: 1rem;
            transition: border-color 0.3s ease;
        }

        .form-input:focus {
            outline: none;
            border-color: #667eea;
            box-shadow: 0 0 0 3px rgba(102, 126, 234, 0.1);
        }

        .btn {
            padding: 12px 24px;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            font-weight: bold;
            transition: all 0.3s ease;
            text-decoration: none;
            display: inline-block;
            font-size: 1rem;
        }

        .btn-primary {
            background: linear-gradient(45deg, #667eea, #764ba2);
            color: white;
        }

        .btn-primary:hover {
            transform: translateY(-2px);
            box-shadow: 0 4px 15px rgba(102, 126, 234, 0.4);
        }

        .btn-secondary {
            background: rgba(255, 255, 255, 0.8);
            color: #4a5568;
            border: 1px solid rgba(102, 126, 234, 0.3);
        }

        .btn-danger {
            background: #f56565;
            color: white;
        }

        .btn-success {
            background: #48bb78;
            color: white;
        }

        .alert {
            padding: 15px;
            border-radius: 8px;
            margin-bottom: 20px;
            border-left: 4px solid;
        }

        .alert-info {
            background: rgba(102, 126, 234, 0.1);
            border-left-color: #667eea;
            color: #4a5568;
        }

        .alert-warning {
            background: rgba(237, 137, 54, 0.1);
            border-left-color: #ed8936;
            color: #744210;
        }

        .alert-danger {
            background: rgba(245, 101, 101, 0.1);
            border-left-color: #f56565;
            color: #742a2a;
        }

        .chart-container {
            height: 300px;
            position: relative;
            margin: 20px 0;
        }

        .logs-container {
            max-height: 300px;
            overflow-y: auto;
            background: rgba(0, 0, 0, 0.05);
            border-radius: 8px;
            padding: 15px;
            font-family: 'Courier New', monospace;
            font-size: 0.9rem;
        }

        .log-entry {
            margin-bottom: 8px;
            padding: 5px;
            border-radius: 4px;
            transition: background 0.3s ease;
        }

        .log-entry:hover {
            background: rgba(102, 126, 234, 0.1);
        }

        .log-time {
            color: #667eea;
            font-weight: bold;
        }

        .log-level {
            padding: 2px 6px;
            border-radius: 3px;
            font-size: 0.8rem;
            font-weight: bold;
            margin-left: 10px;
        }

        .log-level.info {
            background: #48bb78;
            color: white;
        }

        .log-level.warn {
            background: #ed8936;
            color: white;
        }

        .log-level.error {
            background: #f56565;
            color: white;
        }

        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.5);
            z-index: 2000;
            backdrop-filter: blur(5px);
        }

        .modal.show {
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .modal-content {
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(10px);
            padding: 30px;
            border-radius: 15px;
            max-width: 500px;
            width: 90%;
            max-height: 80vh;
            overflow-y: auto;
        }

        .modal-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
        }

        .modal-title {
            font-size: 1.5rem;
            color: #667eea;
        }

        .modal-close {
            background: none;
            border: none;
            font-size: 1.5rem;
            cursor: pointer;
            color: #999;
        }

        .grid-2 {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 20px;
        }

        @media (max-width: 768px) {
            .sidebar {
                transform: translateX(-100%);
            }
            
            .sidebar.show {
                transform: translateX(0);
            }
            
            .main-content {
                margin-left: 0;
            }
            
            .dashboard-grid {
                grid-template-columns: 1fr;
            }
            
            .quick-stats {
                grid-template-columns: repeat(2, 1fr);
            }
            
            .grid-2 {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>
    <!-- Sidebar -->
    <div class="sidebar" id="sidebar">
        <div class="sidebar-header">
            <h2>☁️ Cloud Pro</h2>
            <div class="version">v2.0.1</div>
        </div>
        <nav class="nav-menu">
            <a href="#" class="nav-item active" data-page="dashboard">
                <i>📊</i> Dashboard
            </a>
            <a href="#" class="nav-item" data-page="servers">
                <i>🖥️</i> Servers
            </a>
            <a href="#" class="nav-item" data-page="services">
                <i>⚙️</i> Services
            </a>
            <a href="#" class="nav-item" data-page="storage">
                <i>💾</i> Storage
            </a>
            <a href="#" class="nav-item" data-page="network">
                <i>🌐</i> Network
            </a>
            <a href="#" class="nav-item" data-page="database">
                <i>🗄️</i> Database
            </a>
            <a href="#" class="nav-item" data-page="security">
                <i>🔒</i> Security
            </a>
            <a href="#" class="nav-item" data-page="logs">
                <i>📝</i> Logs
            </a>
            <a href="#" class="nav-item" data-page="billing">
                <i>💰</i> Billing
            </a>
            <a href="#" class="nav-item" data-page="settings">
                <i>⚙️</i> Settings
            </a>
        </nav>
    </div>

    <!-- Main Content -->
    <div class="main-content" id="mainContent">
        <!-- Top Bar -->
        <div class="top-bar">
            <div class="top-bar-left">
                <button class="menu-toggle" onclick="toggleSidebar()">☰</button>
                <div class="breadcrumb" id="breadcrumb">Dashboard</div>
            </div>
            <div class="top-bar-right">
                <div class="notification-icon" onclick="showNotifications()">
                    🔔
                    <span class="notification-badge">3</span>
                </div>
                <div class="user-profile" onclick="showUserMenu()">
                    <div class="user-avatar">AD</div>
                    <span>Admin</span>
                </div>
            </div>
        </div>

        <!-- Dashboard Page -->
        <div class="page-content active" id="page-dashboard">
            <div class="page-header">
                <h1>Cloud Computing Dashboard</h1>
                <p>Tổng quan về hệ thống và hiệu suất cloud infrastructure</p>
                <div class="alert alert-info">
                    <strong>Thông báo:</strong> Hệ thống đang hoạt động bình thường. Backup tự động đã hoàn thành lúc 02:00 AM.
                </div>
            </div>

            <div class="quick-stats">
                <div class="stat-card">
                    <div class="stat-value" id="total-servers">12</div>
                    <div class="stat-label">Servers</div>
                </div>
                <div class="stat-card">
                    <div class="stat-value" id="active-services">8</div>
                    <div class="stat-label">Active Services</div>
                </div>
                <div class="stat-card">
                    <div class="stat-value" id="total-storage">2.4TB</div>
                    <div class="stat-label">Total Storage</div>
                </div>
                <div class="stat-card">
                    <div class="stat-value" id="monthly-cost">$1,248</div>
                    <div class="stat-label">Monthly Cost</div>
                </div>
            </div>

            <div class="dashboard-grid">
                <div class="card">
                    <div class="card-header">
                        <h3 class="card-title">🖥️ System Performance</h3>
                        <div class="card-actions">
                            <button class="btn-icon" onclick="refreshMetrics()">🔄</button>
                            <button class="btn-icon" onclick="showMetricsDetails()">📊</button>
                        </div>
                    </div>
                    <div class="metric-row">
                        <span class="metric-label">CPU Usage</span>
                        <span class="metric-value" id="cpu-usage">45%</span>
                    </div>
                    <div class="progress-bar">
                        <div class="progress-fill" id="cpu-progress" style="width: 45%"></div>
                    </div>
                    <div class="metric-row">
                        <span class="metric-label">Memory Usage</span>
                        <span class="metric-value" id="memory-usage">68%</span>
                    </div>
                    <div class="progress-bar">
                        <div class="progress-fill" id="memory-progress" style="width: 68%"></div>
                    </div>
                    <div class="metric-row">
                        <span class="metric-label">Storage Usage</span>
                        <span class="metric-value" id="storage-usage">34%</span>
                    </div>
                    <div class="progress-bar">
                        <div class="progress-fill" id="storage-progress" style="width: 34%"></div>
                    </div>
                </div>

                <div class="card">
                    <div class="card-header">
                        <h3 class="card-title">☁️ Services Status</h3>
                        <div class="card-actions">
                            <button class="btn-icon" onclick="refreshServices()">🔄</button>
                            <button class="btn-icon" onclick="manageServices()">⚙️</button>
                        </div>
                    </div>
                    <div class="metric-row">
                        <span class="metric-label">Web Server</span>
                        <span class="status-indicator">
                            <span class="status-dot online"></span>
                            Online
                        </span>
                    </div>
                    <div class="metric-row">
                        <span class="metric-label">Database</span>
                        <span class="status-indicator">
                            <span class="status-dot online"></span>
                            Online
                        </span>
                    </div>
                    <div class="metric-row">
                        <span class="metric-label">Load Balancer</span>
                        <span class="status-indicator">
                            <span class="status-dot warning"></span>
                            Warning
                        </span>
                    </div>
                    <div class="metric-row">
                        <span class="metric-label">Backup Service</span>
                        <span class="status-indicator">
                            <span class="status-dot online"></span>
                            Online
                        </span>
                    </div>
                    <div class="metric-row">
                        <span class="metric-label">Monitoring</span>
                        <span class="status-indicator">
                            <span class="status-dot online"></span>
                            Online
                        </span>
                    </div>
                </div>

                <div class="card">
                    <div class="card-header">
                        <h3 class="card-title">🌐 Network Traffic</h3>
                        <div class="card-actions">
                            <button class="btn-icon" onclick="showTrafficDetails()">📈</button>
                        </div>
                    </div>
                    <div class="metric-row">
                        <span class="metric-label">Inbound Traffic</span>
                        <span class="metric-value" id="inbound-traffic">2.4 GB/h</span>
                    </div>
                    <div class="metric-row">
                        <span class="metric-label">Outbound Traffic</span>
                        <span class="metric-value" id="outbound-traffic">1.8 GB/h</span>
                    </div>
                    <div class="metric-row">
                        <span class="metric-label">Active Connections</span>
                        <span class="metric-value" id="active-connections">1,247</span>
                    </div>
                    <div class="metric-row">
                        <span class="metric-label">Response Time</span>
                        <span class="metric-value" id="response-time">85ms</span>
                    </div>
                    <div class="metric-row">
                        <span class="metric-label">Bandwidth Usage</span>
                        <span class="metric-value" id="bandwidth-usage">78%</span>
                    </div>
                </div>

                <div class="card">
                    <div class="card-header">
                        <h3 class="card-title">📝 Recent Activities</h3>
                        <div class="card-actions">
                            <button class="btn-icon" onclick="showAllLogs()">📋</button>
                        </div>
                    </div>
                    <div class="logs-container" id="recent-logs">
                        <div class="log-entry">
                            <span class="log-time">[10:30:15]</span>
                            <span class="log-level info">INFO</span>
                            Server cluster auto-scaling activated
                        </div>
                        <div class="log-entry">
                            <span class="log-time">[10:29:45]</span>
                            <span class="log-level info">INFO</span>
                            Database backup completed successfully
                        </div>
                        <div class="log-entry">
                            <span class="log-time">[10:28:30]</span>
                            <span class="log-level warn">WARN</span>
                            High CPU usage detected on Server-03
                        </div>
                        <div class="log-entry">
                            <span class="log-time">[10:27:12]</span>
                            <span class="log-level info">INFO</span>
                            SSL certificate renewed automatically
                        </div>
                        <div class="log-entry">
                            <span class="log-time">[10:26:08]</span>
                            <span class="log-level info">INFO</span>
                            Load balancer health check passed
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <!-- Servers Page -->
        <div class="page-content" id="page-servers">
            <div class="page-header">
                <h1>Server Management</h1>
                <p>Quản lý và giám sát các máy chủ trong hệ thống</p>
                <button class="btn btn-primary" onclick="addNewServer()">+ Thêm Server</button>
            </div>

            <div class="card">
                <div class="card-header">
                    <h3 class="card-title">🖥️ Server List</h3>
                    <div class="card-actions">
                        <button class="btn-icon" onclick="refreshServerList()">🔄</button>
                        <button class="btn-icon" onclick="exportServerData()">📊</button>
                    </div>
                </div>
                <div class="table-container">
                    <table class="data-table">
                        <thead>
                            <tr>
                                <th>Server Name</th>
                                <th>IP Address</th>
                                <th>Status</th>
                                <th>CPU</th>
                                <th>Memory</th>
                                <th>Uptime</th>
                                <th>Actions</th>
                            </tr>
                        </thead>
                        <tbody id="server-table-body">
                            <tr>
                                <td>Web-Server-01</td>
                                <td>192.168.1.10</td>
                                <td><span class="status-indicator"><span class="status-dot online"></span>Online</span></td>
                                <td>45%</td>
                                <td>68%</td>
                                <td>15d 4h</td>
                                <td>
                                    <button class="btn-icon" onclick="editServer('lb-01')">✏️</button>
                                    <button class="btn-icon" onclick="restartServer('lb-01')">🔄</button>
                                    <button class="btn-icon" onclick="deleteServer('lb-01')">🗑️</button>
                                </td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>
        </div>

        <!-- Services Page -->
        <div class="page-content" id="page-services">
            <div class="page-header">
                <h1>Service Management</h1>
                <p>Quản lý các dịch vụ cloud và ứng dụng</p>
                <button class="btn btn-primary" onclick="deployNewService()">🚀 Deploy Service</button>
            </div>

            <div class="grid-2">
                <div class="card">
                    <div class="card-header">
                        <h3 class="card-title">⚙️ Running Services</h3>
                    </div>
                    <div class="metric-row">
                        <span class="metric-label">Docker Containers</span>
                        <span class="metric-value">24/30</span>
                    </div>
                    <div class="metric-row">
                        <span class="metric-label">Kubernetes Pods</span>
                        <span class="metric-value">18/25</span>
                    </div>
                    <div class="metric-row">
                        <span class="metric-label">Microservices</span>
                        <span class="metric-value">12</span>
                    </div>
                    <div class="metric-row">
                        <span class="metric-label">API Endpoints</span>
                        <span class="metric-value">45</span>
                    </div>
                </div>
                
                <div class="card">
                    <div class="card-header">
                        <h3 class="card-title">📊 Service Health</h3>
                    </div>
                    <div class="metric-row">
                        <span class="metric-label">API Gateway</span>
                        <span class="status-indicator"><span class="status-dot online"></span>Healthy</span>
                    </div>
                    <div class="metric-row">
                        <span class="metric-label">Authentication Service</span>
                        <span class="status-indicator"><span class="status-dot online"></span>Healthy</span>
                    </div>
                    <div class="metric-row">
                        <span class="metric-label">Payment Gateway</span>
                        <span class="status-indicator"><span class="status-dot warning"></span>Degraded</span>
                    </div>
                    <div class="metric-row">
                        <span class="metric-label">Notification Service</span>
                        <span class="status-indicator"><span class="status-dot online"></span>Healthy</span>
                    </div>
                </div>
            </div>
        </div>

        <!-- Storage Page -->
        <div class="page-content" id="page-storage">
            <div class="page-header">
                <h1>Storage Management</h1>
                <p>Quản lý không gian lưu trữ và backup</p>
                <button class="btn btn-primary" onclick="createBackup()">💾 Create Backup</button>
            </div>

            <div class="quick-stats">
                <div class="stat-card">
                    <div class="stat-value">2.4TB</div>
                    <div class="stat-label">Total Storage</div>
                </div>
                <div class="stat-card">
                    <div class="stat-value">1.8TB</div>
                    <div class="stat-label">Used Space</div>
                </div>
                <div class="stat-card">
                    <div class="stat-value">600GB</div>
                    <div class="stat-label">Available</div>
                </div>
                <div class="stat-card">
                    <div class="stat-value">12</div>
                    <div class="stat-label">Backup Points</div>
                </div>
            </div>

            <div class="card">
                <div class="card-header">
                    <h3 class="card-title">💾 Storage Volumes</h3>
                </div>
                <div class="table-container">
                    <table class="data-table">
                        <thead>
                            <tr>
                                <th>Volume Name</th>
                                <th>Type</th>
                                <th>Size</th>
                                <th>Used</th>
                                <th>Mount Point</th>
                                <th>Actions</th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr>
                                <td>system-root</td>
                                <td>SSD</td>
                                <td>500GB</td>
                                <td>45%</td>
                                <td>/</td>
                                <td><button class="btn-icon">⚙️</button></td>
                            </tr>
                            <tr>
                                <td>data-storage</td>
                                <td>HDD</td>
                                <td>2TB</td>
                                <td>78%</td>
                                <td>/data</td>
                                <td><button class="btn-icon">⚙️</button></td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>
        </div>

        <!-- Database Page -->
        <div class="page-content" id="page-database">
            <div class="page-header">
                <h1>Database Management</h1>
                <p>Quản lý cơ sở dữ liệu và performance</p>
                <button class="btn btn-primary" onclick="createDatabase()">🗄️ New Database</button>
            </div>

            <div class="grid-2">
                <div class="card">
                    <div class="card-header">
                        <h3 class="card-title">🗄️ Database Status</h3>
                    </div>
                    <div class="metric-row">
                        <span class="metric-label">MySQL Primary</span>
                        <span class="status-indicator"><span class="status-dot online"></span>Online</span>
                    </div>
                    <div class="metric-row">
                        <span class="metric-label">MySQL Replica</span>
                        <span class="status-indicator"><span class="status-dot online"></span>Online</span>
                    </div>
                    <div class="metric-row">
                        <span class="metric-label">Redis Cache</span>
                        <span class="status-indicator"><span class="status-dot online"></span>Online</span>
                    </div>
                    <div class="metric-row">
                        <span class="metric-label">MongoDB</span>
                        <span class="status-indicator"><span class="status-dot warning"></span>Slow Query</span>
                    </div>
                </div>
                
                <div class="card">
                    <div class="card-header">
                        <h3 class="card-title">📈 Performance Metrics</h3>
                    </div>
                    <div class="metric-row">
                        <span class="metric-label">Queries/sec</span>
                        <span class="metric-value">1,247</span>
                    </div>
                    <div class="metric-row">
                        <span class="metric-label">Connections</span>
                        <span class="metric-value">45/100</span>
                    </div>
                    <div class="metric-row">
                        <span class="metric-label">Cache Hit Rate</span>
                        <span class="metric-value">94.5%</span>
                    </div>
                    <div class="metric-row">
                        <span class="metric-label">Replication Lag</span>
                        <span class="metric-value">2ms</span>
                    </div>
                </div>
            </div>
        </div>

        <!-- Security Page -->
        <div class="page-content" id="page-security">
            <div class="page-header">
                <h1>Security Center</h1>
                <p>Giám sát bảo mật và quản lý access control</p>
                <div class="alert alert-warning">
                    <strong>Cảnh báo:</strong> Phát hiện 3 lần đăng nhập thất bại từ IP 192.168.1.100
                </div>
            </div>

            <div class="grid-2">
                <div class="card">
                    <div class="card-header">
                        <h3 class="card-title">🔒 Security Status</h3>
                    </div>
                    <div class="metric-row">
                        <span class="metric-label">Firewall Status</span>
                        <span class="status-indicator"><span class="status-dot online"></span>Active</span>
                    </div>
                    <div class="metric-row">
                        <span class="metric-label">SSL Certificates</span>
                        <span class="status-indicator"><span class="status-dot online"></span>Valid</span>
                    </div>
                    <div class="metric-row">
                        <span class="metric-label">Antivirus</span>
                        <span class="status-indicator"><span class="status-dot online"></span>Updated</span>
                    </div>
                    <div class="metric-row">
                        <span class="metric-label">Intrusion Detection</span>
                        <span class="status-indicator"><span class="status-dot warning"></span>3 Alerts</span>
                    </div>
                </div>
                
                <div class="card">
                    <div class="card-header">
                        <h3 class="card-title">👥 Access Control</h3>
                    </div>
                    <div class="metric-row">
                        <span class="metric-label">Active Users</span>
                        <span class="metric-value">24</span>
                    </div>
                    <div class="metric-row">
                        <span class="metric-label">Admin Sessions</span>
                        <span class="metric-value">3</span>
                    </div>
                    <div class="metric-row">
                        <span class="metric-label">Failed Logins (24h)</span>
                        <span class="metric-value">12</span>
                    </div>
                    <div class="metric-row">
                        <span class="metric-label">2FA Enabled</span>
                        <span class="metric-value">18/24</span>
                    </div>
                </div>
            </div>
        </div>

        <!-- Settings Page -->
        <div class="page-content" id="page-settings">
            <div class="page-header">
                <h1>System Settings</h1>
                <p>Cấu hình hệ thống và tùy chỉnh</p>
            </div>

            <div class="card">
                <div class="card-header">
                    <h3 class="card-title">⚙️ General Settings</h3>
                </div>
                <form id="settings-form">
                    <div class="form-group">
                        <label class="form-label">System Name</label>
                        <input type="text" class="form-input" value="Cloud Pro System" />
                    </div>
                    <div class="form-group">
                        <label class="form-label">Admin Email</label>
                        <input type="email" class="form-input" value="admin@cloudpro.com" />
                    </div>
                    <div class="form-group">
                        <label class="form-label">Monitoring Interval (seconds)</label>
                        <input type="number" class="form-input" value="30" />
                    </div>
                    <div class="form-group">
                        <label class="form-label">Auto Backup</label>
                        <select class="form-input">
                            <option>Daily</option>
                            <option>Weekly</option>
                            <option>Monthly</option>
                        </select>
                    </div>
                    <button type="submit" class="btn btn-primary">💾 Save Settings</button>
                </form>
            </div>
        </div>
    </div>

    <!-- Modals -->
    <div class="modal" id="notification-modal">
        <div class="modal-content">
            <div class="modal-header">
                <h3 class="modal-title">🔔 Notifications</h3>
                <button class="modal-close" onclick="closeModal('notification-modal')">&times;</button>
            </div>
            <div class="log-entry">
                <span class="log-time">[10:25:30]</span>
                <span class="log-level warn">WARN</span>
                High CPU usage on Server-03
            </div>
            <div class="log-entry">
                <span class="log-time">[10:20:15]</span>
                <span class="log-level info">INFO</span>
                Backup completed successfully
            </div>
            <div class="log-entry">
                <span class="log-time">[10:15:45]</span>
                <span class="log-level error">ERROR</span>
                Failed login attempt detected
            </div>
        </div>
    </div>

    <script>
        // Navigation and UI Functions
        function toggleSidebar() {
            const sidebar = document.getElementById('sidebar');
            const mainContent = document.getElementById('mainContent');
            sidebar.classList.toggle('collapsed');
            mainContent.classList.toggle('expanded');
        }

        function showPage(pageId) {
            // Hide all pages
            document.querySelectorAll('.page-content').forEach(page => {
                page.classList.remove('active');
            });
            
            // Show selected page
            document.getElementById('page-' + pageId).classList.add('active');
            
            // Update breadcrumb
            const pageNames = {
                'dashboard': 'Dashboard',
                'servers': 'Server Management',
                'services': 'Service Management',
                'storage': 'Storage Management',
                'network': 'Network Management',
                'database': 'Database Management',
                'security': 'Security Center',
                'logs': 'System Logs',
                'billing': 'Billing & Usage',
                'settings': 'System Settings'
            };
            document.getElementById('breadcrumb').textContent = pageNames[pageId];
            
            // Update active nav item
            document.querySelectorAll('.nav-item').forEach(item => {
                item.classList.remove('active');
            });
            document.querySelector(`[data-page="${pageId}"]`).classList.add('active');
        }

        // Event listeners for navigation
        document.querySelectorAll('.nav-item').forEach(item => {
            item.addEventListener('click', (e) => {
                e.preventDefault();
                const pageId = item.getAttribute('data-page');
                showPage(pageId);
            });
        });

        // Modal Functions
        function showModal(modalId) {
            document.getElementById(modalId).classList.add('show');
        }

        function closeModal(modalId) {
            document.getElementById(modalId).classList.remove('show');
        }

        function showNotifications() {
            showModal('notification-modal');
        }

        function showUserMenu() {
            alert('User menu functionality coming soon!');
        }

        // Data Update Functions
        function updateMetrics() {
            // CPU Usage
            const cpuUsage = Math.floor(Math.random() * 40) + 30;
            document.getElementById('cpu-usage').textContent = cpuUsage + '%';
            document.getElementById('cpu-progress').style.width = cpuUsage + '%';

            // Memory Usage
            const memoryUsage = Math.floor(Math.random() * 50) + 40;
            document.getElementById('memory-usage').textContent = memoryUsage + '%';
            document.getElementById('memory-progress').style.width = memoryUsage + '%';

            // Storage Usage
            const storageUsage = Math.floor(Math.random() * 30) + 30;
            document.getElementById('storage-usage').textContent = storageUsage + '%';
            document.getElementById('storage-progress').style.width = storageUsage + '%';

            // Network Traffic
            const inbound = (Math.random() * 3 + 1).toFixed(1);
            const outbound = (Math.random() * 2 + 1).toFixed(1);
            const connections = Math.floor(Math.random() * 500) + 1000;
            const responseTime = Math.floor(Math.random() * 50) + 50;

            document.getElementById('inbound-traffic').textContent = inbound + ' GB/h';
            document.getElementById('outbound-traffic').textContent = outbound + ' GB/h';
            document.getElementById('active-connections').textContent = connections.toLocaleString();
            document.getElementById('response-time').textContent = responseTime + 'ms';

            // Quick Stats
            document.getElementById('total-servers').textContent = Math.floor(Math.random() * 5) + 10;
            document.getElementById('active-services').textContent = Math.floor(Math.random() * 3) + 7;
        }

        function addLogEntry() {
            const logContainer = document.getElementById('recent-logs');
            const now = new Date();
            const timeStr = now.toTimeString().split(' ')[0];
            
            const logTypes = ['info', 'warn', 'error'];
            const logMessages = [
                'System health check completed',
                'Database connection pool refreshed',
                'Cache cleared successfully',
                'Security scan completed',
                'Backup verification successful',
                'SSL certificate renewed',
                'Load balancer configuration updated',
                'High memory usage detected',
                'Network latency spike detected',
                'Failed authentication attempt'
            ];
            
            const randomType = logTypes[Math.floor(Math.random() * logTypes.length)];
            const randomMessage = logMessages[Math.floor(Math.random() * logMessages.length)];
            
            const logEntry = document.createElement('div');
            logEntry.className = 'log-entry';
            logEntry.innerHTML = `
                <span class="log-time">[${timeStr}]</span>
                <span class="log-level ${randomType}">${randomType.toUpperCase()}</span>
                ${randomMessage}
            `;
            
            logContainer.insertBefore(logEntry, logContainer.firstChild);
            
            // Keep only last 10 entries
            while (logContainer.children.length > 10) {
                logContainer.removeChild(logContainer.lastChild);
            }
        }

        // Action Functions
        function refreshMetrics() {
            updateMetrics();
            alert('Metrics updated successfully!');
        }

        function refreshServices() {
            alert('Services status refreshed!');
        }

        function addNewServer() {
            const serverName = prompt('Enter server name:');
            if (serverName) {
                alert(`Server "${serverName}" will be added to the system.`);
            }
        }

        function editServer(serverId) {
            alert(`Editing server: ${serverId}`);
        }

        function restartServer(serverId) {
            if (confirm(`Are you sure you want to restart ${serverId}?`)) {
                alert(`Server ${serverId} is being restarted...`);
            }
        }

        function deleteServer(serverId) {
            if (confirm(`Are you sure you want to delete ${serverId}? This action cannot be undone.`)) {
                alert(`Server ${serverId} has been scheduled for deletion.`);
            }
        }

        function deployNewService() {
            alert('Service deployment wizard will open here.');
        }

        function createBackup() {
            alert('Creating new backup... This may take several minutes.');
        }

        function createDatabase() {
            alert('Database creation wizard will open here.');
        }

        // Auto-update functions
        setInterval(updateMetrics, 30000); // Update every 30 seconds
        setInterval(addLogEntry, 20000);   // Add log entry every 20 seconds

        // Settings form handler
        document.getElementById('settings-form').addEventListener('submit', (e) => {
            e.preventDefault();
            alert('Settings saved successfully!');
        });

        // Mobile responsiveness
        function handleResize() {
            if (window.innerWidth <= 768) {
                document.getElementById('sidebar').classList.add('collapsed');
                document.getElementById('mainContent').classList.add('expanded');
            }
        }

        window.addEventListener('resize', handleResize);
        handleResize(); // Check on load

        // Initialize
        updateMetrics();
        console.log('🚀 Advanced Cloud Computing Platform loaded successfully!');
    </script>
</body>
</html> onclick="editServer('web-01')">✏️</button>
                                    <button class="btn-icon" onclick="restartServer('web-01')">🔄</button>
                                    <button class="btn-icon" onclick="deleteServer('web-01')">🗑️</button>
                                </td>
                            </tr>
                            <tr>
                                <td>DB-Server-01</td>
                                <td>192.168.1.20</td>
                                <td><span class="status-indicator"><span class="status-dot online"></span>Online</span></td>
                                <td>32%</td>
                                <td>78%</td>
                                <td>22d 8h</td>
                                <td>
                                    <button class="btn-icon" onclick="editServer('db-01')">✏️</button>
                                    <button class="btn-icon" onclick="restartServer('db-01')">🔄</button>
                                    <button class="btn-icon" onclick="deleteServer('db-01')">🗑️</button>
                                </td>
                            </tr>
                            <tr>
                                <td>Load-Balancer-01</td>
                                <td>192.168.1.30</td>
                                <td><span class="status-indicator"><span class="status-dot warning"></span>Warning</span></td>
                                <td>78%</td>
                                <td>45%</td>
                                <td>8d 12h</td>
                                <td>
                                    <button class="btn-icon"
