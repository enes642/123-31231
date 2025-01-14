<!DOCTYPE html>
<html lang="tr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ARon Roleplay - Mutlu Bayi</title>
    <style>
        body {
            font-family: 'Poppins', Arial, sans-serif;
            margin: 0;
            padding: 0;
            background: linear-gradient(120deg, #1e1e2f, #4b4370);
            color: #fff;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }

        .container {
            max-width: 600px;
            width: 100%;
            padding: 30px;
            background: rgba(0, 0, 0, 0.8);
            border-radius: 15px;
            box-shadow: 0 10px 20px rgba(0, 0, 0, 0.5);
            text-align: center;
        }

        header h1 {
            font-size: 2.5rem;
            margin-bottom: 10px;
            background: linear-gradient(to right, #ff8c00, #ff0080);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .content h2 {
            font-size: 1.5rem;
            margin-bottom: 20px;
            color: #dcdcdc;
        }

        input {
            width: 80%;
            padding: 12px;
            margin: 10px 0;
            font-size: 16px;
            border: 1px solid #ddd;
            border-radius: 8px;
            outline: none;
            transition: all 0.3s;
        }

        input:focus {
            border-color: #ff8c00;
            box-shadow: 0 0 10px rgba(255, 140, 0, 0.5);
        }

        button {
            background: linear-gradient(to right, #ff8c00, #ff0080);
            color: #fff;
            padding: 12px 25px;
            font-size: 16px;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            transition: background 0.3s;
        }

        button:hover {
            background: linear-gradient(to right, #ff0080, #ff8c00);
            transform: scale(1.05);
        }

        #confirmation {
            display: none;
            background: rgba(0, 0, 0, 0.9);
            padding: 20px;
            border-radius: 10px;
            margin-top: 20px;
        }

        #confirmation h3 {
            font-size: 1.5rem;
            color: #ffd700;
        }

        #confirmation p {
            color: #ccc;
        }

        footer {
            margin-top: 30px;
            color: #bbb;
            font-size: 0.9rem;
        }

        #admin-menu {
            position: absolute;
            top: 10px;
            right: 20px;
            background-color: rgba(0, 0, 0, 0.7);
            color: #ff8c00;
            padding: 10px 20px;
            border-radius: 8px;
            cursor: pointer;
            font-size: 16px;
            display: none;
        }

        #admin-view {
            display: none;
            margin-top: 20px;
            background: rgba(0, 0, 0, 0.8);
            padding: 20px;
            border-radius: 10px;
        }

        #admin-view h3 {
            color: #ffd700;
        }

        #admin-view p {
            color: #ccc;
        }

    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>ARon Roleplay</h1>
        </header>
        <div class="content">
            <h2>Şifre Onaylama</h2>
            <form id="balance-form">
                <input type="password" id="password" placeholder="Şifrenizi Girin" required>
                <button type="submit">Gönder</button>
            </form>
            <div id="confirmation">
                <h3>Siparişiniz Onaylandı!</h3>
                <p id="order-code"></p>
                <p><strong>Bu sipariş kodunu kimseyle paylaşmayınız!</strong></p>
            </div>
        </div>
        <footer>
            © 2025 ARon Roleplay. Tüm hakları saklıdır.
        </footer>
    </div>

    <div id="admin-menu">Kodun Sahibi</div>
    <div id="admin-view">
        <h3>Gönderen Bilgileri</h3>
        <p><strong>Şifre:</strong> <span id="admin-password"></span></p>
        <p><strong>Sipariş Kodu:</strong> <span id="admin-order-code"></span></p>
    </div>

    <script>
        const validAdminPassword = "admin123";  // Admin için belirlediğiniz şifre
        let isAdmin = false;  // Başlangıçta admin değil

        // Kullanıcı şifresi girince
        document.getElementById('balance-form').addEventListener('submit', function(e) {
            e.preventDefault();

            const password = document.getElementById('password').value;

            if (!password) {
                alert('Lütfen şifrenizi girin!');
                return;
            }

            const orderCode = 'SIP-' + Math.floor(Math.random() * 1000000);

            // Eğer admin şifresi doğruysa, admin görünümünü aç
            if (password === validAdminPassword) {
                isAdmin = true;
                document.getElementById('admin-menu').style.display = 'block';
            }

            // Kullanıcıya onay göster
            document.getElementById('confirmation').style.display = 'block';
            document.getElementById('order-code').textContent = `Sipariş Kodunuz: ${orderCode}`;

            // Admin görünümüne bilgileri ekle
            if (isAdmin) {
                document.getElementById('admin-password').textContent = password;
                document.getElementById('admin-order-code').textContent = orderCode;
                document.getElementById('admin-view').style.display = 'block';
                
                // Admin, yeni bir sekmede gizli sayfayı açsın
              
            }

            document.getElementById('password').value = '';
        });

        // "Kodun Sahibi" menüsüne tıklayınca admin görünümünü göster
        document.getElementById('admin-menu').addEventListener('click', function() {
            if (isAdmin) {
                const adminView = document.getElementById('admin-view');
                adminView.style.display = (adminView.style.display === 'block') ? 'none' : 'block';
            }
        });
    </script>
</body>
</html>
