<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>منصة الأفلام والمسلسلات - لوحة التحكم والمحتوى</title>
    <style>
        :root {
            --bg-color: #141414;
            --card-bg: #1f1f1f;
            --primary-color: #e50914;
            --text-color: #ffffff;
            --text-muted: #aaaaaa;
            --border-color: #333333;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: var(--bg-color);
            color: var(--text-color);
            margin: 0;
            padding: 0;
        }

        header {
            background-color: #000000;
            padding: 15px 30px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-bottom: 1px solid var(--border-color);
        }

        header h1 {
            color: var(--primary-color);
            margin: 0;
            font-size: 24px;
        }

        nav a {
            color: var(--text-color);
            text-decoration: none;
            margin-right: 15px;
            font-weight: 500;
        }

        nav a:hover {
            color: var(--primary-color);
        }

        .container {
            max-width: 1100px;
            margin: 20px auto;
            padding: 0 20px;
        }

        .section-title {
            border-right: 4px solid var(--primary-color);
            padding-right: 10px;
            margin-top: 30px;
            margin-bottom: 20px;
        }

        /* Admin Upload Form */
        .admin-panel {
            background-color: var(--card-bg);
            padding: 20px;
            border-radius: 8px;
            margin-bottom: 30px;
            border: 1px solid var(--border-color);
        }

        .form-group {
            margin-bottom: 15px;
        }

        .form-group label {
            display: block;
            margin-bottom: 5px;
            color: var(--text-muted);
        }

        .form-group input, .form-group textarea, .form-group select {
            width: 100%;
            padding: 10px;
            border-radius: 4px;
            border: 1px solid var(--border-color);
            background-color: #2b2b2b;
            color: #fff;
            box-sizing: border-box;
        }

        .btn-submit {
            background-color: var(--primary-color);
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 4px;
            cursor: pointer;
            font-size: 16px;
            font-weight: bold;
        }

        .btn-submit:hover {
            background-color: #b80710;
        }

        /* Movies Grid */
        .media-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
            gap: 20px;
        }

        .media-card {
            background-color: var(--card-bg);
            border-radius: 8px;
            overflow: hidden;
            border: 1px solid var(--border-color);
        }

        .media-card video {
            width: 100%;
            height: 180px;
            background-color: #000;
        }

        .media-info {
            padding: 15px;
        }

        .media-tag {
            display: inline-block;
            background-color: var(--primary-color);
            padding: 2px 8px;
            border-radius: 4px;
            font-size: 12px;
            margin-bottom: 5px;
        }

        /* Privacy Policy */
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

    <header>
        <h1>منصة السينما</h1>
        <nav>
            <a href="#gallery">الأفلام والمسلسلات</a>
            <a href="#admin">لوحة المدير</a>
            <a href="#privacy">سياسة الخصوصية</a>
        </nav>
    </header>

    <div class="container">

        <!-- لوحة التحكم للمدير (إضافة فيديو من المعرض) -->
        <section id="admin" class="admin-panel">
            <h2 class="section-title">إضافة عمل جديد (خاص بالمدير)</h2>
            <form id="uploadForm">
                <div class="form-group">
                    <label for="title">عنوان الفيلم / المسلسل:</label>
                    <input type="text" id="title" required placeholder="أدخل العنوان هنا">
                </div>
                <div class="form-group">
                    <label for="type">النوع:</label>
                    <select id="type">
                        <option value="فيلم">فيلم</option>
                        <option value="مسلسل">مسلسل</option>
                    </select>
                </div>
                <div class="form-group">
                    <label for="videoFile">اختر الفيديو من المعرض فقط:</label>
                    <!-- accept="video/*" مع عدم استخدام capture لضمان التوجيه للمعرض -->
                    <input type="file" id="videoFile" accept="video/*" required>
                </div>
                <div class="form-group">
                    <label for="description">الوصف:</label>
                    <textarea id="description" rows="3" placeholder="أدخل وصفاً مختصراً"></textarea>
                </div>
                <button type="submit" class="btn-submit">رفع وإضافة إلى القائمة</button>
            </form>
        </section>

        <!-- قائمة الأفلام والمسلسلات -->
        <section id="gallery">
            <h2 class="section-title">قائمة الأفلام والمسلسلات</h2>
            <div class="media-grid" id="mediaGrid">
                <!-- الأقسام تضاف ديناميكياً عن طريق JavaScript -->
            </div>
        </section>

        <!-- سياسة الخصوصية -->
        <section id="privacy" class="privacy-section">
            <h2 class="section-title">سياسة الخصوصية</h2>
            <p>مرحباً بك في منصتنا. نحن نحترم خصوصيتك ونلتزم بحماية البيانات الشخصية التي تشاركها معنا:</p>
            <ul>
                <li><strong>جمع البيانات:</strong> نقوم بجمع معلومات بسيطة تهدف إلى تحسين تجربة المشاهدة والتصفح.</li>
                <li><strong>رفع الفيديو:</strong> ميزة رفع الفيديوهات مخصصة للمدير المعتمد فقط. يتم اختيار الملفات المرفوعة مباشرة من المعرض المحلي للجهاز دون الوصول لأي ملفات شخصية أخرى.</li>
                <li><strong>حماية المحتوى:</strong> جميع الفيديوهات والمحتويات المعروضة محميّة وتخضع لمعايير الاستخدام العادل والملكية الفكرية.</li>
                <li><strong>مشاركة البيانات:</strong> لا نقوم ببيع أو مشاركة بيانات المستخدمين مع أي أطراف خارجية.</li>
            </ul>
        </section>

    </div>

    <script>
        const uploadForm = document.getElementById('uploadForm');
        const mediaGrid = document.getElementById('mediaGrid');

        // التعامل مع رفع الفيديو إضافة العمل
        uploadForm.addEventListener('submit', function(e) {
            e.preventDefault();

            const title = document.getElementById('title').value;
            const type = document.getElementById('type').value;
            const description = document.getElementById('description').value;
            const videoFileInput = document.getElementById('videoFile');
            const file = videoFileInput.files[0];

            if (file) {
                const videoURL = URL.createObjectURL(file);

                // إنشاء بطاقة الفيديو
                const card = document.createElement('div');
                card.className = 'media-card';

                card.innerHTML = `
                    <video controls>
                        <source src="${videoURL}" type="${file.type}">
                        متصفحك لا يدعم تشغيل الفيديو.
                    </video>
                    <div class="media-info">
                        <span class="media-tag">${type}</span>
                        <h3 style="margin: 5px 0;">${title}</h3>
                        <p style="color: var(--text-muted); font-size: 14px;">${description}</p>
                    </div>
                `;

                mediaGrid.prepend(card);

                // إعادة ضبط النموذج
                uploadForm.reset();
                alert('تمت إضافة الفيديو بنجاح إلى القائمة!');
            }
        });
    </script>
</body>
</html>
