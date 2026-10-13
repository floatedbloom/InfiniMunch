# InfiniMunch

A real-time multiplayer browser game where each player controls a fleet of minions. When fleets collide, the stronger name wins: Gemini judges the names when an API key is set, and the game uses a random winner otherwise. The winning fleet takes over the losing minion.

## Run locally

The Python server serves both the game and its Socket.IO connection. From the repository root:

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r backend/requirements.txt
cd backend
python server.py
```

Open <http://localhost:5000>. Enter a name, then move the mouse to steer your fleet. If your fleet is eliminated, choose a new name to respawn.

For Gemini-powered collisions, set `GEMINI_API_KEY` in the environment or in `backend/.env` before starting the server. Without it, collisions still work using the random fallback. Name pairs and their results are cached in `backend/cache.json`; player names are sent to Gemini when the API is used.

## Code

- `backend/server.py`: game state, collisions, Socket.IO events, and static file serving.
- `backend/ai.py`: Gemini decisions, name checks, and the local collision cache.
- `backend/frontend/`: browser UI, canvas renderer, and assets.
- `backend/requirements.txt`: Python dependencies used by the server.
