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
            font-family: 'Sarabun', 'Prompt', sans-serif;
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

        /* Health Conditions Checkboxes */
        .health-conditions {
            margin-top: 25px;
            padding: 20px;
            background: white;
            border-radius: 15px;
            border: 2px solid #FFCDD2;
        }

        .health-conditions h3 {
            color: #D8627D;
            margin-bottom: 15px;
            font-size: 1.2em;
            text-align: center;
        }

        .conditions-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
            gap: 12px;
        }

        .condition-checkbox {
            display: flex;
            align-items: center;
            padding: 10px 15px;
            background: #FFF5F8;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .condition-checkbox:hover {
            background: #FFE0EC;
        }

        .condition-checkbox input {
            margin-right: 10px;
            width: 18px;
            height: 18px;
            cursor: pointer;
        }

        .condition-checkbox label {
            cursor: pointer;
            font-size: 1em;
            color: #555;
        }

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
            margin: 25px auto 0;
            box-shadow: 0 6px 20px rgba(249, 168, 212, 0.4);
        }

        .generate-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 8px 25px rgba(249, 168, 212, 0.5);
        }

        .generate-btn:active {
            transform: translateY(-1px);
        }
        
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

        .menu-card.not-recommended {
            border-top: 5px solid #FFCDD2;
            background: linear-gradient(to bottom, #FFF5F5, white);
            opacity: 0.85;
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

        .menu-card.not-recommended .menu-card-header {
            background: linear-gradient(135deg, #FFCDD2, #EF9A9A);
            color: #C62828;
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

        .menu-ingredients li.user-ingredient {
            background: #E8F5E9;
            border-radius: 8px;
            margin: 4px 0;
            padding-left: 25px;
        }

        .menu-ingredients li.user-ingredient:before {
            content: '✓';
            color: #43A047;
        }

        .menu-ingredients li.basic-ingredient {
            color: #888;
            font-style: italic;
        }

        .menu-ingredients li.basic-ingredient:before {
            content: '○';
            color: #ccc;
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

        .warning-danger {
            background: #FFEBEE !important;
            border-left-color: #EF5350 !important;
        }

        .warning-danger h4 {
            color: #C62828 !important;
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

        .ingredient-legend {
            margin-top: 15px;
            padding: 10px 15px;
            background: #F5F5F5;
            border-radius: 10px;
            font-size: 0.9em;
            color: #666;
        }

        .ingredient-legend span {
            margin-right: 20px;
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

            <!-- ส่วนเลือกโรคประจำตัว -->
            <div class="health-conditions">
                <h3>🏥 โรคประจำตัวในครอบครัว (ถ้ามี)</h3>
                <div class="conditions-grid">
                    <div class="condition-checkbox">
                        <input type="checkbox" id="diabetes" name="health">
                        <label for="diabetes">🩺 โรคเบาหวาน</label>
                    </div>
                    <div class="condition-checkbox">
                        <input type="checkbox" id="hypertension" name="health">
                        <label for="hypertension">💓 ความดันโลหิตสูง</label>
                    </div>
                    <div class="condition-checkbox">
                        <input type="checkbox" id="cholesterol" name="health">
                        <label for="cholesterol">🧈 ไขมันในเลือดสูง</label>
                    </div>
                    <div class="condition-checkbox">
                        <input type="checkbox" id="gout" name="health">
                        <label for="gout">🦴 โรคเก๊าท์</label>
                    </div>
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
                            <li>อาหารทะเล (กุ้ง หอย ปู ปลาซาร์ดีน)</li>
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
        // ===== ฐานข้อมูลวัตถุดิบพร้อมข้อมูลสุขภาพที่ละเอียด =====
        const ingredientDatabase = {
            // โปรตีน
            'ไก่': { type: 'protein', name: 'ไก่', gout: false, cholesterol: false, highSodium: false, highSugar: false },
            'อกไก่': { type: 'protein', name: 'อกไก่', gout: false, cholesterol: false, highSodium: false, highSugar: false },
            'สะโพกไก่': { type: 'protein', name: 'สะโพกไก่', gout: false, cholesterol: true, highSodium: false, highSugar: false },
            'หมู': { type: 'protein', name: 'หมู', gout: false, cholesterol: true, highSodium: false, highSugar: false },
            'หมูสับ': { type: 'protein', name: 'หมูสับ', gout: false, cholesterol: true, highSodium: false, highSugar: false },
            'หมูสามชั้น': { type: 'protein', name: 'หมูสามชั้น', gout: false, cholesterol: true, highSodium: false, highSugar: false },
            'เนื้อวัว': { type: 'protein', name: 'เนื้อวัว', gout: true, cholesterol: true, highSodium: false, highSugar: false },
            'เนื้อ': { type: 'protein', name: 'เนื้อวัว', gout: true, cholesterol: true, highSodium: false, highSugar: false },
            'ปลา': { type: 'protein', name: 'ปลา', gout: false, cholesterol: false, highSodium: false, highSugar: false },
            'ปลานิล': { type: 'protein', name: 'ปลานิล', gout: false, cholesterol: false, highSodium: false, highSugar: false },
            'ปลาทู': { type: 'protein', name: 'ปลาทู', gout: true, cholesterol: false, highSodium: false, highSugar: false },
            'ปลาซาบะ': { type: 'protein', name: 'ปลาซาบะ', gout: true, cholesterol: false, highSodium: false, highSugar: false },
            'กุ้ง': { type: 'protein', name: 'กุ้ง', gout: true, cholesterol: true, highSodium: false, highSugar: false },
            'หอย': { type: 'protein', name: 'หอย', gout: true, cholesterol: true, highSodium: false, highSugar: false },
            'หอยแมลงภู่': { type: 'protein', name: 'หอยแมลงภู่', gout: true, cholesterol: true, highSodium: false, highSugar: false },
            'ปู': { type: 'protein', name: 'ปู', gout: true, cholesterol: true, highSodium: false, highSugar: false },
            'ปลาหมึก': { type: 'protein', name: 'ปลาหมึก', gout: true, cholesterol: true, highSodium: false, highSugar: false },
            'ไข่': { type: 'protein', name: 'ไข่', gout: false, cholesterol: true, highSodium: false, highSugar: false },
            'ไข่ไก่': { type: 'protein', name: 'ไข่ไก่', gout: false, cholesterol: true, highSodium: false, highSugar: false },
            'ไข่เป็ด': { type: 'protein', name: 'ไข่เป็ด', gout: false, cholesterol: true, highSodium: false, highSugar: false },
            'เต้าหู้': { type: 'protein', name: 'เต้าหู้', gout: false, cholesterol: false, highSodium: false, highSugar: false },
            'เต้าหู้ไข่': { type: 'protein', name: 'เต้าหู้ไข่', gout: false, cholesterol: false, highSodium: false, highSugar: false },
            'ตับ': { type: 'protein', name: 'ตับ', gout: true, cholesterol: true, highSodium: false, highSugar: false },
            'เครื่องใน': { type: 'protein', name: 'เครื่องใน', gout: true, cholesterol: true, highSodium: false, highSugar: false },
            
            // ผัก
            'ผักบุ้ง': { type: 'vegetable', name: 'ผักบุ้ง', gout: false, cholesterol: false, highSodium: false, highSugar: false },
            'คะน้า': { type: 'vegetable', name: 'คะน้า', gout: false, cholesterol: false, highSodium: false, highSugar: false },
            'ผักกาด': { type: 'vegetable', name: 'ผักกาด', gout: false, cholesterol: false, highSodium: false, highSugar: false },
            'ผักกาดขาว': { type: 'vegetable', name: 'ผักกาดขาว', gout: false, cholesterol: false, highSodium: false, highSugar: false },
            'กะหล่ำปลี': { type: 'vegetable', name: 'กะหล่ำปลี', gout: false, cholesterol: false, highSodium: false, highSugar: false },
            'บร็อคโคลี่': { type: 'vegetable', name: 'บร็อคโคลี่', gout: false, cholesterol: false, highSodium: false, highSugar: false },
            'มะเขือเทศ': { type: 'vegetable', name: 'มะเขือเทศ', gout: false, cholesterol: false, highSodium: false, highSugar: false },
            'มะเขือ': { type: 'vegetable', name: 'มะเขือ', gout: false, cholesterol: false, highSodium: false, highSugar: false },
            'มะเขือยาว': { type: 'vegetable', name: 'มะเขือยาว', gout: false, cholesterol: false, highSodium: false, highSugar: false },
            'มะเขือเปราะ': { type: 'vegetable', name: 'มะเขือเปราะ', gout: false, cholesterol: false, highSodium: false, highSugar: false },
            'ฟักทอง': { type: 'vegetable', name: 'ฟักทอง', gout: false, cholesterol: false, highSodium: false, highSugar: false },
            'ฟักเขียว': { type: 'vegetable', name: 'ฟักเขียว', gout: false, cholesterol: false, highSodium: false, highSugar: false },
            'แตงกวา': { type: 'vegetable', name: 'แตงกวา', gout: false, cholesterol: false, highSodium: false, highSugar: false },
            'ถั่วฝักยาว': { type: 'vegetable', name: 'ถั่วฝักยาว', gout: false, cholesterol: false, highSodium: false, highSugar: false },
            'ถั่วงอก': { type: 'vegetable', name: 'ถั่วงอก', gout: false, cholesterol: false, highSodium: false, highSugar: false },
            'ถั่วลันเตา': { type: 'vegetable', name: 'ถั่วลันเตา', gout: false, cholesterol: false, highSodium: false, highSugar: false },
            'แครอท': { type: 'vegetable', name: 'แครอท', gout: false, cholesterol: false, highSodium: false, highSugar: false },
            'หัวไชเท้า': { type: 'vegetable', name: 'หัวไชเท้า', gout: false, cholesterol: false, highSodium: false, highSugar: false },
            'มันฝรั่ง': { type: 'vegetable', name: 'มันฝรั่ง', gout: false, cholesterol: false, highSodium: false, highSugar: true },
            'เห็ด': { type: 'vegetable', name: 'เห็ด', gout: true, cholesterol: false, highSodium: false, highSugar: false },
            'เห็ดหอม': { type: 'vegetable', name: 'เห็ดหอม', gout: true, cholesterol: false, highSodium: false, highSugar: false },
            'เห็ดฟาง': { type: 'vegetable', name: 'เห็ดฟาง', gout: true, cholesterol: false, highSodium: false, highSugar: false },
            'เห็ดนางฟ้า': { type: 'vegetable', name: 'เห็ดนางฟ้า', gout: true, cholesterol: false, highSodium: false, highSugar: false },
            'หน่อไม้': { type: 'vegetable', name: 'หน่อไม้', gout: true, cholesterol: false, highSodium: false, highSugar: false },
            'ข้าวโพด': { type: 'vegetable', name: 'ข้าวโพด', gout: false, cholesterol: false, highSodium: false, highSugar: true },
            'ข้าวโพดอ่อน': { type: 'vegetable', name: 'ข้าวโพดอ่อน', gout: false, cholesterol: false, highSodium: false, highSugar: false },
            'พริกหวาน': { type: 'vegetable', name: 'พริกหวาน', gout: false, cholesterol: false, highSodium: false, highSugar: false },
            'หอมใหญ่': { type: 'vegetable', name: 'หอมใหญ่', gout: false, cholesterol: false, highSodium: false, highSugar: false },
            'ต้นหอม': { type: 'vegetable', name: 'ต้นหอม', gout: false, cholesterol: false, highSodium: false, highSugar: false },
            'ผักชี': { type: 'vegetable', name: 'ผักชี', gout: false, cholesterol: false, highSodium: false, highSugar: false },
            'ผักชีฝรั่ง': { type: 'vegetable', name: 'ผักชีฝรั่ง', gout: false, cholesterol: false, highSodium: false, highSugar: false },
            'กะเพรา': { type: 'herb', name: 'ใบกะเพรา', gout: false, cholesterol: false, highSodium: false, highSugar: false },
            'ใบกะเพรา': { type: 'herb', name: 'ใบกะเพรา', gout: false, cholesterol: false, highSodium: false, highSugar: false },
            'โหระพา': { type: 'herb', name: 'ใบโหระพา', gout: false, cholesterol: false, highSodium: false, highSugar: false },
            'ใบโหระพา': { type: 'herb', name: 'ใบโหระพา', gout: false, cholesterol: false, highSodium: false, highSugar: false },
            
            // สมุนไพรและเครื่องเทศ
            'ตะไคร้': { type: 'herb', name: 'ตะไคร้', gout: false, cholesterol: false, highSodium: false, highSugar: false },
            'ข่า': { type: 'herb', name: 'ข่า', gout: false, cholesterol: false, highSodium: false, highSugar: false },
            'ขิง': { type: 'herb', name: 'ขิง', gout: false, cholesterol: false, highSodium: false, highSugar: false },
            'ใบมะกรูด': { type: 'herb', name: 'ใบมะกรูด', gout: false, cholesterol: false, highSodium: false, highSugar: false },
            'พริก': { type: 'spice', name: 'พริก', gout: false, cholesterol: false, highSodium: false, highSugar: false },
            'พริกขี้หนู': { type: 'spice', name: 'พริกขี้หนู', gout: false, cholesterol: false, highSodium: false, highSugar: false },
            'พริกแห้ง': { type: 'spice', name: 'พริกแห้ง', gout: false, cholesterol: false, highSodium: false, highSugar: false },
            'กระเทียม': { type: 'spice', name: 'กระเทียม', gout: false, cholesterol: false, highSodium: false, highSugar: false },
            'หอมแดง': { type: 'spice', name: 'หอมแดง', gout: false, cholesterol: false, highSodium: false, highSugar: false },
            'มะนาว': { type: 'spice', name: 'มะนาว', gout: false, cholesterol: false, highSodium: false, highSugar: false },
            
            // คาร์โบไฮเดรต
            'เส้นหมี่': { type: 'carb', name: 'เส้นหมี่', gout: false, cholesterol: false, highSodium: false, highSugar: true },
            'เส้นใหญ่': { type: 'carb', name: 'เส้นใหญ่', gout: false, cholesterol: false, highSodium: false, highSugar: true },
            'วุ้นเส้น': { type: 'carb', name: 'วุ้นเส้น', gout: false, cholesterol: false, highSodium: false, highSugar: false },
            'บะหมี่': { type: 'carb', name: 'บะหมี่', gout: false, cholesterol: false, highSodium: false, highSugar: true }
        };

        // ===== ฟังก์ชันวิเคราะห์วัตถุดิบ =====
        function analyzeIngredient(ingredient) {
            const ing = ingredient.trim().toLowerCase();
            
            // ค้นหาตรงๆ ก่อน
            if (ingredientDatabase[ingredient.trim()]) {
                return { ...ingredientDatabase[ingredient.trim()], originalInput: ingredient.trim() };
            }
            
            // ค้นหาแบบ partial match
            for (const [key, value] of Object.entries(ingredientDatabase)) {
                if (ing.includes(key.toLowerCase()) || key.toLowerCase().includes(ing)) {
                    return { ...value, originalInput: ingredient.trim() };
                }
            }
            
            // ถ้าไม่เจอ ให้เป็นวัตถุดิบทั่วไป (ไม่รู้จัก)
            return { 
                type: 'unknown', 
                name: ingredient.trim(), 
                originalInput: ingredient.trim(),
                gout: false, 
                cholesterol: false, 
                highSodium: false, 
                highSugar: false 
            };
        }

        // ===== ฟังก์ชันตรวจสอบสุขภาพ =====
        function checkHealthWarnings(ingredients, seasonings, userConditions) {
            const warnings = [];
            const isDangerous = {
                diabetes: false,
                hypertension: false,
                cholesterol: false,
                gout: false
            };
            
            // ตรวจสอบวัตถุดิบ
            ingredients.forEach(ing => {
                if (userConditions.gout && ing.gout) {
                    warnings.push(`❌ ${ing.name} มีพิวรีนสูง ไม่เหมาะกับผู้ป่วยโรคเก๊าท์`);
                    isDangerous.gout = true;
                }
                if (userConditions.cholesterol && ing.cholesterol) {
                    warnings.push(`⚠️ ${ing.name} มีคอเลสเตอรอลสูง ควรจำกัดปริมาณ`);
                    isDangerous.cholesterol = true;
                }
                if (userConditions.diabetes && ing.highSugar) {
                    warnings.push(`⚠️ ${ing.name} มีคาร์โบไฮเดรตสูง ควรจำกัดปริมาณ`);
                    isDangerous.diabetes = true;
                }
            });
            
            // ตรวจสอบเครื่องปรุงพื้นฐาน (ที่จำเป็นต้องใช้)
            seasonings.forEach(seasoning => {
                if (userConditions.hypertension && seasoning.highSodium) {
                    warnings.push(`⚠️ ${seasoning.name} มีโซเดียมสูง - ใช้ปริมาณน้อยหรืองดใช้`);
                    isDangerous.hypertension = true;
                }
                if (userConditions.diabetes && seasoning.highSugar) {
                    warnings.push(`⚠️ ${seasoning.name} มีน้ำตาล - งดหรือใช้สารให้ความหวานแทน`);
                    isDangerous.diabetes = true;
                }
            });
            
            return { warnings, isDangerous };
        }

        // ===== ฟังก์ชันสร้างเมนู =====
        function generateMenu() {
            const ingredients = [];
            const generateBtn = document.querySelector('.generate-btn');
            const loadingDiv = document.getElementById('loading');
            const menuResultsDiv = document.getElementById('menuResults');
            const healthWarningDiv = document.getElementById('healthWarning');

            // เก็บวัตถุดิบ
            for (let i = 1; i <= 5; i++) {
                const value = document.getElementById(`ingredient${i}`).value.trim();
                if (value) ingredients.push(value);
            }

            if (ingredients.length < 1) {
                alert('กรุณากรอกวัตถุดิบอย่างน้อย 1 รายการค่ะ 😊');
                return;
            }

            // เก็บข้อมูลโรคประจำตัว
            const userConditions = {
                diabetes: document.getElementById('diabetes').checked,
                hypertension: document.getElementById('hypertension').checked,
                cholesterol: document.getElementById('cholesterol').checked,
                gout: document.getElementById('gout').checked
            };

            // แสดง Loading
            generateBtn.disabled = true;
            loadingDiv.classList.add('active');
            menuResultsDiv.innerHTML = '';
            healthWarningDiv.style.display = 'none';

            setTimeout(() => {
                // วิเคราะห์วัตถุดิบ
                const analyzed = ingredients.map(ing => analyzeIngredient(ing));
                const proteins = analyzed.filter(a => a.type === 'protein');
                const vegetables = analyzed.filter(a => a.type === 'vegetable');
                const herbs = analyzed.filter(a => a.type === 'herb');
                const spices = analyzed.filter(a => a.type === 'spice');
                const carbs = analyzed.filter(a => a.type === 'carb');
                const unknowns = analyzed.filter(a => a.type === 'unknown');
                
                let menuHTML = '';

                // ===== ตรรกะการสร้างเมนู (สร้าง 2 เมนู: รสจัด + รสอ่อน) =====
                
                let spicyMenus = [];  // เมนูรสจัด 🌶️
                let mildMenus = [];   // เมนูรสอ่อน 😊

                // ===== เมนูรสจัด (ต้องมีพริก หรือเครื่องเทศ) =====
                
                // 1. ผัดกะเพรา (รสจัด)
                if (proteins.length > 0 && herbs.some(h => h.name === 'ใบกะเพรา')) {
                    spicyMenus.push(createPadKrapao(proteins, vegetables, herbs, spices, analyzed, userConditions, true));
                }

                // 2. ต้มยำ (รสจัด)
                const tomYumHerbs = herbs.filter(h => ['ตะไคร้', 'ข่า', 'ใบมะกรูด'].includes(h.name));
                if (proteins.length > 0 && tomYumHerbs.length >= 1) {
                    spicyMenus.push(createTomYum(proteins, vegetables, herbs, spices, analyzed, userConditions, true));
                }

                // 3. ผัดพริก (รสจัด) - ถ้ามีพริก
                if (proteins.length > 0 && spices.some(s => s.name.includes('พริก'))) {
                    spicyMenus.push(createSpicyStirFry(proteins, vegetables, herbs, spices, analyzed, userConditions));
                }

                // 4. ยำ (รสจัด) - ถ้ามีมะนาว+พริก
                if (proteins.length > 0 && spices.some(s => s.name === 'มะนาว')) {
                    spicyMenus.push(createYum(proteins, vegetables, herbs, spices, analyzed, userConditions));
                }

                // ===== เมนูรสอ่อน (ไม่เผ็ด เหมาะทุกวัย) =====

                // 1. ผัดน้ำมันหอย (รสอ่อน)
                if (proteins.length > 0 && vegetables.length > 0) {
                    mildMenus.push(createStirFry(proteins, vegetables, herbs, spices, analyzed, userConditions));
                }

                // 2. ไข่เจียว (รสอ่อน)
                if (proteins.some(p => p.name.includes('ไข่'))) {
                    mildMenus.push(createOmelette(proteins, vegetables, herbs, spices, analyzed, userConditions));
                }

                // 3. ผัดขิง (รสอ่อน)
                if (proteins.length > 0 && herbs.some(h => h.name === 'ขิง')) {
                    mildMenus.push(createPadKhing(proteins, vegetables, herbs, spices, analyzed, userConditions));
                }

                // 4. แกงจืด/ต้มจืด (รสอ่อน) - ถ้ามีผัก
                if (proteins.length > 0 && vegetables.length > 0) {
                    mildMenus.push(createClearSoup(proteins, vegetables, herbs, spices, analyzed, userConditions));
                }

                // 5. ผัดผักรสอ่อน
                if (vegetables.length > 0) {
                    mildMenus.push(createVegStirFry(vegetables, herbs, spices, analyzed, userConditions));
                }

                // 6. ผัดเส้น (รสอ่อน)
                if (carbs.length > 0 && (proteins.length > 0 || vegetables.length > 0)) {
                    mildMenus.push(createPadNoodle(proteins, vegetables, carbs, herbs, spices, analyzed, userConditions));
                }

                // 7. โปรตีนทอด/ย่าง (รสอ่อน)
                if (proteins.length > 0) {
                    mildMenus.push(createSimpleProtein(proteins, spices, analyzed, userConditions));
                }

                // 8. นึ่ง (รสอ่อน) - สำหรับปลา/ไก่
                if (proteins.some(p => ['ปลา', 'ปลานิล', 'ไก่', 'อกไก่'].includes(p.name))) {
                    mildMenus.push(createSteamed(proteins, vegetables, herbs, spices, analyzed, userConditions));
                }

                // ===== เลือกเมนู 1 รสจัด + 1 รสอ่อน =====
                
                // กรองเมนูที่ซ้ำและ null ออก
                spicyMenus = [...new Map(spicyMenus.filter(m => m).map(m => [m.name, m])).values()];
                mildMenus = [...new Map(mildMenus.filter(m => m).map(m => [m.name, m])).values()];

                // เลือกเมนูที่ดีที่สุด (ไม่อันตรายต่อสุขภาพมาก่อน)
                const sortByHealth = (menus) => {
                    return menus.sort((a, b) => {
                        const aDanger = Object.values(a.isDangerous).filter(v => v).length;
                        const bDanger = Object.values(b.isDangerous).filter(v => v).length;
                        return aDanger - bDanger;
                    });
                };

                spicyMenus = sortByHealth(spicyMenus);
                mildMenus = sortByHealth(mildMenus);

                // รวมเมนู: 1 รสจัด + 1 รสอ่อน
                const uniqueMenus = [];
                if (spicyMenus.length > 0) uniqueMenus.push(spicyMenus[0]);
                if (mildMenus.length > 0) uniqueMenus.push(mildMenus[0]);
                
                if (uniqueMenus.length === 0) {
                    menuHTML = `
                        <div style="text-align: center; padding: 40px; color: #D8627D; font-size: 1.2em;">
                            <p>😢 วัตถุดิบที่กรอกมายังไม่เพียงพอสำหรับสร้างเมนูค่ะ</p>
                            <p style="margin-top: 15px; color: #888; font-size: 0.95em;">
                                <strong>💡 คำแนะนำ:</strong><br>
                                - ลองเพิ่มโปรตีน เช่น ไก่, หมู, ไข่, เต้าหู้<br>
                                - หรือเพิ่มผัก เช่น ผักบุ้ง, คะน้า, ถั่วฝักยาว<br>
                                - หรือเพิ่มสมุนไพร เช่น กะเพรา, ตะไคร้, ข่า
                            </p>
                        </div>
                    `;
                } else if (uniqueMenus.length === 1) {
                    // มีแค่เมนูเดียว แสดงพร้อมคำแนะนำ
                    menuHTML = `
                        <div style="text-align: center; padding: 20px; margin-bottom: 20px; background: #FFF9E7; border-radius: 15px; color: #E65100;">
                            <p>💡 <strong>คำแนะนำ:</strong> เพิ่มวัตถุดิบเพื่อให้ได้เมนูหลากหลายขึ้น</p>
                            <p style="font-size: 0.9em; color: #888; margin-top: 8px;">
                                เช่น เพิ่ม "พริก" หรือ "กะเพรา" สำหรับเมนูรสจัด หรือเพิ่ม "ผัก" สำหรับเมนูรสอ่อน
                            </p>
                        </div>
                    `;
                    uniqueMenus.forEach(menu => {
                        menuHTML += createMenuCard(menu, userConditions);
                    });
                } else {
                    // แสดงหัวข้อแยก 2 รสชาติ
                    menuHTML = `
                        <div style="grid-column: 1 / -1; text-align: center; padding: 15px; margin-bottom: 10px;">
                            <h3 style="color: #D8627D; font-size: 1.5em;">🍽️ 2 เมนูแนะนำสำหรับครอบครัว</h3>
                            <p style="color: #888; font-size: 1em; margin-top: 8px;">รสจัดสำหรับผู้ใหญ่ 🌶️ และรสอ่อนสำหรับทุกวัย 😊</p>
                        </div>
                    `;
                    uniqueMenus.forEach(menu => {
                        menuHTML += createMenuCard(menu, userConditions);
                    });
                }

                // แสดงผล
                loadingDiv.classList.remove('active');
                generateBtn.disabled = false;
                menuResultsDiv.innerHTML = menuHTML;
                
                // แสดงคำเตือนสุขภาพถ้ามีการเลือกโรค
                if (Object.values(userConditions).some(v => v)) {
                    healthWarningDiv.style.display = 'block';
                }

                // ล้าง Input
                for (let i = 1; i <= 5; i++) {
                    document.getElementById(`ingredient${i}`).value = '';
                }

            }, 1500);
        }

        // ===== ฟังก์ชันสร้างเมนูย่อย =====

        // เครื่องปรุงพื้นฐานที่ทุกครัวมี
        const basicSeasonings = {
            oil: { name: 'น้ำมันพืช', amount: '1-2 ช้อนโต๊ะ', highSodium: false, highSugar: false },
            fishSauce: { name: 'น้ำปลา', amount: '1 ช้อนโต๊ะ', highSodium: true, highSugar: false },
            soySauce: { name: 'ซีอิ๊วขาว', amount: '1 ช้อนโต๊ะ', highSodium: true, highSugar: false },
            oysterSauce: { name: 'น้ำมันหอย', amount: '1 ช้อนโต๊ะ', highSodium: true, highSugar: false },
            sugar: { name: 'น้ำตาล', amount: '1/2 ช้อนชา', highSodium: false, highSugar: true },
            salt: { name: 'เกลือ', amount: '1/4 ช้อนชา', highSodium: true, highSugar: false },
            pepper: { name: 'พริกไทย', amount: 'เล็กน้อย', highSodium: false, highSugar: false },
            water: { name: 'น้ำเปล่า', amount: 'ตามต้องการ', highSodium: false, highSugar: false }
        };

        // ผัดธรรมดา (รสอ่อน)
        function createStirFry(proteins, vegetables, herbs, spices, allIngredients, userConditions) {
            const mainProtein = proteins[0];
            const mainVeg = vegetables[0];
            
            const usedIngredients = [mainProtein, mainVeg, ...vegetables.slice(1)];
            const usedSeasonings = [basicSeasonings.oil, basicSeasonings.oysterSauce];
            
            // เพิ่มกระเทียมถ้ามี
            if (spices.some(s => s.name === 'กระเทียม')) {
                usedIngredients.push(spices.find(s => s.name === 'กระเทียม'));
            }

            const healthCheck = checkHealthWarnings(usedIngredients, usedSeasonings, userConditions);
            
            return {
                name: `${mainProtein.name}ผัด${mainVeg.name} 😊`,
                type: 'dry',
                taste: 'mild',
                calories: '180-250',
                price: '40-60',
                time: '15 นาที',
                userIngredients: usedIngredients,
                basicSeasonings: usedSeasonings,
                steps: [
                    spices.some(s => s.name === 'กระเทียม') ? 'ตั้งกระทะใส่น้ำมัน เจียวกระเทียมให้หอม' : 'ตั้งกระทะใส่น้ำมันให้ร้อน',
                    `ใส่${mainProtein.name}หั่นชิ้น ผัดจนสุก`,
                    `ใส่${vegetables.map(v => v.name).join(', ')} ผัดต่อจนผักสลด`,
                    'ปรุงรสด้วยน้ำมันหอย คลุกให้เข้ากัน',
                    'ตักเสิร์ฟร้อนๆ'
                ],
                healthWarnings: healthCheck.warnings,
                isDangerous: healthCheck.isDangerous
            };
        }

        // ผัดกะเพรา
        function createPadKrapao(proteins, vegetables, herbs, spices, allIngredients, userConditions, isSpicy = true) {
            const mainProtein = proteins[0];
            const krapao = herbs.find(h => h.name === 'ใบกะเพรา');
            
            const usedIngredients = [mainProtein, krapao];
            const usedSeasonings = [basicSeasonings.oil, basicSeasonings.fishSauce, basicSeasonings.sugar];
            
            // เพิ่มกระเทียม/พริกถ้ามี
            if (spices.some(s => s.name === 'กระเทียม')) {
                usedIngredients.push(spices.find(s => s.name === 'กระเทียม'));
            }
            
            const hasChili = spices.some(s => s.name.includes('พริก'));
            if (hasChili) {
                usedIngredients.push(spices.find(s => s.name.includes('พริก')));
            }
            
            // เพิ่มผักถ้ามี
            if (vegetables.length > 0) {
                vegetables.forEach(v => usedIngredients.push(v));
            }

            const healthCheck = checkHealthWarnings(usedIngredients, usedSeasonings, userConditions);
            
            const hasGarlic = spices.some(s => s.name === 'กระเทียม');
            
            return {
                name: `ผัดกะเพรา${mainProtein.name}${hasChili ? ' 🌶️' : ' (รสอ่อน)'}`,
                type: 'dry',
                taste: hasChili ? 'strong' : 'mild',
                calories: '250-320',
                price: '45-65',
                time: '10 นาที',
                userIngredients: usedIngredients,
                basicSeasonings: usedSeasonings,
                steps: [
                    hasGarlic && hasChili ? 'โขลกกระเทียมและพริกพอหยาบ ผัดกับน้ำมันให้หอม' : 
                    hasGarlic ? 'เจียวกระเทียมกับน้ำมันให้หอม' : 'ตั้งกระทะใส่น้ำมันให้ร้อน',
                    `ใส่${mainProtein.name}สับ ผัดจนสุก`,
                    vegetables.length > 0 ? `ใส่${vegetables.map(v => v.name).join(', ')} ผัดต่อ` : null,
                    'ปรุงรสด้วยน้ำปลา น้ำตาลเล็กน้อย',
                    'ใส่ใบกะเพรา คลุกเร็วๆ แล้วปิดไฟ',
                    'ตักเสิร์ฟพร้อมข้าวสวยร้อนๆ'
                ].filter(Boolean),
                healthWarnings: healthCheck.warnings,
                isDangerous: healthCheck.isDangerous
            };
        }

        // ต้มยำ (รสจัด)
        function createTomYum(proteins, vegetables, herbs, spices, allIngredients, userConditions, isSpicy = true) {
            const mainProtein = proteins[0];
            const tomYumHerbs = herbs.filter(h => ['ตะไคร้', 'ข่า', 'ใบมะกรูด'].includes(h.name));
            
            const usedIngredients = [mainProtein, ...tomYumHerbs];
            const usedSeasonings = [basicSeasonings.fishSauce, basicSeasonings.water];
            
            // เพิ่มผัก/เห็ดถ้ามี
            if (vegetables.length > 0) {
                vegetables.forEach(v => usedIngredients.push(v));
            }
            
            // เพิ่มพริก/มะนาวถ้ามี
            const hasChili = spices.some(s => s.name.includes('พริก'));
            if (hasChili) {
                usedIngredients.push(spices.find(s => s.name.includes('พริก')));
            }
            if (spices.some(s => s.name === 'มะนาว')) {
                usedIngredients.push(spices.find(s => s.name === 'มะนาว'));
            }

            const healthCheck = checkHealthWarnings(usedIngredients, usedSeasonings, userConditions);
            const hasLime = spices.some(s => s.name === 'มะนาว');
            
            return {
                name: `ต้มยำ${mainProtein.name}น้ำใส 🌶️`,
                type: 'soup',
                taste: 'strong',
                calories: '120-180',
                price: '50-80',
                time: '20 นาที',
                userIngredients: usedIngredients,
                basicSeasonings: usedSeasonings,
                steps: [
                    'ต้มน้ำให้เดือด',
                    tomYumHerbs.length > 0 ? `ใส่${tomYumHerbs.map(h => h.name).join(', ')} ต้มให้หอม` : null,
                    `ใส่${mainProtein.name} ต้มจนสุก`,
                    vegetables.length > 0 ? `ใส่${vegetables.map(v => v.name).join(', ')}` : null,
                    'ปรุงรสด้วยน้ำปลา',
                    hasLime ? 'ปิดไฟ บีบมะนาว' : 'ปิดไฟ',
                    hasChili ? 'โรยพริกขี้หนูตามชอบ' : null
                ].filter(Boolean),
                healthWarnings: healthCheck.warnings,
                isDangerous: healthCheck.isDangerous
            };
        }

        // ผัดพริก (รสจัด)
        function createSpicyStirFry(proteins, vegetables, herbs, spices, allIngredients, userConditions) {
            const mainProtein = proteins[0];
            const chili = spices.find(s => s.name.includes('พริก'));
            
            const usedIngredients = [mainProtein, chili];
            const usedSeasonings = [basicSeasonings.oil, basicSeasonings.fishSauce, basicSeasonings.oysterSauce];
            
            if (spices.some(s => s.name === 'กระเทียม')) {
                usedIngredients.push(spices.find(s => s.name === 'กระเทียม'));
            }
            if (vegetables.length > 0) {
                vegetables.forEach(v => usedIngredients.push(v));
            }

            const healthCheck = checkHealthWarnings(usedIngredients, usedSeasonings, userConditions);
            const hasGarlic = spices.some(s => s.name === 'กระเทียม');
            
            return {
                name: `${mainProtein.name}ผัดพริก 🌶️`,
                type: 'dry',
                taste: 'strong',
                calories: '200-280',
                price: '45-65',
                time: '12 นาที',
                userIngredients: usedIngredients,
                basicSeasonings: usedSeasonings,
                steps: [
                    hasGarlic ? 'โขลกกระเทียมและพริกพอหยาบ' : 'หั่นพริกเป็นชิ้น',
                    'ตั้งกระทะใส่น้ำมัน ผัดพริก' + (hasGarlic ? 'กระเทียม' : '') + 'ให้หอม',
                    `ใส่${mainProtein.name}หั่นชิ้น ผัดจนสุก`,
                    vegetables.length > 0 ? `ใส่${vegetables.map(v => v.name).join(', ')} ผัดต่อ` : null,
                    'ปรุงรสด้วยน้ำปลา น้ำมันหอย',
                    'ตักเสิร์ฟร้อนๆ'
                ].filter(Boolean),
                healthWarnings: healthCheck.warnings,
                isDangerous: healthCheck.isDangerous
            };
        }

        // ยำ (รสจัด)
        function createYum(proteins, vegetables, herbs, spices, allIngredients, userConditions) {
            const mainProtein = proteins[0];
            const lime = spices.find(s => s.name === 'มะนาว');
            
            const usedIngredients = [mainProtein, lime];
            const usedSeasonings = [basicSeasonings.fishSauce, basicSeasonings.sugar];
            
            if (spices.some(s => s.name.includes('พริก'))) {
                usedIngredients.push(spices.find(s => s.name.includes('พริก')));
            }
            if (spices.some(s => s.name === 'กระเทียม')) {
                usedIngredients.push(spices.find(s => s.name === 'กระเทียม'));
            }
            if (vegetables.length > 0) {
                vegetables.forEach(v => usedIngredients.push(v));
            }
            if (herbs.length > 0) {
                herbs.forEach(h => usedIngredients.push(h));
            }

            const healthCheck = checkHealthWarnings(usedIngredients, usedSeasonings, userConditions);
            const hasChili = spices.some(s => s.name.includes('พริก'));
            
            return {
                name: `ยำ${mainProtein.name} 🌶️`,
                type: 'dry',
                taste: 'strong',
                calories: '150-220',
                price: '50-70',
                time: '15 นาที',
                userIngredients: usedIngredients,
                basicSeasonings: usedSeasonings,
                steps: [
                    `ลวก${mainProtein.name}จนสุก พักให้เย็น`,
                    'ผสมน้ำยำ: น้ำมะนาว น้ำปลา น้ำตาล' + (hasChili ? ' พริกขี้หนูบุบ' : ''),
                    vegetables.length > 0 ? `หั่น${vegetables.map(v => v.name).join(', ')}` : null,
                    `ใส่${mainProtein.name}และผักลงในชาม`,
                    'ราดน้ำยำ คลุกให้เข้ากัน',
                    herbs.length > 0 ? `โรย${herbs.map(h => h.name).join(', ')}` : null
                ].filter(Boolean),
                healthWarnings: healthCheck.warnings,
                isDangerous: healthCheck.isDangerous
            };
        }

        // แกงจืด/ต้มจืด (รสอ่อน)
        function createClearSoup(proteins, vegetables, herbs, spices, allIngredients, userConditions) {
            const mainProtein = proteins[0];
            
            const usedIngredients = [mainProtein];
            const usedSeasonings = [basicSeasonings.soySauce, basicSeasonings.water, basicSeasonings.pepper];
            
            if (vegetables.length > 0) {
                vegetables.forEach(v => usedIngredients.push(v));
            }
            if (spices.some(s => s.name === 'กระเทียม')) {
                usedIngredients.push(spices.find(s => s.name === 'กระเทียม'));
            }
            if (herbs.some(h => h.name === 'ผักชี')) {
                usedIngredients.push(herbs.find(h => h.name === 'ผักชี'));
            }

            const healthCheck = checkHealthWarnings(usedIngredients, usedSeasonings, userConditions);
            const hasGarlic = spices.some(s => s.name === 'กระเทียม');
            
            return {
                name: `แกงจืด${vegetables.length > 0 ? vegetables[0].name : ''}${mainProtein.name} 😊`,
                type: 'soup',
                taste: 'mild',
                calories: '100-150',
                price: '40-60',
                time: '20 นาที',
                userIngredients: usedIngredients,
                basicSeasonings: usedSeasonings,
                steps: [
                    'ต้มน้ำให้เดือด',
                    hasGarlic ? 'ใส่กระเทียมทุบลงไป' : null,
                    `ใส่${mainProtein.name}หั่นชิ้น ต้มจนสุก`,
                    vegetables.length > 0 ? `ใส่${vegetables.map(v => v.name).join(', ')} ต้มจนนิ่ม` : null,
                    'ปรุงรสด้วยซีอิ๊วขาว โรยพริกไทย',
                    herbs.some(h => h.name === 'ผักชี') ? 'โรยผักชี' : null,
                    'ตักเสิร์ฟร้อนๆ'
                ].filter(Boolean),
                healthWarnings: healthCheck.warnings,
                isDangerous: healthCheck.isDangerous
            };
        }

        // นึ่ง (รสอ่อน)
        function createSteamed(proteins, vegetables, herbs, spices, allIngredients, userConditions) {
            const steamableProtein = proteins.find(p => ['ปลา', 'ปลานิล', 'ไก่', 'อกไก่'].includes(p.name)) || proteins[0];
            
            const usedIngredients = [steamableProtein];
            const usedSeasonings = [basicSeasonings.soySauce];
            
            if (herbs.some(h => h.name === 'ขิง')) {
                usedIngredients.push(herbs.find(h => h.name === 'ขิง'));
            }
            if (spices.some(s => s.name === 'กระเทียม')) {
                usedIngredients.push(spices.find(s => s.name === 'กระเทียม'));
            }
            if (vegetables.length > 0) {
                vegetables.slice(0, 2).forEach(v => usedIngredients.push(v));
            }

            const healthCheck = checkHealthWarnings(usedIngredients, usedSeasonings, userConditions);
            const hasGinger = herbs.some(h => h.name === 'ขิง');
            
            return {
                name: `${steamableProtein.name}นึ่ง${hasGinger ? 'ขิง' : 'ซีอิ๊ว'} 😊`,
                type: 'dry',
                taste: 'mild',
                calories: '120-180',
                price: '50-80',
                time: '20 นาที',
                userIngredients: usedIngredients,
                basicSeasonings: usedSeasonings,
                steps: [
                    `วาง${steamableProtein.name}บนจาน`,
                    hasGinger ? 'โรยขิงซอยบนตัว' + steamableProtein.name : 'ราดซีอิ๊วขาวเล็กน้อย',
                    vegetables.length > 0 ? `วาง${vegetables.map(v => v.name).join(', ')}รอบๆ` : null,
                    'นำไปนึ่งไฟแรง 15-20 นาที จนสุก',
                    'ตักเสิร์ฟร้อนๆ'
                ].filter(Boolean),
                healthWarnings: healthCheck.warnings,
                isDangerous: healthCheck.isDangerous
            };
        }

        // ไข่เจียว (รสอ่อน)
        function createOmelette(proteins, vegetables, herbs, spices, allIngredients, userConditions) {
            const egg = proteins.find(p => p.name.includes('ไข่'));
            
            const usedIngredients = [egg];
            const usedSeasonings = [basicSeasonings.oil, basicSeasonings.fishSauce];
            
            // เพิ่มผักถ้ามี
            if (vegetables.length > 0) {
                vegetables.forEach(v => usedIngredients.push(v));
            }

            const healthCheck = checkHealthWarnings(usedIngredients, usedSeasonings, userConditions);
            const hasVeg = vegetables.length > 0;
            
            return {
                name: `ไข่เจียว${hasVeg ? `ใส่${vegetables.map(v => v.name).join(', ')}` : 'ฟู'} 😊`,
                type: 'dry',
                taste: 'mild',
                calories: '150-220',
                price: '25-40',
                time: '5 นาที',
                userIngredients: usedIngredients,
                basicSeasonings: usedSeasonings,
                steps: [
                    'ตอกไข่ใส่ชาม เติมน้ำปลาเล็กน้อย',
                    hasVeg ? `ใส่${vegetables.map(v => v.name).join(', ')}สับละเอียด` : null,
                    'ตีไข่ให้เข้ากัน',
                    'ตั้งกระทะใส่น้ำมันให้ร้อนจัด',
                    'เทไข่ลงทอด รอจนเหลืองกรอบด้านล่าง',
                    'พลิกกลับ ทอดต่อจนสุก'
                ].filter(Boolean),
                healthWarnings: healthCheck.warnings,
                isDangerous: healthCheck.isDangerous
            };
        }

        // ผัดผักเจ (รสอ่อน)
        function createVegStirFry(vegetables, herbs, spices, allIngredients, userConditions) {
            const usedIngredients = [...vegetables];
            const usedSeasonings = [basicSeasonings.oil, basicSeasonings.soySauce];
            
            if (spices.some(s => s.name === 'กระเทียม')) {
                usedIngredients.push(spices.find(s => s.name === 'กระเทียม'));
            }

            const healthCheck = checkHealthWarnings(usedIngredients, usedSeasonings, userConditions);
            
            return {
                name: `ผัด${vegetables.map(v => v.name).join('')} 😊`,
                type: 'dry',
                taste: 'mild',
                calories: '80-120',
                price: '30-45',
                time: '10 นาที',
                userIngredients: usedIngredients,
                basicSeasonings: usedSeasonings,
                steps: [
                    spices.some(s => s.name === 'กระเทียม') ? 'เจียวกระเทียมกับน้ำมันให้หอม' : 'ตั้งกระทะใส่น้ำมันให้ร้อน',
                    `ใส่${vegetables.map(v => v.name).join(', ')} ลงผัด`,
                    'เติมน้ำเล็กน้อยถ้าแห้งเกินไป',
                    'ปรุงรสด้วยซีอิ๊วขาว',
                    'ผัดจนผักสุก ตักเสิร์ฟ'
                ],
                healthWarnings: healthCheck.warnings,
                isDangerous: healthCheck.isDangerous
            };
        }

        // ผัดขิง (รสอ่อน)
        function createPadKhing(proteins, vegetables, herbs, spices, allIngredients, userConditions) {
            const mainProtein = proteins[0];
            const ginger = herbs.find(h => h.name === 'ขิง');
            
            const usedIngredients = [mainProtein, ginger];
            const usedSeasonings = [basicSeasonings.oil, basicSeasonings.soySauce, basicSeasonings.oysterSauce];
            
            if (vegetables.length > 0) {
                vegetables.forEach(v => usedIngredients.push(v));
            }
            if (spices.some(s => s.name === 'กระเทียม')) {
                usedIngredients.push(spices.find(s => s.name === 'กระเทียม'));
            }

            const healthCheck = checkHealthWarnings(usedIngredients, usedSeasonings, userConditions);
            
            return {
                name: `${mainProtein.name}ผัดขิง 😊`,
                type: 'dry',
                taste: 'mild',
                calories: '200-280',
                price: '50-70',
                time: '15 นาที',
                userIngredients: usedIngredients,
                basicSeasonings: usedSeasonings,
                steps: [
                    'หั่นขิงเป็นเส้นฝอย',
                    spices.some(s => s.name === 'กระเทียม') ? 'เจียวกระเทียมกับน้ำมันให้หอม' : 'ตั้งกระทะใส่น้ำมันให้ร้อน',
                    `ใส่${mainProtein.name}หั่นชิ้น ผัดจนเกือบสุก`,
                    'ใส่ขิงซอย ผัดให้หอม',
                    vegetables.length > 0 ? `ใส่${vegetables.map(v => v.name).join(', ')} ผัดต่อ` : null,
                    'ปรุงรสด้วยซีอิ๊วขาว น้ำมันหอย',
                    'ตักเสิร์ฟร้อนๆ'
                ].filter(Boolean),
                healthWarnings: healthCheck.warnings,
                isDangerous: healthCheck.isDangerous
            };
        }

        // ผัดเส้น (รสอ่อน)
        function createPadNoodle(proteins, vegetables, carbs, herbs, spices, allIngredients, userConditions) {
            const mainCarb = carbs[0];
            
            const usedIngredients = [mainCarb];
            const usedSeasonings = [basicSeasonings.oil, basicSeasonings.soySauce];
            
            if (proteins.length > 0) {
                usedIngredients.push(proteins[0]);
            }
            if (vegetables.length > 0) {
                vegetables.forEach(v => usedIngredients.push(v));
            }
            if (spices.some(s => s.name === 'กระเทียม')) {
                usedIngredients.push(spices.find(s => s.name === 'กระเทียม'));
            }

            const healthCheck = checkHealthWarnings(usedIngredients, usedSeasonings, userConditions);
            
            return {
                name: `ผัด${mainCarb.name}${proteins.length > 0 ? proteins[0].name : ''} 😊`,
                type: 'dry',
                taste: 'mild',
                calories: '300-400',
                price: '40-60',
                time: '15 นาที',
                userIngredients: usedIngredients,
                basicSeasonings: usedSeasonings,
                steps: [
                    `แช่${mainCarb.name}ในน้ำจนนิ่ม`,
                    spices.some(s => s.name === 'กระเทียม') ? 'เจียวกระเทียมกับน้ำมันให้หอม' : 'ตั้งกระทะใส่น้ำมันให้ร้อน',
                    proteins.length > 0 ? `ใส่${proteins[0].name} ผัดจนสุก` : null,
                    `ใส่${mainCarb.name} ผัดต่อ`,
                    vegetables.length > 0 ? `ใส่${vegetables.map(v => v.name).join(', ')} ผัดรวม` : null,
                    'ปรุงรสด้วยซีอิ๊วขาว',
                    'ตักเสิร์ฟร้อนๆ'
                ].filter(Boolean),
                healthWarnings: healthCheck.warnings,
                isDangerous: healthCheck.isDangerous
            };
        }

        // โปรตีนอย่างเดียว ทอด/ย่าง (รสอ่อน)
        function createSimpleProtein(proteins, spices, allIngredients, userConditions) {
            const mainProtein = proteins[0];
            
            const usedIngredients = [mainProtein];
            const usedSeasonings = [basicSeasonings.oil, basicSeasonings.salt, basicSeasonings.pepper];
            
            if (spices.some(s => s.name === 'กระเทียม')) {
                usedIngredients.push(spices.find(s => s.name === 'กระเทียม'));
            }

            const healthCheck = checkHealthWarnings(usedIngredients, usedSeasonings, userConditions);
            
            return {
                name: `${mainProtein.name}ทอดกระเทียมพริกไทย 😊`,
                type: 'dry',
                taste: 'mild',
                calories: '200-300',
                price: '40-60',
                time: '15 นาที',
                userIngredients: usedIngredients,
                basicSeasonings: usedSeasonings,
                steps: [
                    `หั่น${mainProtein.name}เป็นชิ้นพอคำ`,
                    'หมักกับเกลือ พริกไทย 10 นาที',
                    'ตั้งกระทะใส่น้ำมันให้ร้อน',
                    spices.some(s => s.name === 'กระเทียม') ? 'ใส่กระเทียมสับเจียวให้หอม' : null,
                    `ใส่${mainProtein.name}ลงทอดจนเหลืองกรอบ`,
                    'ตักขึ้นพักให้สะเด็ดน้ำมัน'
                ].filter(Boolean),
                healthWarnings: healthCheck.warnings,
                isDangerous: healthCheck.isDangerous
            };
        }

        // ===== ฟังก์ชันสร้างการ์ดเมนู =====
        function createMenuCard(data, userConditions) {
            const typeText = data.type === 'soup' ? '🍲 อาหารประเภทน้ำ' : '🍳 อาหารประเภทแห้ง';
            const tasteText = data.taste === 'mild' ? '😊 รสอ่อน เหมาะทุกวัย' : '🌶️ รสจัด';
            const tasteClass = data.taste === 'mild' ? 'taste-mild' : 'taste-strong';
            
            // เช็คว่าเมนูนี้อันตรายต่อโรคที่เลือกหรือไม่
            const hasDanger = Object.entries(data.isDangerous).some(([key, val]) => val && userConditions[key]);
            const cardClass = hasDanger ? 'not-recommended' : data.type;

            // สร้างรายการวัตถุดิบ
            let ingredientsHtml = '<h4>🥕 วัตถุดิบที่ใช้ (จากที่คุณกรอก)</h4><ul>';
            data.userIngredients.forEach(ing => {
                ingredientsHtml += `<li class="user-ingredient">${ing.name}</li>`;
            });
            ingredientsHtml += '</ul>';

            ingredientsHtml += '<h4>🧂 เครื่องปรุงพื้นฐาน (ที่ทุกครัวควรมี)</h4><ul>';
            data.basicSeasonings.forEach(s => {
                ingredientsHtml += `<li class="basic-ingredient">${s.name} - ${s.amount}</li>`;
            });
            ingredientsHtml += '</ul>';

            // สร้างคำเตือนสุขภาพ
            let warningsHtml = '';
            const warningClass = hasDanger ? 'warning-danger' : '';
            
            if (data.healthWarnings.length > 0) {
                warningsHtml = `
                    <div class="menu-warnings ${warningClass}">
                        <h4>${hasDanger ? '🚫 ข้อควรระวังสำคัญ!' : '⚠️ คำแนะนำเพื่อสุขภาพ'}</h4>
                        <ul>
                            ${data.healthWarnings.map(w => `<li>${w}</li>`).join('')}
                        </ul>
                    </div>
                `;
            } else if (Object.values(userConditions).some(v => v)) {
                warningsHtml = `
                    <div class="menu-warnings">
                        <h4>✅ เมนูนี้ปลอดภัย</h4>
                        <ul>
                            <li>วัตถุดิบที่ใช้ไม่มีข้อห้ามสำหรับโรคที่คุณเลือก</li>
                            <li>อย่างไรก็ตาม ควรปรุงรสอ่อนๆ และทานในปริมาณพอเหมาะ</li>
                        </ul>
                    </div>
                `;
            }

            return `
                <div class="menu-card ${cardClass}">
                    <div class="menu-card-header">
                        ${hasDanger ? '⚠️ เมนูนี้มีข้อควรระวัง' : typeText}
                    </div>
                    <div class="menu-card-body">
                        <div class="menu-name">
                            ${data.name}
                            <span class="calories-badge">🔥 ${data.calories} แคลอรี่</span>
                        </div>
                        <div class="taste-indicator ${tasteClass}">${tasteText}</div>
                        <div class="price-estimate">💰 งบประมาณ: ${data.price} บาท | ⏱️ เวลา: ${data.time}</div>
                        
                        <div class="menu-ingredients">
                            ${ingredientsHtml}
                        </div>
                        
                        <div class="cooking-method">
                            <h4>👩‍🍳 ขั้นตอนการทำ</h4>
                            <ol>
                                ${data.steps.map(step => `<li>${step}</li>`).join('')}
                            </ol>
                        </div>

                        ${warningsHtml}

                        <div class="nutrition-info">
                            <div class="nutrition-item">
                                <div class="label">โปรตีน</div>
                                <div class="value">15-25 g</div>
                            </div>
                            <div class="nutrition-item">
                                <div class="label">ไขมัน</div>
                                <div class="value">5-15 g</div>
                            </div>
                            <div class="nutrition-item">
                                <div class="label">คาร์โบไฮเดรต</div>
                                <div class="value">5-20 g</div>
                            </div>
                        </div>
                    </div>
                </div>
            `;
        }
    </script>
</body>
</html>
