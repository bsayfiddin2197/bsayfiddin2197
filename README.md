from fastapi import FastAPI
from fastapi.responses import Response
from datetime import datetime
import requests

app = FastAPI()
USERNAME = "USERNAME"

@app.get("/")
def home():
    return {"status": "Animated GOD API 🚀"}

@app.get("/animated")
def animated():
    now = datetime.now().strftime("%H:%M:%S")

    # GitHub data
    url = f"https://api.github.com/users/{USERNAME}"
    data = requests.get(url).json()
    followers = data.get("followers", 0)
    repos = data.get("public_repos", 0)

    svg = f"""
    <svg width="600" height="220" xmlns="http://www.w3.org/2000/svg">

    <style>
        .title {{
            fill: #00ffcc;
            font-size: 24px;
            font-family: monospace;
            animation: glow 2s infinite alternate;
        }}

        .text {{
            fill: white;
            font-size: 14px;
            font-family: monospace;
        }}

        @keyframes glow {{
            from {{ opacity: 0.5; }}
            to {{ opacity: 1; }}
        }}
    </style>

    <!-- Background -->
    <rect width="100%" height="100%" fill="#0d1117"/>

    <!-- Moving bar -->
    <rect x="0" y="0" width="100" height="5" fill="#00ffcc">
        <animate attributeName="x" from="0" to="500" dur="3s" repeatCount="indefinite"/>
    </rect>

    <!-- Title -->
    <text x="20" y="40" class="title">⚡ SAYFIDDIN SYSTEM ⚡</text>

    <!-- Stats -->
    <text x="20" y="90" class="text">Followers: {followers}</text>
    <text x="20" y="115" class="text">Repos: {repos}</text>
    <text x="20" y="140" class="text">Time: {now}</text>
    <text x="20" y="165" class="text">Status: ONLINE 😈</text>

    <!-- Blinking cursor -->
    <rect x="300" y="150" width="10" height="15" fill="#00ffcc">
        <animate attributeName="opacity" values="1;0;1" dur="1s" repeatCount="indefinite"/>
    </rect>

    </svg>
    """

    return Response(content=svg, media_type="image/svg+xml")
