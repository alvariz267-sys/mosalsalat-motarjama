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
      right: -300px;
      width: 270px;
      height: 100%;
      background-color: var(--sidebar-bg);
      box-shadow: -4px 0 15px rgba(0, 0, 0, 0.8);
      transition: right 0.3s cubic-bezier(0.4, 0, 0.2, 1);
      z-index: 200;
      padding: 20px 15px;
      display: flex;
      flex-direction: column;
    }

    .sidebar.open {
      right: 0;
    }

    .sidebar-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      border-bottom: 1px solid var(--border-color);
      padding-bottom: 15px;
      margin-bottom: 15px;
    }

    .sidebar-header h3 {
      font-size: 20px;
      color: var(--primary-color);
    }

    .sidebar-menu {
      list-style: none;
    }

    .sidebar-menu li {
      margin-bottom: 8px;
    }

    .sidebar-menu a, .sidebar-menu button {
      color: var(--text-color);
      text-decoration: none;
      font-size: 16px;
      display: flex;
      align-items: center;
      gap: 12px;
      padding: 12px;
      border-radius: 6px;
      background: none;
      border: none;
      cursor: pointer;
      width: 100%;
      text-align: right;
      transition: background 0.2s;
    }

    .sidebar-menu a:hover, .sidebar-menu button:hover {
      background-color: #222;
      color: var(--primary-color);
    }

    .overlay {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: rgba(0,0,0,0.7);
      backdrop-filter: blur(2px);
      display: none;
      z-index: 150;
    }

    .overlay.active {
      display: block;
    }

    /* Search Box */
    .search-container {
      padding: 12px 15px;
      max-width: 1200px;
      margin: 0 auto;
      display: none;
    }

    .search-container.active {
      display: block;
    }

    .search-input {
      width: 100%;
      padding: 12px 16px;
      border-radius: 8px;
      border: 1px solid var(--border-color);
      background-color: #1a1a1a;
      color: #fff;
      font-size: 15px;
      outline: none;
    }

    .search-input:focus {
      border-color: var(--primary-color);
    }

    /* Main Container & Grid */
    .container {
      max-width: 1200px;
      margin: 15px auto;
      padding: 0 12px;
    }

    /* Ad Banner */
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

    .show-card:hover {
      transform: translateY(-4px);
    }

    .show-badge {
      position: absolute;
      top: 8px;
      right: 8px;
      background-color: var(--primary-color);
      color: #fff;
      padding: 3px 7px;
      font-size: 11px;
      border-radius: 4px;
      font-weight: bold;
      z-index: 2;
    }

    .show-thumb {
      width: 100%;
      height: 220px;
      object-fit: cover;
      display: block;
    }

    @media (min-width: 600px) {
      .show-thumb {
        height: 260px;
      }
    }

    .show-info {
      padding: 10px;
      text-align: center;
    }

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
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background-color: rgba(0,0,0,0.85);
      z-index: 300;
      justify-content: center;
      align-items: center;
      padding: 15px;
    }

    .modal.active {
      display: flex;
    }

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

    /* Security Notice Banner */
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

    .admin-warning-box i {
      font-size: 20px;
      color: var(--primary-color);
    }

    .lockout-msg {
      color: #ff4d4d;
      font-size: 13px;
      margin-top: 10px;
      text-align: center;
      font-weight: bold;
    }

    /* Admin Tabs */
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

    .tab-content {
      display: none;
    }

    .tab-content.active {
      display: block;
    }

    .form-group {
      margin-bottom: 14px;
    }

    .form-group label {
      display: block;
      margin-bottom: 6px;
      font-size: 13px;
      color: var(--text-secondary);
    }

    .form-group input, .form-group select {
      width: 100%;
      padding: 10px 12px;
      border-radius: 6px;
      border: 1px solid var(--border-color);
      background-color: #121212;
      color: #fff;
      font-size: 14px;
      outline: none;
    }

    .form-group input:focus {
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

    .btn:disabled {
      background-color: #555;
      cursor: not-allowed;
    }

    .btn:hover:not(:disabled) {
      background-color: var(--primary-hover);
    }

    .btn-secondary {
      background-color: #333;
      margin-top: 8px;
    }

    .btn-secondary:hover {
      background-color: #444;
    }

    /* Users & Ban List Styling */
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

    .user-info {
      display: flex;
      flex-direction: column;
      gap: 4px;
    }

    .user-name {
      font-size: 14px;
      font-weight: bold;
    }

    .user-email {
      font-size: 12px;
      color: var(--text-secondary);
    }

    .status-badge {
      font-size: 11px;
      padding: 3px 8px;
      border-radius: 4px;
      display: inline-block;
      width: fit-content;
    }

    .status-active { background-color: #27ae60; color: #fff; }
    .status-banned { background-color: #c0392b; color: #fff; }

    /* Video Player Modal Elements */
    .video-container {
      position: relative;
      padding-bottom: 56.25%;
      height: 0;
      overflow: hidden;
      border-radius: 8px;
      background-color: #000;
      margin-bottom: 15px;
    }

    .video-container iframe, .video-container video {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      border: 0;
    }

    .video-details {
      display: flex;
      flex-direction: column;
      gap: 12px;
    }

    .quality-tags {
      display: flex;
      gap: 8px;
      align-items: center;
      flex-wrap: wrap;
    }

    .quality-tag {
      background-color: #2a2a2a;
      color: #fff;
      padding: 4px 8px;
      border-radius: 4px;
      font-size: 12px;
      border: 1px solid var(--border-color);
    }

    .download-btn {
      display: inline-flex;
      align-items: center;
      justify-content: center;
      gap: 8px;
      background-color: #27ae60;
      color: white;
      text-decoration: none;
      padding: 12px;
      border-radius: 6px;
      font-weight: bold;
      font-size: 14px;
      text-align: center;
    }

    .download-btn:hover {
      background-color: #219150;
    }

    /* Admin Show List Items */
    .admin-item {
      display: flex;
      align-items: center;
      justify-content: space-between;
      background-color: #121212;
      padding: 10px;
      border-radius: 6px;
      margin-bottom: 10px;
      border: 1px solid var(--border-color);
    }

    .admin-item-title {
      font-size: 14px;
      font-weight: 500;
      max-width: 60%;
      white-space: nowrap;
      overflow: hidden;
      text-overflow: ellipsis;
    }

    .admin-actions {
      display: flex;
      gap: 8px;
    }

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

  <!-- Navigation Bar -->
  <nav class="navbar">
    <a href="#" class="brand">mrstoud</a>
    <div class="nav-actions">
      <button class="icon-btn" id="searchToggleBtn" title="بحث"><i class="fas fa-search"></i></button>
      <button class="icon-btn" id="menuToggleBtn" title="القائمة"><i class="fas fa-bars"></i></button>
    </div>
  </nav>

  <!-- Sidebar Overlay -->
  <div class="overlay" id="overlay"></div>

  <!-- Sidebar -->
  <aside class="sidebar" id="sidebar">
    <div class="sidebar-header">
      <h3>mrstoud</h3>
      <button class="close-btn" id="closeSidebarBtn">&times;</button>
    </div>
    <ul class="sidebar-menu">
      <li><a href="#"><i class="fas fa-home"></i> الرئيسية</a></li>
      <li><a href="#"><i class="fas fa-tv"></i> المسلسلات</a></li>
      <li><a href="#"><i class="fas fa-film"></i> الأفلام</a></li>
      <hr style="border-color: var(--border-color); margin: 10px 0;">
      <li><button id="adminBtn"><i class="fas fa-user-shield"></i> الإدارة</button></li>
    </ul>
  </aside>

  <!-- Search Bar -->
  <div class="search-container" id="searchContainer">
    <input type="text" class="search-input" id="searchInput" placeholder="ابحث عن مسلسل أو فيلم...">
  </div>

  <!-- Main Content -->
  <main class="container">
    
    <!-- Ad Banner -->
    <div class="ad-banner">
      <p>📢 مساحة إعلانية - ضع كود الإعلان الخاص بك هنا (AdSense / Native Ads)</p>
    </div>

    <!-- Shows Grid -->
    <div class="shows-grid" id="showsGrid">
      <!-- Dynamic Content -->
    </div>

  </main>

  <!-- Login Modal -->
  <div class="modal" id="loginModal">
    <div class="modal-content">
      <div class="modal-header">
        <h3>دخول لوحة الإدارة</h3>
        <button class="close-btn closeModal">&times;</button>
      </div>

      <!-- Warning Box for Security -->
      <div class="admin-warning-box">
        <i class="fas fa-exclamation-triangle"></i>
        <div>
          <strong>تنبيه أمني هام:</strong> هذه اللوحة مخصصة حصراً لمدير الموقع! يُمنع محاولة التخمين أو الدخول غير المصرح به.
        </div>
      </div>

      <form id="loginForm">
        <div class="form-group">
          <label for="adminPassword">كلمة المرور:</label>
          <input type="password" id="adminPassword" placeholder="أدخل كلمة المرور" required autocomplete="off">
        </div>
        <button type="submit" class="btn" id="loginSubmitBtn">دخول</button>
        <div id="lockoutTimer" class="lockout-msg"></div>
      </form>
    </div>
  </div>

  <!-- Admin Control Panel Modal -->
  <div class="modal" id="adminModal">
    <div class="modal-content">
      <div class="modal-header">
        <h3 id="adminModalTitle">لوحة التحكم والتنفيذ</h3>
        <button class="close-btn closeModal">&times;</button>
      </div>

      <!-- Navigation Tabs inside Admin Modal -->
      <div class="admin-tabs">
        <button class="tab-btn active" onclick="switchAdminTab('tab-shows')"><i class="fas fa-film"></i> المسلسلات والأفلام</button>
        <button class="tab-btn" onclick="switchAdminTab('tab-users')"><i class="fas fa-users"></i> إدارة المستخدمين</button>
        <button class="tab-btn" onclick="switchAdminTab('tab-ban')"><i class="fas fa-user-slash"></i> الحظر وفك الحظر</button>
      </div>

      <!-- Tab 1: Shows & Movies -->
      <div id="tab-shows" class="tab-content active">
        <form id="saveShowForm" style="margin-bottom: 25px;">
          <input type="hidden" id="editShowId" value="">
          <h4 style="margin-bottom: 12px; color: var(--primary-color);" id="formSubTitle">إضافة مسلسل / فيلم جديد</h4>
          
          <div class="form-group">
            <label for="showTitle">عنوان العمل:</label>
            <input type="text" id="showTitle" required placeholder="مثال: فيلم/مسلسل كامل (ساعتان ونصف)">
          </div>
          
          <div class="form-group">
            <label for="showBadge">نص الشارة (اختياري):</label>
            <input type="text" id="showBadge" placeholder="مثال: 2:30 ساعة / فيلم">
          </div>

          <div class="form-group">
            <label for="showImage">رابط صورة الغلاف (URL):</label>
            <input type="url" id="showImage" placeholder="https://example.com/image.jpg">
          </div>

          <!-- اختيار فيديو من الهاتف -->
          <div class="form-group" style="background: #181818; padding: 12px; border-radius: 8px; border: 1px dashed var(--primary-color);">
            <label for="showVideoFile" style="color: #fff; font-weight: bold;"><i class="fas fa-file-video"></i> اختيار فيديو طويل من ملفات الهاتف (يدعم الحجم الكبير):</label>
            <input type="file" id="showVideoFile" accept="video/*" style="padding: 6px; cursor: pointer;">
            <small style="color: #27ae60; display: block; margin-top: 4px;">✔ يدعم الأفلام والمسلسلات طويلة المدة (ساعتان ونصف فأكثر) بدون مشاكل ذاكرة.</small>
          </div>

          <div style="text-align: center; margin: 10px 0; color: var(--text-secondary); font-size: 12px;">— أو استخدم رابط فيديو خارجي —</div>

          <div class="form-group">
            <label for="showVideoUrl">رابط البث / مشغل الفيديو (Embed URL):</label>
            <input type="text" id="showVideoUrl" placeholder="https://www.youtube.com/embed/...">
          </div>

          <div class="form-group">
            <label for="showQuality">الجودة المتاحة:</label>
            <input type="text" id="showQuality" placeholder="مثال: 1080p, 720p, 480p" value="1080p Full HD">
          </div>

          <div class="form-group">
            <label for="showDownloadUrl">رابط تحميل الفيديو للهواتف:</label>
            <input type="url" id="showDownloadUrl" placeholder="https://example.com/download.mp4">
          </div>

          <button type="submit" class="btn" id="saveBtn">حفظ وإضافة</button>
          <button type="button" class="btn btn-secondary" id="cancelEditBtn" style="display:none;">إلغاء التعديل</button>
        </form>

        <hr style="border-color: var(--border-color); margin-bottom: 15px;">
        <h4 style="margin-bottom: 12px;">قائمة الفيديوهات الحالية</h4>
        <div id="adminShowsList"></div>
      </div>

      <!-- Tab 2: Users List -->
      <div id="tab-users" class="tab-content">
        <h4 style="margin-bottom: 12px; color: var(--primary-color);">جميع المستخدمين المسجلين في الموقع</h4>
        <div id="usersListContainer">
          <!-- Populated dynamically -->
        </div>
      </div>

      <!-- Tab 3: Ban / Unban Control -->
      <div id="tab-ban" class="tab-content">
        <h4 style="margin-bottom: 12px; color: var(--primary-color);">حظر مستخدم جديد</h4>
        <form id="banUserForm" style="margin-bottom: 20px;">
          <div class="form-group">
            <label for="banEmail">بريد أو معرف المستخدم المراد حظره:</label>
            <input type="text" id="banEmail" placeholder="example@domain.com" required>
          </div>
          <div class="form-group">
            <label for="banReason">سبب الحظر:</label>
            <input type="text" id="banReason" placeholder="مثال: مخالفة الشروط والإرشادات">
          </div>
          <button type="submit" class="btn btn-del"><i class="fas fa-user-slash"></i> تأكيد الحظر</button>
        </form>

        <hr style="border-color: var(--border-color); margin: 20px 0;">

        <h4 style="margin-bottom: 12px; color: #27ae60;">قائمة المحظورين (إمكانية فك الحظر)</h4>
        <div id="bannedUsersContainer">
          <!-- Populated dynamically -->
        </div>
      </div>

    </div>
  </div>

  <!-- Player Modal (For Viewers) -->
  <div class="modal" id="playerModal">
    <div class="modal-content" style="max-width: 700px;">
      <div class="modal-header">
        <h3 id="playerTitle">عرض الفيديو</h3>
        <button class="close-btn closeModal">&times;</button>
      </div>
      
      <!-- Video Player -->
      <div class="video-container" id="videoPlayerBox">
        <iframe id="videoIframe" src="" allowfullscreen></iframe>
      </div>

      <div class="video-details">
        <div class="quality-tags">
          <span style="font-size: 13px; color: var(--text-secondary);">الجودة المتاحة:</span>
          <span class="quality-tag" id="playerQuality">1080p</span>
        </div>

        <div id="downloadContainer">
          <!-- Download Button -->
        </div>
      </div>
    </div>
  </div>

  <script>
    // Security & Sanitization Function
    function sanitizeInput(str) {
      if (!str) return '';
      const temp = document.createElement('div');
      temp.textContent = str;
      return temp.innerHTML;
    }

    // Default Initial Data
    const defaultShows = [
      {
        id: 1,
        title: "مسلسل في السابعة عشر",
        badge: "حلقة 1",
        image: "https://images.unsplash.com/photo-1536440136628-849c177e76a1?auto=format&fit=crop&w=400&q=80",
        videoUrl: "https://www.youtube.com/embed/dQw4w9WgXcQ",
        quality: "1080p Full HD",
        downloadUrl: "https://example.com/download.mp4"
      }
    ];

    // Default Users Data
    const defaultUsers = [
      { id: 101, name: "أحمد علي", email: "ahmed@example.com", status: "active" },
      { id: 102, name: "محمد ياسين", email: "mowin@example.com", status: "active" },
      { id: 103, name: "مستخدم تجريبي", email: "spammer@test.com", status: "banned", banReason: "سلوك غير لائق" }
    ];

    // Data handling
    let shows = JSON.parse(localStorage.getItem('mrstoud_shows')) || defaultShows;
    let users = JSON.parse(localStorage.getItem('mrstoud_users')) || defaultUsers;
    let isAdminLoggedIn = false;

    // Security: Login Attempt Control
    let loginAttempts = parseInt(localStorage.getItem('mrstoud_login_attempts') || '0');
    let lockoutUntil = parseInt(localStorage.getItem('mrstoud_lockout_until') || '0');

    // DOM Elements
    const showsGrid = document.getElementById('showsGrid');
    const menuToggleBtn = document.getElementById('menuToggleBtn');
    const closeSidebarBtn = document.getElementById('closeSidebarBtn');
    const sidebar = document.getElementById('sidebar');
    const overlay = document.getElementById('overlay');
    const searchToggleBtn = document.getElementById('searchToggleBtn');
    const searchContainer = document.getElementById('searchContainer');
    const searchInput = document.getElementById('searchInput');
    
    // Admin DOM Elements
    const adminBtn = document.getElementById('adminBtn');
    const loginModal = document.getElementById('loginModal');
    const adminModal = document.getElementById('adminModal');
    const playerModal = document.getElementById('playerModal');
    const loginForm = document.getElementById('loginForm');
    const saveShowForm = document.getElementById('saveShowForm');
    const adminShowsList = document.getElementById('adminShowsList');
    const closeModalBtns = document.querySelectorAll('.closeModal');
    const cancelEditBtn = document.getElementById('cancelEditBtn');
    const showVideoFile = document.getElementById('showVideoFile');
    const loginSubmitBtn = document.getElementById('loginSubmitBtn');
    const lockoutTimer = document.getElementById('lockoutTimer');
    const usersListContainer = document.getElementById('usersListContainer');
    const bannedUsersContainer = document.getElementById('bannedUsersContainer');
    const banUserForm = document.getElementById('banUserForm');

    // Player Elements
    const videoPlayerBox = document.getElementById('videoPlayerBox');
    const playerTitle = document.getElementById('playerTitle');
    const playerQuality = document.getElementById('playerQuality');
    const downloadContainer = document.getElementById('downloadContainer');

    // Switch Admin Tabs
    window.switchAdminTab = function(tabId) {
      document.querySelectorAll('.tab-btn').forEach(btn => btn.classList.remove('active'));
      document.querySelectorAll('.tab-content').forEach(content => content.classList.remove('active'));

      event.currentTarget.classList.add('active');
      document.getElementById(tabId).classList.add('active');
    };

    // Check Lockout Status
    function checkLockoutStatus() {
      const now = Date.now();
      if (lockoutUntil && now < lockoutUntil) {
        const remainingHours = Math.ceil((lockoutUntil - now) / (1000 * 60 * 60));
        loginSubmitBtn.disabled = true;
        lockoutTimer.innerHTML = `<i class="fas fa-lock"></i> تم حظر محاولات الدخول لكثرة الأخطاء! يرجى الانتظار ${remainingHours} ساعة.`;
        return true;
      } else if (lockoutUntil && now >= lockoutUntil) {
        localStorage.removeItem('mrstoud_lockout_until');
        localStorage.setItem('mrstoud_login_attempts', '0');
        loginAttempts = 0;
        loginSubmitBtn.disabled = false;
        lockoutTimer.innerHTML = '';
      }
      return false;
    }

    // Render Grid for Visitors
    function renderShows(filterText = '') {
      showsGrid.innerHTML = '';
      const cleanFilter = sanitizeInput(filterText.toLowerCase());
      const filtered = shows.filter(show => show.title.toLowerCase().includes(cleanFilter));

      if (filtered.length === 0) {
        showsGrid.innerHTML = '<p style="grid-column: 1/-1; text-align: center; color: #777; padding: 20px;">لا توجد نتائج مطابقة</p>';
        return;
      }

      filtered.forEach(show => {
        const card = document.createElement('div');
        card.className = 'show-card';
        card.onclick = () => openPlayer(show);
        card.innerHTML = `
          ${show.badge ? `<div class="show-badge">${sanitizeInput(show.badge)}</div>` : ''}
          <img src="${sanitizeInput(show.image) || 'https://via.placeholder.com/300x400/222/fff?text=mrstoud'}" alt="${sanitizeInput(show.title)}" class="show-thumb" onerror="this.src='https://via.placeholder.com/300x400/222/fff?text=mrstoud'">
          <div class="show-info">
            <div class="show-title">${sanitizeInput(show.title)}</div>
          </div>
        `;
        showsGrid.appendChild(card);
      });
    }

    // Render Admin Show List
    function renderAdminList() {
      adminShowsList.innerHTML = '';
      shows.forEach(show => {
        const item = document.createElement('div');
        item.className = 'admin-item';
        item.innerHTML = `
          <div class="admin-item-title">${sanitizeInput(show.title)}</div>
          <div class="admin-actions">
            <button class="sm-btn btn-edit" onclick="editShow(${show.id})"><i class="fas fa-edit"></i> تعديل</button>
            <button class="sm-btn btn-del" onclick="deleteShow(${show.id})"><i class="fas fa-trash"></i> حذف</button>
          </div>
        `;
        adminShowsList.appendChild(item);
      });
    }

    // Render All Users & Banned Users
    function renderUsersAndBans() {
      usersListContainer.innerHTML = '';
      bannedUsersContainer.innerHTML = '';

      let bannedCount = 0;

      users.forEach(user => {
        // Users tab element
        const userCard = document.createElement('div');
        userCard.className = 'user-card';
        userCard.innerHTML = `
          <div class="user-info">
            <span class="user-name">${sanitizeInput(user.name)}</span>
            <span class="user-email">${sanitizeInput(user.email)}</span>
          </div>
          <div>
            <span class="status-badge ${user.status === 'banned' ? 'status-banned' : 'status-active'}">
              ${user.status === 'banned' ? 'محظور' : 'نشط'}
            </span>
            ${user.status === 'active' ? `<button class="sm-btn btn-ban" style="margin-right:6px;" onclick="banUserDirect('${user.email}')">حظر</button>` : ''}
          </div>
        `;
        usersListContainer.appendChild(userCard);

        // Banned Tab elements
        if (user.status === 'banned') {
          bannedCount++;
          const banCard = document.createElement('div');
          banCard.className = 'user-card';
          banCard.innerHTML = `
            <div class="user-info">
              <span class="user-name">${sanitizeInput(user.name)} (${sanitizeInput(user.email)})</span>
              <span class="user-email" style="color: #e74c3c;">السبب: ${sanitizeInput(user.banReason || 'غير محدد')}</span>
            </div>
            <button class="sm-btn btn-unban" onclick="unbanUser('${user.email}')"><i class="fas fa-unlock"></i> فك الحظر</button>
          `;
          bannedUsersContainer.appendChild(banCard);
        }
      });

      if (bannedCount === 0) {
        bannedUsersContainer.innerHTML = '<p style="color:#777; font-size:13px; text-align:center;">لا يوجد مستخدمين محظورين حالياً</p>';
      }
    }

    // Direct Ban Action
    window.banUserDirect = function(email) {
      const reason = prompt('أدخل سبب الحظر:');
      if (reason !== null) {
        performBan(email, reason);
      }
    };

    // Perform Ban
    function performBan(email, reason) {
      const targetUser = users.find(u => u.email.toLowerCase() === email.toLowerCase());
      if (targetUser) {
        targetUser.status = 'banned';
        targetUser.banReason = reason || 'تم الحظر بقرار من المدير';
      } else {
        // Add new banned record
        users.push({
          id: Date.now(),
          name: email.split('@')[0],
          email: email,
          status: 'banned',
          banReason: reason || 'تم الحظر بقرار من المدير'
        });
      }
      saveUserData();
      alert(`تم حظر المستخدم (${email}) بنجاح!`);
    }

    // Unban Action
    window.unbanUser = function(email) {
      const user = users.find(u => u.email.toLowerCase() === email.toLowerCase());
      if (user) {
        user.status = 'active';
        delete user.banReason;
        saveUserData();
        alert(`تم فك الحظر عن المستخدم (${email}) بنجاح!`);
      }
    };

    // Ban Form Handler
    banUserForm.addEventListener('submit', (e) => {
      e.preventDefault();
      const email = document.getElementById('banEmail').value;
      const reason = document.getElementById('banReason').value;
      performBan(email, reason);
      banUserForm.reset();
    });

    // Save Users Data
    function saveUserData() {
      localStorage.setItem('mrstoud_users', JSON.stringify(users));
      renderUsersAndBans();
    }

    // Open Player
    function openPlayer(show) {
      playerTitle.textContent = show.title;
      playerQuality.textContent = show.quality || 'عالية';
      
      if (show.isVideoLocal && show.videoObject) {
        const localBlobUrl = URL.createObjectURL(show.videoObject);
        videoPlayerBox.innerHTML = `<video controls autoplay style="width:100%; height:100%;"><source src="${localBlobUrl}" type="${show.videoObject.type}">متصفحك لا يدعم تشغيل هذا الفيديو</video>`;
      } else if (show.videoUrl) {
        const safeUrl = sanitizeInput(show.videoUrl);
        videoPlayerBox.innerHTML = `<iframe id="videoIframe" src="${safeUrl}" allowfullscreen></iframe>`;
      } else {
        videoPlayerBox.innerHTML = `<div style="padding:20px; text-align:center; color:#aaa;">لا يوجد فيديو متاح لهذا العمل</div>`;
      }
      
      if (show.downloadUrl) {
        downloadContainer.innerHTML = `
          <a href="${sanitizeInput(show.downloadUrl)}" download target="_blank" class="download-btn">
            <i class="fas fa-download"></i> تحميل الفيديو على الهاتف
          </a>
        `;
      } else {
        downloadContainer.innerHTML = '';
      }

      playerModal.classList.add('active');
    }

    // Save Data
    function saveData() {
      const cleanShows = shows.map(item => {
        const { videoObject, ...rest } = item;
        return rest;
      });
      localStorage.setItem('mrstoud_shows', JSON.stringify(cleanShows));
      renderShows();
      renderAdminList();
    }

    // Delete Show
    window.deleteShow = function(id) {
      if (confirm('هل أنت تأكد من حذف هذا الفيديو؟')) {
        shows = shows.filter(item => item.id !== id);
        saveData();
      }
    };

    // Edit Show
    window.editShow = function(id) {
      const show = shows.find(item => item.id === id);
      if (show) {
        document.getElementById('editShowId').value = show.id;
        document.getElementById('showTitle').value = show.title;
        document.getElementById('showBadge').value = show.badge || '';
        document.getElementById('showImage').value = show.image || '';
        document.getElementById('showVideoUrl').value = show.videoUrl || '';
        document.getElementById('showQuality').value = show.quality || '';
        document.getElementById('showDownloadUrl').value = show.downloadUrl || '';

        document.getElementById('formSubTitle').textContent = 'تعديل الفيديو الحالي';
        document.getElementById('saveBtn').textContent = 'حفظ التعديلات';
        cancelEditBtn.style.display = 'block';
      }
    };

    // Reset Form
    function resetAdminForm() {
      saveShowForm.reset();
      document.getElementById('editShowId').value = '';
      document.getElementById('formSubTitle').textContent = 'إضافة مسلسل / فيلم جديد';
      document.getElementById('saveBtn').textContent = 'حفظ وإضافة';
      cancelEditBtn.style.display = 'none';
    }

    cancelEditBtn.addEventListener('click', resetAdminForm);

    // Sidebar Handlers
    function toggleSidebar() {
      sidebar.classList.toggle('open');
      overlay.classList.toggle('active');
    }

    menuToggleBtn.addEventListener('click', toggleSidebar);
    closeSidebarBtn.addEventListener('click', toggleSidebar);
    overlay.addEventListener('click', toggleSidebar);

    // Search Toggle
    searchToggleBtn.addEventListener('click', () => {
      searchContainer.classList.toggle('active');
      if (searchContainer.classList.contains('active')) {
        searchInput.focus();
      }
    });

    searchInput.addEventListener('input', (e) => {
      renderShows(e.target.value);
    });

    // Close Modals
    closeModalBtns.forEach(btn => {
      btn.addEventListener('click', () => {
        loginModal.classList.remove('active');
        adminModal.classList.remove('active');
        playerModal.classList.remove('active');
        videoPlayerBox.innerHTML = '';
      });
    });

    // Admin Button Click
    adminBtn.addEventListener('click', () => {
      toggleSidebar();
      if (isAdminLoggedIn) {
        renderAdminList();
        renderUsersAndBans();
        adminModal.classList.add('active');
      } else {
        checkLockoutStatus();
        loginModal.classList.add('active');
      }
    });

    // Login Submission with Brute-Force Security
    loginForm.addEventListener('submit', (e) => {
      e.preventDefault();

      if (checkLockoutStatus()) return;

      const passwordInput = document.getElementById('adminPassword');
      const password = passwordInput.value;

      if (password === 'marwanhacker99') {
        isAdminLoggedIn = true;
        loginAttempts = 0;
        localStorage.setItem('mrstoud_login_attempts', '0');
        loginModal.classList.remove('active');
        renderAdminList();
        renderUsersAndBans();
        adminModal.classList.add('active');
        passwordInput.value = '';
        lockoutTimer.innerHTML = '';
      } else {
        loginAttempts++;
        localStorage.setItem('mrstoud_login_attempts', loginAttempts.toString());
        passwordInput.value = '';

        if (loginAttempts >= 3) {
          const lockoutTime = Date.now() + (24 * 60 * 60 * 1000);
          localStorage.setItem('mrstoud_lockout_until', lockoutTime.toString());
          lockoutUntil = lockoutTime;
          checkLockoutStatus();
          alert('⚠️ أدخلت كلمة المرور خاطئة 3 مرات! تم قفل لوحة الدخول لمدة 24 ساعة لأسباب أمنية.');
        } else {
          const remaining = 3 - loginAttempts;
          alert(`❌ كلمة المرور غير صحيحة! تبقّى لديك ${remaining} محاولة قبل الحظر لمدة 24 ساعة.`);
        }
      }
    });

    // Add / Edit Submission
    saveShowForm.addEventListener('submit', (e) => {
      e.preventDefault();
      const editId = document.getElementById('editShowId').value;
      const title = document.getElementById('showTitle').value;
      const badge = document.getElementById('showBadge').value;
      const image = document.getElementById('showImage').value;
      const videoUrl = document.getElementById('showVideoUrl').value;
      const quality = document.getElementById('showQuality').value;
      const downloadUrl = document.getElementById('showDownloadUrl').value;
      const fileInput = showVideoFile.files[0];

      if (editId) {
        const index = shows.findIndex(item => item.id == editId);
        if (index !== -1) {
          shows[index] = { 
            ...shows[index],
            title, 
            badge, 
            image, 
            videoUrl, 
            quality, 
            downloadUrl,
            ...(fileInput && { isVideoLocal: true, videoObject: fileInput })
          };
        }
      } else {
        const newShow = {
          id: Date.now(),
          title,
          badge,
          image,
          videoUrl,
          quality,
          downloadUrl,
          isVideoLocal: fileInput ? true : false,
          videoObject: fileInput || null
        };
        shows.unshift(newShow);
      }

      saveData();
      resetAdminForm();
      alert('تم إضافه المسلسل / الفيلم بنجاح وسيتوفر فوراً للعرض!');
    });

    // Initial Launch
    renderShows();
  </script>
</body>
</html>
