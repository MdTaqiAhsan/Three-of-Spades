# 🃏 Three of Spades (Kaali ki Teeggi) — Real-Time Multiplayer Web Game

A robust, full-stack, real-time multiplayer implementation of the classic Indian trick-taking card game **Kaali ki Teeggi** (popularly known here as **Three of Spades**). Built using a Python backend and a vanilla JavaScript frontend, this application transitions the strategic complexity of a traditional physical card game into a seamless, secure, web-based multiplayer experience.

## 🚀 Key Features

### 🎮 Game Mechanics & Strategy

* **Dynamic, Hidden Teams:** The core thrill of the game—teams are completely fluid and changing every single round. The highest bidder selects specific cards from the deck; whoever holds those cards becomes a secret teammate, revealed *only* at the end of the round through strategic gameplay.
* **The 3 of Spades Bounty:** A custom point-distribution matrix featuring a special high-value target—the **3 of Spades** is worth an elusive 30 points, completely shifting standard trick-taking dynamics.
* **Strict Trick Resolution Rules:** A complete server-side evaluation engine mapping complex trump card overrides, led-suit obligations, and off-suit discards.

### 🛠️ Technical Architecture & Security

* **Zero-Trust, Server-Driven State:** To prevent client-side memory sniffing or cheating via the browser console, **all game state, deck tracking, and move validations are isolated strictly on the server**.
* **Granular State Serialization:** The server utilizes a dual-state distribution pipeline:
* `public_state()`: Broadcasts non-sensitive room data (current trick, scores, current turn) to the entire lobby.
* `private_state(player_name)`: Serializes and emits specific card arrays strictly to individual WebSocket channels, ensuring a player can *never* access another player's hand via data inspection.


* **Scalable Multi-Room Manager:** Includes an isolated concurrency wrapper (`RoomManager`) allowing multiple independent game sessions to run simultaneously on a single server instance without state cross-contamination.
* **Graceful Session Cleanup:** Real-time disconnection hooks automatically handle mid-game dropouts, purge stale client cards, and immediately clear memory when rooms become empty.

---

## 💻 Tech Stack

* **Backend Engine:** Python, Flask, Flask-SocketIO (WebSocket protocol for real-time bidirectional event handling).
* **Frontend Interface:** Vanilla HTML5, CSS3 (including a responsive, circular virtual card table layout), and pure asynchronous JavaScript—designed completely around event-driven socket listeners without heavy framework overhead.
* **Asset Pipeline:** Integrated dynamically with the *Deck of Cards API* mapping card serialization types into modern graphic layouts (`KH.png`, `0C.png`, etc.).
* **Production Deployment:** Configured natively for production-ready containerized architectures using a customized `render.yaml` orchestration file via **Gunicorn** utilizing asynchronous **eventlet** workers.

---

## 📂 Repository File Hierarchy

```text
ThreeOfSpades/
├── server.py              # Flask-SocketIO entry point; routes WebSocket events & translations
├── game_state.py          # Core game engine logic, state machines, and RoomManager wrapper
├── game/
│   ├── cards.py           # Card model, points matrix definitions, and deck generation logic
│   └── bidder.py          # Historical terminal-based validation logic for auction bids
├── templates/
│   └── index.html         # Single-page interface container holding all UI phase screens
├── static/
│   ├── game.js            # Frontend DOM manipulator driven natively by socket updates
│   ├── style.css          # Game board aesthetics, dark mode table styling, and asset positioning
│   └── cards/             # Serialized playing card graphical assets
├── requirements.txt       # Python environment dependencies
└── render.yaml            # Web Service infrastructure deployment blueprint

```

---

## 🛠️ Local Installation & Development

1. **Clone the repository:**
```bash
git clone https://github.com/YOUR_USERNAME/ThreeOfSpades.git
cd ThreeOfSpades

```


2. **Install dependencies:**
```bash
pip install -r requirements.txt

```


3. **Run the local development server:**
```bash
python server.py

```


4. Open `http://localhost:5000` in multiple browser tabs to simulate and test local multiplayer sessions.

---

### 📝 Project Background

*Developed iteratively, moving from a standard terminal-based pass-and-play CLI layout (`threeofspades.py`) into a decentralized client-server web game optimized for production hosting.*

This project was done in collaboration with Saket Sharma, Aditya Mohan and Parva Chaudhary
