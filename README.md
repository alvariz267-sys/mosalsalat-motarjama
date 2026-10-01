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
      max-width: 550px;
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

    .btn:hover {
      background-color: var(--primary-hover);
    }

    .btn-secondary {
      background-color: #333;
      margin-top: 8px;
    }

    .btn-secondary:hover {
      background-color: #444;
    }

    /* Video Player Modal Elements */
    .video-container {
      position: relative;
      padding-bottom: 56.25%; /* 16:9 Aspect Ratio */
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
      <form id="loginForm">
        <div class="form-group">
          <label for="adminPassword">كلمة المرور:</label>
          <input type="password" id="adminPassword" placeholder="أدخل كلمة المرور" required>
        </div>
        <button type="submit" class="btn">دخول</button>
      </form>
    </div>
  </div>

  <!-- Admin Control Panel Modal -->
  <div class="modal" id="adminModal">
    <div class="modal-content">
      <div class="modal-header">
        <h3 id="adminModalTitle">إدارة الفيديوهات والمحتوى</h3>
        <button class="close-btn closeModal">&times;</button>
      </div>

      <!-- Add/Edit Form -->
      <form id="saveShowForm" style="margin-bottom: 25px;">
        <input type="hidden" id="editShowId" value="">
        <h4 style="margin-bottom: 12px; color: var(--primary-color);" id="formSubTitle">إضافة مسلسل / فيلم جديد</h4>
        
        <div class="form-group">
          <label for="showTitle">عنوان العمل:</label>
          <input type="text" id="showTitle" required placeholder="مثال: مسلسل في السابعة عشر">
        </div>
        
        <div class="form-group">
          <label for="showBadge">نص الشارة (اختياري):</label>
          <input type="text" id="showBadge" placeholder="مثال: حلقة 22 / فيلم">
        </div>

        <div class="form-group">
          <label for="showImage">رابط صورة الغلاف (URL):</label>
          <input type="url" id="showImage" placeholder="https://example.com/image.jpg">
        </div>

        <!-- إضافة خيار رفع فيديو من ملفات الهاتف -->
        <div class="form-group" style="background: #181818; padding: 12px; border-radius: 8px; border: 1px dashed var(--primary-color);">
          <label for="showVideoFile" style="color: #fff; font-weight: bold;"><i class="fas fa-file-video"></i> اختيار فيديو من ملفات الهاتف:</label>
          <input type="file" id="showVideoFile" accept="video/*" style="padding: 6px; cursor: pointer;">
          <small style="color: var(--text-secondary); display: block; margin-top: 4px;">اختر ملف فيديو مباشر من ذاكرة جهازك</small>
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

      <!-- Manage List -->
      <hr style="border-color: var(--border-color); margin-bottom: 15px;">
      <h4 style="margin-bottom: 12px;">قائمة الفيديوهات الحالية</h4>
      <div id="adminShowsList">
        <!-- List Items loaded dynamically -->
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
      
      <!-- إمكانية التبديل بين Iframe ومُشغل فيديو HTML5 محلي -->
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
    // Initial Data
    const defaultShows = [
      {
        id: 1,
        title: "مسلسل في السابعة عشر",
        badge: "حلقة 1",
        image: "https://images.unsplash.com/photo-1536440136628-849c177e76a1?auto=format&fit=crop&w=400&q=80",
        videoUrl: "https://www.youtube.com/embed/dQw4w9WgXcQ",
        quality: "1080p Full HD",
        downloadUrl: "https://example.com/download.mp4"
      },
      {
        id: 2,
        title: "مسلسل هذا البحر سوف يفيض",
        badge: "جديد",
        image: "https://images.unsplash.com/photo-1489599849927-2ee91cede3ba?auto=format&fit=crop&w=400&q=80",
        videoUrl: "https://www.youtube.com/embed/dQw4w9WgXcQ",
        quality: "720p HD",
        downloadUrl: "https://example.com/download.mp4"
      }
    ];

    // Storage Initialization
    let shows = JSON.parse(localStorage.getItem('mrstoud_shows')) || defaultShows;
    let isAdminLoggedIn = false;

    // DOM Elements
    const showsGrid = document.getElementById('showsGrid');
    const menuToggleBtn = document.getElementById('menuToggleBtn');
    const closeSidebarBtn = document.getElementById('closeSidebarBtn');
    const sidebar = document.getElementById('sidebar');
    const overlay = document.getElementById('overlay');
    const searchToggleBtn = document.getElementById('searchToggleBtn');
    const searchContainer = document.getElementById('searchContainer');
    const searchInput = document.getElementById('searchInput');
    
    // Admin & Modals DOM
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

    // Player Elements
    const videoPlayerBox = document.getElementById('videoPlayerBox');
    const videoIframe = document.getElementById('videoIframe');
    const playerTitle = document.getElementById('playerTitle');
    const playerQuality = document.getElementById('playerQuality');
    const downloadContainer = document.getElementById('downloadContainer');

    // Render Grid for Visitors
    function renderShows(filterText = '') {
      showsGrid.innerHTML = '';
      const filtered = shows.filter(show => show.title.toLowerCase().includes(filterText.toLowerCase()));

      if (filtered.length === 0) {
        showsGrid.innerHTML = '<p style="grid-column: 1/-1; text-align: center; color: #777; padding: 20px;">لا توجد نتائج مطابقة</p>';
        return;
      }

      filtered.forEach(show => {
        const card = document.createElement('div');
        card.className = 'show-card';
        card.onclick = () => openPlayer(show);
        card.innerHTML = `
          ${show.badge ? `<div class="show-badge">${show.badge}</div>` : ''}
          <img src="${show.image || 'https://via.placeholder.com/300x400/222/fff?text=mrstoud'}" alt="${show.title}" class="show-thumb" onerror="this.src='https://via.placeholder.com/300x400/222/fff?text=mrstoud'">
          <div class="show-info">
            <div class="show-title">${show.title}</div>
          </div>
        `;
        showsGrid.appendChild(card);
      });
    }

    // Render Admin List inside Admin Panel
    function renderAdminList() {
      adminShowsList.innerHTML = '';
      shows.forEach(show => {
        const item = document.createElement('div');
        item.className = 'admin-item';
        item.innerHTML = `
          <div class="admin-item-title">${show.title}</div>
          <div class="admin-actions">
            <button class="sm-btn btn-edit" onclick="editShow(${show.id})"><i class="fas fa-edit"></i> تعديل</button>
            <button class="sm-btn btn-del" onclick="deleteShow(${show.id})"><i class="fas fa-trash"></i> حذف</button>
          </div>
        `;
        adminShowsList.appendChild(item);
      });
    }

    // Open Player
    function openPlayer(show) {
      playerTitle.textContent = show.title;
      playerQuality.textContent = show.quality || 'عالية';
      
      // التمييز بين ملف فيديو محلي رفع من الهاتف ورابط خارجي
      if (show.isVideoLocal) {
        videoPlayerBox.innerHTML = `<video controls autoplay style="width:100%; height:100%;"><source src="${show.videoUrl}" type="video/mp4">متصفحك لا يدعم هذا الفيديو</video>`;
      } else {
        videoPlayerBox.innerHTML = `<iframe id="videoIframe" src="${show.videoUrl || ''}" allowfullscreen></iframe>`;
      }
      
      if (show.downloadUrl || show.isVideoLocal) {
        const dUrl = show.downloadUrl || show.videoUrl;
        downloadContainer.innerHTML = `
          <a href="${dUrl}" download target="_blank" class="download-btn">
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
      try {
        localStorage.setItem('mrstoud_shows', JSON.stringify(shows));
      } catch (e) {
        alert('حجم ملف الفيديو كبير جداً للتخزين الداخلي المحلي! يفضل استخدام الفيديوهات الخفيفة.');
      }
      renderShows();
      renderAdminList();
    }

    // Delete Show (Admin Only)
    window.deleteShow = function(id) {
      if (confirm('هل أنت تأكد من حذف هذا الفيديو؟')) {
        shows = shows.filter(item => item.id !== id);
        saveData();
      }
    };

    // Edit Show (Admin Only)
    window.editShow = function(id) {
      const show = shows.find(item => item.id === id);
      if (show) {
        document.getElementById('editShowId').value = show.id;
        document.getElementById('showTitle').value = show.title;
        document.getElementById('showBadge').value = show.badge || '';
        document.getElementById('showImage').value = show.image || '';
        document.getElementById('showVideoUrl').value = show.isVideoLocal ? '' : (show.videoUrl || '');
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
        videoPlayerBox.innerHTML = `<iframe id="videoIframe" src="" allowfullscreen></iframe>`; // Stop video
      });
    });

    // Admin Button Click
    adminBtn.addEventListener('click', () => {
      toggleSidebar();
      if (isAdminLoggedIn) {
        renderAdminList();
        adminModal.classList.add('active');
      } else {
        loginModal.classList.add('active');
      }
    });

    // Login Submission
    loginForm.addEventListener('submit', (e) => {
      e.preventDefault();
      const password = document.getElementById('adminPassword').value;
      if (password === 'marwanhacker99') {
        isAdminLoggedIn = true;
        loginModal.classList.remove('active');
        renderAdminList();
        adminModal.classList.add('active');
        document.getElementById('adminPassword').value = '';
      } else {
        alert('كلمة المرور غير صحيحة!');
      }
    });

    // Add / Edit Submission
    saveShowForm.addEventListener('submit', (e) => {
      e.preventDefault();
      const editId = document.getElementById('editShowId').value;
      const title = document.getElementById('showTitle').value;
      const badge = document.getElementById('showBadge').value;
      const image = document.getElementById('showImage').value;
      let videoUrl = document.getElementById('showVideoUrl').value;
      const quality = document.getElementById('showQuality').value;
      const downloadUrl = document.getElementById('showDownloadUrl').value;
      const fileInput = showVideoFile.files[0];

      // معالجة إضافة ملف فيديو من الهاتف
      if (fileInput) {
        const reader = new FileReader();
        reader.onload = function(evt) {
          const fileDataUrl = evt.target.result;
          saveShowObject(editId, title, badge, image, fileDataUrl, quality, downloadUrl, true);
        };
        reader.readAsDataURL(fileInput);
      } else {
        saveShowObject(editId, title, badge, image, videoUrl, quality, downloadUrl, false);
      }
    });

    function saveShowObject(editId, title, badge, image, videoUrl, quality, downloadUrl, isVideoLocal) {
      if (editId) {
        // Update
        const index = shows.findIndex(item => item.id == editId);
        if (index !== -1) {
          shows[index] = { id: Number(editId), title, badge, image, videoUrl, quality, downloadUrl, isVideoLocal };
        }
      } else {
        // Add New
        const newShow = {
          id: Date.now(),
          title,
          badge,
          image,
          videoUrl,
          quality,
          downloadUrl,
          isVideoLocal
        };
        shows.unshift(newShow);
      }

      saveData();
      resetAdminForm();
      alert('تم حفظ الفيديو بنجاح!');
    }

    // Initial Launch
    renderShows();
  </script>
</body>
</html>
