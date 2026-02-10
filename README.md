<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Admin Promo - Ultimate Version</title>
    
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;900&display=swap" rel="stylesheet">

    <style>
        :root {
            --primary: #2c3e50;
            --silver: #bdc3c7;
            --gold: #f1c40f;
            --diamond: #00e5ff;
            --danger: #e74c3c;
            --success: #2ecc71;
            --bg-light: #f8f9fa;
            --text-dark: #34495e;
            --text-muted: #7f8c8d;
        }

        body { 
            font-family: 'Inter', sans-serif; 
            background: #eceff1; /* Background sedikit lebih gelap biar kotaknya pop-up */
            padding: 20px; 
            display: flex; flex-direction: column; align-items: center; 
            margin: 0; 
            min-height: 100vh;
        }
        
        /* KOTAK UTAMA */
        .admin-box { 
            background: white; 
            padding: 35px; 
            border-radius: 20px; /* Sudut lebih bulat */
            box-shadow: 0 10px 30px rgba(0,0,0,0.08); /* Bayangan lebih halus */
            width: 95% !important; 
            max-width: 1000px !important; 
            box-sizing: border-box; 
            position: relative; 
            margin-bottom: 50px;
            overflow: hidden; /* Biar rapi */
        }
        
        /* JUDUL SANGAT KECIL (HALUS) */
        h1 { 
            color: var(--text-muted); 
            margin: 0 0 20px 0; 
            font-size: 0.65rem; /* SANGAT KECIL */
            text-align: center; 
            text-transform: uppercase;
            letter-spacing: 2px;
            font-weight: 700;
            opacity: 0.7;
        }

        /* MENU ZOOM */
        .menu-wrapper { position: absolute; top: 25px; right: 25px; z-index: 100; }
        .hamburger-btn {
            background: var(--bg-light); color: var(--text-dark); border: none; padding: 8px;
            font-size: 24px; cursor: pointer; transition: 0.2s; outline: none; line-height: 1;
            border-radius: 8px;
        }
        .hamburger-btn:hover { background: #e2e6ea; color: var(--primary); }

        .zoom-dropdown {
            display: none; position: absolute; top: 50px; right: 0;
            background: white; border: 1px solid #eee; border-radius: 12px;
            box-shadow: 0 5px 20px rgba(0,0,0,0.1); padding: 15px; z-index: 100;
            width: 180px; text-align: left;
        }
        .show-menu { display: block !important; }
        .zoom-dropdown label { font-size: 0.8rem; font-weight: 700; color: var(--text-dark); margin-bottom: 8px; display: block;}
        .zoom-dropdown select { width: 100%; padding: 10px; border-radius: 8px; border: 1px solid #ddd; font-family: inherit; }

        /* TOMBOL LOGIN / LOGOUT */
        #login-btn {
            background: #4285F4; color: white; border: none; padding: 12px 30px;
            border-radius: 50px; font-weight: 700; cursor: pointer; display: block;
            margin: 0 auto 25px auto;
            font-size: 0.95rem; box-shadow: 0 4px 15px rgba(66, 133, 244, 0.3);
            transition: 0.3s; letter-spacing: 0.5px;
        }
        #login-btn:hover { transform: translateY(-3px); box-shadow: 0 6px 20px rgba(66, 133, 244, 0.4); }

        /* MASTER SWITCH */
        .master-box {
            background: var(--bg-light); padding: 25px; border-radius: 16px;
            display: flex; justify-content: center; align-items: center; text-align: center;
            border: 3px solid #eee; margin-bottom: 30px; cursor: pointer;
            transition: 0.3s;
        }
        .master-box:hover { transform: scale(1.02); box-shadow: 0 5px 15px rgba(0,0,0,0.05); }
        .master-active { border-color: var(--success); background: #e8f8f5; }
        .master-inactive { border-color: var(--danger); background: #fdedec; }

        /* --- ITEM ROW & KATEGORI (LEBIH LEGA) --- */
        .category-head {
            font-weight: 900; font-size: 1.2rem; 
            margin-top: 60px; /* JARAK ATAS LEBIH JAUH */
            margin-bottom: 20px;
            padding-left: 15px; border-left: 6px solid #ccc; color: var(--text-dark); text-transform: uppercase; letter-spacing: 1px;
        }
        .head-silver { border-color: var(--silver); color: #7f8c8d; }
        .head-gold { border-color: var(--gold); color: #f39c12; }
        .head-diamond { border-color: var(--diamond); color: #00a8ff; }

        .item-row { 
            display: flex; justify-content: space-between; align-items: center; 
            background: white; padding: 20px; margin-bottom: 15px; 
            border-radius: 16px; /* Lebih bulat */
            box-shadow: 0 2px 10px rgba(0,0,0,0.03); 
            border: 1px solid #f0f0f0; transition: 0.2s;
        }
        .item-row:hover { border-color: #e0e0e0; box-shadow: 0 5px 15px rgba(0,0,0,0.05); }
        
        .item-left { display: flex; align-items: flex-start; gap: 20px; flex: 1; }
        .key-icon-box {
            width: 60px; height: 60px; background: var(--bg-light); border-radius: 12px;
            display: flex; justify-content: center; align-items: center; font-size: 2rem;
            flex-shrink: 0;
        }

        /* --- TAMPILAN HARGA BARU YANG INDAH --- */
        .item-text { display: flex; flex-direction: column; gap: 4px; }
        .item-name { font-weight: 800; font-size: 1.1rem; color: var(--text-dark); }
        
        .price-container { display: flex; flex-direction: column; }
        .main-price { font-size: 1.3rem; font-weight: 900; color: var(--primary); }
        .promo-info { font-size: 0.85rem; font-weight: 600; color: var(--success); display: flex; align-items: center; gap: 5px;}
        .strikethrough { text-decoration: line-through; color: var(--text-muted); font-weight: 400; }

        /* --- TOGGLE SWITCH SUPER JUMBO (2x LIPAT) --- */
        .switch { 
            position: relative; 
            display: inline-block; 
            width: 140px;   /* SANGAT LEBAR */
            height: 70px;  /* SANGAT TINGGI */
            flex-shrink: 0;
            margin-left: 20px;
        } 
        .switch input { opacity: 0; width: 0; height: 0; }
        .slider {
            position: absolute; cursor: pointer; top: 0; left: 0; right: 0; bottom: 0;
            background-color: #e0e0e0; transition: .4s; border-radius: 70px;
            box-shadow: inset 0 2px 5px rgba(0,0,0,0.1);
        }
        .slider:before {
            position: absolute; content: ""; 
            height: 62px; width: 62px; /* BULATAN RAKSASA */
            left: 4px; bottom: 4px; 
            background-color: white;
            transition: .4s cubic-bezier(0.175, 0.885, 0.32, 1.275); /* Efek membal saat digeser */
            border-radius: 50%;
            box-shadow: 0 5px 15px rgba(0,0,0,0.2);
        }
        input:checked + .slider { background-color: var(--success); }
        input:checked + .slider:before { transform: translateX(70px); }

        .hide { display: none !important; }

    </style>
</head>
<body>

    <div class="admin-box">
        
        <div class="menu-wrapper">
            <button class="hamburger-btn" onclick="toggleZoomMenu()">☰</button>
            <div id="zoom-menu-box" class="zoom-dropdown">
                <label>Ukuran Layar:</label>
                <select id="zoom-level" onchange="setZoom(this.value)">
                    <option value="0.1">Level 1 (10%)</option>
                    <option value="0.2">Level 2 (20%)</option>
                    <option value="0.3">Level 3 (30%)</option>
                    <option value="0.4">Level 4 (40%)</option>
                    <option value="0.5">Level 5 (50%)</option>
                    <option value="0.6">Level 6 (60%)</option>
                    <option value="0.7">Level 7 (70%)</option>
                    <option value="0.8">Level 8 (80%)</option>
                    <option value="0.9">Level 9 (90%)</option>
                    <option value="1.0" selected>Level 10 (Normal)</option>
                    <option value="1.1">Level 11 (110%)</option>
                    <option value="1.2">Level 12 (120%)</option>
                    <option value="1.3">Level 13 (130%)</option>
                    <option value="1.4">Level 14 (140%)</option>
                    <option value="1.5">Level 15 (150%)</option>
                </select>
            </div>
        </div>

        <h1>🛠️ Aktifkan POP UP</h1>

        <button id="login-btn" onclick="loginGoogle()">🔑 LOGIN ADMIN (Google)</button>

        <div id="control-area" class="hide">
            
            <div id="master-switch-ui" class="master-box master-inactive" onclick="toggleMaster()">
                <div id="master-status-text" style="font-weight:900; font-size:1.8rem; color:var(--danger);">OFF (MATI) ⭕</div>
            </div>

            <div class="category-head head-silver">PAKET SILVER</div>
            
            <div class="item-row">
                <div class="item-left">
                    <div class="key-icon-box">🥈</div>
                    <div class="item-text">
                        <span class="item-name">100 Kunci Silver</span>
                        <div class="price-container">
                            <span class="main-price">Rp 3.500.000</span>
                            <span class="promo-info">Hemat 500rb <span class="strikethrough">Rp 4.000.000</span></span>
                        </div>
                    </div>
                </div>
                <label class="switch"><input type="checkbox" id="chk_promo_silver_100" onchange="updateItem('promo_silver_100')"><span class="slider"></span></label>
            </div>

            <div class="item-row">
                <div class="item-left">
                    <div class="key-icon-box">🥈</div>
                    <div class="item-text">
                        <span class="item-name">50 Kunci Silver</span>
                        <div class="price-container">
                            <span class="main-price">Rp 1.800.000</span>
                            <span class="promo-info">Hemat 200rb <span class="strikethrough">Rp 2.000.000</span></span>
                        </div>
                    </div>
                </div>
                <label class="switch"><input type="checkbox" id="chk_promo_silver_50" onchange="updateItem('promo_silver_50')"><span class="slider"></span></label>
            </div>

            <div class="item-row">
                <div class="item-left">
                    <div class="key-icon-box">🥈</div>
                    <div class="item-text">
                        <span class="item-name">20 Kunci Silver</span>
                        <div class="price-container">
                            <span class="main-price">Rp 730.000</span>
                            <span class="promo-info">Hemat 70rb <span class="strikethrough">Rp 800.000</span></span>
                        </div>
                    </div>
                </div>
                <label class="switch"><input type="checkbox" id="chk_promo_silver_20" onchange="updateItem('promo_silver_20')"><span class="slider"></span></label>
            </div>

            <div class="item-row">
                <div class="item-left">
                    <div class="key-icon-box">🥈</div>
                    <div class="item-text">
                        <span class="item-name">10 Kunci Silver</span>
                        <div class="price-container">
                            <span class="main-price">Rp 370.000</span>
                            <span class="promo-info">Hemat 30rb <span class="strikethrough">Rp 400.000</span></span>
                        </div>
                    </div>
                </div>
                <label class="switch"><input type="checkbox" id="chk_promo_silver_10" onchange="updateItem('promo_silver_10')"><span class="slider"></span></label>
            </div>

            <div class="item-row">
                <div class="item-left">
                    <div class="key-icon-box">🥈</div>
                    <div class="item-text">
                        <span class="item-name">5 Kunci Silver</span>
                        <div class="price-container">
                            <span class="main-price">Rp 195.000</span>
                            <span class="promo-info">Hemat 5rb <span class="strikethrough">Rp 200.000</span></span>
                        </div>
                    </div>
                </div>
                <label class="switch"><input type="checkbox" id="chk_promo_silver_5" onchange="updateItem('promo_silver_5')"><span class="slider"></span></label>
            </div>

            <div class="item-row">
                <div class="item-left">
                    <div class="key-icon-box">🥈</div>
                    <div class="item-text">
                        <span class="item-name">1 Kunci Silver</span>
                        <span class="price-container">
                            <span class="main-price" style="font-size: 1.1rem;">Rp 35.000</span>
                        </span>
                    </div>
                </div>
                <label class="switch"><input type="checkbox" id="chk_promo_silver_1" onchange="updateItem('promo_silver_1')"><span class="slider"></span></label>
            </div>


            <div class="category-head head-gold">PAKET GOLD</div>

            <div class="item-row">
                <div class="item-left">
                    <div class="key-icon-box" style="background: #fffcf2;">👑</div>
                    <div class="item-text">
                        <span class="item-name">70 Kunci Gold</span>
                        <span class="main-price" style="font-size: 1.1rem;">Rp 5.000.000</span>
                    </div>
                </div>
                <label class="switch"><input type="checkbox" id="chk_promo_gold_70" onchange="updateItem('promo_gold_70')"><span class="slider"></span></label>
            </div>

            <div class="item-row">
                <div class="item-left">
                    <div class="key-icon-box" style="background: #fffcf2;">👑</div>
                    <div class="item-text">
                        <span class="item-name">50 Kunci Gold</span>
                        <span class="main-price" style="font-size: 1.1rem;">Rp 3.700.000</span>
                    </div>
                </div>
                <label class="switch"><input type="checkbox" id="chk_promo_gold_50" onchange="updateItem('promo_gold_50')"><span class="slider"></span></label>
            </div>

            <div class="item-row">
                <div class="item-left">
                    <div class="key-icon-box" style="background: #fffcf2;">👑</div>
                    <div class="item-text">
                        <span class="item-name">10 Kunci Gold</span>
                        <span class="main-price" style="font-size: 1.1rem;">Rp 760.000</span>
                    </div>
                </div>
                <label class="switch"><input type="checkbox" id="chk_promo_gold_10" onchange="updateItem('promo_gold_10')"><span class="slider"></span></label>
            </div>

            <div class="item-row">
                <div class="item-left">
                    <div class="key-icon-box" style="background: #fffcf2;">👑</div>
                    <div class="item-text">
                        <span class="item-name">5 Kunci Gold</span>
                        <span class="main-price" style="font-size: 1.1rem;">Rp 410.000</span>
                    </div>
                </div>
                <label class="switch"><input type="checkbox" id="chk_promo_gold_5" onchange="updateItem('promo_gold_5')"><span class="slider"></span></label>
            </div>
             <div class="item-row">
                <div class="item-left">
                    <div class="key-icon-box" style="background: #fffcf2;">👑</div>
                    <div class="item-text">
                        <span class="item-name">1 Kunci Gold</span>
                        <span class="main-price" style="font-size: 1.1rem;">Rp 85.000</span>
                    </div>
                </div>
                <label class="switch"><input type="checkbox" id="chk_promo_gold_1" onchange="updateItem('promo_gold_1')"><span class="slider"></span></label>
            </div>


            <div class="category-head head-diamond">PAKET DIAMOND</div>

            <div class="item-row">
                <div class="item-left">
                    <div class="key-icon-box" style="background: #f0fbff;">💎</div>
                    <div class="item-text">
                        <span class="item-name">25 Kunci Diamond</span>
                        <span class="main-price" style="font-size: 1.1rem;">Rp 5.300.000</span>
                    </div>
                </div>
                <label class="switch"><input type="checkbox" id="chk_promo_diamond_25" onchange="updateItem('promo_diamond_25')"><span class="slider"></span></label>
            </div>

            <div class="item-row">
                <div class="item-left">
                    <div class="key-icon-box" style="background: #f0fbff;">💎</div>
                    <div class="item-text">
                        <span class="item-name">15 Kunci Diamond</span>
                        <span class="main-price" style="font-size: 1.1rem;">Rp 3.250.000</span>
                    </div>
                </div>
                <label class="switch"><input type="checkbox" id="chk_promo_diamond_15" onchange="updateItem('promo_diamond_15')"><span class="slider"></span></label>
            </div>

            <div class="item-row">
                <div class="item-left">
                    <div class="key-icon-box" style="background: #f0fbff;">💎</div>
                    <div class="item-text">
                        <span class="item-name">10 Kunci Diamond</span>
                        <span class="main-price" style="font-size: 1.1rem;">Rp 2.200.000</span>
                    </div>
                </div>
                <label class="switch"><input type="checkbox" id="chk_promo_diamond_10" onchange="updateItem('promo_diamond_10')"><span class="slider"></span></label>
            </div>

            <div class="item-row">
                <div class="item-left">
                    <div class="key-icon-box" style="background: #f0fbff;">💎</div>
                    <div class="item-text">
                        <span class="item-name">5 Kunci Diamond</span>
                        <span class="main-price" style="font-size: 1.1rem;">Rp 1.150.000</span>
                    </div>
                </div>
                <label class="switch"><input type="checkbox" id="chk_promo_diamond_5" onchange="updateItem('promo_diamond_5')"><span class="slider"></span></label>
            </div>
             <div class="item-row">
                <div class="item-left">
                    <div class="key-icon-box" style="background: #f0fbff;">💎</div>
                    <div class="item-text">
                        <span class="item-name">1 Kunci Diamond</span>
                        <span class="main-price" style="font-size: 1.1rem;">Rp 250.000</span>
                    </div>
                </div>
                <label class="switch"><input type="checkbox" id="chk_promo_diamond_1" onchange="updateItem('promo_diamond_1')"><span class="slider"></span></label>
            </div>

        </div>

    </div>

    <script>
        function setZoom(val) { 
            document.body.style.zoom = val; 
            localStorage.setItem('adminPromoZoom', val); 
        }

        function toggleZoomMenu() {
            const menu = document.getElementById('zoom-menu-box');
            menu.classList.toggle('show-menu');
        }

        window.onload = function() {
            const lastZoom = localStorage.getItem('adminPromoZoom') || "1.0";
            document.body.style.zoom = lastZoom;
            const selectBox = document.getElementById('zoom-level');
            if(selectBox) selectBox.value = lastZoom;
        }
    </script>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getAuth, signInWithPopup, GoogleAuthProvider, onAuthStateChanged, signOut } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-auth.js";
        import { getDatabase, ref, onValue, set } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";

        const firebaseConfig = {
            apiKey: "AIzaSyBublDvXwqKWK3lACZ_plD3ORMS1h2MvTM",
            authDomain: "kuis-belajar-fc843.firebaseapp.com",
            databaseURL: "https://kuis-belajar-fc843-default-rtdb.asia-southeast1.firebasedatabase.app",
            projectId: "kuis-belajar-fc843",
            storageBucket: "kuis-belajar-fc843.firebasestorage.app",
            messagingSenderId: "851984555383",
            appId: "1:851984555383:web:e47824f590620b73849572"
        };

        const app = initializeApp(firebaseConfig);
        const auth = getAuth(app);
        const db = getDatabase(app);
        const provider = new GoogleAuthProvider();

        const MY_ADMIN_UID = "G6N2sLEF6vX0e3X9ndbmft1oHVg2"; 
        let masterStatus = false;

        const loginBtn = document.getElementById('login-btn');

        window.loginGoogle = () => signInWithPopup(auth, provider);
        
        window.logout = () => {
            signOut(auth).then(() => {
                location.reload();
            });
        };

        function updateMasterUI(status) {
            const box = document.getElementById('master-switch-ui');
            const txt = document.getElementById('master-status-text');
            if(status) {
                box.className = "master-box master-active";
                txt.innerText = "ON (MENYALA) ✅";
                txt.style.color = var(--success);
            } else {
                box.className = "master-box master-inactive";
                txt.innerText = "OFF (MATI) ⭕";
                txt.style.color = var(--danger);
            }
        }

        window.toggleMaster = () => {
            set(ref(db, 'config/promo_active'), !masterStatus);
        };

        window.updateItem = (itemId) => {
            const el = document.getElementById('chk_' + itemId);
            if(el) set(ref(db, `config/promo_items/${itemId}`), el.checked);
        };

        onAuthStateChanged(auth, (user) => {
            if (user && user.uid === MY_ADMIN_UID) {
                
                loginBtn.innerHTML = `✅ Admin: <b>${user.email}</b> (Logout)`;
                loginBtn.style.background = var(--success);
                loginBtn.onclick = window.logout;

                document.getElementById('control-area').classList.remove('hide');
                
                onValue(ref(db, 'config/promo_active'), (snap) => {
                    masterStatus = snap.val() === true;
                    updateMasterUI(masterStatus);
                });

                onValue(ref(db, 'config/promo_items'), (snap) => {
                    const data = snap.val() || {};
                    const keys = [
                        'promo_silver_100', 'promo_silver_50', 'promo_silver_20', 'promo_silver_10', 'promo_silver_5', 'promo_silver_1',
                        'promo_gold_70', 'promo_gold_50', 'promo_gold_10', 'promo_gold_5', 'promo_gold_1',
                        'promo_diamond_25', 'promo_diamond_15', 'promo_diamond_10', 'promo_diamond_5', 'promo_diamond_1'
                    ];
                    keys.forEach(k => {
                        const el = document.getElementById('chk_' + k);
                        if(el) el.checked = data[k] === true;
                    });
                });

            } else if (user) {
                loginBtn.innerHTML = `⛔ AKSES DITOLAK: ${user.email} (Logout)`;
                loginBtn.style.background = var(--danger);
                loginBtn.onclick = window.logout;
                alert("Akses Ditolak: Anda bukan Admin!"); 
            } else {
                loginBtn.innerHTML = "🔑 LOGIN ADMIN (Google)";
                loginBtn.style.background = "#4285F4";
                loginBtn.onclick = window.loginGoogle;
                document.getElementById('control-area').classList.add('hide');
            }
        });
    </script>
</body>
</html>
