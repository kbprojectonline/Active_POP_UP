<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Admin Promo Control V2 - Full Items</title>
    <style>
        body { font-family: 'Segoe UI', sans-serif; display: flex; flex-direction: column; align-items: center; justify-content: center; min-height: 100vh; margin: 0; background: #eef2f3; }
        
        .card { 
            background: white; padding: 25px; border-radius: 20px; 
            box-shadow: 0 10px 25px rgba(0,0,0,0.1); text-align: center; 
            width: 90%; max-width: 420px; margin: 20px 0;
            max-height: 90vh; overflow-y: auto; /* Agar bisa discroll */
        }
        
        h2 { margin-top: 0; color: #2c3e50; font-size: 1.5rem; }
        
        /* Master Switch Style */
        .status-indicator {
            padding: 15px; border-radius: 12px; margin-bottom: 25px;
            font-weight: 800; font-size: 1.2rem; letter-spacing: 1px;
            display: flex; align-items: center; justify-content: center; gap: 10px;
            border: 2px solid transparent; transition: 0.3s;
        }
        .active-on { background: #d4edda; color: #155724; border-color: #c3e6cb; }
        .active-off { background: #f8d7da; color: #721c24; border-color: #f5c6cb; }

        /* Item List Style */
        .item-list { text-align: left; margin-bottom: 20px; }
        .category-title {
            font-size: 0.9rem; font-weight: bold; margin-top: 15px; margin-bottom: 5px;
            text-transform: uppercase; letter-spacing: 1px; border-bottom: 2px solid #eee; padding-bottom: 5px;
        }

        .item-row {
            display: flex; justify-content: space-between; align-items: center;
            padding: 10px 0; border-bottom: 1px solid #f0f0f0;
        }
        .item-name { font-weight: 600; color: #555; font-size: 0.9rem; }
        .item-price { font-size: 0.75rem; color: #888; display: block; }

        /* Toggle Switch CSS */
        .switch { position: relative; display: inline-block; width: 46px; height: 24px; }
        .switch input { opacity: 0; width: 0; height: 0; }
        .slider {
            position: absolute; cursor: pointer; top: 0; left: 0; right: 0; bottom: 0;
            background-color: #ccc; transition: .4s; border-radius: 34px;
        }
        .slider:before {
            position: absolute; content: ""; height: 18px; width: 18px;
            left: 3px; bottom: 3px; background-color: white;
            transition: .4s; border-radius: 50%;
        }
        input:checked + .slider { background-color: #2196F3; }
        input:checked + .slider:before { transform: translateX(22px); }

        /* Tombol Login/Logout */
        .btn-action { 
            padding: 12px; font-size: 1rem; border: none; 
            border-radius: 10px; cursor: pointer; width: 100%; 
            font-weight: bold; margin-top: 10px; color: white;
        }
        .btn-login { background: #4285F4; }
        .btn-logout { background: #95a5a6; margin-top: 20px; }
        
        .hide { display: none !important; }

/* --- TAMBAHAN CSS MENU ZOOM --- */
.card {
    position: relative; /* Wajib ada agar menu menempel di dalam kartu */
}

.menu-wrapper {
    position: absolute;
    top: 20px;
    right: 20px;
    z-index: 100;
}

.hamburger-btn {
    background: transparent;
    border: none;
    font-size: 26px;
    cursor: pointer;
    color: #555;
    line-height: 1;
    padding: 0;
    margin: 0;
}

.hamburger-btn:hover { color: #2196F3; }

.zoom-dropdown {
    display: none;
    position: absolute;
    top: 35px;
    right: 0;
    background: white;
    border: 1px solid #ddd;
    border-radius: 8px;
    box-shadow: 0 4px 15px rgba(0,0,0,0.15);
    padding: 12px;
    width: 150px;
    text-align: left;
    z-index: 101;
}

.show-menu { display: block !important; }

.zoom-dropdown select {
    width: 100%;
    padding: 6px;
    margin-top: 5px;
    border-radius: 5px;
    border: 1px solid #ccc;
}
    </style>
</head>
<body>

    <div class="card">
<div class="menu-wrapper">
            <button class="hamburger-btn" onclick="toggleZoomMenu()">☰</button>
            <div id="zoom-menu-box" class="zoom-dropdown">
                <label style="font-size: 0.85rem; font-weight: bold;">Ukuran Layar:</label>
                <select id="zoom-level" onchange="setZoom(this.value)">
                    <option value="0.5">Level 1 (50%)</option>
                    <option value="0.6">Level 2 (60%)</option>
                    <option value="0.7">Level 3 (70%)</option>
                    <option value="0.8">Level 4 (80%)</option>
                    <option value="0.9">Level 5 (90%)</option>
                    <option value="1.0" selected>Level 6 (Normal)</option>
                    <option value="1.1">Level 7 (110%)</option>
                    <option value="1.2">Level 8 (120%)</option>
                </select>
            </div>
        </div>
        <h2>🎛️ Atur Menu Promo</h2>
        
        <div id="login-area">
            <p>Login sebagai Admin untuk mengatur.</p>
            <button class="btn-action btn-login" onclick="loginGoogle()">Login Google</button>
        </div>

        <div id="control-area" class="hide">
            
            <p style="font-size: 0.85rem; color:#888; margin-bottom:5px;">SAKLAR UTAMA (Semua Promo)</p>
            <div id="status-display" class="status-indicator active-off" onclick="toggleMaster()" style="cursor: pointer;">
                <span id="icon-status">⭕</span> <span id="text-status">MATI</span>
            </div>

            <div class="item-list">

                <div class="category-title" style="color: #7f8c8d;">PAKET SILVER</div>
                
                <div class="item-row">
                    <div><span class="item-name">100 Kunci Silver</span><span class="item-price">Rp 2.950.000</span></div>
                    <label class="switch"><input type="checkbox" id="chk_promo_silver_100" onchange="toggleItem('promo_silver_100')"><span class="slider"></span></label>
                </div>
                <div class="item-row">
                    <div><span class="item-name">50 Kunci Silver</span><span class="item-price">Rp 1.480.000</span></div>
                    <label class="switch"><input type="checkbox" id="chk_promo_silver_50" onchange="toggleItem('promo_silver_50')"><span class="slider"></span></label>
                </div>
                <div class="item-row">
                    <div><span class="item-name">20 Kunci Silver</span><span class="item-price">Rp 600.000</span></div>
                    <label class="switch"><input type="checkbox" id="chk_promo_silver_20" onchange="toggleItem('promo_silver_20')"><span class="slider"></span></label>
                </div>
                <div class="item-row">
                    <div><span class="item-name">10 Kunci Silver</span><span class="item-price">Rp 310.000</span></div>
                    <label class="switch"><input type="checkbox" id="chk_promo_silver_10" onchange="toggleItem('promo_silver_10')"><span class="slider"></span></label>
                </div>
                <div class="item-row">
                    <div><span class="item-name">5 Kunci Silver</span><span class="item-price">Rp 165.000</span></div>
                    <label class="switch"><input type="checkbox" id="chk_promo_silver_5" onchange="toggleItem('promo_silver_5')"><span class="slider"></span></label>
                </div>
                <div class="item-row">
                    <div><span class="item-name">1 Kunci Silver</span><span class="item-price">Rp 35.000</span></div>
                    <label class="switch"><input type="checkbox" id="chk_promo_silver_1" onchange="toggleItem('promo_silver_1')"><span class="slider"></span></label>
                </div>


                <div class="category-title" style="color: #f39c12;">PAKET GOLD</div>

                <div class="item-row">
                    <div><span class="item-name">70 Kunci Gold</span><span class="item-price">Rp 5.000.000</span></div>
                    <label class="switch"><input type="checkbox" id="chk_promo_gold_70" onchange="toggleItem('promo_gold_70')"><span class="slider"></span></label>
                </div>
                <div class="item-row">
                    <div><span class="item-name">50 Kunci Gold</span><span class="item-price">Rp 3.700.000</span></div>
                    <label class="switch"><input type="checkbox" id="chk_promo_gold_50" onchange="toggleItem('promo_gold_50')"><span class="slider"></span></label>
                </div>
                <div class="item-row">
                    <div><span class="item-name">10 Kunci Gold</span><span class="item-price">Rp 760.000</span></div>
                    <label class="switch"><input type="checkbox" id="chk_promo_gold_10" onchange="toggleItem('promo_gold_10')"><span class="slider"></span></label>
                </div>
                <div class="item-row">
                    <div><span class="item-name">5 Kunci Gold</span><span class="item-price">Rp 410.000</span></div>
                    <label class="switch"><input type="checkbox" id="chk_promo_gold_5" onchange="toggleItem('promo_gold_5')"><span class="slider"></span></label>
                </div>
                <div class="item-row">
                    <div><span class="item-name">1 Kunci Gold</span><span class="item-price">Rp 85.000</span></div>
                    <label class="switch"><input type="checkbox" id="chk_promo_gold_1" onchange="toggleItem('promo_gold_1')"><span class="slider"></span></label>
                </div>

                <div class="category-title" style="color: #00a8ff;">PAKET DIAMOND</div>

                <div class="item-row">
                    <div><span class="item-name">25 Kunci Diamond</span><span class="item-price">Rp 5.300.000</span></div>
                    <label class="switch"><input type="checkbox" id="chk_promo_diamond_25" onchange="toggleItem('promo_diamond_25')"><span class="slider"></span></label>
                </div>
                <div class="item-row">
                    <div><span class="item-name">15 Kunci Diamond</span><span class="item-price">Rp 3.250.000</span></div>
                    <label class="switch"><input type="checkbox" id="chk_promo_diamond_15" onchange="toggleItem('promo_diamond_15')"><span class="slider"></span></label>
                </div>
                <div class="item-row">
                    <div><span class="item-name">10 Kunci Diamond</span><span class="item-price">Rp 2.200.000</span></div>
                    <label class="switch"><input type="checkbox" id="chk_promo_diamond_10" onchange="toggleItem('promo_diamond_10')"><span class="slider"></span></label>
                </div>
                <div class="item-row">
                    <div><span class="item-name">5 Kunci Diamond</span><span class="item-price">Rp 1.150.000</span></div>
                    <label class="switch"><input type="checkbox" id="chk_promo_diamond_5" onchange="toggleItem('promo_diamond_5')"><span class="slider"></span></label>
                </div>
                <div class="item-row">
                    <div><span class="item-name">1 Kunci Diamond</span><span class="item-price">Rp 250.000</span></div>
                    <label class="switch"><input type="checkbox" id="chk_promo_diamond_1" onchange="toggleItem('promo_diamond_1')"><span class="slider"></span></label>
                </div>

            </div>

<button class="btn-action btn-logout" onclick="logout()">Logout</button>
        </div> </div> <script>
        function setZoom(val) {
            document.body.style.zoom = val;
            localStorage.setItem('adminPromoZoom', val);
        }

        function toggleZoomMenu() {
            document.getElementById('zoom-menu-box').classList.toggle('show-menu');
        }

        window.onload = function() {
            const savedZoom = localStorage.getItem('adminPromoZoom') || "1.0";
            document.body.style.zoom = savedZoom;
            
            const selectBox = document.getElementById('zoom-level');
            if(selectBox) {
                selectBox.value = savedZoom;
            }
        }
    </script>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getAuth, signInWithPopup, GoogleAuthProvider, onAuthStateChanged, signOut } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-auth.js";
        import { getDatabase, ref, onValue, set, update } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";

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

        const MY_ADMIN_UID = "G6N2sLEF6vX0e3X9ndbmft1oHVg2"; // PASTIKAN INI UID ADMIN YANG BENAR

        let masterStatus = false;

        window.loginGoogle = () => signInWithPopup(auth, provider);
        window.logout = () => signOut(auth).then(() => location.reload());

        onAuthStateChanged(auth, (user) => {
            if (user && user.uid === MY_ADMIN_UID) {
                document.getElementById('login-area').classList.add('hide');
                document.getElementById('control-area').classList.remove('hide');
                startListening();
            } else if (user) {
                alert("Akses Ditolak: Anda bukan Admin!"); signOut(auth);
            }
        });

        function startListening() {
            // 1. Dengar Master Switch
            onValue(ref(db, 'config/promo_active'), (snap) => {
                masterStatus = snap.val() === true;
                updateMasterUI(masterStatus);
            });

            // 2. Dengar Item Switches (Semua Item)
            onValue(ref(db, 'config/promo_items'), (snap) => {
                const items = snap.val() || {};
                
                // Daftar semua ID yang harus dicek statusnya
                const allKeys = [
                    'promo_silver_100', 'promo_silver_50', 'promo_silver_20', 'promo_silver_10', 'promo_silver_5', 'promo_silver_1',
                    'promo_gold_70', 'promo_gold_50', 'promo_gold_10', 'promo_gold_5', 'promo_gold_1',
                    'promo_diamond_25', 'promo_diamond_15', 'promo_diamond_10', 'promo_diamond_5', 'promo_diamond_1'
                ];

                // Loop otomatis untuk update checkbox UI
                allKeys.forEach(key => {
                    const el = document.getElementById('chk_' + key);
                    if (el) {
                        el.checked = items[key] === true;
                    }
                });
            });
        }

        function updateMasterUI(status) {
            const display = document.getElementById('status-display');
            const icon = document.getElementById('icon-status');
            const text = document.getElementById('text-status');

            if (status) {
                display.className = "status-indicator active-on";
                icon.innerText = "✅"; text.innerText = "ON (MENYALA)";
            } else {
                display.className = "status-indicator active-off";
                icon.innerText = "⭕"; text.innerText = "OFF (MATI)";
            }
        }

        // Toggle Saklar Utama
        window.toggleMaster = () => {
            set(ref(db, 'config/promo_active'), !masterStatus);
        };

        // Toggle Per Item
        window.toggleItem = (itemId) => {
            const el = document.getElementById('chk_' + itemId);
            if(el) {
                const isChecked = el.checked;
                // Update spesifik item di database
                set(ref(db, `config/promo_items/${itemId}`), isChecked);
            }
        };
    </script>
</body>
</html>
