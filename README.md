<!DOCTYPE html>
<html lang="tr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>VOLTERX // Official Store</title>
    
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;500;600;700;800&display=swap" rel="stylesheet">

    <style>
        :root {
            --bg-main: #ffffff;
            --bg-secondary: #f7f7f8;
            --bg-card: #ffffff;
            --text-main: #000000;
            --text-muted: #666666;
            --border-color: #e5e5e7;
            --border-dark: #000000;
            --radius-sm: 8px;
            --radius-md: 14px;
            --radius-lg: 20px;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Plus Jakarta Sans', -apple-system, BlinkMacSystemFont, sans-serif;
            -webkit-tap-highlight-color: transparent;
        }

        body {
            background-color: var(--bg-main);
            color: var(--text-main);
            line-height: 1.5;
            padding-bottom: 90px;
            max-width: 480px;
            margin: 0 auto;
            border-left: 1px solid #f0f0f0;
            border-right: 1px solid #f0f0f0;
            min-height: 100vh;
        }

        #splash-screen {
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            background-color: #000000;
            display: flex; flex-direction: column; align-items: center; justify-content: center;
            z-index: 9999;
            transition: opacity 0.6s ease, visibility 0.6s ease;
        }

        #splash-screen.fade-out {
            opacity: 0; visibility: hidden;
        }

        .splash-logo {
            font-size: 32px; font-weight: 800; letter-spacing: 4px; color: #ffffff;
            opacity: 0; transform: translateY(20px);
            animation: logoAppear 1s forwards ease-out 0.2s;
        }

        .splash-sub {
            font-size: 10px; letter-spacing: 3px; color: #888888; margin-top: 8px; text-transform: uppercase;
            opacity: 0; animation: logoAppear 1s forwards ease-out 0.5s;
        }

        .splash-loader {
            width: 36px; height: 2px; background: rgba(255,255,255,0.2); margin-top: 24px; position: relative; overflow: hidden; border-radius: 2px;
        }

        .splash-loader::after {
            content: ''; position: absolute; top: 0; left: -100%; width: 100%; height: 100%;
            background: #ffffff; animation: loadingBar 1.5s infinite ease-in-out;
        }

        @keyframes logoAppear { to { opacity: 1; transform: translateY(0); } }
        @keyframes loadingBar { 0% { left: -100%; } 50% { left: 0%; } 100% { left: 100%; } }

        .toast {
            position: fixed; top: 20px; left: 50%;
            transform: translateX(-50%) translateY(-100px);
            background: #000000; color: #ffffff;
            padding: 12px 20px; border-radius: var(--radius-md);
            font-size: 12px; font-weight: 700; z-index: 300;
            transition: transform 0.3s ease; box-shadow: 0 10px 25px rgba(0,0,0,0.15);
            text-align: center; width: calc(100% - 40px); max-width: 440px;
        }
        .toast.show { transform: translateX(-50%) translateY(0); }

        .top-announcement {
            background-color: #000000; color: #ffffff; font-size: 10px; font-weight: 700; letter-spacing: 1.5px; text-transform: uppercase; padding: 6px 0; overflow: hidden; white-space: nowrap;
        }
        .marquee-track { display: inline-block; animation: marquee 18s linear infinite; }
        @keyframes marquee { 0% { transform: translateX(0%); } 100% { transform: translateX(-50%); } }

        header {
            position: sticky; top: 0; background: rgba(255, 255, 255, 0.92); backdrop-filter: blur(12px); -webkit-backdrop-filter: blur(12px); z-index: 90; display: flex; align-items: center; justify-content: space-between; padding: 14px 20px; border-bottom: 1px solid var(--border-color);
        }
        .brand-logo { font-size: 20px; font-weight: 800; letter-spacing: -0.8px; color: var(--text-main); text-decoration: none; display: flex; align-items: center; gap: 4px; }
        .brand-logo span { display: inline-block; width: 6px; height: 6px; background-color: #000000; border-radius: 50%; }

        .header-actions { display: flex; align-items: center; gap: 10px; }
        .header-btn { background: var(--bg-secondary); border: 1px solid var(--border-color); color: var(--text-main); width: 38px; height: 38px; border-radius: 50%; display: flex; align-items: center; justify-content: center; cursor: pointer; position: relative; }
        .cart-badge { position: absolute; top: -2px; right: -2px; background: #000000; color: #ffffff; font-size: 9px; font-weight: 800; width: 17px; height: 17px; border-radius: 50%; display: flex; align-items: center; justify-content: center; border: 2px solid #ffffff; }

        .user-status-bar { background: var(--bg-secondary); padding: 8px 20px; font-size: 11px; font-weight: 700; display: flex; align-items: center; justify-content: space-between; border-bottom: 1px solid var(--border-color); }
        .user-status-actions { display: flex; gap: 10px; }
        .user-status-bar .status-link { cursor: pointer; text-decoration: underline; }
        .user-status-bar .logout-link { color: #ff0000; }

        .search-container { padding: 12px 20px; background: var(--bg-main); }
        .search-box { display: flex; align-items: center; background: var(--bg-secondary); border: 1px solid var(--border-color); border-radius: var(--radius-md); padding: 10px 14px; gap: 10px; }
        .search-box input { border: none; background: transparent; width: 100%; font-size: 13px; font-weight: 500; color: var(--text-main); outline: none; }

        .category-scroll { display: flex; gap: 8px; overflow-x: auto; padding: 0 20px 14px 20px; scrollbar-width: none; }
        .category-scroll::-webkit-scrollbar { display: none; }
        .chip { white-space: nowrap; padding: 8px 16px; background: var(--bg-secondary); border: 1px solid var(--border-color); border-radius: 20px; font-size: 12px; font-weight: 600; color: var(--text-main); cursor: pointer; }
        .chip.active { background: #000000; color: #ffffff; border-color: #000000; }

        .hero-card { margin: 0 20px 24px 20px; background: var(--bg-secondary); border: 1px solid var(--border-color); border-radius: var(--radius-lg); padding: 24px 20px; }
        .hero-tag { display: inline-block; font-size: 10px; font-weight: 800; letter-spacing: 1px; text-transform: uppercase; background: #000000; color: #ffffff; padding: 3px 8px; border-radius: 4px; margin-bottom: 12px; }
        .hero-title { font-size: 24px; font-weight: 800; line-height: 1.2; letter-spacing: -0.5px; margin-bottom: 8px; }
        .hero-subtitle { font-size: 13px; color: var(--text-muted); margin-bottom: 18px; }
        .hero-btn { display: inline-flex; background: #000000; color: #ffffff; font-size: 12px; font-weight: 700; padding: 12px 20px; border-radius: var(--radius-md); border: none; cursor: pointer; }

        .section-header { display: flex; align-items: center; justify-content: space-between; padding: 0 20px 14px 20px; }
        .section-title { font-size: 16px; font-weight: 800; }

        .product-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 14px; padding: 0 20px; margin-bottom: 30px; }
        .product-card { background: var(--bg-card); border: 1px solid var(--border-color); border-radius: var(--radius-md); padding: 12px; display: flex; flex-direction: column; }
        .product-card.out-of-stock { opacity: 0.7; }

        .product-thumb-wrapper { position: relative; width: 100%; height: 160px; border-radius: var(--radius-sm); overflow: hidden; margin-bottom: 8px; background: var(--bg-secondary); }
        .product-thumb { width: 100%; height: 100%; background-size: cover; background-position: center; transition: background-image 0.2s ease; cursor: pointer; }
        .slider-btn { position: absolute; top: 50%; transform: translateY(-50%); background: rgba(255,255,255,0.85); border: none; width: 24px; height: 24px; border-radius: 50%; display: flex; align-items: center; justify-content: center; cursor: pointer; font-weight: bold; font-size: 12px; z-index: 5; }
        .slider-btn.prev { left: 4px; }
        .slider-btn.next { right: 4px; }

        .thumb-gallery { display: flex; gap: 4px; margin-bottom: 8px; overflow-x: auto; scrollbar-width: none; }
        .thumb-gallery::-webkit-scrollbar { display: none; }
        .thumb-mini { width: 28px; height: 28px; border-radius: 4px; border: 1px solid var(--border-color); background-size: cover; background-position: center; cursor: pointer; opacity: 0.6; flex-shrink: 0; }
        .thumb-mini.active { border-color: #000; opacity: 1; }

        .product-tag { position: absolute; top: 6px; left: 6px; background: #ffffff; border: 1px solid var(--border-color); color: #000000; font-size: 9px; font-weight: 800; padding: 2px 6px; border-radius: 4px; z-index: 2; }
        .product-tag.out { background: #ff0000; color: #fff; border-color: #ff0000; }
        .product-name { font-size: 13px; font-weight: 700; margin-bottom: 2px; white-space: nowrap; overflow: hidden; text-overflow: ellipsis; }
        .product-stock { font-size: 10px; font-weight: 700; color: #008000; margin-bottom: 4px; }
        .product-stock.no-stock { color: #ff0000; }
        .product-desc { font-size: 11px; color: var(--text-muted); margin-bottom: 8px; display: -webkit-box; -webkit-line-clamp: 1; -webkit-box-orient: vertical; overflow: hidden; }
        .product-footer { display: flex; align-items: center; justify-content: space-between; margin-top: auto; }
        .product-price { font-size: 14px; font-weight: 800; }
        .add-cart-btn { background: var(--text-main); color: #ffffff; border: none; width: 32px; height: 32px; border-radius: 50%; display: flex; align-items: center; justify-content: center; cursor: pointer; }
        .add-cart-btn:disabled { background: #ccc; cursor: not-allowed; }

        .admin-panel { display: none; margin: 0 20px 24px 20px; padding: 18px; background: var(--bg-secondary); border: 2px solid var(--border-dark); border-radius: var(--radius-md); }
        body.is-admin .admin-panel { display: block; }
        .user-log-box { margin-top: 18px; padding-top: 14px; border-top: 1px solid var(--border-color); }
        .user-log-list { max-height: 120px; overflow-y: auto; background: #fff; border: 1px solid var(--border-color); border-radius: var(--radius-sm); padding: 8px; font-size: 11px; }
        .user-log-item { display: flex; justify-content: space-between; padding: 4px 0; border-bottom: 1px dashed #eee; }
        .user-log-item:last-child { border-bottom: none; }

        .modal-backdrop { display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(255, 255, 255, 0.9); backdrop-filter: blur(8px); z-index: 200; align-items: center; justify-content: center; padding: 20px; }
        .modal-card { background: #ffffff; border: 1px solid var(--border-dark); border-radius: var(--radius-lg); width: 100%; max-width: 360px; padding: 24px; box-shadow: 0 20px 40px rgba(0,0,0,0.08); position: relative; }
        .close-btn { position: absolute; top: 16px; right: 16px; font-size: 20px; font-weight: 700; cursor: pointer; color: var(--text-muted); z-index: 10; }

        .auth-tabs { display: flex; border-bottom: 1px solid var(--border-color); margin-bottom: 18px; }
        .auth-tab { flex: 1; padding: 10px 0; text-align: center; font-size: 12px; font-weight: 800; color: var(--text-muted); cursor: pointer; border-bottom: 2px solid transparent; }
        .auth-tab.active { color: var(--text-main); border-bottom-color: var(--text-main); }

        .input-group { margin-bottom: 14px; }
        .input-group label { display: block; font-size: 11px; font-weight: 700; text-transform: uppercase; margin-bottom: 6px; color: var(--text-muted); }
        .input-group input, .input-group textarea { width: 100%; padding: 12px; background: var(--bg-secondary); border: 1px solid var(--border-color); border-radius: var(--radius-md); font-size: 13px; font-weight: 600; outline: none; }

        .btn-full { width: 100%; background: #000000; color: #ffffff; border: none; padding: 14px; border-radius: var(--radius-md); font-size: 13px; font-weight: 700; cursor: pointer; }
        .btn-full:disabled { background: #888; cursor: not-allowed; }

        .cart-drawer { position: fixed; bottom: -100%; left: 0; right: 0; max-width: 480px; margin: 0 auto; background: #ffffff; border-top: 1px solid var(--border-dark); border-radius: 24px 24px 0 0; padding: 24px 20px; z-index: 150; transition: bottom 0.3s ease; box-shadow: 0 -10px 40px rgba(0, 0, 0, 0.1); }
        .cart-drawer.open { bottom: 0; }
        .cart-drawer-header { display: flex; align-items: center; justify-content: space-between; margin-bottom: 18px; padding-bottom: 12px; border-bottom: 1px solid var(--border-color); }
        .cart-items-wrapper { max-height: 220px; overflow-y: auto; margin-bottom: 18px; }
        .cart-item-row { display: flex; align-items: center; justify-content: space-between; padding: 10px 0; border-bottom: 1px solid var(--bg-secondary); }

        .bottom-nav { position: fixed; bottom: 0; left: 0; right: 0; max-width: 480px; margin: 0 auto; background: rgba(255, 255, 255, 0.95); backdrop-filter: blur(10px); border-top: 1px solid var(--border-color); display: flex; justify-content: space-around; padding: 10px 0 14px 0; z-index: 99; }
        .nav-item { display: flex; flex-direction: column; align-items: center; gap: 3px; color: var(--text-muted); font-size: 10px; font-weight: 700; cursor: pointer; }
        .nav-item.active { color: var(--text-main); }
        .nav-item svg { width: 20px; height: 20px; fill: none; stroke: currentColor; stroke-width: 2; }

        .preview-main-img { width: 100%; height: 260px; border-radius: var(--radius-md); background-size: cover; background-position: center; margin-bottom: 12px; }
        .preview-thumbs { display: flex; gap: 8px; overflow-x: auto; padding-bottom: 8px; }
        .preview-thumb-item { width: 50px; height: 50px; border-radius: var(--radius-sm); border: 2px solid transparent; background-size: cover; background-position: center; cursor: pointer; flex-shrink: 0; }
        .preview-thumb-item.active { border-color: #000; }
    </style>
</head>
<body>

    <div id="splash-screen">
        <div class="splash-logo">VOLTERX</div>
        <div class="splash-sub">Official Store</div>
        <div class="splash-loader"></div>
    </div>

    <div id="toast" class="toast"></div>

    <div class="top-announcement">
        <div class="marquee-track">
            VOLTERX // YENİ SEZON KOLEKSİYONU // ANLIK STOK TAKİBİ // VOLTERX //
        </div>
    </div>

    <header>
        <a href="#" class="brand-logo">VOLTERX<span></span></a>
        <div class="header-actions">
            <button class="header-btn" onclick="handleAccountClick()" title="Hesap / Profil">
                <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M20 21v-2a4 4 0 0 0-4-4H8a4 4 0 0 0-4 4v2"></path><circle cx="12" cy="7" r="4"></circle></svg>
            </button>
            <button class="header-btn" onclick="toggleCartDrawer(true)">
                <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M6 2L3 6v14a2 2 0 0 0 2 2h14a2 2 0 0 0 2-2V6l-3-4z"></path><line x1="3" y1="6" x2="21" y2="6"></line><path d="M16 10a4 4 0 0 1-8 0"></path></svg>
                <div class="cart-badge" id="cartBadge">0</div>
            </button>
        </div>
    </header>

    <div class="user-status-bar" id="userStatusBar">
        <span id="userStatusText">Oturum Açılmadı</span>
        <div class="user-status-actions">
            <span id="profileEditBtn" class="status-link" onclick="openProfileModal()" style="display:none;">[ Profil Düzenle ]</span>
            <span id="authActionBtn" class="status-link logout-link" onclick="openAuthModal()">[ Giriş Yap ]</span>
        </div>
    </div>

    <div class="search-container">
        <div class="search-box">
            <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="#999" stroke-width="2"><circle cx="11" cy="11" r="8"></circle><line x1="21" y1="21" x2="16.65" y2="16.65"></line></svg>
            <input type="text" id="searchInput" placeholder="VOLTERX katalogunda ara..." onkeyup="filterProducts()">
        </div>
    </div>

    <div class="category-scroll">
        <div class="chip active" onclick="filterCategory('all', this)">Tümü</div>
        <div class="chip" onclick="filterCategory('apparel', this)">Giyim</div>
        <div class="chip" onclick="filterCategory('tech', this)">Aksesuar</div>
        <div class="chip" onclick="filterCategory('drop', this)">Drop 2026</div>
    </div>

    <div class="hero-card">
        <span class="hero-tag">SÖZLEŞMELİ ÖZEL KOLEKSİYON</span>
        <h1 class="hero-title">VOLTERX</h1>
        <p class="hero-subtitle">Maksimum performans, minimal tasarım. Alışverişe başlamak için giriş yapın.</p>
        <button class="hero-btn" onclick="scrollToProducts()">ÜRÜNLERİ İNCELE</button>
    </div>

    <!-- YÖNETİCİ PANELİ -->
    <div id="adminPanel" class="admin-panel">
        <div style="display:flex; justify-content:space-between; align-items:center; margin-bottom:12px;">
            <h3 style="font-size:13px; font-weight:800; text-transform:uppercase;">[YÖNETİCİ PANELİ] ÜRÜN EKLE</h3>
            <span style="font-size:10px; background:#000; color:#fff; padding:2px 6px; border-radius:4px;">ADMIN</span>
        </div>
        <form id="prodAddForm" onsubmit="handleNewProduct(event)">
            <div class="input-group">
                <label>Ürün Başlığı</label>
                <input type="text" id="newTitle" placeholder="VOLTERX Özel Seri" required>
            </div>
            <div style="display:flex; gap:10px;">
                <div class="input-group" style="flex:1;">
                    <label>Fiyat (TL)</label>
                    <input type="number" id="newPrice" placeholder="1200" required>
                </div>
                <div class="input-group" style="flex:1;">
                    <label>Stok Adedi</label>
                    <input type="number" id="newStock" placeholder="10" required min="0">
                </div>
            </div>
            <div class="input-group">
                <label>Fotoğraf URL'leri (Virgül ile ayırarak birden fazla girin)</label>
                <textarea id="newImages" rows="2" placeholder="https://link1.jpg, https://link2.jpg"></textarea>
            </div>
            <button class="btn-full" type="submit">ÜRÜNÜ YAYINLA</button>
        </form>

        <div class="user-log-box">
            <h4 style="font-size:11px; font-weight:800; margin-bottom:8px; text-transform:uppercase;">Son Giriş Yapan Müşteriler</h4>
            <div class="user-log-list" id="userLogList">
                <div style="color:#888;">Henüz giriş kaydı yok.</div>
            </div>
        </div>
    </div>

    <div class="section-header" id="productsSection">
        <div class="section-title">VOLTERX KATALOG</div>
    </div>

    <div class="product-grid" id="productGrid"></div>

    <!-- ÜRÜN DETAY / GALERİ MODALI -->
    <div class="modal-backdrop" id="productDetailModal">
        <div class="modal-card">
            <span class="close-btn" onclick="closeProductDetailModal()">&times;</span>
            <div id="modalProductDetailContent"></div>
        </div>
    </div>

    <div class="modal-backdrop" id="authModal">
        <div class="modal-card">
            <span class="close-btn" onclick="closeAuthModal()">&times;</span>
            <div class="auth-tabs">
                <div class="auth-tab active" id="tabUser" onclick="switchAuthTab('user')">MÜŞTERİ GİRİŞİ</div>
                <div class="auth-tab" id="tabAdmin" onclick="switchAuthTab('admin')">YÖNETİCİ GİRİŞİ</div>
            </div>

            <div id="formUser">
                <div class="input-group">
                    <label>Kullanıcı Adı veya E-posta</label>
                    <input type="text" id="userUsername" placeholder="kullanici">
                </div>
                <div class="input-group">
                    <label>Şifre</label>
                    <input type="password" id="userPassword" placeholder="••••••••">
                </div>
                <button class="btn-full" onclick="loginUser()">GİRİŞ YAP</button>
            </div>

            <div id="formAdmin" style="display: none;">
                <div class="input-group">
                    <label>Yönetici Kullanıcı Adı</label>
                    <input type="text" id="adminUsername" placeholder="Yönetici Adı">
                </div>
                <div class="input-group">
                    <label>Yönetici Şifresi</label>
                    <input type="password" id="adminPassword" placeholder="••••••••">
                </div>
                <button class="btn-full" onclick="loginAdmin()">YÖNETİCİ GİRİŞİ</button>
            </div>
        </div>
    </div>

    <div class="modal-backdrop" id="profileModal">
        <div class="modal-card">
            <span class="close-btn" onclick="closeProfileModal()">&times;</span>
            <h3 style="font-size:16px; font-weight:800; margin-bottom:16px; text-transform:uppercase;">PROFİL DÜZENLE</h3>
            
            <div class="input-group">
                <label>Ad Soyad / Kullanıcı Adı</label>
                <input type="text" id="profileName" placeholder="Adınız">
            </div>
            <div class="input-group">
                <label>Telefon Numarası</label>
                <input type="tel" id="profilePhone" placeholder="05XXXXXXXXX">
            </div>
            <div class="input-group">
                <label>Teslimat Adresi</label>
                <textarea id="profileAddress" rows="3" placeholder="Açık adresiniz..."></textarea>
            </div>
            <button class="btn-full" onclick="saveProfile()">BİLGİLERİ KAYDET</button>
        </div>
    </div>

    <div class="cart-drawer" id="cartDrawer">
        <div class="cart-drawer-header">
            <h3 style="font-size:16px; font-weight:800;">SEPETİM</h3>
            <span style="cursor:pointer; font-weight:700;" onclick="toggleCartDrawer(false)">&times; Kapat</span>
        </div>
        <div class="cart-items-wrapper" id="cartItemsList"></div>
        <div style="border-top: 1px solid var(--border-color); padding-top: 12px;">
            <div style="display:flex; justify-content:space-between; font-weight:800; font-size:16px; margin-bottom:14px;">
                <span>TOPLAM:</span>
                <span id="cartTotalPrice">0 TL</span>
            </div>
            <button class="btn-full" onclick="checkoutWhatsApp()">WHATSAPP İLE SİPARİŞ ET</button>
        </div>
    </div>

    <div class="bottom-nav">
        <div class="nav-item active" onclick="window.scrollTo({top:0, behavior:'smooth'})">
            <svg viewBox="0 0 24 24"><path d="M3 9l9-7 9 7v11a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2z"></path></svg>
            Anasayfa
        </div>
        <div class="nav-item" onclick="scrollToProducts()">
            <svg viewBox="0 0 24 24"><rect x="2" y="3" width="20" height="14" rx="2" ry="2"></rect><line x1="8" y1="21" x2="16" y2="21"></line></svg>
            Katalog
        </div>
        <div class="nav-item" onclick="toggleCartDrawer(true)">
            <svg viewBox="0 0 24 24"><path d="M6 2L3 6v14a2 2 0 0 0 2 2h14a2 2 0 0 0 2-2V6l-3-4z"></path></svg>
            Sepetim
        </div>
        <div class="nav-item" onclick="handleAccountClick()">
            <svg viewBox="0 0 24 24"><path d="M20 21v-2a4 4 0 0 0-4-4H8a4 4 0 0 0-4 4v2"></path><circle cx="12" cy="7" r="4"></circle></svg>
            Hesabım
        </div>
    </div>

    <script>
        const initialProducts = [
            { 
                id: 1, 
                name: "VOLTERX Core Tee", 
                category: "apparel", 
                price: 850, 
                stock: 15,
                desc: "%100 Saf Pamuk Heavyweight", 
                tag: "POPÜLER", 
                images: [
                    "https://images.unsplash.com/photo-1521572267360-ee0c2909d518?w=500&auto=format&fit=crop",
                    "https://images.unsplash.com/photo-1503342217505-b0a15ec3261c?w=500&auto=format&fit=crop"
                ] 
            },
            { 
                id: 2, 
                name: "VOLTERX Tech Hoodie", 
                category: "apparel", 
                price: 1650, 
                stock: 8,
                desc: "Siyah nakış detaylı oversize", 
                tag: "YENİ", 
                images: [
                    "https://images.unsplash.com/photo-1556905055-8f358a7a47b2?w=500&auto=format&fit=crop",
                    "https://images.unsplash.com/photo-1509967419530-da38b4704bc6?w=500&auto=format&fit=crop"
                ] 
            },
            { 
                id: 3, 
                name: "VOLTERX Waterproof Cap", 
                category: "tech", 
                price: 550, 
                stock: 0,
                desc: "Su geçirmez kumaş şapka", 
                tag: "TÜKENDİ", 
                images: [
                    "https://images.unsplash.com/photo-1588850561407-ed78c282e89b?w=500&auto=format&fit=crop"
                ] 
            },
            { 
                id: 4, 
                name: "VOLTERX Drop 01", 
                category: "drop", 
                price: 1100, 
                stock: 5,
                desc: "Sınırlı sayıda sweatshirt", 
                tag: "DROP 2026", 
                images: [
                    "https://images.unsplash.com/photo-1503342217505-b0a15ec3261c?w=500&auto=format&fit=crop"
                ] 
            }
        ];

        let products = JSON.parse(localStorage.getItem('volterx_prods')) || initialProducts;
        let userLogs = JSON.parse(localStorage.getItem('volterx_user_logs')) || [];
        let cart = [];
        let currentUser = JSON.parse(localStorage.getItem('volterx_user')) || null;
        let selectedImageIndices = {};

        window.addEventListener('load', () => {
            setTimeout(() => {
                const splash = document.getElementById('splash-screen');
                splash.classList.add('fade-out');
            }, 1800);
        });

        function showToast(msg) {
            const toast = document.getElementById('toast');
            toast.textContent = msg;
            toast.classList.add('show');
            setTimeout(() => { toast.classList.remove('show'); }, 3000);
        }

        function renderProducts(items = products) {
            const grid = document.getElementById('productGrid');
            grid.innerHTML = '';

            items.forEach(p => {
                if(!selectedImageIndices[p.id]) selectedImageIndices[p.id] = 0;
                const activeImgIndex = selectedImageIndices[p.id];
                const activeImg = p.images[activeImgIndex] || p.images[0];

                const isOutOfStock = p.stock <= 0;

                const card = document.createElement('div');
                card.className = `product-card ${isOutOfStock ? 'out-of-stock' : ''}`;

                let galleryHtml = '';
                if(p.images.length > 1) {
                    galleryHtml = `<div class="thumb-gallery">` + p.images.map((img, idx) => `
                        <div class="thumb-mini ${idx === activeImgIndex ? 'active' : ''}" style="background-image: url('${img}')" onclick="changeProductImage(${p.id}, ${idx})"></div>
                    `).join('') + `</div>`;
                }

                card.innerHTML = `
                    <div class="product-thumb-wrapper">
                        <span class="product-tag ${isOutOfStock ? 'out' : ''}">${isOutOfStock ? 'STOK TÜKENDİ' : (p.tag || 'VOLTERX')}</span>
                        ${p.images.length > 1 ? `<button class="slider-btn prev" onclick="shiftImage(${p.id}, -1)">‹</button>` : ''}
                        <div class="product-thumb" style="background-image: url('${activeImg}');" onclick="openProductDetailModal(${p.id})"></div>
                        ${p.images.length > 1 ? `<button class="slider-btn next" onclick="shiftImage(${p.id}, 1)">›</button>` : ''}
                    </div>
                    ${galleryHtml}
                    <div class="product-name" onclick="openProductDetailModal(${p.id})" style="cursor:pointer;">${p.name}</div>
                    <div class="product-stock ${isOutOfStock ? 'no-stock' : ''}">${isOutOfStock ? 'Stok Yok' : 'Stok: ' + p.stock + ' adet'}</div>
                    <div class="product-desc">${p.desc}</div>
                    <div class="product-footer">
                        <div class="product-price">${p.price} TL</div>
                        <button class="add-cart-btn" onclick="addToCart(${p.id})" ${isOutOfStock ? 'disabled' : ''}>
                            <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="#fff" stroke-width="3"><line x1="12" y1="5" x2="12" y2="19"></line><line x1="5" y1="12" x2="19" y2="12"></line></svg>
                        </button>
                    </div>
                `;
                grid.appendChild(card);
            });
        }

        function changeProductImage(productId, index) {
            selectedImageIndices[productId] = index;
            renderProducts();
        }

        function shiftImage(productId, step) {
            const prod = products.find(p => p.id === productId);
            if(!prod) return;
            let current = selectedImageIndices[productId] || 0;
            current = (current + step + prod.images.length) % prod.images.length;
            selectedImageIndices[productId] = current;
            renderProducts();
        }

        function openProductDetailModal(id) {
            const prod = products.find(p => p.id === id);
            if (!prod) return;

            let activeIdx = selectedImageIndices[id] || 0;
            const isOutOfStock = prod.stock <= 0;

            const modalContent = document.getElementById('modalProductDetailContent');
            modalContent.innerHTML = `
                <div class="preview-main-img" id="detailMainImg" style="background-image: url('${prod.images[activeIdx]}');"></div>
                ${prod.images.length > 1 ? `
                    <div class="preview-thumbs">
                        ${prod.images.map((img, i) => `
                            <div class="preview-thumb-item ${i === activeIdx ? 'active' : ''}" style="background-image: url('${img}');" onclick="setDetailModalImage('${img}', this)"></div>
                        `).join('')}
                    </div>
                ` : ''}
                <h2 style="font-size:18px; font-weight:800; margin-top:10px;">${prod.name}</h2>
                <div style="font-size:12px; font-weight:700; color:${isOutOfStock ? '#ff0000' : '#008000'}; margin-bottom:6px;">
                    ${isOutOfStock ? 'Stok Tükenmiştir' : 'Kalan Stok: ' + prod.stock + ' Adet'}
                </div>
                <p style="font-size:12px; color:var(--text-muted); margin-bottom:12px;">${prod.desc}</p>
                <div style="font-size:18px; font-weight:800; margin-bottom:14px;">${prod.price} TL</div>
                <button class="btn-full" onclick="addToCart(${prod.id}); closeProductDetailModal();" ${isOutOfStock ? 'disabled' : ''}>
                    ${isOutOfStock ? 'STOKTA YOK' : 'SEPETE EKLE'}
                </button>
            `;

            document.getElementById('productDetailModal').style.display = 'flex';
        }

        function setDetailModalImage(imgUrl, el) {
            document.getElementById('detailMainImg').style.backgroundImage = `url('${imgUrl}')`;
            document.querySelectorAll('.preview-thumb-item').forEach(item => item.classList.remove('active'));
            el.classList.add('active');
        }

        function closeProductDetailModal() {
            document.getElementById('productDetailModal').style.display = 'none';
        }

        function renderUserLogs() {
            const logList = document.getElementById('userLogList');
            if (!userLogs || userLogs.length === 0) {
                logList.innerHTML = '<div style="color:#888;">Henüz giriş kaydı yok.</div>';
                return;
            }
            logList.innerHTML = userLogs.map(log => `
                <div class="user-log-item">
                    <strong>${log.name}</strong>
                    <span style="color:#666;">${log.time}</span>
                </div>
            `).join('');
        }

        function addToCart(id) {
            if (!currentUser) {
                showToast("⚠️ Sepete eklemek için önce giriş yapmalısınız!");
                openAuthModal();
                return;
            }

            const prod = products.find(p => p.id === id);
            if (!prod) return;

            if (prod.stock <= 0) {
                showToast("⚠️ Bu ürünün stoku tükenmiştir!");
                return;
            }

            const item = cart.find(c => c.id === id);
            const currentQtyInCart = item ? item.qty : 0;

            if (currentQtyInCart + 1 > prod.stock) {
                showToast(`⚠️ Stok sınırına ulaşıldı! Maksimum ${prod.stock} adet eklenebilir.`);
                return;
            }

            if (item) {
                item.qty++;
            } else {
                cart.push({ ...prod, qty: 1 });
            }
            updateCartUI();
            showToast(`✓ ${prod.name} sepete eklendi.`);
        }

        function updateCartUI() {
            const count = cart.reduce((acc, curr) => acc + curr.qty, 0);
            document.getElementById('cartBadge').textContent = count;

            const list = document.getElementById('cartItemsList');
            list.innerHTML = '';

            let total = 0;
            cart.forEach(c => {
                total += c.price * c.qty;
                const row = document.createElement('div');
                row.className = 'cart-item-row';
                row.innerHTML = `
                    <div>
                        <div style="font-size:13px; font-weight:700;">${c.name}</div>
                        <div style="font-size:11px; color:#666;">${c.qty} adet x ${c.price} TL</div>
                    </div>
                    <div style="font-size:13px; font-weight:800;">${c.price * c.qty} TL</div>
                `;
                list.appendChild(row);
            });

            document.getElementById('cartTotalPrice').textContent = total + " TL";
        }

        function toggleCartDrawer(open) {
            if (open && !currentUser) {
                showToast("⚠️ Sepeti görmek için lütfen giriş yapın.");
                openAuthModal();
                return;
            }
            const drawer = document.getElementById('cartDrawer');
            if (open) drawer.classList.add('open');
            else drawer.classList.remove('open');
        }

        function openAuthModal() { document.getElementById('authModal').style.display = 'flex'; }
        function closeAuthModal() { document.getElementById('authModal').style.display = 'none'; }

        function handleAccountClick() {
            if (currentUser) openProfileModal();
            else openAuthModal();
        }

        function switchAuthTab(type) {
            document.getElementById('tabUser').classList.toggle('active', type === 'user');
            document.getElementById('tabAdmin').classList.toggle('active', type === 'admin');
            document.getElementById('formUser').style.display = type === 'user' ? 'block' : 'none';
            document.getElementById('formAdmin').style.display = type === 'admin' ? 'block' : 'none';
        }

        function openProfileModal() {
            if (!currentUser) return;
            document.getElementById('profileName').value = currentUser.name || '';
            document.getElementById('profilePhone').value = currentUser.phone || '';
            document.getElementById('profileAddress').value = currentUser.address || '';
            document.getElementById('profileModal').style.display = 'flex';
        }

        function closeProfileModal() { document.getElementById('profileModal').style.display = 'none'; }

        function saveProfile() {
            if (!currentUser) return;
            const newName = document.getElementById('profileName').value.trim();
            const phone = document.getElementById('profilePhone').value.trim();
            const address = document.getElementById('profileAddress').value.trim();

            if (!newName) {
                alert("İsim alanı boş bırakılamaz.");
                return;
            }

            currentUser.name = newName;
            currentUser.phone = phone;
            currentUser.address = address;

            localStorage.setItem('volterx_user', JSON.stringify(currentUser));
            updateUserStatus();
            closeProfileModal();
            showToast("✓ Profil bilgileriniz güncellendi.");
        }

        function recordUserLogin(username) {
            const timeString = new Date().toLocaleTimeString('tr-TR', { hour: '2-digit', minute: '2-digit' });
            userLogs.unshift({ name: username, time: timeString });
            if (userLogs.length > 20) userLogs.pop();
            localStorage.setItem('volterx_user_logs', JSON.stringify(userLogs));
            renderUserLogs();
        }

        function loginUser() {
            const username = document.getElementById('userUsername').value.trim();
            if (!username) {
                alert("Lütfen kullanıcı adı girin.");
                return;
            }
            currentUser = { name: username, role: 'user', phone: '', address: '' };
            localStorage.setItem('volterx_user', JSON.stringify(currentUser));
            recordUserLogin(username);
            onLoginSuccess();
            showToast(`Hoş geldiniz, ${username}!`);
        }

        function loginAdmin() {
            const adminName = document.getElementById('adminUsername').value.trim();
            const adminPass = document.getElementById('adminPassword').value;

            if (adminName === "taha" && adminPass === "taha123") {
                currentUser = { name: "Yönetici (" + adminName + ")", role: 'admin', phone: '', address: '' };
                localStorage.setItem('volterx_user', JSON.stringify(currentUser));
                onLoginSuccess();
                showToast("⚡ Yönetici paneli aktif edildi.");
            } else {
                alert("Hatalı yönetici bilgileri!");
            }
        }

        function onLoginSuccess() {
            closeAuthModal();
            updateUserStatus();
        }

        function logout() {
            currentUser = null;
            cart = [];
            localStorage.removeItem('volterx_user');
            document.body.classList.remove('is-admin');
            updateCartUI();
            updateUserStatus();
            showToast("Oturum kapatıldı.");
        }

        function updateUserStatus() {
            const text = document.getElementById('userStatusText');
            const btn = document.getElementById('authActionBtn');
            const profileBtn = document.getElementById('profileEditBtn');

            if (currentUser) {
                text.textContent = `Aktif: ${currentUser.name}`;
                btn.textContent = "[ Çıkış Yap ]";
                btn.onclick = logout;
                profileBtn.style.display = "inline";

                if (currentUser.role === 'admin') {
                    document.body.classList.add('is-admin');
                    renderUserLogs();
                } else {
                    document.body.classList.remove('is-admin');
                }
            } else {
                text.textContent = "Oturum Açılmadı";
                btn.textContent = "[ Giriş Yap ]";
                btn.onclick = openAuthModal;
                profileBtn.style.display = "none";
                document.body.classList.remove('is-admin');
            }
        }

        function handleNewProduct(e) {
            e.preventDefault();
            if (!currentUser || currentUser.role !== 'admin') {
                alert("Bu işlem için yönetici yetkisi gerekiyor.");
                return;
            }

            const title = document.getElementById('newTitle').value;
            const price = parseFloat(document.getElementById('newPrice').value);
            const stock = parseInt(document.getElementById('newStock').value) || 0;
            const rawImages = document.getElementById('newImages').value.trim();

            let imagesArray = rawImages.split(',').map(u => u.trim()).filter(u => u.length > 0);
            if (imagesArray.length === 0) {
                imagesArray = ["https://images.unsplash.com/photo-1521572267360-ee0c2909d518?w=500&auto=format&fit=crop"];
            }

            const newProd = {
                id: Date.now(),
                name: title,
                category: "apparel",
                price: price,
                stock: stock,
                desc: "VOLTERX Yeni Sezon Ürünü",
                tag: stock > 0 ? "YENİ" : "TÜKENDİ",
                images: imagesArray
            };

            products.unshift(newProd);
            localStorage.setItem('volterx_prods', JSON.stringify(products));
            renderProducts();
            document.getElementById('prodAddForm').reset();
            showToast("✓ Yeni ürün stok miktarıyla eklendi.");
        }

        function filterCategory(cat, element) {
            document.querySelectorAll('.chip').forEach(c => c.classList.remove('active'));
            element.classList.add('active');

            if (cat === 'all') {
                renderProducts(products);
            } else {
                const filtered = products.filter(p => p.category === cat);
                renderProducts(filtered);
            }
        }

        function filterProducts() {
            const query = document.getElementById('searchInput').value.toLowerCase();
            const filtered = products.filter(p => p.name.toLowerCase().includes(query) || p.desc.toLowerCase().includes(query));
            renderProducts(filtered);
        }

        function scrollToProducts() {
            document.getElementById('productsSection').scrollIntoView({ behavior: 'smooth' });
        }

        function checkoutWhatsApp() {
            if (cart.length === 0) {
                alert("Sepetiniz boş!");
                return;
            }
            
            // Stok düşme işlemi
            cart.forEach(cartItem => {
                const prod = products.find(p => p.id === cartItem.id);
                if (prod) {
                    prod.stock = Math.max(0, prod.stock - cartItem.qty);
                    if (prod.stock === 0) prod.tag = "TÜKENDİ";
                }
            });
            localStorage.setItem('volterx_prods', JSON.stringify(products));

            let message = "*VOLTERX SİPARİŞİ*\n";
            message += `*Müşteri:* ${currentUser.name}\n`;
            if (currentUser.phone) message += `*Tel:* ${currentUser.phone}\n`;
            if (currentUser.address) message += `*Adres:* ${currentUser.address}\n\n`;
            message += "*Ürünler:*\n";

            let totalPrice = 0;
            let firstProduct = null;

            cart.forEach((c, index) => {
                if (index === 0) firstProduct = c;
                message += `• ${c.qty}x ${c.name} - ${c.price * c.qty} TL\n`;
                totalPrice += c.price * c.qty;
            });
            
            message += `\n*Toplam:* ${totalPrice} TL\n`;
            
            if (firstProduct) {
                message += `\nÜrünü WhatsApp'ta gör: wa.me/c/905413147488?product=${firstProduct.id}`;
            }

            // Sepeti temizle ve görünümü yenile
            cart = [];
            updateCartUI();
            toggleCartDrawer(false);
            renderProducts();

            window.open(`https://wa.me/905413147488?text=${encodeURIComponent(message)}`, '_blank');
        }

        window.onload = function() {
            renderProducts();
            updateUserStatus();
        };
    </script>
</body>
</html>
