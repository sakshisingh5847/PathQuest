# Pathfinding Visualizer

An interactive, grid-based web app that shows you **how pathfinding algorithms think**. Draw walls, drag the start and target nodes anywhere on the board, hit "Visualize!", and watch the algorithm explore the grid node-by-node before drawing the shortest path.

Built with vanilla JavaScript and a tiny Express server.

---

## ✨ Features

- **Interactive grid** — click and drag to draw walls, or hold **W** and drag to place weighted nodes.
- **Draggable start, target, and bomb node** — pick them up and drop them anywhere on the board; if an algorithm has already run, it re-runs automatically.
- **4 pathfinding algorithms, implemented:**
  - 🔵 **Dijkstra's Algorithm** (weighted) — always finds the shortest path.
  - 🟢 **Greedy Best-First Search** (weighted) — fast, but doesn't guarantee the shortest path.
  - 🟡 **Breadth-First Search / BFS** (unweighted) — guarantees the shortest path.
  - 🔴 **Depth-First Search / DFS** (unweighted) — explores deeply first, does *not* guarantee the shortest path.
- **Step-by-step animation** — every visited node and the final shortest path animate in real time, with three speed options (Fast / Average / Slow).
- **Bomb node** — force the path to pass through an extra node before reaching the target.

## 🖼️ How It Works (Quick Tour)

1. **Pick an algorithm** from the "Algorithms" dropdown.
2. **Draw walls** by clicking and dragging on empty squares.
3. *(Optional)* Hold **W** while dragging to paint weighted nodes instead of walls.
4. *(Optional)* Click "Add Bomb" to place a node the path must pass through.
5. Hit **Visualize!** and watch the algorithm search the grid.
6. Use **Clear Path**, **Clear Walls & Weights**, or **Clear Board** to reset and try again.

## 🛠️ Tech Stack

| Layer      | Tool/Library                          |
|------------|----------------------------------------|
| Server     | Node.js + Express                      |
| Frontend   | Vanilla JavaScript, jQuery, Bootstrap 3 |
| Bundling   | Browserify + Watchify                  |
| Rendering  | Plain HTML `<table>` grid + CSS classes |

## 📂 Project Structure

```
├── index.html                  # Main HTML page (loads the compiled bundle)
├── server.js                   # Express server — serves index.html and static files
├── board.js                    # Core app logic — grid, drag events, UI wiring
├── node.js                     # Node "class" — data structure for a single grid cell
├── getDistance.js              # Direction/turn helper used for path arrow rendering
├── pathfindingAlgorithms/
│   ├── weightedSearchAlgorithm.js    # Dijkstra, Greedy Best-First, A*-style search
│   └── unweightedSearchAlgorithm.js  # BFS and DFS
├── animations/
│   └── launchAnimations.js     # Timed animation of the search + shortest path
├── public/browser/bundle.js    # Browserify-bundled output actually loaded by the browser
├── package.json / package-lock.json   # Dependencies & npm scripts
└── .gitignore                  # Files Git should ignore
```

## 🚀 Getting Started

### Prerequisites
- [Node.js](https://nodejs.org/) installed (comes with npm)

### Installation & Running

```bash
# 1. Clone the repository
git clone <your-repo-url>
cd pathfinding-visualizer

# 2. Install dependencies
npm install

# 3. Start the server
npm start
```

The app will be running at **http://localhost:1337**.

### Rebuilding the frontend bundle

The browser only loads `public/browser/bundle.js`, which is a **Browserify bundle** compiled from `board.js` and everything it `require()`s. If you edit `board.js` or any file it depends on, rebuild the bundle with:

```bash
npm run watch
```

## 🧠 Algorithm Notes

| Algorithm | Weighted? | Guarantees Shortest Path? | Search Style |
|-----------|-----------|----------------------------|--------------|
| Dijkstra's Algorithm | ✅ | ✅ | Explores outward evenly by distance |
| Greedy Best-First Search | ✅ | ❌ | Always moves toward the target — fast but can be misled |
| Breadth-First Search (BFS) | ❌ | ✅ | Explores in expanding "rings" from the start |
| Depth-First Search (DFS) | ❌ | ❌ | Dives down one path as far as possible before backtracking |
