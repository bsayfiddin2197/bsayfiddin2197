# =========================
# ⚡ SAYFIDDIN GOD API ⚡
# =========================

from fastapi import FastAPI
from fastapi.responses import Response
from datetime import datetime
import requests

app = FastAPI()

GITHUB_USERNAME = "USERNAME"   # 🔥 o'zgartir
CITY = "Tashkent"

# =========================
# 🏠 HOME
# =========================
@app.get("/")
def home():
    return {"message": "🚀 Sayfiddin GOD API ishlayapti"}

# =========================
# 🧠 SYSTEM INFO
# =========================
@app.get("/system")
def system():
    return {
        "user": "Sayfiddin",
        "role": "AI Backend Dev",
        "status": "ONLINE ⚡",
        "time": datetime.now().strftime("%Y-%m-%d %H:%M:%S")
    }

# =========================
# 📊 GITHUB DATA
# =========================
@app.get("/github")
def github():
    url = f"https://api.github.com/users/{GITHUB_USERNAME}"
    data = requests.get(url).json()

    return {
        "followers": data.get("followers"),
        "repos": data.get("public_repos"),
        "profile": data.get("html_url")
    }

# =========================
# 🌍 WEATHER
# =========================
@app.get("/weather")
def weather():
    url = f"https://wttr.in/{CITY}?format=j1"
    data = requests.get(url).json()

    return {
        "city": CITY,
        "temp": data["current_condition"][0]["temp_C"],
        "desc": data["current_condition"][0]["weatherDesc"][0]["value"]
    }

# =========================
# 🤖 AI FAKE TEXT
# =========================
@app.get("/ai")
def ai():
    return {
        "thought": "Learning new patterns...",
        "status": "EVOLVING 🚀"
    }

# =========================
# 🎨 SVG BADGE (REAL MAGIC)
# =========================
@app.get("/badge")
def badge():
    now = datetime.now().strftime("%H:%M:%S")

    svg = f"""
    <svg width="420" height="140" xmlns="http://www.w3.org/2000/svg">
        <style>
            .title {{ fill: #00ff00; font-size: 20px; font-family: monospace; }}
            .text {{ fill: #ffffff; font-size: 14px; font-family: monospace; }}
        </style>

        <rect width="100%" height="100%" fill="black"/>

        <text x="20" y="30" class="title">⚡ SAYFIDDIN OS ⚡</text>
        <text x="20" y="60" class="text">Status: ONLINE</text>
        <text x="20" y="85" class="text">Mode: GOD MODE 😈</text>
        <text x="20" y="110" class="text">Time: {now}</text>
    </svg>
    """

    return Response(content=svg, media_type="image/svg+xml")

# =========================
# 🔥 FULL DASHBOARD SVG
# =========================
@app.get("/dashboard")
def dashboard():
    now = datetime.now().strftime("%H:%M:%S")

    # GitHub API
    url = f"https://api.github.com/users/{GITHUB_USERNAME}"
    data = requests.get(url).json()

    followers = data.get("followers", 0)
    repos = data.get("public_repos", 0)

    svg = f"""
    <svg width="500" height="200" xmlns="http://www.w3.org/2000/svg">
        <style>
            .title {{ fill: #00ffcc; font-size: 22px; font-family: monospace; }}
            .text {{ fill: #ffffff; font-size: 14px; font-family: monospace; }}
        </style>

        <rect width="100%" height="100%" fill="#0d1117"/>

        <text x="20" y="40" class="title">🚀 SAYFIDDIN DASHBOARD</text>

        <text x="20" y="80" class="text">Followers: {followers}</text>
        <text x="20" y="105" class="text">Repos: {repos}</text>
        <text x="20" y="130" class="text">Time: {now}</text>
        <text x="20" y="155" class="text">Status: ONLINE ⚡</text>
    </svg>
    """

    return Response(content=svg, media_type="image/svg+xml")
