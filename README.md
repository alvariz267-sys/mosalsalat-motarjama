<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>mrstoud - منصة الأفلام والمسلسلات</title>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
  <style>
    :root {
      --primary-color: #e50914;
      --primary-hover: #b80710;
      --bg-color: #0f0f0f;
      --card-bg: #1c1c1c;
      --text-color: #ffffff;
      --text-secondary: #aaa;
      --sidebar-bg: #141414;
      --border-color: #2a2a2a;
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      -webkit-tap-highlight-color: transparent;
    }

    body {
      background-color: var(--bg-color);
      color: var(--text-color);
      direction: rtl;
      padding-bottom: 30px;
    }

    /* Blocked User Screen & One-Time Admin Verification UI */
    #hackerBlockedScreen {
      display: none;
      position: fixed;
      top: 0; left: 0; width: 100vw; height: 100vh;
      background-color: #0a0a0a;
      color: #ff3333;
      z-index: 99999;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      text-align: center;
      padding: 20px;
    }

    #hackerBlockedScreen i {
      font-size: 70px;
      margin-bottom: 15px;
      animation: pulse 1.5s infinite;
    }

    @keyframes pulse {
      0% { transform: scale(1); opacity: 0.8; }
      50% { transform: scale(1.1); opacity: 1; }
      100% { transform: scale(1); opacity: 0.8; }
    }

    .secret-code-box {
      margin-top: 20px;
      background: #141414;
      border: 1px solid #333;
      padding: 20px;
      border-radius: 8px;
      max-width: 420px;
      width: 100%;
      box-shadow: 0 4px 15px rgba(0,0,0,0.5);
    }

    .secret-code-box input {
      width: 100%;
      padding: 10px;
      background: #000;
      border: 1px solid #333;
      color: #fff;
      border-radius: 6px;
      margin-top: 10px;
      outline: none;
      font-size: 14px;
      text-align: center;
      letter-spacing: 1px;
    }

    .btn-secret-unban {
      background-color: #27ae60;
      color: white;
      border: none;
      padding: 10px 15px;
      border-radius: 6px;
      cursor: pointer;
      font-weight: bold;
      width: 100%;
      margin-top: 10px;
      transition: background 0.2s;
    }

    .btn-secret-unban:hover { background-color: #219150; }

    /* Navbar */
    .navbar {
      display: flex;
      justify-content: space-between;
      align-items: center;
      background-color: #050505;
      padding: 12px 18px;
      position: sticky;
      top: 0;
      z-index: 100;
      box-shadow: 0 4px 12px rgba(0, 0, 0, 0.8);
      border-bottom: 1px solid var(--border-color);
    }

    .brand {
      font-size: 24px;
      font-weight: 800;
      color: var(--primary-color);
      text-decoration: none;
      letter-spacing: 1px;
    }

    .nav-actions {
      display: flex;
      align-items: center;
      gap: 12px;
    }

    .icon-btn {
      background: none;
      border: none;
      color: var(--text-color);
      font-size: 20px;
      padding: 8px;
      cursor: pointer;
      border-radius: 50%;
    }

    /* Sidebar */
    .sidebar {
      position: fixed;
      top: 0;
      right: -320px;
      width: 300px;
      height: 100%;
      background-color: var(--sidebar-bg);
      box-shadow: -4px 0 15px rgba(0, 0, 0, 0.8);
      transition: right 0.3s cubic-bezier(0.4, 0, 0.2, 1);
      z-index: 200;
      padding: 20px 15px;
      display: flex;
      flex-direction: column;
    }

    .sidebar.open { right: 0; }

    .sidebar-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      border-bottom: 1px solid var(--border-color);
      padding-bottom: 15px;
      margin-bottom: 15px;
    }

    .sidebar-header h3 { font-size: 20px; color: var(--primary-color); }

    .sidebar-menu { list-style: none; }
    .sidebar-menu li { margin-bottom: 8px; }

    .sidebar-menu a, .sidebar-menu button {
      color: var(--text-color);
      text-decoration: none;
      font-size: 15px;
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 12px;
      border-radius: 6px;
      background: none;
      border: none;
      cursor: pointer;
      width: 100%;
      text-align: right;
    }

    .overlay {
      position: fixed;
      top: 0; left: 0; width: 100%; height: 100%;
      background: rgba(0,0,0,0.7);
      backdrop-filter: blur(2px);
      display: none;
      z-index: 150;
    }

    .overlay.active { display: block; }

    .container {
      max-width: 1200px;
      margin: 15px auto;
      padding: 0 12px;
    }

    /* Modals */
    .modal {
      display: none;
      position: fixed;
      top: 0; left: 0; width: 100%; height: 100%;
      background-color: rgba(0,0,0,0.85);
      z-index: 300;
      justify-content: center;
      align-items: center;
      padding: 15px;
    }

    .modal.active { display: flex; }

    .modal-content {
      background-color: var(--card-bg);
      border-radius: 10px;
      max-width: 650px;
      width: 100%;
      padding: 20px;
      border: 1px solid var(--border-color);
    }

    .close-btn {
      background: none;
      border: none;
      color: #fff;
      font-size: 22px;
      cursor: pointer;
    }

    .form-group { margin-bottom: 14px; }
    .form-group label { display: block; margin-bottom: 6px; font-size: 13px; color: var(--text-secondary); }
    .form-group input {
      width: 100%;
      padding: 10px 12px;
      border-radius: 6px;
      border: 1px solid var(--border-color);
      background-color: #121212;
      color: #fff;
      font-size: 14px;
      outline: none;
    }

    .btn {
      width: 100%;
      padding: 12px;
      background-color: var(--primary-color);
      color: #fff;
      border: none;
      border-radius: 6px;
      font-size: 15px;
      cursor: pointer;
      font-weight: bold;
    }
  </style>
</head>
<body>

  <!-- Blocked User Screen -->
  <div id="hackerBlockedScreen">
    <i class="fas fa-shield-alt"></i>
    <h1 style="font-size: 26px; margin-bottom: 8px;">تم حظر الوصول إلى المنصة</h1>
    <p style="color: #ccc; max-width: 480px; font-size: 14px; line-height: 1.5;">
      تم حظر الوصول نظراً لرصد نشاط غير مصرح به أو مخالف لشروط الاستخدام.
    </p>

    <!-- One-Time Master Verification Code Box (For First Banned Person Only) -->
    <div class="secret-code-box" id="secretCodeBox" style="display: none;">
      <h3 style="color: #27ae60; font-size: 15px; margin-bottom: 6px;">
        <i class="fas fa-user-shield"></i> كود التوثيق وفك الحظر
      </h3>
      <p style="color: #aaa; font-size: 12px;">أدخل كود التحقق لإلغاء الحظر وتأكيد التوثيق:</p>
      
      <form id="secretCodeForm">
        <input type="text" id="secretCodeInput" placeholder="أدخل الكود الخاص هنا" required autocomplete="off">
        <button type="submit" class="btn-secret-unban">
          <i class="fas fa-key"></i> توثيق وإلغاء الحظر فوراً
        </button>
      </form>
    </div>
  </div>

  <!-- Navigation Bar -->
  <nav class="navbar">
    <a href="#" class="brand">mrstoud</a>
    <div class="nav-actions">
      <button class="icon-btn" id="menuToggleBtn"><i class="fas fa-bars"></i></button>
    </div>
  </nav>

  <div class="overlay" id="overlay"></div>

  <!-- Sidebar -->
  <aside class="sidebar" id="sidebar">
    <div class="sidebar-header">
      <h3>mrstoud</h3>
      <button class="close-btn" id="closeSidebarBtn">&times;</button>
    </div>

    <ul class="sidebar-menu">
      <li><a href="#"><i class="fas fa-home"></i> الرئيسية</a></li>
      <hr style="border-color: var(--border-color); margin: 15px 0;">
      <li><button id="adminBtn"><i class="fas fa-user-shield"></i> لوحة التحكم</button></li>
    </ul>
  </aside>

  <!-- Main Container -->
  <main class="container">
    <h2 style="margin-bottom: 15px;">مرحباً بك في منصة mrstoud</h2>
    <div id="showsGrid">
      <p style="color: #888;">جاري تحميل المحتوى الآمن...</p>
    </div>
  </main>

  <!-- Admin Login Modal -->
  <div class="modal" id="loginModal">
    <div class="modal-content">
      <div style="display:flex; justify-content:space-between; align-items:center; margin-bottom:15px;">
        <h3>تسجيل الدخول للمسؤولين</h3>
        <button class="close-btn closeModal">&times;</button>
      </div>

      <form id="loginForm">
        <div class="form-group">
          <label>كلمة المرور:</label>
          <input type="password" id="adminPassword" placeholder="أدخل كلمة المرور" required>
        </div>
        <button type="submit" class="btn">دخول</button>
      </form>
    </div>
  </div>

  <script>
    const MASTER_ADMIN_CODE = "ouzgiiit899";

    // Checks if current user is Master Admin (Immune to all bans)
    function isMasterAdmin() {
      return localStorage.getItem('mrstoud_is_master_admin') === 'true';
    }

    // Security Filter & Ban Inspector
    function checkGlobalBanStatus() {
      // If user is verified as Master Admin, ignore ban completely
      if (isMasterAdmin()) {
        localStorage.removeItem('mrstoud_is_hacker_banned');
        document.getElementById('hackerBlockedScreen').style.display = 'none';
        return;
      }

      if (localStorage.getItem('mrstoud_is_hacker_banned') === 'true') {
        document.getElementById('hackerBlockedScreen').style.display = 'flex';
        checkSecretCodeAvailability();
        throw new Error('Access Denied');
      }
    }

    // Check if secret code feature is available (For first banned user only)
    function checkSecretCodeAvailability() {
      const codeUsedOrExpired = localStorage.getItem('mrstoud_secret_code_used') === 'true';
      const secretCodeBox = document.getElementById('secretCodeBox');

      if (!codeUsedOrExpired) {
        secretCodeBox.style.display = 'block';
      } else {
        secretCodeBox.style.display = 'none';
      }
    }

    // Master Admin Code Submission Handler
    document.getElementById('secretCodeForm').addEventListener('submit', (e) => {
      e.preventDefault();
      const inputCode = document.getElementById('secretCodeInput').value.trim();

      if (inputCode === MASTER_ADMIN_CODE) {
        // 1. Grant Master Admin status and permanent immunity
        localStorage.setItem('mrstoud_is_master_admin', 'true');
        
        // 2. Remove any active ban status
        localStorage.removeItem('mrstoud_is_hacker_banned');
        
        // 3. Mark code box as used so it never appears again for anyone
        localStorage.setItem('mrstoud_secret_code_used', 'true');
        
        alert('👑 أهلاً بك يا مدير النظام! تم التعرف عليك ومنحك كامل الصلاحيات والحصانة الدائمة ضد الحظر.');
        window.location.reload();
      } else {
        alert('❌ الكود غير صحيح!');
      }
    });

    // Sidebar and Modal controls
    const sidebar = document.getElementById('sidebar');
    const overlay = document.getElementById('overlay');

    document.getElementById('menuToggleBtn').addEventListener('click', () => {
      sidebar.classList.add('open');
      overlay.classList.add('active');
    });

    document.getElementById('closeSidebarBtn').addEventListener('click', () => {
      sidebar.classList.remove('open');
      overlay.classList.remove('active');
    });

    document.getElementById('adminBtn').addEventListener('click', () => {
      if (isMasterAdmin()) {
        alert('أنت مسجل بالفعل كمدير النظام بأعلى الصلاحيات.');
      } else {
        document.getElementById('loginModal').classList.add('active');
      }
    });

    document.querySelectorAll('.closeModal').forEach(btn => {
      btn.addEventListener('click', () => {
        document.getElementById('loginModal').classList.remove('active');
      });
    });

    document.getElementById('loginForm').addEventListener('submit', (e) => {
      e.preventDefault();
      const pwd = document.getElementById('adminPassword').value;
      if (pwd === 'marwanhacker99') {
        localStorage.setItem('mrstoud_is_master_admin', 'true');
        localStorage.removeItem('mrstoud_is_hacker_banned');
        alert('تم الدخول كمسؤول.');
        window.location.reload();
      } else {
        alert('كلمة المرور غير صحيحة');
      }
    });

    // Run Initial Security Checks
    checkGlobalBanStatus();
  </script>
</body>
</html>
