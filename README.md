<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Catch the Falling Object Game</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <h1>Catch the Falling Object Game</h1>
    <p>Use the left and right arrow keys to move and catch the falling items!</p>
    <div id="game-area">
        <div id="catcher"></div>
        <div id="falling-item"></div>
    </div>
    <p id="score">Score: 0</p>

    <script src="script.js"></script>
</body>
</html>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    font-family: Arial, sans-serif;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    height: 100vh;
    background-color: #f4f4f9;
}

#game-area {
    position: relative;
    width: 400px;
    height: 500px;
    border: 2px solid #333;
    background-color: #e0e0e0;
    overflow: hidden;
}

#catcher {
    position: absolute;
    bottom: 10px;
    width: 60px;
    height: 20px;
    background-color: #333;
    left: 170px;
}

#falling-item {
    position: absolute;
    width: 20px;
    height: 20px;
    background-color: #ff6347;
    top: 0;
    left: 50%;
    transform: translateX(-50%);
}

h1, p {
    margin-bottom: 20px;
}

#score {
    font-size: 1.2rem;
    margin-top: 10px;
}
// Select game elements
const gameArea = document.getElementById('game-area');
const catcher = document.getElementById('catcher');
const fallingItem = document.getElementById('falling-item');
const scoreDisplay = document.getElementById('score');

// Variables to track game state
let score = 0;
let catcherPosition = 170;
let itemPosition = { top: 0, left: Math.random() * 380 };

// Update the falling item's position
function updateFallingItem() {
    itemPosition.top += 5;
    if (itemPosition.top > 480) {
        // Check if the catcher caught the item
        if (itemPosition.left >= catcherPosition && itemPosition.left <= catcherPosition + 60) {
            score++;
            scoreDisplay.textContent = `Score: ${score}`;
        }
        // Reset falling item
        itemPosition.top = 0;
        itemPosition.left = Math.random() * 380;
    }
    fallingItem.style.top = itemPosition.top + 'px';
    fallingItem.style.left = itemPosition.left + 'px';
}

// Move catcher left and right
document.addEventListener('keydown', (event) => {
    if (event.key === 'ArrowLeft' && catcherPosition > 0) {
        catcherPosition -= 20;
    }
    if (event.key === 'ArrowRight' && catcherPosition < 340) {
        catcherPosition += 20;
    }
    catcher.style.left = catcherPosition + 'px';
});

// Game loop to keep the game running
function gameLoop() {
    updateFallingItem();
    requestAnimationFrame(gameLoop);
}

// Start the game loop
gameLoop();
