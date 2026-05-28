# Chessbridge ♟️

Chessbridge is a low-latency Chrome extension that acts as a real-time bridge between Chess.com and your local Searchless Chess Transformer AI (the M4 engine). It streams the game board state over WebSockets and physically highlights the AI's recommended moves directly on the browser board.

## How to Run This from Scratch

This pipeline requires two components to run: the **Backend Server (Searchless Chess)** and the **Frontend Extension (Chessbridge)**.

### 1. Start the Searchless Chess Backend
The backend engine runs inside a Jupyter Notebook and hosts a WebSocket server on port 8000.
1. Open your Mac Terminal.
2. Activate your conda environment and start Jupyter Notebook:
   ```bash
   conda activate searchless
   cd /Users/shanesarosh/searchless_chess/src
   jupyter notebook
   ```
3. A new tab will open in Google Chrome showing the Jupyter directory.
4. Click on **`searchless_chess.ipynb`**.
5. *Important Fix:* Ensure the very first cell contains:
   ```python
   import sys
   sys.path.append("/Users/shanesarosh/")
   ```
6. Click **Kernel -> Restart & Run All** in the top menu bar.
7. Scroll to the bottom of the notebook—it takes a few seconds to load the neural network weights into memory. You should eventually see `🚀 Stream Engine running on ws://127.0.0.1:8000`. Leave this tab open in the background.

### 2. Load the Chessbridge Extension
1. Open a new tab in Google Chrome and go to `chrome://extensions/`.
2. Ensure **Developer mode** is toggled ON (top right corner).
3. Click the **Load unpacked** button (top left).
4. Select the `chessbridge` folder located at `/Users/shanesarosh/Desktop/chessbridge`.

### 3. Play!
1. Open a new tab and go to [Chess.com/play/computer](https://www.chess.com/play/computer).
2. As soon as the page loads, the extension will automatically connect to your Jupyter WebSocket server. 
3. When it is your opponent's turn, it silently streams the FEN position to warm up the cache (`speculate`).
4. When your opponent completes their turn, the engine instantly computes the best move and highlights the "from" and "to" squares on your board in **orange** and **green**.
