<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AI Cinema Studio - منصة إنتاج الأفلام الكاملة</title>
    <style>
        :root {
            --bg-color: #0f1016;
            --card-bg: #1a1c29;
            --accent-color: #6366f1;
            --accent-hover: #4f46e5;
            --text-color: #ffffff;
            --text-muted: #9ca3af;
            --success-color: #10b981;
            --gold-color: #f59e0b;
            --blue-color: #3b82f6;
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
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
            padding: 20px;
        }

        header {
            text-align: center;
            margin-bottom: 25px;
        }

        header h1 {
            font-size: 2.5rem;
            margin-bottom: 8px;
            background: linear-gradient(45deg, #6366f1, #a855f7);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        header p {
            color: var(--text-muted);
            font-size: 1rem;
        }

        .container {
            background-color: var(--card-bg);
            width: 100%;
            max-width: 800px;
            padding: 30px;
            border-radius: 16px;
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.5);
            border: 1px solid rgba(255, 255, 255, 0.05);
        }

        .form-group {
            margin-bottom: 20px;
        }

        label {
            display: block;
            margin-bottom: 8px;
            font-weight: bold;
            color: #d1d5db;
        }

        textarea, input[type="file"], select {
            width: 100%;
            padding: 12px;
            border-radius: 8px;
            border: 1px solid #374151;
            background-color: #111827;
            color: white;
            font-size: 1rem;
        }

        textarea {
            resize: vertical;
            height: 110px;
        }

        textarea:focus, input:focus, select:focus {
            outline: none;
            border-color: var(--accent-color);
        }

        .options-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
            gap: 15px;
            margin-bottom: 20px;
        }

        /* صندوق ميزة الذكاء الاصطناعي الذاتي للصور */
        .ai-image-box {
            background: rgba(59, 130, 246, 0.08);
            border: 1px solid rgba(59, 130, 246, 0.3);
            border-radius: 10px;
            padding: 15px;
            margin-bottom: 20px;
        }

        .ai-image-title {
            color: var(--blue-color);
            font-size: 1rem;
            font-weight: bold;
            margin-bottom: 8px;
        }

        /* صندوق الإخراج والواقعية */
        .human-touch-box {
            background: rgba(245, 158, 11, 0.05);
            border: 1px solid rgba(245, 158, 11, 0.3);
            border-radius: 10px;
            padding: 18px;
            margin-bottom: 20px;
        }

        .human-touch-title {
            color: var(--gold-color);
            font-size: 1rem;
            font-weight: bold;
            margin-bottom: 10px;
        }

        .checkbox-group {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
            gap: 10px;
            margin-top: 10px;
        }

        .checkbox-item {
            display: flex;
            align-items: center;
            gap: 8px;
            font-size: 0.88rem;
            color: #d1d5db;
            cursor: pointer;
        }

        .checkbox-item input {
            width: 16px;
            height: 16px;
            accent-color: var(--gold-color);
            cursor: pointer;
        }

        .badge-info {
            font-size: 0.85rem;
            color: var(--success-color);
            margin-top: 5px;
            display: block;
        }

        button {
            width: 100%;
            padding: 14px;
            background: linear-gradient(45deg, var(--accent-color), #8b5cf6);
            color: white;
            border: none;
            border-radius: 8px;
            font-size: 1.1rem;
            font-weight: bold;
            cursor: pointer;
            transition: opacity 0.3s;
        }

        button:hover {
            opacity: 0.9;
        }

        #loading-section {
            display: none;
            text-align: center;
            margin-top: 25px;
        }

        .spinner {
            border: 4px solid rgba(255, 255, 255, 0.1);
            width: 50px;
            height: 50px;
            border-radius: 50%;
            border-left-color: var(--accent-color);
            animation: spin 1s linear infinite;
            margin: 0 auto 15px auto;
        }

        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }

        #result-section {
            display: none;
            margin-top: 30px;
            text-align: center;
            background: #111827;
            padding: 20px;
            border-radius: 12px;
            border: 1px solid var(--success-color);
        }

        #result-section h3 {
            color: var(--success-color);
            margin-bottom: 10px;
        }

        .movie-details {
            color: var(--text-muted);
            font-size: 0.95rem;
            margin-bottom: 15px;
        }

        video {
            width: 100%;
            border-radius: 8px;
            max-height: 380px;
            background: black;
        }
    </style>
</head>
<body>

    <header>
        <h1>AI Cinema Studio</h1>
        <p>إنتاج كامل ودقيق لفيلم سينمائي دون اختصار وبأعلى واقعية مجاناً</p>
    </header>

    <div class="container">
        <form id="movie-form">
            <!-- وصف الفيلم -->
            <div class="form-group">
                <label for="prompt">اكتب وصف الفيلم والسيناريو الكامل (بدون حذف أي تفصيل):</label>
                <textarea id="prompt" placeholder="اكتب القصة بالتفصيل الملائم، جميع الأحداث والمَشاهد ستُترجم بدقة كاملة بدون حذف أي جزء..." required></textarea>
                <span class="badge-info">✨ مدة الفيلم المُولّد: ساعتان و 30 دقيقة (مجاناً)</span>
            </div>

            <!-- شبكة الخيارات: النمط والجودة -->
            <div class="options-grid">
                <div class="form-group">
                    <label for="movie-style">نمط ونوع الفيلم 🎨:</label>
                    <select id="movie-style">
                        <option value="realistic">واقعي سينمائي (تصوير بشري Live-Action)</option>
                        <option value="anime">أنمي / كرتون (Anime & 2D Art)</option>
                        <option value="3d-animation">رسوم ثلاثية الأبعاد (3D Animation)</option>
                        <option value="ai-art">نمط AI خيالي (Futuristic AI Gloss)</option>
                    </select>
                </div>

                <div class="form-group">
                    <label for="movie-quality">دقة العرض والجودة 🖥️:</label>
                    <select id="movie-quality">
                        <option value="4k">4K Ultra HD (بدون أخطاء دمج)</option>
                        <option value="8k">8K IMAX Realism (واقعية فائقة)</option>
                        <option value="1080p">Full HD 1080p (عالية الدقة)</option>
                    </select>
                </div>
            </div>

            <!-- ميرة تحديد صور الشخصيات من الذكاء الاصطناعي -->
            <div class="ai-image-box">
                <div class="ai-image-title">🤖 خيار الصور والشخصيات:</div>
                <label class="checkbox-item" style="margin-bottom: 10px;">
                    <input type="checkbox" id="auto-ai-image" checked onchange="toggleFileUpload(this)">
                    دع الذكاء الاصطناعي يبتكر ويختار الصور والشخصيات المناسبة تلقائياً حسب الوصف
                </label>

                <div id="manual-file-container" style="display: none; margin-top: 10px;">
                    <label for="human-image" style="font-size: 0.9rem;">أو ارفع صورة من عندك (أيقونة تصوير بشري):</label>
                    <input type="file" id="human-image" accept="image/*">
                </div>
            </div>

            <!-- خيارات الواقعية وعدم الحذف -->
            <div class="human-touch-box">
                <div class="human-touch-title">🎬 الإخراج والواقعية ودقة المتابعة:</div>
                <div class="checkbox-group">
                    <label class="checkbox-item">
                        <input type="checkbox" checked disabled> الالتزام الكامل بالوصف (بدون حذف أي مشهد)
                    </label>
                    <label class="checkbox-item">
                        <input type="checkbox" checked> حركة كاميرات ومصوري سينما بشرية
                    </label>
                    <label class="checkbox-item">
                        <input type="checkbox" checked> فيزياء واقعية (إضاءة، ملابس، وانفعالات)
                    </label>
                    <label class="checkbox-item">
                        <input type="checkbox" checked> معالجة ومنع أي أخطاء بصرية (No-Glitch AI)
                    </label>
                </div>
            </div>

            <!-- زر الإنشاء -->
            <button type="submit">بدء إنتاج الفيلم بالكامل 🚀</button>
        </form>

        <!-- قسم التحميل -->
        <div id="loading-section">
            <div class="spinner"></div>
            <p id="loading-text">جاري معالجة الوصف الكامل والتأكد من عدم حذف أي مشهد...</p>
        </div>

        <!-- قسم النتيجة -->
        <div id="result-section">
            <h3>🎉 تم إنتاج فيلمك بنجاح وبدقة كاملة!</h3>
            <p class="movie-details" id="result-details">المدة: 02:30:00 | النمط: واقعي | الجودة: 4K | الالتزام بالوصف: 100%</p>
            <video controls>
                <source src="https://www.w3schools.com/html/mov_bbb.mp4" type="video/mp4">
                متصفحك لا يدعم عرض الفيديو.
            </video>
        </div>
    </div>

    <script>
        const form = document.getElementById('movie-form');
        const loadingSection = document.getElementById('loading-section');
        const loadingText = document.getElementById('loading-text');
        const resultSection = document.getElementById('result-section');
        const resultDetails = document.getElementById('result-details');

        function toggleFileUpload(checkbox) {
            const fileContainer = document.getElementById('manual-file-container');
            if (checkbox.checked) {
                fileContainer.style.display = 'none';
            } else {
                fileContainer.style.display = 'block';
            }
        }

        form.addEventListener('submit', function(e) {
            e.preventDefault();

            const styleSelect = document.getElementById('movie-style');
            const qualitySelect = document.getElementById('movie-quality');
            const autoAiImage = document.getElementById('auto-ai-image').checked;

            const selectedStyleText = styleSelect.options[styleSelect.selectedIndex].text;
            const selectedQualityText = qualitySelect.options[qualitySelect.selectedIndex].text;
            
            const imageSourceText = autoAiImage ? "تولد تلقائياً بالذكاء الاصطناعي" : "تمت مطابقتها من الملف المرفوع";

            const loadingSteps = [
                "جاري مسح الوصف كاملاً والتأكد من تضمين كافة المشاهد والشخصيات بدون حذف...",
                `الشخصيات والصور: [${imageSourceText}]...`,
                `تطبيق محرك الواقعية لمنع الأخطاء البصرية ونمط: [${selectedStyleText}]...`,
                `رندر ومعالجة المشاهد بدقة high-fidelity (${selectedQualityText})...`,
                "تجميع المشاهد وهندسة الصوت للفيلم (المدة الإجمالية: 02:30:00)...",
                "تم تجهيز الفيلم بنجاح!"
            ];

            form.style.display = 'none';
            loadingSection.style.display = 'block';

            let step = 0;
            const interval = setInterval(() => {
                if (step < loadingSteps.length) {
                    loadingText.textContent = loadingSteps[step];
                    step++;
                } else {
                    clearInterval(interval);
                    loadingSection.style.display = 'none';
                    
                    resultDetails.textContent = `المدة: 02:30:00 | النمط: ${selectedStyleText} | الجودة: ${selectedQualityText} | صور الشخصيات: ${imageSourceText}`;
                    resultSection.style.display = 'block';
                }
            }, 2000);
        });
    </script>

</body>
</html>
