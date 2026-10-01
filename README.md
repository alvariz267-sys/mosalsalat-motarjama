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

    /* Sidebar Search Box */
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

    .sidebar-search-input:focus {
      border-color: var(--primary-color);
    }

    .sidebar-search-icon {
      position: absolute;
      left: 10px;
      top: 50%;
      transform: translateY(-50%);
      color: var(--text-secondary);
      font-size: 14px;
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

    /* Main Header Title */
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

    /* Main Container & Grid */
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

    .show-type-tag {
      position: absolute;
      top: 8px;
      left: 8px;
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
      top: 0; left: 0; width: 100%; height: 100%; border: 0;
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

    .download-btn:hover { background-color: #219150; }

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

    .admin-actions { display: flex; gap: 8px; }

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

    /* Multi-Server & Features CSS */
    .server-btn-group {
      display: flex;
      gap: 8px;
      margin-bottom: 12px;
      flex-wrap: wrap;
    }

    .server-btn {
      background: #1f1f1f;
      border: 1px solid var(--border-color);
      color: var(--text-color);
      padding: 8px 14px;
      border-radius: 6px;
      cursor: pointer;
      font-size: 13px;
      transition: all 0.2s;
    }

    .server-btn.active, .server-btn:hover {
      background: var(--primary-color);
      border-color: var(--primary-color);
    }

    /* Player Tools Bar (Subtitles & Enhance Controls) */
    .player-tools-bar {
      background: #141414;
      border: 1px solid var(--border-color);
      border-radius: 8px;
      padding: 12px;
      margin-bottom: 15px;
      display: flex;
      flex-direction: column;
      gap: 12px;
    }

    .tool-row {
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 10px;
      flex-wrap: wrap;
    }

    .tool-group {
      display: flex;
      align-items: center;
      gap: 8px;
      font-size: 13px;
      color: var(--text-secondary);
    }

    .tool-group select, .tool-group input[type="range"] {
      background: #222;
      color: #fff;
      border: 1px solid var(--border-color);
      padding: 5px 8px;
      border-radius: 4px;
      font-size: 12px;
      outline: none;
    }

    .slider-container {
      display: flex;
      align-items: center;
      gap: 6px;
      font-size: 12px;
    }

    .slider-container input {
      width: 90px;
      accent-color: var(--primary-color);
    }

    .comments-section {
      margin-top: 20px;
      border-top: 1px solid var(--border-color);
      padding-top: 15px;
    }

    .comments-title {
      font-size: 16px;
      font-weight: bold;
      margin-bottom: 12px;
      color: var(--primary-color);
    }

    .comment-item {
      background: #121212;
      border: 1px solid var(--border-color);
      padding: 10px 12px;
      border-radius: 6px;
      margin-bottom: 8px;
      font-size: 13px;
    }

    .comment-header {
      display: flex;
      justify-content: space-between;
      color: var(--text-secondary);
      font-size: 11px;
      margin-bottom: 4px;
    }
  </style>
</head>
<body>

  <!-- Hacker Blocked Overlay Screen -->
  <div id="hackerBlockedScreen">
    <i class="fas fa-user-ninja"></i>
    <h1 style="font-size: 28px; margin-bottom: 10px;">تم اكتشاف محاولة اختراق!</h1>
    <p style="color: #ccc; max-width: 500px; font-size: 15px; line-height: 1.6;">
      تم حظر جهازك ومعرفك فوراً بواسطة جدار حماية المنصة (MRSTOUD Firewall WAF). يُمنع منعاً باتاً الوصول إلى أي جزء من الموقع.
    </p>
    <div style="margin-top: 25px; font-size: 12px; color: #777;">
      IP status: <span style="color: red;">PERMANENTLY BANNED</span>
    </div>
  </div>

  <!-- Navigation Bar -->
  <nav class="navbar">
    <a href="#" class="brand" onclick="filterByCategory('all')">mrstoud</a>
    <div class="nav-actions">
      <button class="icon-btn" id="menuToggleBtn" title="القائمة الجانبية"><i class="fas fa-bars"></i></button>
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

    <!-- Sidebar Search Box -->
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
      <li>
        <a href="#" id="privacyBtn">
          <div class="sidebar-menu-left"><i class="fas fa-user-lock"></i> سياسة الخصوصية</div>
        </a>
      </li>
      <hr style="border-color: var(--border-color); margin: 15px 0;">
      <li><button id="adminBtn"><div class="sidebar-menu-left"><i class="fas fa-user-shield"></i> الإدارة</div></button></li>
    </ul>
  </aside>

  <!-- Main Content -->
  <main class="container">
    <div class="ad-banner">
      <p>📢 مساحة إعلانية - ضع كود الإعلان الخاص بك هنا (AdSense / Native Ads)</p>
    </div>

    <div class="section-title" id="sectionTitle">
      <i class="fas fa-play-circle"></i> جميع الأعمال
    </div>

    <div class="shows-grid" id="showsGrid"></div>
  </main>

  <!-- Welcome Modal for First-time Visitors -->
  <div class="modal" id="welcomeModal">
    <div class="modal-content" style="text-align: center; max-width: 450px;">
      <i class="fas fa-film" style="font-size: 50px; color: var(--primary-color); margin-bottom: 15px;"></i>
      <h2 style="margin-bottom: 10px; color: #fff;">مرحباً بك في منصة mrstoud!</h2>
      <p style="color: var(--text-secondary); font-size: 14px; line-height: 1.6; margin-bottom: 20px;">
        يسعدنا انضمامك إلينا. يمكنك الآن مشاهدة أحدث الأفلام والمسلسلات عالية الجودة بكل أمان وسهولة. نتمنى لك تجربة ممتعة!
      </p>
      <button class="btn closeModal">ابدأ المشاهدة الآن</button>
    </div>
  </div>

  <!-- Privacy Policy Modal -->
  <div class="modal" id="privacyModal">
    <div class="modal-content" style="max-width: 600px;">
      <div class="modal-header">
        <h3><i class="fas fa-user-lock"></i> سياسة الخصوصية</h3>
        <button class="close-btn closeModal">&times;</button>
      </div>
      <div style="font-size: 13px; color: #ccc; line-height: 1.7; display: flex; flex-direction: column; gap: 12px;">
        <p>مرحباً بك في منصة <strong>mrstoud</strong>. نحن نولي أهمية قصوى لخصوصية مستخدمينا وأمان بياناتهم الشخصية.</p>
        <h4 style="color: var(--primary-color); margin-top: 5px;">1. جمع البيانات</h4>
        <p>قد نقوم بجمع بعض البيانات غير الشخصية مثل نوع المتصفح، عنوان IP، والتعليقات التي توضع على المحتوى لغرض تحسين الأداء وتجربة المستخدم.</p>
        <h4 style="color: var(--primary-color); margin-top: 5px;">2. حماية البيانات وأمانها</h4>
        <p>نحن نستخدم أنظمة جدار حماية (WAF) متطورة لرصد أي هجمات أو محاولات اختراق وضمان حماية المستخدمين والسيرفرات من أي استغلال خبيث.</p>
        <h4 style="color: var(--primary-color); margin-top: 5px;">3. الإعلانات وملفات الكوكيز (Cookies)</h4>
        <p>قد تستخدم المنصة شبكات إعلانية خارجية (مثل Google AdSense) تضع ملفات تعريف ارتباط لتقديم إعلانات مخصصة للمستخدم بناءً على زياراته للموقع.</p>
        <h4 style="color: var(--primary-color); margin-top: 5px;">4. التعليقات والاستخدام المقبول</h4>
        <p>يتحمل المستخدم المسؤولية كاملة عن أي تعليق يتم نشره عبر المنصة، ويُمنع استخدام ألفاظ خرسانية أو محاولات إغراق، وتخضع المدخلات لفحص أمني آلي.</p>
      </div>
      <button class="btn closeModal" style="margin-top: 20px;">إغلاق</button>
    </div>
  </div>

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
          <strong>تنبيه أمني مشدد:</strong> هذه اللوحة محمية بنظام WAF لصد الهجمات. أي محاولة حقن أو تخمين ستؤدي لحظر الجهاز فوراً!
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

      <div class="admin-tabs">
        <button class="tab-btn active" onclick="switchAdminTab('tab-shows')"><i class="fas fa-film"></i> المسلسلات والأفلام</button>
        <button class="tab-btn" onclick="switchAdminTab('tab-users')"><i class="fas fa-users"></i> إدارة المستخدمين</button>
        <button class="tab-btn" onclick="switchAdminTab('tab-ban')"><i class="fas fa-user-slash"></i> الحظر وفك الحظر</button>
      </div>

      <!-- Tab 1: Shows & Movies -->
      <div id="tab-shows" class="tab-content active">
        <form id="saveShowForm" style="margin-bottom: 25px;">
          <input type="hidden" id="editShowId" value="">
          <h4 style="margin-bottom: 12px; color: var(--primary-color);" id="formSubTitle">إضافة عمل جديد (فيلم / مسلسل)</h4>
          
          <div class="form-group">
            <label for="showCategory">نوع العمل / التصنيف:</label>
            <select id="showCategory" required>
              <option value="series">مسلسل</option>
              <option value="movie">فيلم</option>
            </select>
          </div>

          <div class="form-group">
            <label for="showTitle">عنوان العمل:</label>
            <input type="text" id="showTitle" required placeholder="مثال: فيلم/مسلسل كامل">
          </div>
          
          <div class="form-group">
            <label for="showBadge">نص الشارة (مثال: حلقة 1 / 2:30 ساعة):</label>
            <input type="text" id="showBadge" placeholder="مثال: حلقة 1">
          </div>

          <div class="form-group">
            <label for="showImage">رابط صورة الغلاف (URL):</label>
            <input type="url" id="showImage" placeholder="https://example.com/image.jpg">
          </div>

          <div class="form-group" style="background: #181818; padding: 12px; border-radius: 8px; border: 1px dashed var(--primary-color);">
            <label for="showVideoFile" style="color: #fff; font-weight: bold;"><i class="fas fa-file-video"></i> اختيار فيديو من الهاتف:</label>
            <input type="file" id="showVideoFile" accept="video/*" style="padding: 6px; cursor: pointer;">
          </div>

          <div style="text-align: center; margin: 10px 0; color: var(--text-secondary); font-size: 12px;">— أو روابط السيرفرات الخارجية —</div>

          <div class="form-group">
            <label for="showVideoUrl">سيرفر المشغل الرئيسي (Server 1):</label>
            <input type="text" id="showVideoUrl" placeholder="https://www.youtube.com/embed/...">
          </div>

          <div class="form-group">
            <label for="showVideoUrl2">سيرفر المشغل الاحتياطي (Server 2):</label>
            <input type="text" id="showVideoUrl2" placeholder="https://www.youtube.com/embed/...">
          </div>

          <div class="form-group">
            <label for="showVideoUrl3">سيرفر المشغل السريع (Server 3):</label>
            <input type="text" id="showVideoUrl3" placeholder="https://www.youtube.com/embed/...">
          </div>

          <div class="form-group">
            <label for="showQuality">الجودة المتاحة:</label>
            <input type="text" id="showQuality" placeholder="مثال: 1080p, 720p" value="1080p Full HD">
          </div>

          <div class="form-group">
            <label for="showDownloadUrl">رابط تحميل الفيديو:</label>
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
        <h4 style="margin-bottom: 12px; color: var(--primary-color);">جميع المستخدمين المسجلين</h4>
        <div id="usersListContainer"></div>
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
            <input type="text" id="banReason" placeholder="مثال: محاولة اختراق أو مخالفة القوانين">
          </div>
          <button type="submit" class="btn btn-del"><i class="fas fa-user-slash"></i> تأكيد الحظر</button>
        </form>

        <hr style="border-color: var(--border-color); margin: 20px 0;">

        <h4 style="margin-bottom: 12px; color: #27ae60;">قائمة المحظورين</h4>
        <div id="bannedUsersContainer"></div>
      </div>

    </div>
  </div>

  <!-- Player Modal -->
  <div class="modal" id="playerModal">
    <div class="modal-content" style="max-width: 750px;">
      <div class="modal-header">
        <h3 id="playerTitle">عرض الفيديو</h3>
        <button class="close-btn closeModal">&times;</button>
      </div>

      <!-- Server Selector Section -->
      <div id="serverSelectorContainer" class="server-btn-group"></div>

      <!-- Interactive Player Tools (Subtitles, Quality & Audio Booster) -->
      <div class="player-tools-bar">
        <div class="tool-row">
          <div class="tool-group">
            <i class="fas fa-closed-captioning" style="color:var(--primary-color);"></i>
            <label>الترجمة الآلية:</label>
            <select id="subtitleSelect" onchange="applySubtitleLanguage(this.value)">
              <option value="ar">العربية (تلقائي)</option>
              <option value="en">الإنجليزية (English)</option>
              <option value="fr">الفرنسية (Français)</option>
              <option value="off">إيقاف الترجمة</option>
            </select>
          </div>

          <div class="tool-group">
            <i class="fas fa-sliders-h" style="color:var(--primary-color);"></i>
            <label>نمط الجودة:</label>
            <select id="qualityBoostSelect" onchange="applyQualityBoost(this.value)">
              <option value="standard">1080p قياسي</option>
              <option value="vivid">4K AI محصّن (ألوان مشبعة)</option>
              <option value="sharp">Ultra Sharp (وضوح حدة)</option>
            </select>
          </div>
        </div>

        <div class="tool-row">
          <div class="slider-container">
            <i class="fas fa-volume-up" style="color:#27ae60;"></i>
            <span>مضخم الصوت (Boost):</span>
            <input type="range" id="volumeBoostSlider" min="100" max="200" value="100" oninput="applyVolumeBoost(this.value)">
            <span id="volumeVal">100%</span>
          </div>

          <div class="slider-container">
            <i class="fas fa-sun" style="color:#f39c12;"></i>
            <span>السطوع:</span>
            <input type="range" id="brightnessSlider" min="80" max="150" value="100" oninput="applyVideoFilters()">
          </div>

          <div class="slider-container">
            <i class="fas fa-adjust" style="color:#3498db;"></i>
            <span>التباين:</span>
            <input type="range" id="contrastSlider" min="80" max="150" value="100" oninput="applyVideoFilters()">
          </div>
        </div>
      </div>

      <div class="video-container" id="videoPlayerBox"></div>

      <div class="video-details">
        <div class="quality-tags">
          <span style="font-size: 13px; color: var(--text-secondary);">الجودة المتاحة:</span>
          <span class="quality-tag" id="playerQuality">1080p</span>
        </div>
        <div id="downloadContainer"></div>
      </div>

      <!-- Comments Section -->
      <div class="comments-section">
        <div class="comments-title"><i class="fas fa-comments"></i> قسم التعليقات</div>
        
        <form id="commentForm" style="margin-bottom: 15px;">
          <div class="form-group">
            <input type="text" id="commentUserName" placeholder="اسمك (اختياري)" style="margin-bottom: 8px;">
            <textarea id="commentText" rows="2" placeholder="اكتب تعليقك هنا..." required></textarea>
          </div>
          <button type="submit" class="btn" style="padding: 8px 15px; font-size: 13px;">إرسال التعليق</button>
        </form>

        <div id="commentsList"></div>
      </div>

    </div>
  </div>

  <script>
    /* =========================================================
       🔐 ADVANCED ANTI-HACK & SECURITY SYSTEM (WAF)
       ========================================================= */

    function checkGlobalBanStatus() {
      // إذا كان المالك موثقاً نهائياً، امنع تفعيل الحظر تماماً
      if (localStorage.getItem('mrstoud_verified_owner') === 'true') {
        return;
      }
      if (localStorage.getItem('mrstoud_is_hacker_banned') === 'true') {
        document.getElementById('hackerBlockedScreen').style.display = 'flex';
        throw new Error('Access denied: Security violation detected.');
      }
    }

    function triggerAutoHackerBan(reason) {
      // استثناء المدير المالك الموثق نهائياً من أي حظر
      if (localStorage.getItem('mrstoud_verified_owner') === 'true') {
        return;
      }

      localStorage.setItem('mrstoud_is_hacker_banned', 'true');
      
      let users = JSON.parse(localStorage.getItem('mrstoud_users')) || defaultUsers;
      users.push({
        id: Date.now(),
        name: "Hacker Detected",
        email: "HACK_ATTEMPT_" + Math.floor(Math.random() * 10000),
        status: "banned",
        banReason: "محاولة اختراق النظام (" + reason + ")"
      });
      localStorage.setItem('mrstoud_users', JSON.stringify(users));

      document.getElementById('hackerBlockedScreen').style.display = 'flex';
    }

    function inspectSecurityInput(inputStr) {
      if (!inputStr) return inputStr;

      const attackPatterns = [
        /<script\b[^>]*>([\s\S]*?)<\/script>/gi,
        /javascript:/gi,
        /onerror=/gi,
        /onload=/gi,
        /SELECT\s+.*\s+FROM/gi,
        /UNION\s+SELECT/gi,
        /INSERT\s+INTO/gi,
        /DELETE\s+FROM/gi,
        /DROP\s+TABLE/gi,
        /'\s*OR\s*'\d+'='\d+/gi,
        /--/g,
        /\.\.\//g
      ];

      for (let pattern of attackPatterns) {
        if (pattern.test(inputStr)) {
          triggerAutoHackerBan("حقن أكواد خبيثة: " + pattern.toString());
          return '';
        }
      }
      return inputStr;
    }

    let requestHistory = [];
    function checkRateLimit() {
      if (localStorage.getItem('mrstoud_verified_owner') === 'true') return;
      const now = Date.now();
      requestHistory.push(now);
      requestHistory = requestHistory.filter(timestamp => now - timestamp < 5000);
      
      if (requestHistory.length > 25) {
        triggerAutoHackerBan("هجوم إغراق DDoS / Rate-Limit Exceeded");
      }
    }

    document.addEventListener('input', (e) => {
      checkRateLimit();
      if (e.target.tagName === 'INPUT' || e.target.tagName === 'TEXTAREA') {
        inspectSecurityInput(e.target.value);
      }
    });

    function sanitizeInput(str) {
      if (!str) return '';
      inspectSecurityInput(str);
      const temp = document.createElement('div');
      temp.textContent = str;
      return temp.innerHTML;
    }

    checkGlobalBanStatus();

    /* =========================================================
       DATA & APPLICATION LOGIC
       ========================================================= */

    const defaultShows = [
      {
        id: 1,
        category: "series",
        title: "مسلسل في السابعة عشر",
        badge: "حلقة 1",
        image: "https://images.unsplash.com/photo-1536440136628-849c177e76a1?auto=format&fit=crop&w=400&q=80",
        videoUrl: "https://www.youtube.com/embed/dQw4w9WgXcQ",
        videoUrl2: "",
        videoUrl3: "",
        quality: "1080p Full HD",
        downloadUrl: "https://example.com/download.mp4"
      },
      {
        id: 2,
        category: "movie",
        title: "فيلم الأكشن والمغامرة",
        badge: "2:15 ساعة",
        image: "https://images.unsplash.com/photo-1489599849927-2ee91cede3ba?auto=format&fit=crop&w=400&q=80",
        videoUrl: "https://www.youtube.com/embed/dQw4w9WgXcQ",
        videoUrl2: "",
        videoUrl3: "",
        quality: "4K Ultra HD",
        downloadUrl: "https://example.com/download.mp4"
      }
    ];

    const defaultUsers = [
      { id: 101, name: "أحمد علي", email: "ahmed@example.com", status: "active" },
      { id: 102, name: "محمد ياسين", email: "mowin@example.com", status: "active" }
    ];

    let shows = JSON.parse(localStorage.getItem('mrstoud_shows')) || defaultShows;
    let users = JSON.parse(localStorage.getItem('mrstoud_users')) || defaultUsers;
    let commentsData = JSON.parse(localStorage.getItem('mrstoud_comments')) || {};
    let currentShowId = null;
    let currentCategory = 'all';
    let isAdminLoggedIn = false;

    let loginAttempts = parseInt(localStorage.getItem('mrstoud_login_attempts') || '0');
    let lockoutUntil = parseInt(localStorage.getItem('mrstoud_lockout_until') || '0');
    
    // عداد الإدخال الناجح لكلمة المرور للمالك
    let ownerCorrectStreak = parseInt(localStorage.getItem('mrstoud_owner_streak') || '0');

    // DOM Elements
    const showsGrid = document.getElementById('showsGrid');
    const menuToggleBtn = document.getElementById('menuToggleBtn');
    const closeSidebarBtn = document.getElementById('closeSidebarBtn');
    const sidebar = document.getElementById('sidebar');
    const overlay = document.getElementById('overlay');
    const sidebarSearchInput = document.getElementById('sidebarSearchInput');
    const sectionTitle = document.getElementById('sectionTitle');
    
    const countAll = document.getElementById('countAll');
    const countSeries = document.getElementById('countSeries');
    const countMovies = document.getElementById('countMovies');

    const adminBtn = document.getElementById('adminBtn');
    const privacyBtn = document.getElementById('privacyBtn');
    const loginModal = document.getElementById('loginModal');
    const adminModal = document.getElementById('adminModal');
    const playerModal = document.getElementById('playerModal');
    const welcomeModal = document.getElementById('welcomeModal');
    const privacyModal = document.getElementById('privacyModal');
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

    const videoPlayerBox = document.getElementById('videoPlayerBox');
    const playerTitle = document.getElementById('playerTitle');
    const playerQuality = document.getElementById('playerQuality');
    const downloadContainer = document.getElementById('downloadContainer');
    const serverSelectorContainer = document.getElementById('serverSelectorContainer');
    const commentForm = document.getElementById('commentForm');
    const commentsList = document.getElementById('commentsList');

    // Elements for Video Adjustments
    const brightnessSlider = document.getElementById('brightnessSlider');
    const contrastSlider = document.getElementById('contrastSlider');
    const volumeBoostSlider = document.getElementById('volumeBoostSlider');
    const volumeVal = document.getElementById('volumeVal');
    const subtitleSelect = document.getElementById('subtitleSelect');
    const qualityBoostSelect = document.getElementById('qualityBoostSelect');

    // Audio & Video Enhance Functions
    window.applyVideoFilters = function() {
      const b = brightnessSlider.value;
      const c = contrastSlider.value;
      const target = videoPlayerBox.querySelector('iframe') || videoPlayerBox.querySelector('video');
      if (target) {
        target.style.filter = `brightness(${b}%) contrast(${c}%)`;
      }
    };

    window.applyVolumeBoost = function(val) {
      volumeVal.textContent = `${val}%`;
      const videoEl = videoPlayerBox.querySelector('video');
      if (videoEl) {
        videoEl.volume = Math.min(val / 100, 1.0);
      }
    };

    window.applySubtitleLanguage = function(lang) {
      const videoEl = videoPlayerBox.querySelector('video');
      if (videoEl && videoEl.textTracks && videoEl.textTracks.length > 0) {
        for (let i = 0; i < videoEl.textTracks.length; i++) {
          videoEl.textTracks[i].mode = (videoEl.textTracks[i].language === lang) ? 'showing' : 'disabled';
        }
      }
    };

    window.applyQualityBoost = function(type) {
      if (type === 'vivid') {
        brightnessSlider.value = 110;
        contrastSlider.value = 125;
      } else if (type === 'sharp') {
        brightnessSlider.value = 105;
        contrastSlider.value = 115;
      } else {
        brightnessSlider.value = 100;
        contrastSlider.value = 100;
      }
      applyVideoFilters();
    };

    function resetVideoTools() {
      brightnessSlider.value = 100;
      contrastSlider.value = 100;
      volumeBoostSlider.value = 100;
      volumeVal.textContent = '100%';
      subtitleSelect.value = 'ar';
      qualityBoostSelect.value = 'standard';
    }

    // First visit welcome check
    function checkFirstVisit() {
      if (!localStorage.getItem('mrstoud_visited_before')) {
        welcomeModal.classList.add('active');
        localStorage.setItem('mrstoud_visited_before', 'true');
      }
    }

    window.switchAdminTab = function(tabId) {
      document.querySelectorAll('.tab-btn').forEach(btn => btn.classList.remove('active'));
      document.querySelectorAll('.tab-content').forEach(content => content.classList.remove('active'));

      event.currentTarget.classList.add('active');
      document.getElementById(tabId).classList.add('active');
    };

    function updateCounters() {
      const seriesCount = shows.filter(s => s.category === 'series').length;
      const moviesCount = shows.filter(s => s.category === 'movie').length;

      countAll.textContent = shows.length;
      countSeries.textContent = seriesCount;
      countMovies.textContent = moviesCount;
    }

    function checkLockoutStatus() {
      // إذا كان المالك موثقاً نهائياً، لا يوجد قفل أبداً
      if (localStorage.getItem('mrstoud_verified_owner') === 'true') {
        return false;
      }

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

    function renderShows(filterText = '') {
      showsGrid.innerHTML = '';
      const cleanFilter = sanitizeInput(filterText.toLowerCase());

      let filtered = shows;

      if (currentCategory === 'series') {
        filtered = filtered.filter(show => show.category === 'series');
      } else if (currentCategory === 'movie') {
        filtered = filtered.filter(show => show.category === 'movie');
      }

      if (cleanFilter) {
        filtered = filtered.filter(show => show.title.toLowerCase().includes(cleanFilter));
      }

      if (filtered.length === 0) {
        showsGrid.innerHTML = '<p style="grid-column: 1/-1; text-align: center; color: #777; padding: 30px;">لا توجد أية نتائج مطابقة لهذا القسم أو البحث</p>';
        return;
      }

      filtered.forEach(show => {
        const card = document.createElement('div');
        card.className = 'show-card';
        card.onclick = () => openPlayer(show);
        card.innerHTML = `
          ${show.badge ? `<div class="show-badge">${sanitizeInput(show.badge)}</div>` : ''}
          <div class="show-type-tag">${show.category === 'movie' ? 'فيلم' : 'مسلسل'}</div>
          <img src="${sanitizeInput(show.image) || 'https://via.placeholder.com/300x400/222/fff?text=mrstoud'}" alt="${sanitizeInput(show.title)}" class="show-thumb" onerror="this.src='https://via.placeholder.com/300x400/222/fff?text=mrstoud'">
          <div class="show-info">
            <div class="show-title">${sanitizeInput(show.title)}</div>
          </div>
        `;
        showsGrid.appendChild(card);
      });

      updateCounters();
    }

    window.filterByCategory = function(category, event = null) {
      currentCategory = category;
      
      document.querySelectorAll('.sidebar-menu a').forEach(a => a.classList.remove('active-link'));
      if (event && event.currentTarget) {
        event.currentTarget.classList.add('active-link');
      }

      if (category === 'series') {
        sectionTitle.innerHTML = '<i class="fas fa-tv"></i> قائمة المسلسلات';
      } else if (category === 'movie') {
        sectionTitle.innerHTML = '<i class="fas fa-film"></i> قائمة الأفلام';
      } else {
        sectionTitle.innerHTML = '<i class="fas fa-play-circle"></i> جميع الأعمال';
      }

      renderShows(sidebarSearchInput.value);
    };

    sidebarSearchInput.addEventListener('input', (e) => {
      renderShows(e.target.value);
    });

    function renderAdminList() {
      adminShowsList.innerHTML = '';
      shows.forEach(show => {
        const item = document.createElement('div');
        item.className = 'admin-item';
        item.innerHTML = `
          <div class="admin-item-title">[${show.category === 'movie' ? 'فيلم' : 'مسلسل'}] ${sanitizeInput(show.title)}</div>
          <div class="admin-actions">
            <button class="sm-btn btn-edit" onclick="editShow(${show.id})"><i class="fas fa-edit"></i> تعديل</button>
            <button class="sm-btn btn-del" onclick="deleteShow(${show.id})"><i class="fas fa-trash"></i> حذف</button>
          </div>
        `;
        adminShowsList.appendChild(item);
      });
    }

    function renderUsersAndBans() {
      usersListContainer.innerHTML = '';
      bannedUsersContainer.innerHTML = '';
      let bannedCount = 0;

      users.forEach(user => {
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

    window.banUserDirect = function(email) {
      const reason = prompt('أدخل سبب الحظر:');
      if (reason !== null) {
        performBan(email, reason);
      }
    };

    function performBan(email, reason) {
      const targetUser = users.find(u => u.email.toLowerCase() === email.toLowerCase());
      if (targetUser) {
        targetUser.status = 'banned';
        targetUser.banReason = reason || 'تم الحظر بقرار من المدير';
      } else {
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

    window.unbanUser = function(email) {
      const user = users.find(u => u.email.toLowerCase() === email.toLowerCase());
      if (user) {
        user.status = 'active';
        delete user.banReason;
        saveUserData();
        alert(`تم فك الحظر عن المستخدم (${email}) بنجاح!`);
      }
    };

    banUserForm.addEventListener('submit', (e) => {
      e.preventDefault();
      const email = document.getElementById('banEmail').value;
      const reason = document.getElementById('banReason').value;
      performBan(email, reason);
      banUserForm.reset();
    });

    function saveUserData() {
      localStorage.setItem('mrstoud_users', JSON.stringify(users));
      renderUsersAndBans();
    }

    /* Multi-Server & Video Stream Logic with Subtitles */
    function playVideoServer(url, isLocal = false, localObj = null) {
      if (isLocal && localObj) {
        const localBlobUrl = URL.createObjectURL(localObj);
        videoPlayerBox.innerHTML = `
          <video controls autoplay style="width:100%; height:100%;">
            <source src="${localBlobUrl}" type="${localObj.type}">
            <track kind="subtitles" srclang="ar" label="العربية" default>
            <track kind="subtitles" srclang="en" label="English">
            <track kind="subtitles" srclang="fr" label="Français">
            متصفحك لا يدعم تشغيل هذا الفيديو
          </video>`;
      } else if (url) {
        const safeUrl = sanitizeInput(url);
        videoPlayerBox.innerHTML = `<iframe id="videoIframe" src="${safeUrl}" allowfullscreen></iframe>`;
      } else {
        videoPlayerBox.innerHTML = `<div style="padding:20px; text-align:center; color:#aaa;">لا يوجد فيديو متاح في هذا السيرفر</div>`;
      }
      applyVideoFilters();
    }

    function renderServerButtons(show) {
      serverSelectorContainer.innerHTML = '';
      const servers = [];

      if (show.isVideoLocal) {
        servers.push({ name: 'سيرفر الهاتف المحلي', action: () => playVideoServer(null, true, show.videoObject) });
      }
      if (show.videoUrl) {
        servers.push({ name: 'سيرفر 1 (الرئيسي)', action: () => playVideoServer(show.videoUrl) });
      }
      if (show.videoUrl2) {
        servers.push({ name: 'سيرفر 2 (احتياطي)', action: () => playVideoServer(show.videoUrl2) });
      }
      if (show.videoUrl3) {
        servers.push({ name: 'سيرفر 3 (سريع)', action: () => playVideoServer(show.videoUrl3) });
      }

      if (servers.length > 1) {
        servers.forEach((srv, index) => {
          const btn = document.createElement('button');
          btn.className = `server-btn ${index === 0 ? 'active' : ''}`;
          btn.innerHTML = `<i class="fas fa-server"></i> ${srv.name}`;
          btn.onclick = (e) => {
            document.querySelectorAll('.server-btn').forEach(b => b.classList.remove('active'));
            btn.classList.add('active');
            srv.action();
          };
          serverSelectorContainer.appendChild(btn);
        });
      }
    }

    /* Comments Handling */
    function renderComments(showId) {
      commentsList.innerHTML = '';
      const list = commentsData[showId] || [];

      if (list.length === 0) {
        commentsList.innerHTML = '<p style="color:#777; font-size:12px; text-align:center;">لا توجد تعليقات بعد. كن أول من يعلق!</p>';
        return;
      }

      list.forEach(item => {
        const commentBox = document.createElement('div');
        commentBox.className = 'comment-item';
        commentBox.innerHTML = `
          <div class="comment-header">
            <span><i class="fas fa-user-circle"></i> ${sanitizeInput(item.user)}</span>
            <span>${item.date}</span>
          </div>
          <div>${sanitizeInput(item.text)}</div>
        `;
        commentsList.appendChild(commentBox);
      });
    }

    commentForm.addEventListener('submit', (e) => {
      e.preventDefault();
      const nameInput = document.getElementById('commentUserName');
      const textInput = document.getElementById('commentText');

      const userName = nameInput.value.trim() || 'زائر';
      const commentText = textInput.value.trim();

      if (commentText && currentShowId) {
        if (!commentsData[currentShowId]) {
          commentsData[currentShowId] = [];
        }

        const newComment = {
          user: userName,
          text: commentText,
          date: new Date().toLocaleDateString('ar-EG')
        };

        commentsData[currentShowId].unshift(newComment);
        localStorage.setItem('mrstoud_comments', JSON.stringify(commentsData));

        renderComments(currentShowId);
        textInput.value = '';
      }
    });

    function openPlayer(show) {
      currentShowId = show.id;
      playerTitle.textContent = show.title;
      playerQuality.textContent = show.quality || 'عالية';
      
      resetVideoTools();
      renderServerButtons(show);

      if (show.isVideoLocal && show.videoObject) {
        playVideoServer(null, true, show.videoObject);
      } else {
        playVideoServer(show.videoUrl);
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

      renderComments(show.id);
      playerModal.classList.add('active');
    }

    function saveData() {
      const cleanShows = shows.map(item => {
        const { videoObject, ...rest } = item;
        return rest;
      });
      localStorage.setItem('mrstoud_shows', JSON.stringify(cleanShows));
      renderShows(sidebarSearchInput.value);
      renderAdminList();
    }

    window.deleteShow = function(id) {
      if (confirm('هل أنت تأكد من حذف هذا الفيديو؟')) {
        shows = shows.filter(item => item.id !== id);
        saveData();
      }
    };

    window.editShow = function(id) {
      const show = shows.find(item => item.id === id);
      if (show) {
        document.getElementById('editShowId').value = show.id;
        document.getElementById('showCategory').value = show.category || 'series';
        document.getElementById('showTitle').value = show.title;
        document.getElementById('showBadge').value = show.badge || '';
        document.getElementById('showImage').value = show.image || '';
        document.getElementById('showVideoUrl').value = show.videoUrl || '';
        document.getElementById('showVideoUrl2').value = show.videoUrl2 || '';
        document.getElementById('showVideoUrl3').value = show.videoUrl3 || '';
        document.getElementById('showQuality').value = show.quality || '';
        document.getElementById('showDownloadUrl').value = show.downloadUrl || '';

        document.getElementById('formSubTitle').textContent = 'تعديل العمل الحالي';
        document.getElementById('saveBtn').textContent = 'حفظ التعديلات';
        cancelEditBtn.style.display = 'block';
      }
    };

    function resetAdminForm() {
      saveShowForm.reset();
      document.getElementById('editShowId').value = '';
      document.getElementById('formSubTitle').textContent = 'إضافة عمل جديد (فيلم / مسلسل)';
      document.getElementById('saveBtn').textContent = 'حفظ وإضافة';
      cancelEditBtn.style.display = 'none';
    }

    cancelEditBtn.addEventListener('click', resetAdminForm);

    function toggleSidebar() {
      sidebar.classList.toggle('open');
      overlay.classList.toggle('active');
    }

    menuToggleBtn.addEventListener('click', toggleSidebar);
    closeSidebarBtn.addEventListener('click', toggleSidebar);
    overlay.addEventListener('click', toggleSidebar);

    privacyBtn.addEventListener('click', () => {
      toggleSidebar();
      privacyModal.classList.add('active');
    });

    closeModalBtns.forEach(btn => {
      btn.addEventListener('click', () => {
        welcomeModal.classList.remove('active');
        loginModal.classList.remove('active');
        adminModal.classList.remove('active');
        playerModal.classList.remove('active');
        privacyModal.classList.remove('active');
        videoPlayerBox.innerHTML = '';
      });
    });

    adminBtn.addEventListener('click', () => {
      toggleSidebar();
      if (isAdminLoggedIn || localStorage.getItem('mrstoud_verified_owner') === 'true') {
        renderAdminList();
        renderUsersAndBans();
        adminModal.classList.add('active');
      } else {
        checkLockoutStatus();
        loginModal.classList.add('active');
      }
    });

    loginForm.addEventListener('submit', (e) => {
      e.preventDefault();
      if (checkLockoutStatus()) return;

      const passwordInput = document.getElementById('adminPassword');
      const password = passwordInput.value;

      inspectSecurityInput(password);

      if (password === 'marwanhacker99') {
        isAdminLoggedIn = true;
        loginAttempts = 0;
        localStorage.setItem('mrstoud_login_attempts', '0');
        
        // زيادة عداد إدخال الكود الصحيح للمالك
        if (localStorage.getItem('mrstoud_verified_owner') !== 'true') {
          ownerCorrectStreak++;
          localStorage.setItem('mrstoud_owner_streak', ownerCorrectStreak.toString());
          
          if (ownerCorrectStreak >= 5) {
            localStorage.setItem('mrstoud_verified_owner', 'true');
            alert('🎉 تم توثيقك رسمياً بأنك المدير المالك للمنصة! لن يتم حظرك نهائياً.');
          }
        }

        loginModal.classList.remove('active');
        renderAdminList();
        renderUsersAndBans();
        adminModal.classList.add('active');
        passwordInput.value = '';
        lockoutTimer.innerHTML = '';
      } else {
        // إذا كتب كلمة المرور خطأ، يتم تصفير عداد الـ 5 مرات المتتالية للتوثيق
        ownerCorrectStreak = 0;
        localStorage.setItem('mrstoud_owner_streak', '0');

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

    saveShowForm.addEventListener('submit', (e) => {
      e.preventDefault();
      const editId = document.getElementById('editShowId').value;
      const category = document.getElementById('showCategory').value;
      const title = document.getElementById('showTitle').value;
      const badge = document.getElementById('showBadge').value;
      const image = document.getElementById('showImage').value;
      const videoUrl = document.getElementById('showVideoUrl').value;
      const videoUrl2 = document.getElementById('showVideoUrl2').value;
      const videoUrl3 = document.getElementById('showVideoUrl3').value;
      const quality = document.getElementById('showQuality').value;
      const downloadUrl = document.getElementById('showDownloadUrl').value;
      const fileInput = showVideoFile.files[0];

      if (editId) {
        const index = shows.findIndex(item => item.id == editId);
        if (index !== -1) {
          shows[index] = { 
            ...shows[index],
            category, title, badge, image, videoUrl, videoUrl2, videoUrl3, quality, downloadUrl,
            ...(fileInput && { isVideoLocal: true, videoObject: fileInput })
          };
        }
      } else {
        const newShow = {
          id: Date.now(),
          category, title, badge, image, videoUrl, videoUrl2, videoUrl3, quality, downloadUrl,
          isVideoLocal: fileInput ? true : false,
          videoObject: fileInput || null
        };
        shows.unshift(newShow);
      }

      saveData();
      resetAdminForm();
      alert('تم إضافة العمل بنجاح وسيتوفر فوراً للعرض!');
    });

    renderShows();
    checkFirstVisit();
  </script>
</body>
</html>
