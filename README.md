<html lang="th">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Happy Home Recipes - สร้างความสุขในทุกมื้ออาหารของครอบครัว</title>
    <link href="https://fonts.googleapis.com/css2?family=Sarabun:wght@400;600;700&display=swap" rel="stylesheet">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Sarabun', 'Prompt', sans-serif; /* Sarabun เป็นตัวเลือกแรก */
            background: linear-gradient(135deg, #FFE5F1 0%, #FFF0F5 50%, #E6E6FA 100%);
            min-height: 100vh;
            padding: 20px;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            background: rgba(255, 255, 255, 0.98);
            border-radius: 25px;
            padding: 40px;
            box-shadow: 0 15px 35px rgba(255, 182, 193, 0.2);
        }

        .header {
            text-align: center;
            margin-bottom: 40px;
            padding-bottom: 30px;
            border-bottom: 3px solid #FFE0EC;
        }

        .header h1 {
            color: #D8627D;
            font-size: 2.8em;
            margin-bottom: 15px;
            font-weight: bold;
            text-shadow: 2px 2px 4px rgba(255, 182, 193, 0.3);
        }
        
        .header .subtitle {
            color: #F9A8D4;
            font-size: 1.4em;
            margin-bottom: 10px;
            font-weight: 600;
        }

        .header .tagline {
            color: #9CA3AF;
            font-size: 1.1em;
            line-height: 1.6;
            max-width: 800px;
            margin: 0 auto;
            padding: 0 20px;
        }

        .ingredients-section {
            background: linear-gradient(135deg, #FFF5F8, #FCE4EC);
            border-radius: 20px;
            padding: 35px;
            margin-bottom: 35px;
            border: 2px solid #FFCDD2;
        }

        .ingredients-section h2 {
            color: #D8627D;
            margin-bottom: 25px;
            text-align: center;
            font-size: 1.8em;
        }

        .ingredients-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 15px;
            margin-bottom: 30px;
        }

        .ingredient-input {
            position: relative;
        }

        .ingredient-input input {
            width: 100%;
            padding: 14px 14px 14px 45px;
            border: 2px solid #FFCDD2;
            border-radius: 12px;
            font-size: 1.05em;
            background: white;
            transition: all 0.3s ease;
        }

        .ingredient-input input:focus {
            outline: none;
            border-color: #F9A8D4;
            box-shadow: 0 0 0 4px rgba(249, 168, 212, 0.1);
        }

        .ingredient-input::before {
            content: '🥘';
            position: absolute;
            left: 14px;
            top: 50%;
            transform: translateY(-50%);
            font-size: 1.3em;
        }

        .ingredient-input:nth-child(2)::before { content: '🥬'; }
        .ingredient-input:nth-child(3)::before { content: '🧄'; }
        .ingredient-input:nth-child(4)::before { content: '🌶️'; }
        .ingredient-input:nth-child(5)::before { content: '🥕'; }

        .generate-btn {
            background: linear-gradient(135deg, #F9A8D4, #C084FC);
            color: white;
            border: none;
            padding: 18px 50px;
            font-size: 1.3em;
            font-weight: bold;
            border-radius: 50px;
            cursor: pointer;
            transition: all 0.3s ease;
            display: block;
            margin: 0 auto;
            box-shadow: 0 6px 20px rgba(249, 168, 212, 0.4);
        }

        .generate-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 8px 25px rgba(249, 168, 212, 0.5);
        }

        .generate-btn:active {
            transform: translateY(-1px);
        }
        
        /* เพิ่มสไตล์สำหรับปุ่มที่ถูกปิดการใช้งาน (เมื่อกำลังโหลด) */
        .generate-btn:disabled {
            background: #ccc;
            cursor: not-allowed;
            box-shadow: none;
            transform: none;
        }

        .loading {
            display: none;
            text-align: center;
            padding: 40px;
        }

        .loading.active {
            display: block;
        }

        .spinner {
            border: 5px solid #FCE4EC;
            border-top: 5px solid #F9A8D4;
            border-radius: 50%;
            width: 60px;
            height: 60px;
            animation: spin 1s linear infinite;
            margin: 0 auto 20px;
        }

        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }

        .menu-results {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(500px, 1fr));
            gap: 30px;
            margin-bottom: 30px;
        }

        .menu-card {
            background: white;
            border-radius: 20px;
            overflow: hidden;
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.1);
            transition: transform 0.3s ease;
        }

        .menu-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 15px 35px rgba(0, 0, 0, 0.15);
        }

        .menu-card.soup {
            border-top: 5px solid #B4E7F8;
            background: linear-gradient(to bottom, #E8F8FF, white);
        }

        .menu-card.dry {
            border-top: 5px solid #FFD4BA;
            background: linear-gradient(to bottom, #FFF9F5, white);
        }

        .menu-card-header {
            padding: 20px;
            font-size: 1.2em;
            font-weight: bold;
            color: #6B7280;
        }

        .menu-card.soup .menu-card-header {
            background: linear-gradient(135deg, #B4E7F8, #A8DADC);
            color: #1E88E5;
        }

        .menu-card.dry .menu-card-header {
            background: linear-gradient(135deg, #FFD4BA, #FFDAB9);
            color: #F57C00;
        }

        .menu-card-body {
            padding: 25px;
        }

        .menu-name {
            font-size: 1.8em;
            font-weight: bold;
            color: #374151;
            margin-bottom: 15px;
            display: flex;
            align-items: center;
            flex-wrap: wrap;
            gap: 10px;
        }

        .taste-indicator {
            display: inline-block;
            padding: 6px 14px;
            border-radius: 20px;
            font-size: 0.9em;
            margin-bottom: 15px;
        }

        .taste-mild {
            background: #E8F5E9;
            color: #43A047;
        }

        .taste-strong {
            background: #FFE5B4;
            color: #FF6F00;
        }

        .price-estimate {
            background: linear-gradient(135deg, #FFF9C4, #FFEB3B);
            padding: 8px 15px;
            border-radius: 15px;
            display: inline-block;
            font-weight: bold;
            color: #F57F17;
            margin-bottom: 20px;
        }

        .menu-ingredients {
            background: linear-gradient(135deg, #F3E5F5, #FCE4EC);
            padding: 20px;
            border-radius: 15px;
            margin-bottom: 20px;
        }

        .menu-ingredients h4 {
            color: #7B1FA2;
            margin-bottom: 12px;
            font-size: 1.15em;
        }

        .menu-ingredients ul {
            list-style: none;
            padding-left: 0;
        }

        .menu-ingredients li {
            padding: 6px 0;
            color: #555;
            line-height: 1.6;
            position: relative;
            padding-left: 25px;
        }

        .menu-ingredients li:before {
            content: '•';
            position: absolute;
            left: 8px;
            color: #F9A8D4;
            font-size: 1.3em;
        }

        .cooking-method {
            background: linear-gradient(135deg, #E8F5E9, #F1F8E9);
            padding: 20px;
            border-radius: 15px;
            margin-bottom: 20px;
        }

        .cooking-method h4 {
            color: #388E3C;
            margin-bottom: 12px;
            font-size: 1.15em;
        }

        .cooking-method ol {
            padding-left: 20px;
            color: #555;
        }

        .cooking-method li {
            padding: 8px 0;
            line-height: 1.6;
        }

        .nutrition-info {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 15px;
            margin-top: 20px;
        }

        .nutrition-item {
            background: linear-gradient(135deg, #FFE0EC, #FCE4EC);
            padding: 12px;
            border-radius: 12px;
            text-align: center;
        }

        .nutrition-item .label {
            color: #9CA3AF;
            font-size: 0.9em;
            margin-bottom: 5px;
        }

        .nutrition-item .value {
            color: #374151;
            font-weight: bold;
            font-size: 1.1em;
        }

        .calories-badge {
            display: inline-block;
            background: linear-gradient(135deg, #FFE0B2, #FFCC80);
            padding: 5px 12px;
            border-radius: 15px;
            color: #E65100;
            font-weight: bold;
            margin-left: 10px;
            font-size: 0.9em;
        }

        .menu-warnings {
            background: linear-gradient(135deg, #FFF9E7, #FFECB3);
            padding: 15px;
            border-radius: 12px;
            margin-top: 15px;
            border-left: 4px solid #FFA726;
        }

        .menu-warnings h4 {
            color: #E65100;
            margin-bottom: 10px;
            font-size: 1.05em;
        }

        .menu-warnings ul {
            list-style: none;
            padding: 0;
        }

        .menu-warnings li {
            padding: 5px 0;
            color: #666;
            font-size: 0.95em;
            line-height: 1.5;
        }

        .menu-warnings strong {
            color: #E65100;
        }

        .health-warning-section {
            margin-top: 30px;
            padding: 30px;
            background: linear-gradient(135deg, #FFF5F5, #FFEBEE);
            border-radius: 20px;
            border: 2px solid #FFCDD2;
        }

        .health-warning-section h3 {
            color: #D32F2F;
            text-align: center;
            margin-bottom: 25px;
            font-size: 1.6em;
        }

        .disease-cards {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 20px;
        }

        .disease-card {
            padding: 20px;
            border-radius: 15px;
            background: white;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
        }

        .disease-card h4 {
            margin-bottom: 15px;
            font-size: 1.2em;
        }

        .disease-card.diabetes {
            border-top: 4px solid #FCE4EC;
        }

        .disease-card.hypertension {
            border-top: 4px solid #E3F2FD;
        }

        .disease-card.cholesterol {
            border-top: 4px solid #FFF9C4;
        }

        .disease-card.gout {
            border-top: 4px solid #F3E5F5;
        }

        .disease-card ul {
            margin: 10px 0;
            padding-left: 20px;
            color: #666;
        }

        .disease-card li {
            padding: 5px 0;
            font-size: 0.95em;
        }

        .disease-card strong {
            color: #D32F2F;
            display: block;
            margin-top: 10px;
        }

        .disease-card .recommend {
            background: #F5F5F5;
            padding: 10px;
            border-radius: 8px;
            margin-top: 10px;
            font-size: 0.95em;
            color: #388E3C;
        }

        .tips-section {
            margin-top: 30px;
            padding: 25px;
            background: linear-gradient(135deg, #F0F4C3, #DCEDC8);
            border-radius: 20px;
            text-align: center;
        }

        .tips-section h3 {
            color: #689F38;
            margin-bottom: 15px;
            font-size: 1.4em;
        }

        .tips-section ul {
            list-style: none;
            padding: 0;
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 15px;
            margin-top: 20px;
        }

        .tips-section li {
            background: white;
            padding: 15px;
            border-radius: 10px;
            color: #555;
            box-shadow: 0 3px 10px rgba(0, 0, 0, 0.1);
        }

        .footer {
            text-align: center;
            margin-top: 40px;
            padding: 20px;
            color: #9CA3AF;
            font-size: 0.95em;
        }

        .footer p {
            margin: 5px 0;
        }

        @media (max-width: 768px) {
            .container {
                padding: 20px;
            }

            .header h1 {
                font-size: 2em;
            }

            .menu-results {
                grid-template-columns: 1fr;
            }

            .ingredients-grid {
                grid-template-columns: 1fr;
            }

            .disease-cards {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>🏡 Happy Home Recipes 🍽️</h1>
            <p class="subtitle">สร้างความสุขในทุกมื้ออาหารของครอบครัว</p>
            <p class="tagline">
                เพียงแค่บอก "วัตถุดิบที่คุณมี" เราพร้อมออกแบบสูตรอาหารโฮมเมดง่าย ๆ 
                ที่เติมเต็มความอบอุ่น และกลายเป็นจานโปรดที่เหมาะสมกับทุกวัยในครอบครัว
            </p>
        </div>

        <div class="ingredients-section">
            <h2>📝 วัตถุดิบที่คุณมีในครัว</h2>
            <div class="ingredients-grid">
                <div class="ingredient-input">
                    <input type="text" id="ingredient1" placeholder="วัตถุดิบที่ 1 เช่น ไก่">
                </div>
                <div class="ingredient-input">
                    <input type="text" id="ingredient2" placeholder="วัตถุดิบที่ 2 เช่น ผักบุ้ง">
                </div>
                <div class="ingredient-input">
                    <input type="text" id="ingredient3" placeholder="วัตถุดิบที่ 3 เช่น มะเขือเทศ">
                </div>
                <div class="ingredient-input">
                    <input type="text" id="ingredient4" placeholder="วัตถุดิบที่ 4 (ถ้ามี)">
                </div>
                <div class="ingredient-input">
                    <input type="text" id="ingredient5" placeholder="วัตถุดิบที่ 5 (ถ้ามี)">
                </div>
            </div>
            <button class="generate-btn" onclick="generateMenu()">🍳 สร้างเมนูอาหาร</button>
        </div>

        <div class="loading" id="loading">
            <div class="spinner"></div>
            <p style="color: #F9A8D4; font-size: 1.2em; font-weight: bold;">กำลังสร้างสรรค์เมนูอาหารแสนอร่อย...</p>
        </div>

        <div class="menu-results" id="menuResults"></div>

        <div class="health-warning-section" id="healthWarning" style="display: none;">
            <h3>⚠️ ข้อควรระวังสำหรับผู้ป่วยโรคเรื้อรัง</h3>
            <div class="disease-cards">
                <div class="disease-card diabetes">
                    <h4>🩺 โรคเบาหวาน</h4>
                    <div class="avoid-list">
                        <strong>อาหารที่ควรหลีกเลี่ยง:</strong>
                        <ul>
                            <li>น้ำตาล น้ำผึ้ง น้ำเชื่อม</li>
                            <li>ข้าวเหนียว ขนมหวาน</li>
                            <li>ผลไม้หวานจัด (ทุเรียน ลำไย องุ่น)</li>
                            <li>เครื่องดื่มที่มีน้ำตาล</li>
                        </ul>
                    </div>
                    <div class="recommend">
                        <strong>แนะนำ:</strong> เลือกคาร์โบไฮเดรตเชิงซ้อน ผักใบเขียว โปรตีนไม่ติดมัน
                    </div>
                </div>

                <div class="disease-card hypertension">
                    <h4>💓 ความดันโลหิตสูง</h4>
                    <div class="avoid-list">
                        <strong>อาหารที่ควรหลีกเลี่ยง:</strong>
                        <ul>
                            <li>อาหารเค็มจัด (ปลาเค็ม ไข่เค็ม)</li>
                            <li>อาหารหมักดอง กะปิ น้ำปลา</li>
                            <li>อาหารสำเร็จรูป บะหมี่กึ่งสำเร็จรูป</li>
                            <li>เนื้อสัตว์แปรรูป (ไส้กรอก แฮม เบคอน)</li>
                        </ul>
                    </div>
                    <div class="recommend">
                        <strong>แนะนำ:</strong> ลดเกลือเหลือไม่เกิน 1 ช้อนชาต่อวัน เพิ่มผักผลไม้ที่มีโพแทสเซียม
                    </div>
                </div>

                <div class="disease-card cholesterol">
                    <h4>🧈 ไขมันในเลือดสูง</h4>
                    <div class="avoid-list">
                        <strong>อาหารที่ควรหลีกเลี่ยง:</strong>
                        <ul>
                            <li>อาหารทอดน้ำมันท่วม</li>
                            <li>เนื้อติดมัน หนังสัตว์</li>
                            <li>เครื่องในสัตว์ ไข่แดง (เกิน 3 ฟอง/สัปดาห์)</li>
                            <li>กะทิ ครีม เนย ชีส</li>
                        </ul>
                    </div>
                    <div class="recommend">
                        <strong>แนะนำ:</strong> เลือกเนื้อไม่ติดมัน ใช้น้ำมันพืช ปรุงด้วยการต้ม นึ่ง ย่าง
                    </div>
                </div>

                <div class="disease-card gout">
                    <h4>🦴 โรคเก๊าท์</h4>
                    <div class="avoid-list">
                        <strong>อาหารที่ควรหลีกเลี่ยง:</strong>
                        <ul>
                            <li>เครื่องในสัตว์ (ตับ ไต หัวใจ)</li>
                            <li>อาหารทะเล (กุ้ง หอย ปู ปลาทูน่า)</li>
                            <li>เนื้อแดง เป็ด ห่าน</li>
                            <li>ถั่วเมล็ดแห้ง เห็ดหอม หน่อไม้</li>
                            <li>เครื่องดื่มแอลกอฮอล์</li>
                        </ul>
                    </div>
                    <div class="recommend">
                        <strong>แนะนำ:</strong> ดื่มน้ำมากๆ วันละ 2-3 ลิตร เลือกโปรตีนจากไข่ นม เต้าหู้
                    </div>
                </div>
            </div>
        </div>

        <div class="tips-section">
            <h3>💡 เคล็ดลับการทำอาหารสุขภาพ</h3>
            <ul>
                <li>🥬 เพิ่มผักใบเขียวในทุกมื้อ</li>
                <li>🧂 ลดเค็ม หวาน มัน</li>
                <li>🥘 นึ่ง ต้ม อบ ดีกว่าทอด</li>
                <li>🌾 เลือกข้าวกล้องแทนข้าวขาว</li>
                <li>💧 ดื่มน้ำเปล่าวันละ 8 แก้ว</li>
                <li>🍽️ กินอาหารให้ครบ 5 หมู่</li>
            </ul>
        </div>

        <div class="footer">
            <p>💕 สร้างด้วยความรักเพื่อสุขภาพที่ดีของทุกคนในครอบครัว</p>
            <p>Happy Home Recipes © 2024 - ความสุขเริ่มต้นจากจานอาหารที่บ้าน</p>
        </div>
    </div>

    <script>
        // ฟังก์ชันวิเคราะห์ประเภทวัตถุดิบ (ปรับปรุงให้ยืดหยุ่นด้วย RegExp)
        function analyzeIngredient(ingredient) {
            const ing = ingredient.toLowerCase();
            
            // โปรตีนและไขมัน
            if (ing.match(/ไก่|chicken|อกไก่|สะโพกไก่/)) return { type: 'protein', name: 'ไก่', gout: false, cholesterol: false };
            if (ing.match(/หมู|pork|เนื้อหมู/)) return { type: 'protein', name: 'หมู', gout: false, cholesterol: true };
            if (ing.match(/ปลา|fish/)) return { type: 'protein', name: 'ปลา', gout: false, cholesterol: false };
            if (ing.match(/กุ้ง|shrimp/)) return { type: 'protein', name: 'กุ้ง', gout: true, cholesterol: true };
            if (ing.match(/หอย|shell/)) return { type: 'protein', name: 'หอย', gout: true, cholesterol: true };
            if (ing.match(/ไข่|egg|ไข่แดง/)) return { type: 'protein', name: 'ไข่', cholesterol: true };
            if (ing.match(/เต้าหู้|tofu/)) return { type: 'protein', name: 'เต้าหู้', gout: false, cholesterol: false };
            
            // ผักและคาร์โบไฮเดรต
            if (ing.match(/ผักบุ้ง/)) return { type: 'vegetable', name: 'ผักบุ้ง', gout: false };
            if (ing.match(/คะน้า/)) return { type: 'vegetable', name: 'คะน้า', gout: false };
            if (ing.match(/มะเขือ|tomato/)) return { type: 'vegetable', name: 'มะเขือเทศ', gout: false };
            if (ing.match(/ฟักทอง|pumpkin/)) return { type: 'vegetable', name: 'ฟักทอง', gout: false };
            if (ing.match(/เห็ด|mushroom/)) return { type: 'vegetable', name: 'เห็ด', gout: true }; // เห็ดบางชนิดมีพิวรีนสูง
            if (ing.match(/หน่อไม้/)) return { type: 'vegetable', name: 'หน่อไม้', gout: true }; // พิวรีนสูง
            
            // สมุนไพรและเครื่องเทศ
            if (ing.match(/ตะไคร้|lemongrass/)) return { type: 'herb', name: 'ตะไคร้' };
            if (ing.match(/ข่า|galangal/)) return { type: 'herb', name: 'ข่า' };
            if (ing.match(/ใบมะกรูด|kaffir lime/)) return { type: 'herb', name: 'ใบมะกรูด' };
            if (ing.match(/พริก|chili/)) return { type: 'spice', name: 'พริก' };
            
            // ถ้าไม่พบ ให้เป็นผักทั่วไป
            return { type: 'vegetable', name: ingredient, gout: false, cholesterol: false };
        }

        // ฟังก์ชันสร้างเมนู (ปรับปรุงการจัดการสถานะ Loading)
        function generateMenu() {
            const ingredients = [];
            const generateBtn = document.querySelector('.generate-btn');
            const loadingDiv = document.getElementById('loading');
            const menuResultsDiv = document.getElementById('menuResults');
            const healthWarningDiv = document.getElementById('healthWarning');

            // 1. เก็บวัตถุดิบ
            for (let i = 1; i <= 5; i++) {
                const value = document.getElementById(`ingredient${i}`).value.trim();
                if (value) ingredients.push(value);
            }

            if (ingredients.length < 2) {
                alert('กรุณากรอกวัตถุดิบอย่างน้อย 2 รายการค่ะ 😊');
                return;
            }

            // 2. จัดการสถานะ Loading
            generateBtn.disabled = true; // ปิดการใช้งานปุ่ม
            loadingDiv.classList.add('active'); // แสดง loading
            menuResultsDiv.innerHTML = '';
            healthWarningDiv.style.display = 'none';

            // 3. เริ่มสร้างเมนู (จำลองการทำงาน 2 วินาที)
            setTimeout(() => {
                const analyzed = ingredients.map(ing => analyzeIngredient(ing));
                const proteins = analyzed.filter(a => a.type === 'protein');
                const vegetables = analyzed.filter(a => a.type === 'vegetable');
                const herbs = analyzed.filter(a => a.type === 'herb' || a.type === 'spice');

                let soupMenu, dryMenu;

                // ตรรกะการสร้างเมนูน้ำ
                if (proteins.length > 0) {
                    const mainProtein = proteins[0];
                    if (herbs.some(h => h.name === 'ตะไคร้' || h.name === 'ข่า')) {
                        soupMenu = createTomYum(mainProtein, vegetables, ingredients);
                    } else {
                        soupMenu = createClearSoup(mainProtein, vegetables, ingredients);
                    }
                } else {
                    // ถ้าไม่มีโปรตีน ใช้เมนูมังสวิรัติแบบน้ำ
                    soupMenu = createVegSoup(vegetables[0] || analyzed[0], ingredients);
                }

                // ตรรกะการสร้างเมนูแห้ง
                if (proteins.length > 0) {
                    const mainProtein = proteins[0];
                    if (herbs.some(h => h.name === 'พริก')) {
                        dryMenu = createSpicyStirFry(mainProtein, vegetables, ingredients);
                    } else {
                        dryMenu = createMildStirFry(mainProtein, vegetables, ingredients);
                    }
                } else {
                    // ถ้าไม่มีโปรตีน ใช้เมนูมังสวิรัติแบบแห้ง
                    dryMenu = createVegStirFry(vegetables[0] || analyzed[0], ingredients);
                }

                // 4. แสดงผลและเคลียร์สถานะ
                loadingDiv.classList.remove('active');
                generateBtn.disabled = false; // เปิดการใช้งานปุ่ม
                menuResultsDiv.innerHTML = soupMenu + dryMenu;
                healthWarningDiv.style.display = 'block';

                // 5. ล้าง Input เพื่อให้พร้อมใช้งานรอบถัดไป
                for (let i = 1; i <= 5; i++) {
                    document.getElementById(`ingredient${i}`).value = '';
                }

            }, 2000);
        }

        // ฟังก์ชันสร้างเมนูย่อย: ต้มยำ
        function createTomYum(protein, vegetables, ingredients) {
            const vegName = vegetables.length > 0 ? 'ใส่' + vegetables[0].name : '';
            const menuName = `ต้มยำ${protein.name}${vegName}`;
            
            return createMenuCard({
                name: menuName,
                type: 'soup',
                taste: 'strong',
                calories: '120-180',
                price: '50-80',
                time: '20 นาที',
                ingredients: [
                    `${protein.name}${protein.name === 'กุ้ง' ? 'สด' : 'หั่นชิ้น'} - 200 กรัม`,
                    'เห็ดฟาง - 100 กรัม',
                    'มะเขือเทศ - 2 ลูก',
                    'หอมแดง - 3 หัว'
                ],
                seasonings: [
                    'ตะไคร้ทุบ - 2 ต้น',
                    'ข่าหั่น - 5 แว่น', 
                    'ใบมะกรูด - 4 ใบ',
                    'พริกขี้หนูทุบ - 5-10 เม็ด',
                    'น้ำปลา - 2 ช้อนโต๊ะ',
                    'น้ำมะนาว - 3 ช้อนโต๊ะ'
                ],
                steps: [
                    'ต้มน้ำ 2 ถ้วย ใส่สมุนไพร',
                    `ใส่${protein.name} ต้มจนสุก`,
                    'ใส่เห็ดและมะเขือเทศ',
                    'ปิดไฟ ใส่พริก',
                    'ปรุงรสด้วยน้ำปลา น้ำมะนาว'
                ],
                warnings: {
                    diabetes: '✅ เหมาะสม - ไม่มีน้ำตาล',
                    hypertension: '⚠️ ลดน้ำปลา (โซเดียมสูง)',
                    cholesterol: protein.cholesterol ? `⚠️ ${protein.name}มีคอเลสเตอรอล/ไขมัน ควรตักมันออก` : '✅ ดี',
                    gout: protein.gout ? `❌ ${protein.name}มีพิวรีนสูง (เสี่ยงต่ออาการกำเริบ)` : '✅ ปลอดภัย'
                }
            });
        }

        // ฟังก์ชันสร้างเมนูย่อย: แกงจืด
        function createClearSoup(protein, vegetables, ingredients) {
            const vegName = vegetables.length > 0 ? vegetables[0].name : 'ผักกาด';
            const menuName = `แกงจืด${protein.name}${vegName}`;
            
            return createMenuCard({
                name: menuName,
                type: 'soup', 
                taste: 'mild',
                calories: '100-130',
                price: '40-50',
                time: '15 นาที',
                ingredients: [
                    `${protein.name}สับ - 200 กรัม`,
                    `${vegName} - 150 กรัม`,
                    'เต้าหู้ขาว - 1 แผ่น'
                ],
                seasonings: [
                    'น้ำซุป - 3 ถ้วย',
                    'กระเทียมทุบ - 3 กลีบ',
                    'ซีอิ๊วขาว - 1 ช้อนโต๊ะ',
                    'เกลือ - 1/4 ช้อนชา',
                    'พริกไทย - เล็กน้อย'
                ],
                steps: [
                    'ต้มน้ำซุปให้เดือด',
                    `ปั้น${protein.name}สับเป็นก้อน ใส่ต้ม`,
                    'รอลอยขึ้น ต้ม 3 นาที',
                    `ใส่${vegName}และเต้าหู้`,
                    'ปรุงรสด้วยซีอิ๊วขาว เกลือ'
                ],
                warnings: {
                    diabetes: '✅ ดีมาก - คาร์บต่ำ',
                    hypertension: '⚠️ ลดเกลือและซีอิ๊วขาว',
                    cholesterol: protein.cholesterol ? '⚠️ ถ้าใช้หมู/ไข่ ควรลดปริมาณ' : '✅ ดี',
                    gout: protein.gout ? `❌ ${protein.name}มีพิวรีนสูง` : '✅ ปลอดภัย'
                }
            });
        }

        // ฟังก์ชันสร้างเมนูย่อย: ผัดเผ็ด (กะเพรา)
        function createSpicyStirFry(protein, vegetables, ingredients) {
            const vegName = vegetables.length > 0 ? vegetables[0].name : '';
            const menuName = `ผัดกะเพรา${protein.name}${vegName ? `ใส่${vegName}` : ''}`;
            
            return createMenuCard({
                name: menuName,
                type: 'dry',
                taste: 'strong',
                calories: '250-300',
                price: '45-55',
                time: '10 นาที',
                ingredients: [
                    `${protein.name}สับ - 250 กรัม`,
                    'ใบกะเพรา - 1 กำมือ',
                    'ถั่วฝักยาว - 100 กรัม'
                ],
                seasonings: [
                    'น้ำมัน - 3 ช้อนโต๊ะ',
                    'กระเทียม - 5 กลีบ',
                    'พริกขี้หนู - 5-10 เม็ด',
                    'น้ำปลา - 1 ช้อนโต๊ะ',
                    'ซีอิ๊วดำ - 1 ช้อนโต๊ะ',
                    'น้ำตาล - 1 ช้อนชา'
                ],
                steps: [
                    'ตั้งกระทะไฟแรง',
                    'ผัดกระเทียมพริก',
                    `ใส่${protein.name} ผัดสุก`,
                    'ปรุงรส ใส่น้ำนิดหน่อย',
                    'ปิดไฟ ใส่กะเพรา'
                ],
                warnings: {
                    diabetes: '⚠️ ลดน้ำตาล (1 ช้อนชา)',
                    hypertension: '⚠️ ลดน้ำปลา/ซีอิ๊วขาว',
                    cholesterol: '⚠️ ใช้น้ำมันน้อย (อย่าให้ท่วม)',
                    gout: protein.gout ? `❌ ไม่เหมาะ (พิวรีนสูง)` : '✅ ดี'
                }
            });
        }

        // ฟังก์ชันสร้างเมนูย่อย: ผัดธรรมดา
        function createMildStirFry(protein, vegetables, ingredients) {
            const vegName = vegetables.length > 0 ? vegetables[0].name : 'ผัก';
            const menuName = `${protein.name}ผัด${vegName}`;
            
            return createMenuCard({
                name: menuName,
                type: 'dry',
                taste: 'mild',
                calories: '200-250',
                price: '50-60',
                time: '15 นาที',
                ingredients: [
                    `${protein.name}หั่น - 250 กรัม`,
                    `${vegName} - 150 กรัม`,
                    'หอมใหญ่ - 1/2 หัว'
                ],
                seasonings: [
                    'น้ำมัน - 2 ช้อนโต๊ะ',
                    'กระเทียม - 3 กลีบ',
                    'น้ำมันหอย - 1 ช้อนโต๊ะ',
                    'ซีอิ๊วขาว - 1 ช้อนโต๊ะ',
                    'น้ำตาล - 1/2 ช้อนชา'
                ],
                steps: [
                    'ผัดกระเทียมให้หอม',
                    `ใส่${protein.name} ผัดสุก`,
                    `ใส่${vegName} ผัดต่อ`,
                    'ปรุงรสด้วยซอส',
                    'ผัดให้เข้ากัน'
                ],
                warnings: {
                    diabetes: '✅ ดี',
                    hypertension: '⚠️ ลดซอสและน้ำปลา',
                    cholesterol: protein.cholesterol ? '⚠️ ระวังถ้าใช้เนื้อติดมัน' : '✅ ดี',
                    gout: protein.gout ? `❌ ไม่ดี (พิวรีนสูง)` : '✅ ปลอดภัย'
                }
            });
        }

        // ฟังก์ชันสร้างเมนูย่อย: มังสวิรัติ (น้ำ)
        function createVegSoup(veg, ingredients) {
            return createMenuCard({
                name: `แกงจืด${veg.name}ใส่เต้าหู้`,
                type: 'soup',
                taste: 'mild',
                calories: '80-100',
                price: '30-40',
                time: '15 นาที',
                ingredients: [`${veg.name} - 200 กรัม`, 'เต้าหู้ - 1 แผ่น'],
                seasonings: ['น้ำ - 3 ถ้วย', 'ซีอิ๊วขาว - 1 ช้อนโต๊ะ', 'เกลือ - 1/4 ช้อนชา'],
                steps: ['ต้มน้ำ', 'ใส่เต้าหู้', `ใส่${veg.name}`, 'ปรุงรส'],
                warnings: {
                    diabetes: '✅ ดีมาก (มีใยอาหารสูง)',
                    hypertension: '⚠️ ลดเกลือ/ซีอิ๊ว',
                    cholesterol: '✅ ดีมาก (ไม่มีไขมันสัตว์)',
                    gout: veg.gout ? `❌ ${veg.name}มีพิวรีนสูง (เช่น เห็ด หน่อไม้)` : '✅ ปลอดภัย'
                }
            });
        }

        // ฟังก์ชันสร้างเมนูย่อย: มังสวิรัติ (แห้ง)
        function createVegStirFry(veg, ingredients) {
            return createMenuCard({
                name: `ผัด${veg.name}น้ำมันหอย`,
                type: 'dry',
                taste: 'mild',
                calories: '120-150',
                price: '35-45',
                time: '10 นาที',
                ingredients: [`${veg.name} - 300 กรัม`],
                seasonings: ['น้ำมัน - 2 ช้อนโต๊ะ', 'กระเทียม - 3 กลีบ', 'น้ำมันหอย - 1 ช้อนโต๊ะ'],
                steps: ['เจียวกระเทียม', `ใส่${veg.name}`, 'ใส่น้ำมันหอย', 'ผัดให้สุก'],
                warnings: {
                    diabetes: '✅ ดี (ลดน้ำตาล)',
                    hypertension: '⚠️ ลดซอสปรุงรส', 
                    cholesterol: '✅ ดีมาก',
                    gout: veg.gout ? `❌ ${veg.name}มีพิวรีนสูง` : '✅ ปลอดภัย'
                }
            });
        }

        // ฟังก์ชันสร้างการ์ดเมนู (ปรับปรุงให้แสดงคำเตือนสุขภาพอัตโนมัติ)
        function createMenuCard(data) {
            const typeText = data.type === 'soup' ? '🍲 อาหารประเภทน้ำ' : '🍳 อาหารประเภทแห้ง';
            const tasteText = data.taste === 'mild' ? '😊 รสอ่อน เหมาะทุกวัย' : '🌶️ รสจัด';
            const tasteClass = data.taste === 'mild' ? 'taste-mild' : 'taste-strong';

            // สร้างรายการคำเตือนสุขภาพจาก Object warnings
            let warningsHtml = '';
            const warningLabels = {
                diabetes: '🩺 โรคเบาหวาน',
                hypertension: '💓 ความดันโลหิตสูง',
                cholesterol: '🧈 ไขมันในเลือดสูง',
                gout: '🦴 โรคเก๊าท์'
            };

            warningsHtml += '<h4>⚠️ คำแนะนำเฉพาะบุคคล</h4><ul>';
            for (const key in data.warnings) {
                if (data.warnings.hasOwnProperty(key)) {
                    const label = warningLabels[key] || key;
                    const message = data.warnings[key];
                    warningsHtml += `<li><strong>${label}:</strong> ${message}</li>`;
                }
            }
            warningsHtml += '</ul>';

            return `
                <div class="menu-card ${data.type}">
                    <div class="menu-card-header">${typeText}</div>
                    <div class="menu-card-body">
                        <div class="menu-name">
                            ${data.name}
                            <span class="calories-badge">🔥 ${data.calories} แคลอรี่</span>
                        </div>
                        <div class="taste-indicator ${tasteClass}">${tasteText}</div>
                        <div class="price-estimate">💰 งบประมาณ: ${data.price} บาท/มื้อ (โดยประมาณ)</div>
                        
                        <div class="menu-ingredients">
                            <h4>ส่วนผสมหลักที่ต้องใช้ 🥕</h4>
                            <ul>
                                ${[...data.ingredients, ...data.seasonings].map(item => `<li>${item}</li>`).join('')}
                            </ul>
                        </div>
                        
                        <div class="cooking-method">
                            <h4>ขั้นตอนการทำ (ใช้เวลา ${data.time}) ⏱️</h4>
                            <ol>
                                ${data.steps.map(step => `<li>${step}</li>`).join('')}
                            </ol>
                        </div>

                        <div class="menu-warnings">
                            ${warningsHtml}
                        </div>

                        <div class="nutrition-info">
                            <div class="nutrition-item">
                                <div class="label">โปรตีน</div>
                                <div class="value">20 g</div>
                            </div>
                            <div class="nutrition-item">
                                <div class="label">ไขมัน</div>
                                <div class="value">5-10 g</div>
                            </div>
                            <div class="nutrition-item">
                                <div class="label">คาร์โบไฮเดรต</div>
                                <div class="value">5-15 g</div>
                            </div>
                        </div>

                    </div>
                </div>
            `;
        }
    </script>
</body>
</html>
