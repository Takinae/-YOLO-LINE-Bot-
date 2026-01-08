# -YOLO-LINE-Bot-
本專題系統主要應用於校園內人潮容易聚集的場域，例如學生餐廳、影印區、公共服務櫃檯等。透過架設攝影設備與嵌入式系統，即可即時偵測現場人數，並將結果提供給場域管理者進行人流掌握，同時讓一般使用者能透過 LINE 平台查詢即時人數，作為是否前往該場域的參考依據。
📊 AIoT 校園人流即時監測系統

AIoT-based Real-time People Counting System for Campus

📌 專題簡介

本專題利用 Raspberry Pi 搭配 AI 影像辨識技術（YOLO），建置一套低成本且具即時性的人流偵測系統。
系統可自動偵測畫面中的人數，並透過 MQTT 進行資料傳輸，最後整合 LINE Bot，讓使用者能即時查詢目前場域的人流狀況。

適用場域包含校園餐廳、影印區與其他人潮易聚集之公共空間。

🧱 系統架構

硬體平台：Raspberry Pi 5 + Camera Module

影像辨識：YOLOv8（Person Detection）

通訊協定：MQTT

即時通訊：LINE Messaging API

後端服務：Python + Flask

📂 專案目錄結構
.
├── yolo_people_mqtt.py        # YOLO 人流偵測與 MQTT 發送
├── line_bot_people.py         # LINE Bot（接收 MQTT 人數）
├── .env                       # LINE Bot Token 設定
├── requirements.txt           # Python 套件清單
└── README.md

⚙️ 環境需求

Raspberry Pi OS (Debian Bookworm)

Python 3.9 以上

Raspberry Pi Camera 已啟用

已安裝 Mosquitto MQTT Broker

📦 套件安裝
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt

requirements.txt 範例
ultralytics
opencv-python
paho-mqtt
flask
python-dotenv
line-bot-sdk

📷 相機測試

確認相機正常運作：

rpicam-hello

▶️ 系統執行流程
Step 1️⃣ 啟動 MQTT Broker
sudo systemctl start mosquitto

Step 2️⃣ 執行 YOLO 人流偵測（發布人數）
python yolo_people_mqtt.py


成功後終端機會顯示：

PUB: {'people': 3, 'ts': 1712345678}

Step 3️⃣ 設定 LINE Bot 環境變數

建立 .env 檔案：

LINE_CHANNEL_ACCESS_TOKEN=你的_TOKEN
LINE_CHANNEL_SECRET=你的_SECRET
PORT=5001

Step 4️⃣ 啟動 LINE Bot
python line_bot_people.py

💬 LINE Bot 使用方式

在 LINE 聊天室輸入以下指令：

指令	功能
people	查詢目前即時人數
help	顯示指令說明
📊 系統成果

即時偵測畫面中的人數

自動發布人數至 MQTT Topic

LINE Bot 可即時回傳人數資訊

系統低成本、具擴充性

⚠️ 注意事項

YOLO 偵測效能與影像解析度有關，建議使用 640×480

建議於光線充足環境下使用以提升準確率

若系統重啟，請依序重新啟動 MQTT、YOLO、LINE Bot
