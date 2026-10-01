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
      --success-color: #27ae60;
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

    /* Screen for Blocked Users */
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
    }

    .btn-secret-unban {
      background-color: var(--success-color);
      color: white;
      border: none;
      padding: 10px 15px;
      border-radius: 6px;
      cursor: pointer;
      font-weight: bold;
      width: 100%;
      margin-top: 10px;
    }

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
    }

    .nav-actions {
      display: flex;
      align-items: center;
      gap: 10px;
    }

    .icon-btn {
      background: none;
      border: none;
      color: var(--text-color);
      font-size: 20px;
      padding: 8px;
      cursor: pointer;
    }

    .btn-switch-mode {
      background-color: #2980b9;
      color: white;
      border: none;
      padding: 8px 14px;
      border-radius: 20px;
      cursor: pointer;
      font-size: 13px;
      font-weight: bold;
      display: none; /* Shows for Admin Only */
      align-items: center;
      gap: 6px;
    }

    .btn-switch-mode:hover { background-color: #3498db; }

    /* Sidebar */
    .sidebar {
      position: fixed;
      top: 0;
      right: -320px;
      width: 300px;
      height: 100%;
      background-color: var(--sidebar-bg);
      box-shadow: -4px 0 15px rgba(0, 0, 0, 0.8);
      transition: right 0.3s ease;
      z-index: 200;
      padding: 20px 15px;
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

    .sidebar-menu { list-style: none; }
    .sidebar-menu li { margin-bottom: 8px; }

    .sidebar-menu button, .sidebar-menu a {
      color: var(--text-color);
      text-decoration: none;
      font-size: 15px;
      display: flex;
      align-items: center;
      gap: 10px;
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
      display: none;
      z-index: 150;
    }

    .overlay.active { display: block; }

    .container {
      max-width: 1200px;
      margin: 15px auto;
      padding: 0 12px;
    }

    /* Modals & Admin Panel */
    .modal {
      display: none;
      position: fixed;
      top: 0; left: 0; width: 100%; height: 100%;
      background-color: rgba(0,0,0,0.85);
      z-index: 300;
      justify-content: center;
      align-items: center;
      padding: 15px;
      overflow-y: auto;
    }

    .modal.active { display: flex; }

    .modal-content {
      background-color: var(--card-bg);
      border-radius: 10px;
      max-width: 750px;
      width: 100%;
      padding: 20px;
      border: 1px solid var(--border-color);
      max-height: 90vh;
      overflow-y: auto;
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
    .form-group input, .form-group textarea, .form-group select {
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

    /* Admin Panel Tabs */
    .admin-tabs {
      display: flex;
      gap: 8px;
      border-bottom: 1px solid var(--border-color);
      padding-bottom: 10px;
      margin-bottom: 15px;
      overflow-x: auto;
    }

    .admin-tab-btn {
      background: #111;
      border: 1px solid var(--border-color);
      color: #ccc;
      padding: 8px 12px;
      border-radius: 6px;
      cursor: pointer;
      font-size: 13px;
      white-space: nowrap;
    }

    .admin-tab-btn.active {
      background: var(--primary-color);
      color: white;
      border-color: var(--primary-color);
    }

    .tab-content { display: none; }
    .tab-content.active { display: block; }

    /* Admin List Styles */
    .data-table {
      width: 100%;
      border-collapse: collapse;
      margin-top: 10px;
      font-size: 13px;
    }

    .data-table th, .data-table td {
      border: 1px solid var(--border-color);
      padding: 8px 10px;
      text-align: right;
    }

    .data-table th { background: #111; color: var(--primary-color); }

    .action-btn-small {
      padding: 4px 8px;
      border-radius: 4px;
      border: none;
      cursor: pointer;
      font-size: 11px;
      color: #fff;
    }
    .btn-danger { background-color: #e74c3c; }
    .btn-success { background-color: #2ecc71; }

    /* Shows Cards Layout */
    .shows-grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(260px, 1fr));
      gap: 20px;
      margin-top: 15px;
    }

    .show-card {
      background: var(--card-bg);
      border-radius: 8px;
      overflow: hidden;
      border: 1px solid var(--border-color);
    }

    .show-card video, .show-card img {
      width: 100%;
      height: 200px;
      object-fit: cover;
      background-color: #000;
    }

    .show-info { padding: 12px; }
    .show-title { font-size: 16px; font-weight: bold; margin-bottom: 5px; }
    
    /* Comment Section for User View */
    .comments-box {
      margin-top: 10px;
      border-top: 1px solid var(--border-color);
      padding-top: 10px;
    }

    .comment-item {
      background: #111;
      padding: 6px 10px;
      border-radius: 4px;
      font-size: 12px;
      margin-bottom: 5px;
    }

    .comment-input-group {
      display: flex;
      gap: 5px;
      margin-top: 8px;
    }

    .comment-input-group input {
      flex: 1;
      padding: 6px;
      background: #000;
      border: 1px solid var(--border-color);
      color: #fff;
      border-radius: 4px;
      font-size: 12px;
    }

    .comment-input-group button {
      padding: 6px 10px;
      background: var(--primary-color);
      color: #fff;
      border: none;
      border-radius: 4px;
      cursor: pointer;
      font-size: 12px;
    }

    /* Privacy Policy Section */
    .privacy-section {
      background-color: var(--card-bg);
      padding: 25px;
      border-radius: 8px;
      margin-top: 40px;
      border: 1px solid var(--border-color);
      line-height: 1.6;
    }

    .privacy-section h3 {
      color: var(--primary-color);
    }
  </style>
</head>
<body>

  <!-- Blocked Screen -->
  <div id="hackerBlockedScreen">
    <i class="fas fa-shield-alt"></i>
    <h1 style="font-size: 26px; margin-bottom: 8px;">تم حظر الوصول إلى المنصة</h1>
    <p style="color: #ccc; max-width: 480px; font-size: 14px;">
      تم حظر الوصول نظراً لرصد نشاط غير مصرح به.
    </p>

    <div class="secret-code-box" id="secretCodeBox" style="display: none;">
      <h3 style="color: #27ae60; font-size: 15px; margin-bottom: 6px;">
        <i class="fas fa-user-shield"></i> كود توثيق المدير
      </h3>
      <p style="color: #aaa; font-size: 12px;">أدخل الكود الخاص لفك الحظر وتوثيق صلاحيات المدير:</p>
      
      <form id="secretCodeForm">
        <input type="text" id="secretCodeInput" placeholder="أدخل الكود هنا" required autocomplete="off">
        <button type="submit" class="btn-secret-unban">
          <i class="fas fa-key"></i> توثيق وإلغاء الحظر
        </button>
      </form>
    </div>
  </div>

  <!-- Navbar -->
  <nav class="navbar">
    <a href="#" class="brand">mrstoud</a>
    <div class="nav-actions">
      <!-- Admin Mode Switcher Button -->
      <button class="btn-switch-mode" id="toggleAdminModeBtn" onclick="toggleAdminUserMode()">
        <i class="fas fa-exchange-alt"></i> <span id="modeBtnText">التحول للوحة التحكم</span>
      </button>

      <button class="icon-btn" id="menuToggleBtn"><i class="fas fa-bars"></i></button>
    </div>
  </nav>

  <div class="overlay" id="overlay"></div>

  <!-- Sidebar -->
  <aside class="sidebar" id="sidebar">
    <div class="sidebar-header">
      <h3 style="color: var(--primary-color);">mrstoud</h3>
      <button class="close-btn" id="closeSidebarBtn">&times;</button>
    </div>

    <ul class="sidebar-menu">
      <li><a href="#gallery"><i class="fas fa-film"></i> الأفلام والمسلسلات</a></li>
      <li><a href="#privacy"><i class="fas fa-user-lock"></i> سياسة الخصوصية</a></li>
      <hr style="border-color: var(--border-color); margin: 15px 0;">
      <li><button id="adminBtn"><i class="fas fa-user-shield"></i> لوحة التحكم (للمدير)</button></li>
    </ul>
  </aside>

  <!-- Main Grid View (User Mode View) -->
  <main class="container" id="userViewSection">
    <h2 style="margin-bottom: 15px;"><i class="fas fa-play-circle"></i> قائمة الأفلام والمسلسلات</h2>
    <div class="shows-grid" id="showsGrid">
      <!-- Displays dynamic items and comment section -->
    </div>

    <!-- Privacy Policy Section -->
    <section id="privacy" class="privacy-section">
      <h3 style="margin-bottom: 10px;"><i class="fas fa-shield-alt"></i> سياسة الخصوصية</h3>
      <p>مرحباً بك في منصتنا. نحن نحترم خصوصيتك ونلتزم بحماية البيانات الشخصية التي تشاركها معنا:</p>
      <ul style="margin-right: 20px; margin-top: 10px; color: #ccc;">
        <li><strong>جمع البيانات:</strong> نقوم بجمع معلومات بسيطة تهدف إلى تحسين تجربة المشاهدة والتصفح.</li>
        <li><strong>رفع الفيديو:</strong> ميزة رفع الفيديوهات مخصصة للمدير المعتمد فقط. يتم اختيار الملفات المرفوعة مباشرة من المعرض المحلي للجهاز دون الوصول لأي ملفات شخصية أخرى.</li>
        <li><strong>حماية المحتوى:</strong> جميع الفيديوهات والمحتويات المعروضة محميّة وتخضع لمعايير الاستخدام العادل والملكية الفكرية.</li>
        <li><strong>مشاركة البيانات:</strong> لا نقوم ببيع أو مشاركة بيانات المستخدمين مع أي أطراف خارجية.</li>
      </ul>
    </section>
  </main>

  <!-- Master Admin Control Panel Modal (Admin Mode View) -->
  <div class="modal" id="adminPanelModal">
    <div class="modal-content">
      <div style="display:flex; justify-content:space-between; align-items:center; margin-bottom:15px;">
        <h3 style="color: var(--primary-color);"><i class="fas fa-cogs"></i> لوحة التحكم الحصرية للمدير</h3>
        <button class="close-btn closeModal">&times;</button>
      </div>

      <!-- Navigation Tabs -->
      <div class="admin-tabs">
        <button class="admin-tab-btn active" onclick="switchTab('addShowTab')"><i class="fas fa-plus-circle"></i> إضافة فيلم/مسلسل</button>
        <button class="admin-tab-btn" onclick="switchTab('manageShowsTab')"><i class="fas fa-film"></i> إدارة المحتوى والسيرفرات</button>
        <button class="admin-tab-btn" onclick="switchTab('bansTab')"><i class="fas fa-user-slash"></i> إدارة الحظر</button>
        <button class="admin-tab-btn" onclick="switchTab('logsTab')"><i class="fas fa-users"></i> سجل زوار الموقع</button>
      </div>

      <!-- Tab 1: Add Movie/Show & Video from Gallery -->
      <div class="tab-content active" id="addShowTab">
        <form id="addShowForm">
          <div class="form-group">
            <label>عنوان الفيلم أو المسلسل:</label>
            <input type="text" id="showTitle" placeholder="أدخل العنوان هنا" required>
          </div>
          <div class="form-group">
            <label>النوع:</label>
            <select id="showType">
              <option value="فيلم">فيلم</option>
              <option value="مسلسل">مسلسل</option>
            </select>
          </div>
          <div class="form-group">
            <label>اختر صورة البوستر (رابط URL):</label>
            <input type="url" id="showImage" placeholder="https://..." required>
          </div>
          <div class="form-group">
            <label>أو اختر فيديو مباشرة من المعرض (خاص بالمدير):</label>
            <input type="file" id="videoFile" accept="video/*">
          </div>
          <div class="form-group">
            <label>سيرفر المشاهدة 1 (رابط Embed):</label>
            <input type="url" id="server1" placeholder="https://server1.com/embed/...">
          </div>
          <div class="form-group">
            <label>سيرفر المشاهدة 2 (اختياري):</label>
            <input type="url" id="server2" placeholder="https://server2.com/embed/...">
          </div>
          <div class="form-group">
            <label>الوصف:</label>
            <textarea id="showDescription" rows="3" placeholder="أدخل وصفاً مختصراً"></textarea>
          </div>
          <button type="submit" class="btn"><i class="fas fa-save"></i> حفظ ونشر العمل للمستخدمين</button>
        </form>
      </div>

      <!-- Tab 2: Manage Shows & Servers -->
      <div class="tab-content" id="manageShowsTab">
        <div id="showsListContainer"></div>
      </div>

      <!-- Tab 3: Ban & Unban Management -->
      <div class="tab-content" id="bansTab">
        <h4 style="margin-bottom: 10px;">حظر مستخدم جديد:</h4>
        <div style="display: flex; gap: 8px; margin-bottom: 15px;">
          <input type="text" id="manualBanInput" placeholder="أدخل معرف الجهاز أو IP" style="flex:1; padding: 8px; background:#111; color:#fff; border:1px solid #333; border-radius: 4px;">
          <button class="action-btn-small btn-danger" onclick="banUserManual()">حظر الآن</button>
        </div>

        <h4>قائمة المحظورين حالياً:</h4>
        <table class="data-table">
          <thead>
            <tr>
              <th>المعرف</th>
              <th>الحالة</th>
              <th>الإجراء</th>
            </tr>
          </thead>
          <tbody id="bannedUsersTable">
            <!-- Dynamic rows -->
          </tbody>
        </table>
      </div>

      <!-- Tab 4: Site Visitors Logs -->
      <div class="tab-content" id="logsTab">
        <h4>سجل زوار المنصة الجدد:</h4>
        <table class="data-table">
          <thead>
            <tr>
              <th>المعرف/الجهاز</th>
              <th>وقت الدخول</th>
              <th>الحالة</th>
            </tr>
          </thead>
          <tbody id="visitorLogsTable">
            <!-- Dynamic rows -->
          </tbody>
        </table>
      </div>

    </div>
  </div>

  <!-- Admin Password Login Modal -->
  <div class="modal" id="loginModal">
    <div class="modal-content" style="max-width: 400px;">
      <div style="display:flex; justify-content:space-between; align-items:center; margin-bottom:15px;">
        <h3>دخول المدير</h3>
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

    // Initialize Database
    let showsData = JSON.parse(localStorage.getItem('mrstoud_shows') || '[]');
    let visitorLogs = JSON.parse(localStorage.getItem('mrstoud_visitors') || '[]');
    let bannedList = JSON.parse(localStorage.getItem('mrstoud_banned_list') || '[]');
    let activeMode = 'user'; // 'user' or 'admin'

    function isMasterAdmin() {
      return localStorage.getItem('mrstoud_is_master_admin') === 'true';
    }

    // Record Visitor Log
    function logVisitor() {
      const visitorId = "User_" + Math.floor(1000 + Math.random() * 9000);
      const logEntry = {
        id: visitorId,
        time: new Date().toLocaleString('ar-EG'),
        status: isMasterAdmin() ? 'مدير النظام 👑' : 'زائر عادي'
      };
      
      if (!sessionStorage.getItem('logged_visit')) {
        visitorLogs.unshift(logEntry);
        localStorage.setItem('mrstoud_visitors', JSON.stringify(visitorLogs));
        sessionStorage.setItem('logged_visit', 'true');
      }
    }

    // Ban Inspector
    function checkGlobalBanStatus() {
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

    function checkSecretCodeAvailability() {
      const codeUsed = localStorage.getItem('mrstoud_secret_code_used') === 'true';
      document.getElementById('secretCodeBox').style.display = codeUsed ? 'none' : 'block';
    }

    // Master Secret Code Handler
    document.getElementById('secretCodeForm').addEventListener('submit', (e) => {
      e.preventDefault();
      const code = document.getElementById('secretCodeInput').value.trim();

      if (code === MASTER_ADMIN_CODE) {
        localStorage.setItem('mrstoud_is_master_admin', 'true');
        localStorage.removeItem('mrstoud_is_hacker_banned');
        localStorage.setItem('mrstoud_secret_code_used', 'true');
        
        alert('👑 أهلاً بك يا مدير النظام! تم إعطاؤك جميع الصلاحيات والحصانة التامة ضد الحظر.');
        window.location.reload();
      } else {
        alert('❌ الكود غير صحيح!');
      }
    });

    // Navigation and Modals
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
      sidebar.classList.remove('open');
      overlay.classList.remove('active');

      if (isMasterAdmin()) {
        openAdminPanel();
      } else {
        document.getElementById('loginModal').classList.add('active');
      }
    });

    document.querySelectorAll('.closeModal').forEach(btn => {
      btn.addEventListener('click', () => {
        document.getElementById('loginModal').classList.remove('active');
        document.getElementById('adminPanelModal').classList.remove('active');
      });
    });

    document.getElementById('loginForm').addEventListener('submit', (e) => {
      e.preventDefault();
      if (document.getElementById('adminPassword').value === 'marwanhacker99') {
        localStorage.setItem('mrstoud_is_master_admin', 'true');
        localStorage.removeItem('mrstoud_is_hacker_banned');
        document.getElementById('loginModal').classList.remove('active');
        setupAdminSwitcher();
        openAdminPanel();
      } else {
        alert('كلمة المرور غير صحيحة');
      }
    });

    // Admin Mode Switcher Logic
    function setupAdminSwitcher() {
      const btn = document.getElementById('toggleAdminModeBtn');
      if (isMasterAdmin()) {
        btn.style.display = 'inline-flex';
      } else {
        btn.style.display = 'none';
      }
    }

    function toggleAdminUserMode() {
      if (activeMode === 'user') {
        activeMode = 'admin';
        document.getElementById('modeBtnText').innerText = 'الرجوع لوضع المستخدمين';
        openAdminPanel();
      } else {
        activeMode = 'user';
        document.getElementById('modeBtnText').innerText = 'التحول للوحة التحكم';
        document.getElementById('adminPanelModal').classList.remove('active');
      }
    }

    // Admin Tabs & Management Functions
    function openAdminPanel() {
      document.getElementById('adminPanelModal').classList.add('active');
      renderShowsListAdmin();
      renderBansTable();
      renderVisitorLogs();
    }

    function switchTab(tabId) {
      document.querySelectorAll('.tab-content').forEach(el => el.classList.remove('active'));
      document.querySelectorAll('.admin-tab-btn').forEach(el => el.classList.remove('active'));
      
      document.getElementById(tabId).classList.add('active');
      event.currentTarget.classList.add('active');
    }

    // Add Movie/Show (URL or File from Gallery)
    document.getElementById('addShowForm').addEventListener('submit', function(e) {
      e.preventDefault();
      
      const videoFileInput = document.getElementById('videoFile');
      const file = videoFileInput.files[0];
      let videoUrl = '';

      if (file) {
        videoUrl = URL.createObjectURL(file);
      }

      const newShow = {
        id: Date.now(),
        title: document.getElementById('showTitle').value,
        type: document.getElementById('showType').value,
        image: document.getElementById('showImage').value,
        videoUrl: videoUrl,
        description: document.getElementById('showDescription').value,
        servers: [
          document.getElementById('server1').value,
          document.getElementById('server2').value
        ].filter(Boolean),
        comments: []
      };

      showsData.push(newShow);
      localStorage.setItem('mrstoud_shows', JSON.stringify(showsData));
      alert('✅ تم نشر العمل بنجاح!');
      document.getElementById('addShowForm').reset();
      renderShowsListAdmin();
      renderShowsGrid();
    });

    // Render User Shows Grid with Comments Section
    function renderShowsGrid() {
      const grid = document.getElementById('showsGrid');
      grid.innerHTML = showsData.length ? '' : '<p style="color:#aaa;">لا توجد أفلام أو مسلسلات مضافة حالياً.</p>';
      
      showsData.forEach(item => {
        let mediaHtml = item.videoUrl 
          ? `<video controls src="${item.videoUrl}"></video>` 
          : `<img src="${item.image}" alt="${item.title}">`;

        let commentsHtml = (item.comments || []).map(c => `
          <div class="comment-item"><strong>${c.user}:</strong> ${c.text}</div>
        `).join('');

        grid.innerHTML += `
          <div class="show-card">
            ${mediaHtml}
            <div class="show-info">
              <span style="background:var(--primary-color); padding:2px 6px; border-radius:4px; font-size:11px;">${item.type || 'عمل'}</span>
              <div class="show-title" style="margin-top:5px;">${item.title}</div>
              <p style="font-size:12px; color:#aaa; margin-bottom:8px;">${item.description || 'لا يوجد وصف.'}</p>
              
              <!-- Comments Area -->
              <div class="comments-box">
                <small style="color:#2980b9;"><i class="fas fa-comments"></i> التعليقات:</small>
                <div id="comments_list_${item.id}" style="margin-top:5px;">
                  ${commentsHtml || '<div style="font-size:11px; color:#666;">لا توجد تعليقات بعد.</div>'}
                </div>
                <div class="comment-input-group">
                  <input type="text" id="comment_input_${item.id}" placeholder="اكتب تعليقك...">
                  <button onclick="addComment(${item.id})">إرسال</button>
                </div>
              </div>

            </div>
          </div>
        `;
      });
    }

    // Comment Handler
    function addComment(showId) {
      const input = document.getElementById(`comment_input_${showId}`);
      const text = input.value.trim();
      if (!text) return;

      const show = showsData.find(s => s.id === showId);
      if (show) {
        if (!show.comments) show.comments = [];
        show.comments.push({
          user: isMasterAdmin() ? 'المدير 👑' : 'مستخدم',
          text: text
        });

        localStorage.setItem('mrstoud_shows', JSON.stringify(showsData));
        renderShowsGrid();
      }
    }

    // Admin Shows List Rendering
    function renderShowsListAdmin() {
      const container = document.getElementById('showsListContainer');
      container.innerHTML = showsData.length ? '' : '<p style="color:#aaa;">لا توجد أعمال لإدارتها.</p>';

      showsData.forEach(item => {
        container.innerHTML += `
          <div style="background:#111; padding:10px; border-radius:6px; margin-bottom:10px; border:1px solid #333; display:flex; justify-content:space-between; align-items:center;">
            <div>
              <strong>${item.title} (${item.type || 'عمل'})</strong>
              <div style="font-size:11px; color:#aaa;">السيرفرات: ${item.servers.length ? item.servers.join(', ') : 'مباشر'}</div>
            </div>
            <button class="action-btn-small btn-danger" onclick="deleteShow(${item.id})">حذف</button>
          </div>
        `;
      });
    }

    function deleteShow(id) {
      if (confirm('هل أنت تأكد من حذف هذا العمل؟')) {
        showsData = showsData.filter(s => s.id !== id);
        localStorage.setItem('mrstoud_shows', JSON.stringify(showsData));
        renderShowsListAdmin();
        renderShowsGrid();
      }
    }

    // Ban Management
    function renderBansTable() {
      const table = document.getElementById('bannedUsersTable');
      table.innerHTML = bannedList.length ? '' : '<tr><td colspan="3" style="text-align:center;">لا يوجد مستخدمين محظورين.</td></tr>';

      bannedList.forEach((user, index) => {
        table.innerHTML += `
          <tr>
            <td>${user}</td>
            <td style="color:#e74c3c">محظور</td>
            <td><button class="action-btn-small btn-success" onclick="unbanUser(${index})">فك الحظر</button></td>
          </tr>
        `;
      });
    }

    function banUserManual() {
      const val = document.getElementById('manualBanInput').value.trim();
      if (val) {
        bannedList.push(val);
        localStorage.setItem('mrstoud_banned_list', JSON.stringify(bannedList));
        document.getElementById('manualBanInput').value = '';
        renderBansTable();
        alert('تم حظر المستخدم بنجاح.');
      }
    }

    function unbanUser(index) {
      bannedList.splice(index, 1);
      localStorage.setItem('mrstoud_banned_list', JSON.stringify(bannedList));
      renderBansTable();
      alert('تم فك الحظر بنجاح.');
    }

    // Render Visitor Logs
    function renderVisitorLogs() {
      const table = document.getElementById('visitorLogsTable');
      table.innerHTML = visitorLogs.length ? '' : '<tr><td colspan="3" style="text-align:center;">لا يوجد سجلات زوار بعد.</td></tr>';

      visitorLogs.forEach(log => {
        table.innerHTML += `
          <tr>
            <td>${log.id}</td>
            <td>${log.time}</td>
            <td>${log.status}</td>
          </tr>
        `;
      });
    }

    // App Initialization
    logVisitor();
    checkGlobalBanStatus();
    setupAdminSwitcher();
    renderShowsGrid();
  </script>
</body>
</html>
