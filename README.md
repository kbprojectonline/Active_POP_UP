<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Admin Promo - Final Version</title>
    
    <link href="https://fonts.googleapis.com/css2?family=Segoe+UI:wght@400;600;700;900&display=swap" rel="stylesheet">

    <style>
        :root {
            --primary: #2c3e50;
            --silver: #bdc3c7;
            --gold: #f1c40f;
            --diamond: #00e5ff;
            --danger: #c0392b;
        }

        body { 
            font-family: 'Segoe UI', sans-serif; 
            background: #f4f7f6; 
            padding: 15px; 
            display: flex; flex-direction: column; align-items: center; 
            margin: 0; 
            transition: zoom 0.2s ease; 
        }
        
        /* KOTAK UTAMA LEBAR 1000PX */
        .admin-box { 
            background: white; 
            padding: 30px; 
            border-radius: 15px; 
            box-shadow: 0 5px 25px rgba(0,0,0,0.1); 
            width: 95% !important; 
            max-width: 1000px !important; 
            box-sizing: border-box; 
            position: relative; 
            margin-bottom: 50px;
        }
        
        /* JUDUL DIPERKECIL 25% */
        h1 { 
            color: var(--primary); 
            margin: 0 0 20px 0; 
            font-size: 1.2rem; /* Sebelumnya 1.5rem, sekarang lebih kecil */
            text-align: center; 
            border-bottom: 2px solid #eee; 
            padding-bottom: 15px; 
        }

        /* MENU ZOOM */
        .menu-wrapper { position: absolute; top: 20px; right: 20px; z-index: 100; }
        .hamburger-btn {
            background: transparent; color: #555; border: none; padding: 5px;
            font-size: 24px; cursor: pointer; transition: 0.2s; outline: none; line-height: 1;
        }
        .hamburger-btn:hover { color: var(--primary); }

        .zoom-dropdown {
            display: none; position: absolute; top: 40px; right: 0;
            background: white; border: 1px solid #ddd; border-radius: 8px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.15); padding: 10px; z-index: 100;
            width: 160px; text-align: left;
        }
        .show-menu { display: block !important; }
        .zoom-dropdown select { width: 100%; padding: 8px; border-radius: 5px; border: 1px solid #ccc; }

        /* ITEM ROW */
        .category-head {
            font-weight: 900; font-size: 1.1rem; margin-top: 30px; margin-bottom: 10px;
            padding-left: 10px; border-left: 5px solid #ccc; color: #555; text-transform: uppercase;
        }
        .head-silver { border-color: var(--silver); color: #7f8c8d; }
        .head-gold { border-color: var(--gold); color: #f39c12; }
        .head-diamond { border-color: var(--diamond); color: #00a8ff; }

        .item-row { 
            display: flex; justify-content: space-between; align-items: center; 
            background: white; padding: 15px; margin-bottom: 10px; 
            border-radius: 8px; box-shadow: 0 2px 5px rgba(0,0,0,0.05); 
            border: 1px solid #eee;
        }
        
        .item-left { display: flex; align-items: center; gap: 15px; }
        .key-icon { font-size: 1.5rem; }

        .item-text { display: flex; flex-direction: column; }
        .item-name { font-weight: 700; font-size: 1rem; color: #333; }
        .item-price { font-size: 0.9rem; color: #888; }

        #login-btn {
            background: #4285F4; color: white; border: none; padding: 12px 30px;
            border-radius: 30px; font-weight: bold; cursor: pointer; display: block;
            margin: 20px auto; font-size: 1rem; box-shadow: 0 4px 10px rgba(66, 133, 244, 0.3);
        }

        /* --- TOGGLE SWITCH JUMBO (50% LEBIH BESAR) --- */
        .switch { 
            position: relative; 
            display: inline-block; 
            width: 90px;    /* Diperlebar */
            height: 48px;   /* Dipertinggi */
        } 
        .switch input { opacity: 0; width: 0; height: 0; }
        .slider {
            position: absolute; cursor: pointer; top: 0; left: 0; right: 0; bottom: 0;
            background-color: #ccc; transition: .4s; border-radius: 50px;
        }
        .slider:before {
            position: absolute; content: ""; 
            height: 40px; width: 40px; /* BULATAN JADI RAKSASA (40px) */
            left: 4px; bottom: 4px; 
            background-color: white;
            transition: .4s; border-radius: 50%;
            box-shadow: 0 2px 5px rgba(0,0,0,0.3);
        }
        input:checked + .slider { background-color: #27ae60; }
        input:checked + .slider:before { transform: translateX(42px); } /* Jarak geser disesuaikan */

        .hide { display: none !important; }

        /* MASTER SWITCH */
        .master-box {
            background: #f8f9fa; padding: 20px; border-radius: 12px;
            display: flex; justify-content: center;
            align-items: center; text-align: center;
            border: 2px solid #eee; margin-bottom: 20px; cursor: pointer;
            transition: 0.2s;
        }
        .master-box:hover { transform: scale(1.02); }
        .master-active { border-color: #27ae60; background: #e8f8f5; }
        .master-inactive { border-color: #c0392b; background: #fdedec; }

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
                    <option value="1.0" selected>Level 10 (100% - Normal)</option>
                    <option value="1.1">Level 11 (110%)</option>
                    <option value="1.2">Level 12 (120%)</option>
                    <option value="1.3">Level 13 (130%)</option>
                    <option value="1.4">Level 14 (140%)</option>
                    <option value="1.5">Level 15 (150%)</option>
                </select>
            </div>
        </div>

        <h1>🛠️ Aktifkan POP UP</h1>

        <div id="login-area" style="text-align: center; padding: 40px;">
            <p style="color:#777; font-size: 1.1rem;">Silakan Login Admin Terlebih Dahulu</p>
            <button id="login-btn" onclick="loginGoogle()">🔑 LOGIN ADMIN (Google)</button>
        </div>

        <div id="control-area" class="hide">
            
            <div id="master-switch-ui" class="master-box master-inactive" onclick="toggleMaster()">
                <div id="master-status-text" style="font-weight:900; font-size:1.5rem; color:#c0392b;">OFF (MATI) ⭕</div>
            </div>

            <div class="category-head head-silver">PAKET SILVER</div>
            
            <div class="item-row">
                <div class="item-left">
                    <div class="key-icon">🗝️</div>
                    <div class="item-text">
                        <span class="item-name">100 Kunci Silver</span>
                        <span class="item-price">Rp 2.950.000</span>
                    </div>
                </div>
                <label class="switch"><input type="checkbox" id="chk_promo_silver_100" onchange="updateItem('promo_silver_100')"><span class="slider"></span></label>
            </div>

            <div class="item-row">
                <div class="item-left">
                    <div class="key-icon">🗝️</div>
                    <div class="item-text">
                        <span class="item-name">50 Kunci Silver</span>
                        <span class="item-price">Rp 1.480.000</span>
                    </div>
                </div>
                <label class="switch"><input type="checkbox" id="chk_promo_silver_50" onchange="updateItem('promo_silver_50')"><span class="slider"></span></label>
            </div>

            <div class="item-row">
                <div class="item-left">
                    <div class="key-icon">🗝️</div>
                    <div class="item-text">
                        <span class="item-name">20 Kunci Silver</span>
                        <span class="item-price">Rp 600.000</span>
                    </div>
                </div>
                <label class="switch"><input type="checkbox" id="chk_promo_silver_20" onchange="updateItem('promo_silver_20')"><span class="slider"></span></label>
            </div>

            <div class="item-row">
                <div class="item-left">
                    <div class="key-icon">🗝️</div>
                    <div class="item-text">
                        <span class="item-name">10 Kunci Silver</span>
                        <span class="item-price">Rp 310.000</span>
                    </div>
                </div>
                <label class="switch"><input type="checkbox" id="chk_promo_silver_10" onchange="updateItem('promo_silver_10')"><span class="slider"></span></label>
            </div>

            <div class="item-row">
                <div class="item-left">
                    <div class="key-icon">🗝️</div>
                    <div class="item-text">
                        <span class="item-name">5 Kunci Silver</span>
                        <span class="item-price">Rp 165.000</span>
                    </div>
                </div>
                <label class="switch"><input type="checkbox" id="chk_promo_silver_5" onchange="updateItem('promo_silver_5')"><span class="slider"></span></label>
            </div>

            <div class="item-row">
                <div class="item-left">
                    <div class="key-icon">🗝️</div>
                    <div class="item-text">
                        <span class="item-name">1 Kunci Silver</span>
                        <span class="item-price">Rp 35.000</span>
                    </div>
                </div>
                <label class="switch"><input type="checkbox" id="chk_promo_silver_1" onchange="updateItem('promo_silver_1')"><span class="slider"></span></label>
            </div>


            <div class="category-head head-gold">PAKET GOLD</div>

            <div class="item-row">
                <div class="item-left">
                    <div class="key-icon">👑</div>
                    <div class="item-text">
                        <span class="item-name">70 Kunci Gold</span>
                        <span class="item-price">Rp 5.000.000</span>
                    </div>
                </div>
                <label class="switch"><input type="checkbox" id="chk_promo_gold_70" onchange="updateItem('promo_gold_70')"><span class="slider"></span></label>
            </div>

            <div class="item-row">
                <div class="item-left">
                    <div class="key-icon">👑</div>
                    <div class="item-text">
                        <span class="item-name">50 Kunci Gold</span>
                        <span class="item-price">Rp 3.700.000</span>
                    </div>
                </div>
                <label class="switch"><input type="checkbox" id="chk_promo_gold_50" onchange="updateItem('promo_gold_50')"><span class="slider"></span></label>
            </div>

            <div class="item-row">
                <div class="item-left">
                    <div class="key-icon">👑</div>
                    <div class="item-text">
                        <span class="item-name">10 Kunci Gold</span>
                        <span class="item-price">Rp 760.000</span>
                    </div>
                </div>
                <label class="switch"><input type="checkbox" id="chk_promo_gold_10" onchange="updateItem('promo_gold_10')"><span class="slider"></span></label>
            </div>

            <div class="item-row">
                <div class="item-left">
                    <div class="key-icon">👑</div>
                    <div class="item-text">
                        <span class="item-name">5 Kunci Gold</span>
                        <span class="item-price">Rp 410.000</span>
                    </div>
                </div>
                <label class="switch"><input type="checkbox" id="chk_promo_gold_5" onchange="updateItem('promo_gold_5')"><span class="slider"></span></label>
            </div>
             <div class="item-row">
                <div class="item-left">
                    <div class="key-icon">👑</div>
                    <div class="item-text">
                        <span class="item-name">1 Kunci Gold</span>
                        <span class="item-price">Rp 85.000</span>
                    </div>
                </div>
                <label class="switch"><input type="checkbox" id="chk_promo_gold_1" onchange="updateItem('promo_gold_1')"><span class="slider"></span></label>
            </div>


            <div class="category-head head-diamond">PAKET DIAMOND</div>

            <div class="item-row">
                <div class="item-left">
                    <div class="key-icon">💎</div>
                    <div class="item-text">
                        <span class="item-name">25 Kunci Diamond</span>
                        <span class="item-price">Rp 5.300.000</span>
                    </div>
                </div>
                <label class="switch"><input type="checkbox" id="chk_promo_diamond_25" onchange="updateItem('promo_diamond_25')"><span class="slider"></span></label>
            </div>

            <div class="item-row">
                <div class="item-left">
                    <div class="key-icon">💎</div>
                    <div class="item-text">
                        <span class="item-name">15 Kunci Diamond</span>
                        <span class="item-price">Rp 3.250.000</span>
                    </div>
                </div>
                <label class="switch"><input type="checkbox" id="chk_promo_diamond_15" onchange="updateItem('promo_diamond_15')"><span class="slider"></span></label>
            </div>

            <div class="item-row">
                <div class="item-left">
                    <div class="key-icon">💎</div>
                    <div class="item-text">
                        <span class="item-name">10 Kunci Diamond</span>
                        <span class="item-price">Rp 2.200.000</span>
                    </div>
                </div>
                <label class="switch"><input type="checkbox" id="chk_promo_diamond_10" onchange="updateItem('promo_diamond_10')"><span class="slider"></span></label>
            </div>

            <div class="item-row">
                <div class="item-left">
                    <div class="key-icon">💎</div>
                    <div class="item-text">
                        <span class="item-name">5 Kunci Diamond</span>
                        <span class="item-price">Rp 1.150.000</span>
                    </div>
                </div>
                <label class="switch"><input type="checkbox" id="chk_promo_diamond_5" onchange="updateItem('promo_diamond_5')"><span class="slider"></span></label>
            </div>
             <div class="item-row">
                <div class="item-left">
                    <div class="key-icon">💎</div>
                    <div class="item-text">
                        <span class="item-name">1 Kunci Diamond</span>
                        <span class="item-price">Rp 250.000</span>
                    </div>
                </div>
                <label class="switch"><input type="checkbox" id="chk_promo_diamond_1" onchange="updateItem('promo_diamond_1')"><span class="slider"></span></label>
            </div>

            <button onclick="logout()" style="background:#c0392b; color:white; border:none; padding:15px; width:100%; border-radius:10px; font-weight:bold; margin-top:30px; cursor:pointer;">KELUAR ADMIN (LOGOUT)</button>
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

        window.loginGoogle = () => signInWithPopup(auth, provider);
        window.logout = () => signOut(auth).then(() => location.reload());

        function updateMasterUI(status) {
            const box = document.getElementById('master-switch-ui');
            const txt = document.getElementById('master-status-text');
            if(status) {
                box.className = "master-box master-active";
                txt.innerText = "ON (MENYALA) ✅";
                txt.style.color = "#27ae60";
            } else {
                box.className = "master-box master-inactive";
                txt.innerText = "OFF (MATI) ⭕";
                txt.style.color = "#c0392b";
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
                document.getElementById('login-area').classList.add('hide');
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
                alert("Akses Ditolak: Anda bukan Admin!"); signOut(auth);
            }
        });
    </script>
</body>
</html>
