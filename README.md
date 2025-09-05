# Recreate the Cordova admin project ZIP because the previous one expired
import os, zipfile, shutil

base = "/mnt/data/pixel_farm_admin_project"
if os.path.exists(base):
    shutil.rmtree(base)
os.makedirs(base, exist_ok=True)

# Files
config_xml = """<?xml version='1.0' encoding='utf-8'?>
<widget id="com.pixelfarm.admin" version="0.1.0" xmlns="http://www.w3.org/ns/widgets" xmlns:cdv="http://cordova.apache.org/ns/1.0">
  <name>Pixel Farm Admin</name>
  <description>Admin APK (Cordova) for Pixel Farm - demo</description>
  <author>itzME Studio</author>
  <content src="index.html" />
  <access origin="*" />
  <platform name="android">
    <allow-intent href="market:*" />
  </platform>
</widget>
"""

index_html = """<!doctype html>
<html>
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width,initial-scale=1">
  <title>Pixel Farm Admin</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <div class="container">
    <h1>Pixel Farm — Admin</h1>
    <div id="loginBox" class="card">
      <h2>Login Admin</h2>
      <input id="pwd" type="password" placeholder="Masukkan sandi admin" />
      <button id="btnLogin">Login</button>
      <div class="hint">Sandi: <b>itzME Studio PIXEL FARM</b></div>
    </div>
    <div id="adminPanel" class="hidden">
      <div class="card">
        <h2>Kontrol Admin</h2>
        <div class="row">
          <label>Pengumuman:</label>
          <input id="announcement" placeholder="Tulis pengumuman..." />
          <button id="sendAnn">Kirim</button>
        </div>
        <div class="row">
          <label>Atur Cuaca Random:</label>
          <select id="weatherMode">
            <option value="random">Random (On)</option>
            <option value="manual">Manual (Off)</option>
          </select>
        </div>
        <div class="row">
          <label>Set Event:</label>
          <select id="eventType">
            <option value="capybara">Capybara (Pulau)</option>
            <option value="owl">Event Owl</option>
            <option value="venus">Venus Trap</option>
            <option value="tedy">Tedy</option>
          </select>
          <button id="setEvent">Atur Event</button>
        </div>
        <div class="row">
          <label>Redeem Code:</label>
          <input id="redeemCode" placeholder="CODE123" />
          <input id="redeemReward" placeholder="Hadiah (mis. 100 koin)" />
          <button id="addRedeem">Tambah Redeem</button>
        </div>
        <div class="row">
          <label>Player Name (ubah):</label>
          <input id="playerName" placeholder="Nama pemain" />
          <input id="playerNewName" placeholder="Nama baru" />
          <button id="changeName">Ganti Nama</button>
        </div>
        <h3>Log Aksi</h3>
        <pre id="log" class="logbox"></pre>
      </div>
      <button id="btnLogout" class="danger">Logout</button>
    </div>
  </div>
<script src="admin.js"></script>
</body>
</html>
"""

style_css = """*{box-sizing:border-box;font-family:Arial,Helvetica,sans-serif}
body{background:#f6f8fa;margin:0;padding:16px;color:#111}
.container{max-width:720px;margin:0 auto}
.card{background:white;padding:12px;border-radius:8px;box-shadow:0 2px 6px rgba(0,0,0,0.08);margin-bottom:12px}
.hidden{display:none}
h1{margin:0 0 8px 0}
.row{display:flex;gap:8px;align-items:center;margin:8px 0}
.row input, .row select{flex:1;padding:8px;border:1px solid #ccc;border-radius:6px}
button{padding:8px 12px;border-radius:6px;border:0;background:#2d9cdb;color:white;cursor:pointer}
button.danger{background:#e24}
.hint{font-size:12px;color:#666;margin-top:8px}
.logbox{height:150px;overflow:auto;background:#0f1720;color:#fff;padding:8px;border-radius:6px}
"""

admin_js = """const PASSWORD = "itzME Studio PIXEL FARM";
const loginBox = document.getElementById('loginBox');
const adminPanel = document.getElementById('adminPanel');
const pwd = document.getElementById('pwd');
const btnLogin = document.getElementById('btnLogin');
const btnLogout = document.getElementById('btnLogout');
const logEl = document.getElementById('log');
function log(msg){const t
