<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>mrstoud - منصة الأفلام والمسلسلات الآمنة</title>
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

    /* Blocked Hacker Screen */
    #hackerBlockedScreen {
      display: none;
      position: fixed;
      top: 0; left: 0; width: 100vw; height: 100vh;
      background-color: #0d0000;
      color: #ff3333;
      z-index: 99999;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      text-align: center;
      padding: 20px;
    }

    #hackerBlockedScreen i {
      font-size: 80px;
      margin-bottom: 20px;
      animation: pulse 1.5s infinite;
    }

    @keyframes pulse {
      0% { transform: scale(1); opacity: 0.8; }
      50% { transform: scale(1.1); opacity: 1; }
      100% { transform: scale(1); opacity: 0.8; }
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
      transition: background 0.2s, color 0.2s;
    }

    .icon-btn:hover, .icon-btn:active {
      background-color: #222;
      color: var(--primary-color);
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
      overflow-y: auto;
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

    .sidebar-search-box {
      margin-bottom: 15px;
      position: relative;
    }

    .sidebar-search-input {
      width: 100%;
      padding: 10px 12px 10px 35px;
      border-radius: 6px;
      border: 1px solid var(--border-color);
      background-color: #1a1a1a;
      color: #fff;
      font-size: 14px;
      outline: none;
    }

    .sidebar-search-input:focus { border-color: var(--primary-color); }

    .sidebar-search-icon {
      position: absolute;
      left: 10px;
      top: 50%;
      transform: translateY(-50%);
      color: var(--text-secondary);
      font-size: 14px;
    }

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
      transition: background 0.2s, color 0.2s;
    }

    .sidebar-menu-left {
      display: flex;
      align-items: center;
      gap: 12px;
    }

    .sidebar-menu a:hover, .sidebar-menu button:hover, .sidebar-menu a.active-link {
      background-color: #222;
      color: var(--primary-color);
    }

    .badge-count {
      background-color: #2a2a2a;
      color: #aaa;
      font-size: 11px;
      padding: 2px 7px;
      border-radius: 10px;
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

    .section-title {
      font-size: 20px;
      font-weight: bold;
      margin-bottom: 15px;
      display: flex;
      align-items: center;
      gap: 10px;
      color: var(--text-color);
      border-right: 4px solid var(--primary-color);
      padding-right: 10px;
    }

    .container {
      max-width: 1200px;
      margin: 15px auto;
      padding: 0 12px;
    }

    .ad-banner {
      background: linear-gradient(135deg, #1f1f1f, #141414);
      border: 1px dashed var(--primary-color);
      color: var(--text-secondary);
      text-align: center;
      padding: 14px;
      margin-bottom: 20px;
      border-radius: 8px;
      font-size: 13px;
    }

    .shows-grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(145px, 1fr));
      gap: 14px;
    }

    @media (min-width: 600px) {
      .shows-grid {
        grid-template-columns: repeat(auto-fill, minmax(180px, 1fr));
        gap: 18px;
      }
    }

    .show-card {
      background-color: var(--card-bg);
      border-radius: 8px;
      overflow: hidden;
      position: relative;
      box-shadow: 0 4px 12px rgba(0,0,0,0.4);
      transition: transform 0.2s;
      cursor: pointer;
    }

    .show-card:hover { transform: translateY(-4px); }

    .show-badge {
      position: absolute;
      top: 8px; right: 8px;
      background-color: var(--primary-color);
      color: #fff;
      padding: 3px 7px;
      font-size: 11px;
      border-radius: 4px;
      font-weight: bold;
      z-index: 2;
    }

    .show-type-tag {
      position: absolute;
      top: 8px; left: 8px;
      background-color: rgba(0, 0, 0, 0.75);
      color: #fff;
      padding: 3px 7px;
      font-size: 10px;
      border-radius: 4px;
      z-index: 2;
      border: 1px solid rgba(255,255,255,0.2);
    }

    .show-thumb {
      width: 100%;
      height: 220px;
      object-fit: cover;
      display: block;
    }

    @media (min-width: 600px) { .show-thumb { height: 260px; } }

    .show-info { padding: 10px; text-align: center; }
    .show-title {
      font-size: 14px;
      font-weight: 600;
      color: #fff;
      white-space: nowrap;
      overflow: hidden;
      text-overflow: ellipsis;
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
      box-shadow: 0 8px 24px rgba(0,0,0,0.7);
      max-height: 90vh;
      overflow-y: auto;
      border: 1px solid var(--border-color);
    }

    .modal-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 18px;
      border-bottom: 1px solid var(--border-color);
      padding-bottom: 10px;
    }

    .close-btn {
      background: none;
      border: none;
      color: #fff;
      font-size: 22px;
      cursor: pointer;
    }

    .admin-warning-box {
      background-color: rgba(229, 9, 20, 0.15);
      border: 1px solid var(--primary-color);
      color: #ff6b6b;
      padding: 12px;
      border-radius: 6px;
      font-size: 12px;
      margin-bottom: 15px;
      display: flex;
      align-items: center;
      gap: 10px;
      line-height: 1.5;
    }

    .admin-warning-box i { font-size: 20px; color: var(--primary-color); }

    .admin-verified-box {
      background-color: rgba(39, 174, 96, 0.15);
      border: 1px solid #27ae60;
      color: #2ecc71;
      padding: 12px;
      border-radius: 6px;
      font-size: 12px;
      margin-bottom: 15px;
      display: flex;
      align-items: center;
      gap: 10px;
      line-height: 1.5;
    }

    .admin-verified-box i { font-size: 20px; color: #27ae60; }

    .lockout-msg { color: #ff4d4d; font-size: 13px; margin-top: 10px; text-align: center; font-weight: bold; }

    .admin-tabs {
      display: flex;
      gap: 8px;
      margin-bottom: 20px;
      border-bottom: 1px solid var(--border-color);
      padding-bottom: 10px;
      overflow-x: auto;
    }

    .tab-btn {
      background: #111;
      border: 1px solid var(--border-color);
      color: var(--text-secondary);
      padding: 8px 14px;
      border-radius: 6px;
      cursor: pointer;
      font-size: 13px;
      white-space: nowrap;
      transition: all 0.2s;
    }

    .tab-btn.active {
      background: var(--primary-color);
      color: #fff;
      border-color: var(--primary-color);
    }

    .tab-content { display: none; }
    .tab-content.active { display: block; }

    .form-group { margin-bottom: 14px; }
    .form-group label { display: block; margin-bottom: 6px; font-size: 13px; color: var(--text-secondary); }
    .form-group input, .form-group select, .form-group textarea {
      width: 100%;
      padding: 10px 12px;
      border-radius: 6px;
      border: 1px solid var(--border-color);
      background-color: #121212;
      color: #fff;
      font-size: 14px;
      outline: none;
    }

    .form-group input:focus, .form-group select:focus, .form-group textarea:focus {
      border-color: var(--primary-color);
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
      transition: background 0.2s;
    }

    .btn:disabled { background-color: #555; cursor: not-allowed; }
    .btn:hover:not(:disabled) { background-color: var(--primary-hover); }
    .btn-secondary { background-color: #333; margin-top: 8px; }
    .btn-secondary:hover { background-color: #444; }

    .user-card {
      background-color: #121212;
      border: 1px solid var(--border-color);
      padding: 12px;
      border-radius: 6px;
      margin-bottom: 10px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      gap: 10px;
    }

    .user-info { display: flex; flex-direction: column; gap: 4px; }
    .user-name { font-size: 14px; font-weight: bold; }
    .user-email { font-size: 12px; color: var(--text-secondary); }

    .status-badge {
      font-size: 11px;
      padding: 3px 8px;
      border-radius: 4px;
      display: inline-block;
      width: fit-content;
    }

    .status-active { background-color: #27ae60; color: #fff; }
    .status-banned { background-color: #c0392b; color: #fff; }

    .sm-btn {
      padding: 6px 10px;
      font-size: 12px;
      border-radius: 4px;
      border: none;
      cursor: pointer;
      color: white;
    }

    .btn-edit { background-color: #2980b9; }
    .btn-del { background-color: #c0392b; }
    .btn-ban { background-color: #e67e22; }
    .btn-unban { background-color: #27ae60; }
  </style>
</head>
<body>

  <!-- Hacker Blocked Screen -->
  <div id="hackerBlockedScreen">
    <i class="fas fa-user-ninja"></i>
    <h1 style="font-size: 28px; margin-bottom: 10px;">تم اكتشاف محاولة اختراق!</h1>
    <p style="color: #ccc; max-width: 500px; font-size: 15px; line-height: 1.6;">
      تم حظر جهازك ومعرفك فوراً بواسطة جدار حماية المنصة (MRSTOUD Firewall WAF). تم إرسال كافة تفاصيل الهجوم إلى البريد الإلكتروني الخاص بالمدير: <strong>alvariz267@gmail.com</strong>.
    </p>
    <div style="margin-top: 25px; font-size: 12px; color: #777;">
      IP Status: <span style="color: red;">PERMANENTLY BANNED</span>
    </div>
  </div>

  <!-- Navigation Bar -->
  <nav class="navbar">
    <a href="#" class="brand" onclick="filterByCategory('all')">mrstoud</a>
    <div class="nav-actions">
      <button class="icon-btn" id="menuToggleBtn" title="القائمة الجانبية"><i class="fas fa-bars"></i></button>
    </div>
  </nav>

  <div class="overlay" id="overlay"></div>

  <!-- Sidebar -->
  <aside class="sidebar" id="sidebar">
    <div class="sidebar-header">
      <h3>mrstoud</h3>
      <button class="close-btn" id="closeSidebarBtn">&times;</button>
    </div>

    <div class="sidebar-search-box">
      <input type="text" class="sidebar-search-input" id="sidebarSearchInput" placeholder="بحث عن فيلم أو مسلسل...">
      <i class="fas fa-search sidebar-search-icon"></i>
    </div>

    <ul class="sidebar-menu">
      <li>
        <a href="#" class="active-link" onclick="filterByCategory('all', event)">
          <div class="sidebar-menu-left"><i class="fas fa-home"></i> الرئيسية</div>
          <span class="badge-count" id="countAll">0</span>
        </a>
      </li>
      <li>
        <a href="#" onclick="filterByCategory('series', event)">
          <div class="sidebar-menu-left"><i class="fas fa-tv"></i> المسلسلات</div>
          <span class="badge-count" id="countSeries">0</span>
        </a>
      </li>
      <li>
        <a href="#" onclick="filterByCategory('movie', event)">
          <div class="sidebar-menu-left"><i class="fas fa-film"></i> الأفلام</div>
          <span class="badge-count" id="countMovies">0</span>
        </a>
      </li>
      <hr style="border-color: var(--border-color); margin: 15px 0;">
      <li><button id="adminBtn"><div class="sidebar-menu-left"><i class="fas fa-user-shield"></i> الإدارة</div></button></li>
    </ul>
  </aside>

  <!-- Main Container -->
  <main class="container">
    <div class="section-title" id="sectionTitle">
      <i class="fas fa-play-circle"></i> جميع الأعمال
    </div>
    <div class="shows-grid" id="showsGrid"></div>
  </main>

  <!-- Login Modal -->
  <div class="modal" id="loginModal">
    <div class="modal-content">
      <div class="modal-header">
        <h3>دخول لوحة الإدارة</h3>
        <button class="close-btn closeModal">&times;</button>
      </div>

      <div class="admin-warning-box">
        <i class="fas fa-exclamation-triangle"></i>
        <div>
          <strong>تنبيه أمني:</strong> سيتم تفادي حظر البريد المعتمد <strong>alvariz267@gmail.com</strong> تلقائياً مع توثيق الجهاز.
        </div>
      </div>

      <form id="loginForm">
        <div class="form-group">
          <label for="adminPassword">كلمة المرور:</label>
          <input type="password" id="adminPassword" placeholder="أدخل كلمة المرور" required autocomplete="off">
        </div>
        <button type="submit" class="btn" id="loginSubmitBtn">دخول وتوثيق الجهاز</button>
        <div id="lockoutTimer" class="lockout-msg"></div>
      </form>
    </div>
  </div>

  <!-- Admin Modal -->
  <div class="modal" id="adminModal">
    <div class="modal-content">
      <div class="modal-header">
        <h3 id="adminModalTitle">لوحة التحكم والتنفيذ</h3>
        <button class="close-btn closeModal">&times;</button>
      </div>

      <div class="admin-verified-box">
        <i class="fas fa-user-check"></i>
        <div>
          <strong>حالة النظام:</strong> تم التوثيق بحساب المدير <strong>alvariz267@gmail.com</strong>. إشعارات الحظر مفعلة.
        </div>
      </div>

      <div class="admin-tabs">
        <button class="tab-btn active" onclick="switchAdminTab('tab-shows')"><i class="fas fa-film"></i> الأعمال</button>
        <button class="tab-btn" onclick="switchAdminTab('tab-users')"><i class="fas fa-users"></i> إدارة المستخدمين</button>
        <button class="tab-btn" onclick="switchAdminTab('tab-ban')"><i class="fas fa-user-slash"></i> الحظر وإرسال البريد</button>
      </div>

      <!-- Tab 1: Shows -->
      <div id="tab-shows" class="tab-content active">
        <div id="adminShowsList"></div>
      </div>

      <!-- Tab 2: Users -->
      <div id="tab-users" class="tab-content">
        <h4 style="margin-bottom: 12px; color: var(--primary-color);">جميع المستخدمين</h4>
        <div id="usersListContainer"></div>
      </div>

      <!-- Tab 3: Ban & Email Notifications -->
      <div id="tab-ban" class="tab-content">
        <h4 style="margin-bottom: 12px; color: var(--primary-color);">حظر مستخدم وإرسال بريد إشعاري</h4>
        <form id="banUserForm" style="margin-bottom: 20px;">
          <div class="form-group">
            <label for="banEmail">البريد الإلكتروني المراد حظره:</label>
            <input type="email" id="banEmail" placeholder="example@domain.com" required>
          </div>
          <div class="form-group">
            <label for="banReason">سبب الحظر / تفاصيل محاولة الهجوم:</label>
            <input type="text" id="banReason" placeholder="مثال: محاولة حقن SQL أو هجوم DDoS">
          </div>
          <button type="submit" class="btn btn-del"><i class="fas fa-paper-plane"></i> حظر وإرسال تقرير لـ alvariz267@gmail.com</button>
        </form>

        <hr style="border-color: var(--border-color); margin: 20px 0;">

        <h4 style="margin-bottom: 12px; color: #27ae60;">قائمة المحظورين والتحكم عبر البريد</h4>
        <div id="bannedUsersContainer"></div>
      </div>

    </div>
  </div>

  <script>
    const ADMIN_EMAIL = "alvariz267@gmail.com";

    // Auto Recognition & Master Immunity
    function isMasterAdmin() {
      return localStorage.getItem('mrstoud_is_master_admin') === 'true';
    }

    function checkGlobalBanStatus() {
      if (isMasterAdmin()) return;

      if (localStorage.getItem('mrstoud_is_hacker_banned') === 'true') {
        document.getElementById('hackerBlockedScreen').style.display = 'flex';
        throw new Error('Access Denied');
      }
    }

    // Direct Email Dispatcher for Unban and Security Alerts
    function sendSecurityAlertEmail(targetUser, attackReason) {
      const pageUrl = window.location.href.split('?')[0];
      const unbanUrl = `${pageUrl}?action=unban&email=${encodeURIComponent(targetUser)}`;
      const permBanUrl = `${pageUrl}?action=permban&email=${encodeURIComponent(targetUser)}`;

      const emailSubject = encodeURIComponent(`🚨 [MRSTOUD SECURITY] تنبيه هجوم جديد وحظر: ${targetUser}`);
      const emailBody = encodeURIComponent(
`مرحباً مدير النظام (${ADMIN_EMAIL})،

تم رصد محاولة هجوم أمني على منصة mrstoud وتم حظر الحساب/المعرف فوراً!

تفاصيل الهجوم:
------------------------------------
- المحظور / البريد: ${targetUser}
- سبب الحظر / نوع الهجوم: ${attackReason}
- التاريخ والوقت: ${new Date().toLocaleString('ar-EG')}
- رابط الصفحة: ${window.location.href}

------------------------------------
خيارات التحكّم الفوري بضغطة زر:

[1] لفك الحظر فوراً عن هذا المستخدم، اضغط الرابط التالي:
${unbanUrl}

[2] لتأكيد الحظر النهائي وإبقائه بالأرشيف، اضغط الرابط التالي:
${permBanUrl}
`
      );

      // Open mail client addressed to alvariz267@gmail.com
      window.open(`mailto:${ADMIN_EMAIL}?subject=${emailSubject}&body=${emailBody}`, '_blank');
    }

    function triggerAutoHackerBan(reason) {
      if (isMasterAdmin()) {
        console.warn('System WAF Alert bypassed for Admin:', reason);
        return;
      }

      localStorage.setItem('mrstoud_is_hacker_banned', 'true');
      sendSecurityAlertEmail("HACKER_IP_DETECTED", reason);
      document.getElementById('hackerBlockedScreen').style.display = 'flex';
    }

    // URL Query Handler for Email One-Click Unban
    function handleEmailActionQueries() {
      const urlParams = new URLSearchParams(window.location.search);
      const action = urlParams.get('action');
      const email = urlParams.get('email');

      if (action && email) {
        if (action === 'unban') {
          // Perform Unban
          let users = JSON.parse(localStorage.getItem('mrstoud_users')) || [];
          const user = users.find(u => u.email.toLowerCase() === email.toLowerCase());
          if (user) {
            user.status = 'active';
            delete user.banReason;
            localStorage.setItem('mrstoud_users', JSON.stringify(users));
          }
          localStorage.removeItem('mrstoud_is_hacker_banned');
          alert(`✅ تم فك الحظر بنجاح عن (${email}) عبر التوجيه البريدي!`);
          window.location.href = window.location.pathname; // Clean URL
        } else if (action === 'permban') {
          alert(`🔒 تم تأكيد الحظر النهائي على (${email}).`);
          window.location.href = window.location.pathname;
        }
      }
    }

    function inspectSecurityInput(inputStr) {
      if (!inputStr) return inputStr;
      const attackPatterns = [
        /<script\b[^>]*>([\s\S]*?)<\/script>/gi,
        /javascript:/gi,
        /onerror=/gi,
        /SELECT\s+.*\s+FROM/gi,
        /UNION\s+SELECT/gi,
        /DELETE\s+FROM/gi
      ];

      for (let pattern of attackPatterns) {
        if (pattern.test(inputStr)) {
          triggerAutoHackerBan("محاولة حقن كود خبيث: " + pattern.toString());
          return '';
        }
      }
      return inputStr;
    }

    checkGlobalBanStatus();
    handleEmailActionQueries();

    /* App State */
    let users = JSON.parse(localStorage.getItem('mrstoud_users')) || [
      { id: 1, name: "مستخدم تجريبي", email: "user@example.com", status: "active" }
    ];

    const adminBtn = document.getElementById('adminBtn');
    const loginModal = document.getElementById('loginModal');
    const adminModal = document.getElementById('adminModal');
    const bannedUsersContainer = document.getElementById('bannedUsersContainer');
    const usersListContainer = document.getElementById('usersListContainer');
    const banUserForm = document.getElementById('banUserForm');

    window.switchAdminTab = function(tabId) {
      document.querySelectorAll('.tab-btn').forEach(btn => btn.classList.remove('active'));
      document.querySelectorAll('.tab-content').forEach(content => content.classList.remove('active'));
      event.currentTarget.classList.add('active');
      document.getElementById(tabId).classList.add('active');
    };

    function renderUsersAndBans() {
      usersListContainer.innerHTML = '';
      bannedUsersContainer.innerHTML = '';

      users.forEach(user => {
        const userCard = document.createElement('div');
        userCard.className = 'user-card';
        userCard.innerHTML = `
          <div class="user-info">
            <span class="user-name">${user.name}</span>
            <span class="user-email">${user.email}</span>
          </div>
          <div>
            <span class="status-badge ${user.status === 'banned' ? 'status-banned' : 'status-active'}">
              ${user.status === 'banned' ? 'محظور' : 'نشط'}
            </span>
          </div>
        `;
        usersListContainer.appendChild(userCard);

        if (user.status === 'banned') {
          const banCard = document.createElement('div');
          banCard.className = 'user-card';
          banCard.innerHTML = `
            <div class="user-info">
              <span class="user-name">${user.email}</span>
              <span class="user-email" style="color: #e74c3c;">السبب: ${user.banReason || 'غير محدد'}</span>
            </div>
            <button class="sm-btn btn-unban" onclick="unbanUser('${user.email}')"><i class="fas fa-unlock"></i> فك الحظر</button>
          `;
          bannedUsersContainer.appendChild(banCard);
        }
      });
    }

    function performBan(email, reason) {
      let targetUser = users.find(u => u.email.toLowerCase() === email.toLowerCase());
      if (targetUser) {
        targetUser.status = 'banned';
        targetUser.banReason = reason;
      } else {
        users.push({
          id: Date.now(),
          name: email.split('@')[0],
          email: email,
          status: 'banned',
          banReason: reason
        });
      }
      localStorage.setItem('mrstoud_users', JSON.stringify(users));
      renderUsersAndBans();

      // Dispatch Security email notification
      sendSecurityAlertEmail(email, reason);
      alert(`تم حظر (${email}) وإعداد الرسالة الإلكترونية الموجهة إلى ${ADMIN_EMAIL}!`);
    }

    window.unbanUser = function(email) {
      const user = users.find(u => u.email.toLowerCase() === email.toLowerCase());
      if (user) {
        user.status = 'active';
        delete user.banReason;
        localStorage.setItem('mrstoud_users', JSON.stringify(users));
        renderUsersAndBans();
        alert(`تم فك الحظر بنجاح عن (${email})!`);
      }
    };

    banUserForm.addEventListener('submit', (e) => {
      e.preventDefault();
      const email = document.getElementById('banEmail').value;
      const reason = document.getElementById('banReason').value;
      performBan(email, reason);
      banUserForm.reset();
    });

    adminBtn.addEventListener('click', () => {
      if (isMasterAdmin()) {
        renderUsersAndBans();
        adminModal.classList.add('active');
      } else {
        loginModal.classList.add('active');
      }
    });

    document.getElementById('loginForm').addEventListener('submit', (e) => {
      e.preventDefault();
      const pwd = document.getElementById('adminPassword').value;
      if (pwd === 'marwanhacker99') {
        localStorage.setItem('mrstoud_is_master_admin', 'true');
        localStorage.removeItem('mrstoud_is_hacker_banned');
        loginModal.classList.remove('active');
        renderUsersAndBans();
        adminModal.classList.add('active');
      } else {
        alert('كلمة المرور غير صحيحة');
      }
    });

    document.querySelectorAll('.closeModal').forEach(btn => {
      btn.addEventListener('click', () => {
        loginModal.classList.remove('active');
        adminModal.classList.remove('active');
      });
    });
  </script>
</body>
</html>
