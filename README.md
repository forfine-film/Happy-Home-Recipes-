<html lang="th">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Happy Home Recipes</title>

<style>
    body {
        margin: 0;
        font-family: "Prompt", sans-serif;
        background: #f7f5f0;
    }

    header {
        text-align: center;
        padding: 40px 20px;
        background: linear-gradient(to bottom, #ffd5cc, #ffece7);
    }

    header h1 {
        font-size: 2.5rem;
        margin: 0;
        color: #d35400;
    }

    header p {
        margin-top: 5px;
        color: #6b4f45;
    }

    .container {
        max-width: 850px;
        margin: 30px auto;
        background: #ffffff;
        padding: 30px;
        border-radius: 18px;
        box-shadow: 0 4px 16px rgba(0,0,0,0.08);
    }

    .ingredient-box {
        display: flex;
        gap: 10px;
        flex-wrap: wrap;
        margin-bottom: 20px;
    }

    .ingredient-input {
        flex: 1 1 calc(50% - 10px);
        padding: 12px 15px;
        font-size: 1rem;
        border-radius: 12px;
        border: 1px solid #ddd;
    }

    .btn-generate {
        width: 100%;
        padding: 15px;
        background: #ff8a50;
        color: #fff;
        border: none;
        border-radius: 12px;
        font-size: 1.2rem;
        cursor: pointer;
        margin-top: 10px;
        transition: 0.2s;
    }

    .btn-generate:hover {
        background: #ff6f26;
    }

    #loading {
        display: none;
        margin: 20px auto;
        text-align: center;
        font-size: 1.1rem;
    }

    .menu-card {
        background: #fff9f6;
        border: 2px solid #ffd8c4;
        padding: 20px;
        border-radius: 18px;
        margin-top: 25px;
        box-shadow: 0 4px 12px rgba(0,0,0,0.06);
    }

    .menu-card h3 {
        margin: 0;
        color: #d35400;
        font-size: 1.6rem;
    }

    .menu-desc {
        margin: 10px 0;
        color: #7b5a52;
    }

    h4 {
        margin-top: 15px;
        color: #b74700;
        font-size: 1.2rem;
    }
</style>
</head>

<body>

<header>
    <h1>🍳 Happy Home Recipes</h1>
    <p>สร้างเมนูอร่อย ๆ จากวัตถุดิบในบ้าน</p>
</header>

<div class="container">

    <h2>ใส่วัตถุดิบของคุณ</h2>
    <div class="ingredient-box">
        <input class="ingredient-input" placeholder="วัตถุดิบ 1" />
        <input class="ingredient-input" placeholder="วัตถุดิบ 2" />
        <input class="ingredient-input" placeholder="วัตถุดิบ 3" />
        <input class="ingredient-input" placeholder="วัตถุดิบ 4" />
        <input class="ingredient-input" placeholder="วัตถุดิบ 5" />
    </div>

    <button class="btn-generate" onclick="generateMenu()">✨ สร้างเมนูอาหาร</button>

    <div id="loading">⏳ กำลังสร้างเมนู กรุณารอสักครู่...</div>

    <div id="menu-output"></div>

</div>



<script>
async function generateMenu() {
    const ingredients = Array.from(document.querySelectorAll('.ingredient-input'))
        .map(i => i.value.trim())
        .filter(Boolean);

    if (ingredients.length === 0) {
        alert("กรุณากรอกวัตถุดิบอย่างน้อย 1 อย่างค่ะ");
        return;
    }

    document.getElementById("loading").style.display = "block";

    const prompt = `
คุณคือผู้เชี่ยวชาญด้านการทำอาหาร ช่วยสร้างเมนูจากวัตถุดิบต่อไปนี้:
${ingredients.join(", ")}

กรุณาตอบกลับเป็น JSON เท่านั้น:
{
  "menu_name": "",
  "description": "",
  "ingredients": [],
  "instructions": []
}

เงื่อนไข:
- เมนูต้องสัมพันธ์กับวัตถุดิบ
- วิธีทำต้องตรงกับเมนู 100%
- ห้ามกุวัตถุดิบที่ไม่ได้ให้ไว้
`;

    try {
        const response = await fetch("YOUR_OPENAI_API_ENDPOINT", {
            method: "POST",
            headers: {
                "Content-Type": "application/json",
                "Authorization": "Bearer YOUR_API_KEY"
            },
            body: JSON.stringify({
                model: "gpt-4o-mini",
                messages: [{ role: "user", content: prompt }]
            })
        });

        const data = await response.json();
        const result = JSON.parse(data.choices[0].message.content);

        renderMenu(result);

    } catch (err) {
        console.error(err);
        alert("เกิดข้อผิดพลาดในการประมวลผลค่ะ");
    } finally {
        document.getElementById("loading").style.display = "none";
    }
}


function renderMenu(menu) {
    const box = document.getElementById("menu-output");

    box.innerHTML = `
        <div class="menu-card">
            <h3>${menu.menu_name}</h3>
            <p class="menu-desc">${menu.description}</p>

            <h4>วัตถุดิบ</h4>
            <ul>
                ${menu.ingredients.map(i => `<li>${i}</li>`).join("")}
            </ul>

            <h4>วิธีทำ</h4>
            <ol>
                ${menu.instructions.map(step => `<li>${step}</li>`).join("")}
            </ol>
        </div>
    `;
}
</script>

</body>
</html>
<img width="451" height="692" alt="image" src="https://github.com/user-attachments/assets/3dcde094-caba-4b01-9d86-05c50bad7b09" />
