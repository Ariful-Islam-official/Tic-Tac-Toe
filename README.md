# Tic Tac Toe Game

This project is a simple **Tic Tac Toe game** built using HTML, CSS, and JavaScript. The game includes a user-friendly interface and allows two players to play alternately. The game announces the winner and provides an option to reset or start a new game.

## Features
- Two-player functionality with alternating turns.
- Highlights the winning player.
- Allows resetting the game board.
- Responsive design for a better user experience.

## Table of Contents
1. [HTML Code](#html-code)
2. [CSS Code](#css-code)
3. [JavaScript Code](#javascript-code)
4. [Explanation](#explanation)
   - [HTML Structure](#html-structure)
   - [CSS Styling](#css-styling)
   - [JavaScript Logic](#javascript-logic)
5. [How to Run](#how-to-run)

---

## HTML Code
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tic Tac Toe Game</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <div class="msg-container hide">
        <p id="msg"></p>
        <button id="new">New Game</button>
    </div>
    <main>
        <h1>Tic Tac Toe</h1>
        <div class="container">
            <div class="game">
                <button class="box"></button>
                <button class="box"></button>
                <button class="box"></button>
                <button class="box"></button>
                <button class="box"></button>
                <button class="box"></button>
                <button class="box"></button>
                <button class="box"></button>
                <button class="box"></button>
            </div>
        </div>
        <button id="reset">Reset Game</button>
    </main>
    <script src="tic_tac.js"></script>
</body>
</html>
```
### Explanation
1. **`<head>`**:
   - Includes metadata, title, and a link to the external CSS file.
2. **Message Container (`div.msg-container`)**:
   - Displays the winning message and a button for starting a new game.
3. **Game Board (`div.game`)**:
   - Contains 9 buttons representing the Tic Tac Toe grid.
4. **Reset Button (`#reset`)**:
   - Resets the game without a winning message.

---

## CSS Code
```css
* {
    margin: 0;
    padding: 0;
}
body {
    background-color: #548687;
    text-align: center;
}
.container {
    height: 70vh;
    display: flex;
    justify-content: center;
    align-items: center;
}
.game {
    height: 60vmin;
    width: 60vmin;
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    align-items: center;
    gap: 1.5vmin;
}
.box {
    height: 18vmin;
    width: 18vmin;
    border-radius: 1rem;
    border: none;
    box-shadow: 0 0 1rem rgba(0, 0, 0, 0.3);
    font-size: 8vmin;
    color: #b0413e;
}
#reset, #new {
    border-radius: 0.5rem;
    padding: 20px;
    border: none;
    box-shadow: 0 0 1rem rgba(0, 0, 0, 0.3);
    font-size: 2vmin;
    font-weight: bold;
    color: #000000;
}
#msg {
    color: white;
    font-size: 5vmin;
}
.msg-container {
    height: 100vmin;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    gap: 4rem;
}
.hide {
    display: none;
}
```
### Explanation
1. **Global Styles**:
   - Reset margins and padding for all elements.
2. **Body Styling**:
   - Background color and centered text.
3. **Game Grid**:
   - Flexbox layout for aligning buttons.
   - Styling for buttons with shadows and rounded corners.
4. **Message Container**:
   - Flexbox for centering the message.

---

## JavaScript Code
```javascript
let boxes = document.querySelectorAll(".box");
let resetBtn = document.querySelector("#reset");
let newGameBtn = document.querySelector("#new");
let msgContainer = document.querySelector(".msg-container");
let msg = document.querySelector("#msg");

let turnO = true;
let winPatterns = [
    [0, 1, 2], [0, 3, 6], [0, 4, 8], [1, 4, 7],
    [2, 5, 8], [2, 4, 6], [3, 4, 5], [6, 7, 8]
];

boxes.forEach((box) => {
    box.addEventListener("click", () => {
        if (turnO) {
            box.innerText = "O";
            turnO = false;
        } else {
            box.innerText = "X";
            turnO = true;
        }
        box.disabled = true;
        checkWinner();
    });
});

const checkWinner = () => {
    for (let pattern of winPatterns) {
        let pos1val = boxes[pattern[0]].innerText;
        let pos2val = boxes[pattern[1]].innerText;
        let pos3val = boxes[pattern[2]].innerText;

        if (pos1val !== "" && pos2val !== "" && pos3val !== "") {
            if (pos1val === pos2val && pos2val === pos3val) {
                showWinner(pos1val);
            }
        }
    }
};

const showWinner = (winner) => {
    msg.innerText = `Congratulations, Winner is ${winner}`;
    msgContainer.classList.remove("hide");
    disableBoxes();
};

const disableBoxes = () => {
    boxes.forEach((box) => box.disabled = true);
};

const enableBoxes = () => {
    boxes.forEach((box) => {
        box.disabled = false;
        box.innerText = "";
    });
};

const resetGame = () => {
    turnO = true;
    enableBoxes();
    msgContainer.classList.add("hide");
};

resetBtn.addEventListener("click", resetGame);
newGameBtn.addEventListener("click", resetGame);
```
### Explanation
1. **Selecting Elements**:
   - Use `querySelector` and `querySelectorAll` to get DOM elements like boxes, reset button, and message container.
2. **Turn Management**:
   - Use a `turnO` boolean to alternate between `O` and `X` turns.
3. **Check Winner**:
   - Loop through predefined winning patterns.
   - Check if three boxes in any pattern contain the same value.
4. **Display Winner**:
   - Show a congratulatory message and disable all boxes.
5. **Reset Game**:
   - Clear all boxes, reset turns, and hide the message container.

---

## How to Run
1. Save the provided code into three separate files:
   - `index.html`
   - `style.css`
   - `tic_tac.js`
2. Open the `index.html` file in your browser.
3. Play the game by clicking on the boxes and alternating turns.
4. Use the **Reset** or **New Game** button to restart the game.
