<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>قرمزي - منصة المسلسلات والأفلام</title>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
  <style>
    :root {
      --primary-color: #d32f2f;
      --primary-hover: #b71c1c;
      --bg-color: #121212;
      --card-bg: #1e1e1e;
      --text-color: #ffffff;
      --text-secondary: #aaa;
      --sidebar-bg: #181818;
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    }

    body {
      background-color: var(--bg-color);
      color: var(--text-color);
      direction: rtl;
    }

    /* Navbar */
    .navbar {
      display: flex;
      justify-content: space-between;
      align-items: center;
      background-color: #000;
      padding: 15px 20px;
      position: sticky;
      top: 0;
      z-index: 100;
      box-shadow: 0 2px 10px rgba(0, 0, 0, 0.8);
    }

    .brand {
      font-size: 26px;
      font-weight: bold;
      color: var(--primary-color);
      text-decoration: none;
      display: flex;
      align-items: center;
      gap: 10px;
    }

    .nav-actions {
      display: flex;
      align-items: center;
      gap: 15px;
    }

    .icon-btn {
      background: none;
      border: none;
      color: var(--text-color);
      font-size: 22px;
      cursor: pointer;
      transition: color 0.3s;
    }

    .icon-btn:hover {
      color: var(--primary-color);
    }

    /* Sidebar */
    .sidebar {
      position: fixed;
      top: 0;
      right: -300px;
      width: 280px;
      height: 100%;
      background-color: var(--sidebar-bg);
      box-shadow: -2px 0 10px rgba(0, 0, 0, 0.7);
      transition: right 0.3s ease;
      z-index: 200;
      padding: 20px;
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
      border-bottom: 1px solid #333;
      padding-bottom: 15px;
      margin-bottom: 20px;
    }

    .sidebar-menu {
      list-style: none;
    }

    .sidebar-menu li {
      margin-bottom: 15px;
    }

    .sidebar-menu a, .sidebar-menu button {
      color: var(--text-color);
      text-decoration: none;
      font-size: 18px;
      display: flex;
      align-items: center;
      gap: 10px;
      background: none;
      border: none;
      cursor: pointer;
      width: 100%;
      text-align: right;
    }

    .sidebar-menu a:hover, .sidebar-menu button:hover {
      color: var(--primary-color);
    }

    .overlay {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: rgba(0,0,0,0.6);
      display: none;
      z-index: 150;
    }

    .overlay.active {
      display: block;
    }

    /* Search Box */
    .search-container {
      padding: 15px 20px;
      max-width: 1200px;
      margin: 0 auto;
      display: none;
    }

    .search-container.active {
      display: block;
    }

    .search-input {
      width: 100%;
      padding: 12px 15px;
      border-radius: 6px;
      border: 1px solid #333;
      background-color: #222;
      color: #fff;
      font-size: 16px;
    }

    /* Main Container & Grid */
    .container {
      max-width: 1200px;
      margin: 20px auto;
      padding: 0 15px;
    }

    .ad-banner {
      background-color: #222;
      border: 1px dashed var(--primary-color);
      color: var(--text-secondary);
      text-align: center;
      padding: 15px;
      margin-bottom: 25px;
      border-radius: 8px;
    }

    .shows-grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(180px, 1fr));
      gap: 20px;
    }

    .show-card {
      background-color: var(--card-bg);
      border-radius: 8px;
      overflow: hidden;
      position: relative;
      box-shadow: 0 4px 10px rgba(0,0,0,0.5);
      transition: transform 0.3s;
    }

    .show-card:hover {
      transform: translateY(-5px);
    }

    .show-badge {
      position: absolute;
      top: 10px;
      right: 10px;
      background-color: var(--primary-color);
      color: #fff;
      padding: 3px 8px;
      font-size: 12px;
      border-radius: 4px;
      font-weight: bold;
      z-index: 2;
    }

    .show-thumb {
      width: 100%;
      height: 260px;
      object-fit: cover;
      display: block;
    }

    .show-info {
      padding: 12px;
      text-align: center;
    }

    .show-title {
      font-size: 15px;
      font-weight: bold;
      color: #fff;
      white-space: nowrap;
      overflow: hidden;
      text-overflow: ellipsis;
    }

    /* Modal / Admin Panel */
    .modal {
      display: none;
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background-color: rgba(0,0,0,0.8);
      z-index: 300;
      justify-content: center;
      align-items: center;
      padding: 20px;
    }

    .modal.active {
      display: flex;
    }

    .modal-content {
      background-color: var(--card-bg);
      border-radius: 8px;
      max-width: 500px;
      width: 100%;
      padding: 25px;
      box-shadow: 0 5px 15px rgba(0,0,0,0.5);
      max-height: 90vh;
      overflow-y: auto;
    }

    .modal-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 20px;
      border-bottom: 1px solid #333;
      padding-bottom: 10px;
    }

    .close-btn {
      background: none;
      border: none;
      color: #fff;
      font-size: 20px;
      cursor: pointer;
    }

    .form-group {
      margin-bottom: 15px;
    }

    .form-group label {
      display: block;
      margin-bottom: 5px;
      font-size: 14px;
      color: var(--text-secondary);
    }

    .form-group input, .form-group select {
      width: 100%;
      padding: 10px;
      border-radius: 4px;
      border: 1px solid #333;
      background-color: #2a2a2a;
      color: #fff;
    }

    .btn {
      width: 100%;
      padding: 12px;
      background-color: var(--primary-color);
      color: #fff;
      border: none;
      border-radius: 4px;
      font-size: 16px;
      cursor: pointer;
      font-weight: bold;
    }

    .btn:hover {
      background-color: var(--primary-hover);
    }

    .delete-btn {
      background-color: #555;
      margin-top: 8px;
      font-size: 12px;
      padding: 4px 8px;
      border: none;
      color: #fff;
      border-radius: 4px;
      cursor: pointer;
    }

    .delete-btn:hover {
      background-color: #d32f2f;
    }
  </style>
</head>
<body>

  <!-- Navigation Bar -->
  <nav class="navbar">
    <a href="#" class="brand">قرمزي</a>
    <div class="nav-actions">
      <button class="icon-btn" id="searchToggleBtn"><i class="fas fa-search"></i></button>
      <button class="icon-btn" id="menuToggleBtn"><i class="fas fa-bars"></i></button>
    </div>
  </nav>

  <!-- Sidebar Overlay -->
  <div class="overlay" id="overlay"></div>

  <!-- Sidebar -->
  <aside class="sidebar" id="sidebar">
    <div class="sidebar-header">
      <h3>القائمة</h3>
      <button class="close-btn" id="closeSidebarBtn">&times;</button>
    </div>
    <ul class="sidebar-menu">
      <li><a href="#"><i class="fas fa-home"></i> الرئيسية</a></li>
      <li><a href="#"><i class="fas fa-tv"></i> المسلسلات</a></li>
      <li><a href="#"><i class="fas fa-film"></i> الأفلام</a></li>
      <hr style="border-color: #333; margin: 10px 0;">
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
      <!-- Will be dynamically populated -->
    </div>

  </main>

  <!-- Password Modal -->
  <div class="modal" id="loginModal">
    <div class="modal-content">
      <div class="modal-header">
        <h3>دخول الإدارة</h3>
        <button class="close-btn" class="closeModal">&times;</button>
      </div>
      <form id="loginForm">
        <div class="form-group">
          <label for="adminPassword">كلمة المرور:</label>
          <input type="password" id="adminPassword" required>
        </div>
        <button type="submit" class="btn">دخول</button>
      </form>
    </div>
  </div>

  <!-- Add Show Modal -->
  <div class="modal" id="adminModal">
    <div class="modal-content">
      <div class="modal-header">
        <h3>إضافة مسلسل / فيلم جديد</h3>
        <button class="close-btn" class="closeModal">&times;</button>
      </div>
      <form id="addShowForm">
        <div class="form-group">
          <label for="showTitle">عنوان العمل:</label>
          <input type="text" id="showTitle" required placeholder="مثال: مسلسل في السابعة عشر">
        </div>
        <div class="form-group">
          <label for="showBadge">نص الشارة (اختياري):</label>
          <input type="text" id="showBadge" placeholder="مثال: حلقة 22 أو فيلم">
        </div>
        <div class="form-group">
          <label for="showImage">رابط الصورة (URL):</label>
          <input type="url" id="showImage" required placeholder="https://example.com/image.jpg">
        </div>
        <button type="submit" class="btn">إضافة إلى القائمة</button>
      </form>
    </div>
  </div>

  <script>
    // Initial Data
    const defaultShows = [
      { id: 1, title: "مسلسل في السابعة عشر", badge: "", image: "https://via.placeholder.com/300x400/1e1e1e/d32f2f?text=في+السابعة+عشر" },
      { id: 2, title: "مسلسل هذا البحر سوف يفيض", badge: "", image: "https://via.placeholder.com/300x400/1e1e1e/d32f2f?text=هذا+البحر+سوف+يفيض" },
      { id: 3, title: "مسلسل أخي الحلقة 22", badge: "حلقة 22", image: "https://via.placeholder.com/300x400/1e1e1e/d32f2f?text=مسلسل+أخي" },
      { id: 4, title: "مسلسل حبك نار الحلقة 4", badge: "حلقة 4", image: "https://via.placeholder.com/300x400/1e1e1e/d32f2f?text=حبك+نار" }
    ];

    // Load from LocalStorage or default
    let shows = JSON.parse(localStorage.getItem('krmzi_shows')) || defaultShows;
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
    const adminBtn = document.getElementById('adminBtn');
    const loginModal = document.getElementById('loginModal');
    const adminModal = document.getElementById('adminModal');
    const loginForm = document.getElementById('loginForm');
    const addShowForm = document.getElementById('addShowForm');
    const closeModalBtns = document.querySelectorAll('.closeModal');

    // Render Function
    function renderShows(filterText = '') {
      showsGrid.innerHTML = '';
      const filtered = shows.filter(show => show.title.toLowerCase().includes(filterText.toLowerCase()));

      filtered.forEach(show => {
        const card = document.createElement('div');
        card.className = 'show-card';
        card.innerHTML = `
          ${show.badge ? `<div class="show-badge">${show.badge}</div>` : ''}
          <img src="${show.image}" alt="${show.title}" class="show-thumb" onerror="this.src='https://via.placeholder.com/300x400/333/fff?text=لا+توجد+صورة'">
          <div class="show-info">
            <div class="show-title">${show.title}</div>
            ${isAdminLoggedIn ? `<button class="delete-btn" onclick="deleteShow(${show.id})">حذف</button>` : ''}
          </div>
        `;
        showsGrid.appendChild(card);
      });
    }

    // Save Data
    function saveData() {
      localStorage.setItem('krmzi_shows', JSON.stringify(shows));
      renderShows();
    }

    // Delete Show
    window.deleteShow = function(id) {
      if (confirm('هل أنت تأكد من حذف هذا العمل؟')) {
        shows = shows.filter(item => item.id !== id);
        saveData();
      }
    };

    // Sidebar Handlers
    function toggleSidebar() {
      sidebar.classList.toggle('open');
      overlay.classList.toggle('active');
    }

    menuToggleBtn.addEventListener('click', toggleSidebar);
    closeSidebarBtn.addEventListener('click', toggleSidebar);
    overlay.addEventListener('click', toggleSidebar);

    // Search Handler
    searchToggleBtn.addEventListener('click', () => {
      searchContainer.classList.toggle('active');
      if (searchContainer.classList.contains('active')) {
        searchInput.focus();
      }
    });

    searchInput.addEventListener('input', (e) => {
      renderShows(e.target.value);
    });

    // Modal Close Handlers
    closeModalBtns.forEach(btn => {
      btn.addEventListener('click', () => {
        loginModal.classList.remove('active');
        adminModal.classList.remove('active');
      });
    });

    // Admin Access
    adminBtn.addEventListener('click', () => {
      toggleSidebar();
      if (isAdminLoggedIn) {
        adminModal.classList.add('active');
      } else {
        loginModal.classList.add('active');
      }
    });

    // Password Form
    loginForm.addEventListener('submit', (e) => {
      e.preventDefault();
      const password = document.getElementById('adminPassword').value;
      if (password === 'marwanhacker99') {
        isAdminLoggedIn = true;
        loginModal.classList.remove('active');
        adminModal.classList.add('active');
        document.getElementById('adminPassword').value = '';
        renderShows();
      } else {
        alert('كلمة المرور غير صحيحة!');
      }
    });

    // Add Show Form
    addShowForm.addEventListener('submit', (e) => {
      e.preventDefault();
      const title = document.getElementById('showTitle').value;
      const badge = document.getElementById('showBadge').value;
      const image = document.getElementById('showImage').value;

      const newShow = {
        id: Date.now(),
        title,
        badge,
        image
      };

      shows.unshift(newShow);
      saveData();
      addShowForm.reset();
      adminModal.classList.remove('active');
    });

    // Initial Init
    renderShows();
  </script>
</body>
</html>

