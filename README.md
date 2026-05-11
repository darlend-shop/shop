<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>DARLEND — Магазин доната</title>
    <style>
        body { background: #0f0f1b; font-family: 'Segoe UI', sans-serif; color: white; text-align: center; margin: 0; padding-bottom: 50px; }
        .hero { padding: 40px 20px; background: linear-gradient(180deg, #1a1a2e 0%, #0f0f1b 100%); border-bottom: 2px solid #3f37c9; }
        .brand { font-size: 42px; font-weight: 900; letter-spacing: 3px; color: #4cc9f0; margin: 0; }
        .about { max-width: 600px; margin: 20px auto; padding: 15px; background: rgba(255,255,255,0.05); border-radius: 15px; font-size: 14px; line-height: 1.5; text-align: left; }
        .shop-container { display: flex; flex-wrap: wrap; justify-content: center; gap: 20px; padding: 20px; }
        .card { background: #1b1b2f; border-radius: 20px; width: 280px; padding: 20px; border: 1px solid #333; transition: 0.3s; }
        .card:hover { border-color: #4cc9f0; transform: translateY(-5px); }
        .price { font-size: 28px; font-weight: bold; color: #4cc9f0; margin: 10px 0; }
        input { width: 100%; padding: 12px; margin: 10px 0; border-radius: 10px; border: 1px solid #444; background: #050510; color: white; box-sizing: border-box; }
        .btn-buy { background: #f72585; color: white; border: none; padding: 15px; width: 100%; border-radius: 12px; font-weight: bold; cursor: pointer; text-transform: uppercase; font-size: 16px; }
        
        /* Стили окна оплаты */
        #paymentModal { display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.9); z-index: 100; justify-content: center; align-items: center; }
        .pay-box { background: #1b1b2f; padding: 30px; border-radius: 25px; max-width: 350px; border: 2px solid #4cc9f0; }
        .card-num { background: #000; padding: 15px; border-radius: 10px; font-size: 18px; color: #00ffcc; margin: 15px 0; border: 1px dashed #f72585; cursor: pointer; }
    </style>
</head>
<body>

    <div class="hero">
        <h1 class="brand">DARLEND</h1>
        <p>Донат в игры • Быстро • Честно</p>
    </div>

    <div class="about">
        <b>DARLEND</b> — твой сервис пополнения игр. <br><br>
        🚀 <b>Скорость:</b> от 5 до 15 минут. <br>
        🛡️ <b>Безопасность:</b> Работаем официально. <br>
        💰 <b>Выгода:</b> Цены ниже игровых магазинов.
    </div>

    <div class="shop-container">
        <div class="card">
            <h3>Brawl Stars</h3>
            <p>Гемы / Бравл Пасс</p>
            <div class="price">от 199₽</div>
            <input type="text" id="bs_data" placeholder="Почта Supercell ID">
            <button class="btn-buy" onclick="openPay('Brawl Stars', document.getElementById('bs_data').value)">Купить</button>
        </div>

        <div class="card">
            <h3>PUBG Mobile</h3>
            <p>UC пополнение</p>
            <div class="price">от 149₽</div>
            <input type="text" id="pubg_data" placeholder="Ваш UID">
            <button class="btn-buy" onclick="openPay('PUBG Mobile', document.getElementById('pubg_data').value)">Купить</button>
        </div>
    </div>

    <!-- Модальное окно оплаты -->
    <div id="paymentModal">
        <div class="pay-box">
            <h3>Оплата заказа</h3>
            <p>Переведите сумму на карту <b>Ozon Банк</b>:</p>
            <div class="card-num" onclick="copyCard()" id="myCard">2204 3211 4831 8157</div>
            <p style="font-size: 12px; color: #aaa;">Нажмите на номер, чтобы скопировать</p>
            <button class="btn-buy" style="background: #4cc9f0; color: #000;" onclick="confirmPay()">Я ОПЛАТИЛ(А)</button>
            <button onclick="document.getElementById('paymentModal').style.display='none'" style="background:none; border:none; color:white; margin-top:15px; cursor:pointer;">Отмена</button>
        </div>
    </div>

    <script>
        let currentOrder = { game: '', info: '' };

        function openPay(game, info) {
            if(!info) { alert('Введите данные (UID или почту)!'); return; }
            currentOrder.game = game;
            currentOrder.info = info;
            document.getElementById('paymentModal').style.display = 'flex';
        }

        function copyCard() {
            navigator.clipboard.writeText("2204321148318157");
            alert('Номер карты скопирован!');
        }

        function confirmPay() {
            let msg = `Привет, DARLEND! Я оплатил заказ.\nИгра: ${currentOrder.game}\nДанные: ${currentOrder.info}`;
            window.location.href = `https://t.me{encodeURIComponent(msg)}`;
        }
    </script>
</body>
</html>
