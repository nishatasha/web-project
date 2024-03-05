# web-project
Tic Tac Toe Game in JavaScript.

Click [here](https://nishatasha.github.io/web-project/) to have fun!

To create this program [Tic Tac Toe Game] 

First, you need to create three files, ``` HTML ``` File, ```CSS``` File, and ```JavaScript``` File. 

After creating these files just paste those following codes into your files.

For ```HTML```  [index.html](https://github.com/nishatasha/web-project/blob/ebb8b9775a6082e67c494c9fc5ad6e468db8f9dd/index.html)

For ```CSS```  [index.css](https://github.com/nishatasha/web-project/blob/ebb8b9775a6082e67c494c9fc5ad6e468db8f9dd/assets/style/index.css)

For ```JavaScript```

``` JavaScript
const selectBox = document.querySelector(".select-box"),
    selectBtnX = selectBox.querySelector(".options .playerX"),
    selectBtnO = selectBox.querySelector(".options .playerO"),
    playBoard = document.querySelector(".play-board"),
    players = document.querySelector(".players"),
    allBox = document.querySelectorAll("section span"),
    resultBox = document.querySelector(".result-box"),
    wonText = resultBox.querySelector(".won-text"),
    replayBtn = resultBox.querySelector("button");

window.onload = () => {
    for (let i = 0; i < allBox.length; i++) {
       allBox[i].setAttribute("onclick", "clickedBox(this)");
    }
}

selectBtnX.onclick = () => {
    selectBox.classList.add("hide"); // hide select box
    playBoard.classList.add("show"); // show playboard section
}

selectBtnO.onclick = () => {
    selectBox.classList.add("hide"); // hide select box
    playBoard.classList.add("show"); // show playboard section
    players.setAttribute("class", "players active player"); // set class attribute in players with players active player values
}

let playerXIcon = "fas fa-times"; // fontawesome cross icon
let playerOIcon = "far fa-circle"; // fontawesome circle icon
let playerSign = "X"; // global variable for player's sign
let runBot = true; // global variable to stop the bot once match won or drawn

function clickedBox(element) {
    if(players.classList.contains("player")) {
        playerSign = "O"; // if player chooses O, change playerSign to O
        element.innerHTML = `<i class="${playerOIcon}"></i>`; // add circle icon inside clicked element/box
        players.classList.remove("active"); // add active class in players
        element.setAttribute("id", playerSign); // set id attribute in span/box with player's sign
    } else {
        element.innerHTML = `<i class="${playerXIcon}"></i>`; // add cross icon inside clicked element/box
        element.setAttribute("id", playerSign); // set id attribute in span/box with player's sign
        players.classList.add("active"); // add active class in players
    }
    selectWinner(); // call selectWinner function
    element.style.pointerEvents = "none"; // disable further clicking on the box
    playBoard.style.pointerEvents = "none"; // disable clicking on other boxes until bot selects
    let randomTimeDelay = ((Math.random() * 1000) + 200).toFixed(); // generate random delay for bot's selection
    setTimeout(() => bot(runBot), randomTimeDelay); // call bot function after delay
}

function bot() {
    let array = []; // array to store unclicked box indices
    if(runBot) {
        playerSign = "O"; // change playerSign to O for bot's turn
        for (let i = 0; i < allBox.length; i++) {
            if(allBox[i].childElementCount == 0) array.push(i); // insert unclicked box index into array
        }
        let randomBox = array[Math.floor(Math.random() * array.length)]; // get random index for bot's selection
        if(array.length > 0) {
            if(players.classList.contains("player")) {
                playerSign = "X"; // if player has chosen O, bot will be X
                allBox[randomBox].innerHTML = `<i class="${playerXIcon}"></i>`; // add cross icon for bot's selection
                allBox[randomBox].setAttribute("id", playerSign); // set id attribute for bot's selection
                players.classList.add("active"); // add active class in players
            } else {
                allBox[randomBox].innerHTML = `<i class="${playerOIcon}"></i>`; // add circle icon for bot's selection
                players.classList.remove("active"); // remove active class in players
                allBox[randomBox].setAttribute("id", playerSign); // set id attribute for bot's selection
            }
            selectWinner(); // call selectWinner function
        }
        allBox[randomBox].style.pointerEvents = "none"; // disable clicking on bot's selection
        playBoard.style.pointerEvents = "auto"; // enable clicking on playboard after bot's selection
        playerSign = "X"; // set playerSign to X for user's turn
    }
}

function getIdVal(classname) {
    return document.querySelector(".box" + classname).id; // return id value
}

function checkIdSign(val1, val2, val3, sign) {
    return getIdVal(val1) == sign && getIdVal(val2) == sign && getIdVal(val3) == sign; // check if all id values match sign
}

function selectWinner() {
    if(checkIdSign(1,2,3,playerSign) || checkIdSign(4,5,6,playerSign) || checkIdSign(7,8,9,playerSign) || checkIdSign(1,4,7,playerSign) || checkIdSign(2,5,8,playerSign) || checkIdSign(3,6,9,playerSign) || checkIdSign(1,5,9,playerSign) || checkIdSign(3,5,7,playerSign)) {
        runBot = false; // stop bot if someone wins
        bot(runBot); // call bot function
        setTimeout(() => {
            resultBox.classList.add("show"); // show result box after match won
            playBoard.classList.remove("show"); // hide playboard after match won
        }, 700); // 1s = 1000ms
        wonText.innerHTML = `Player <p>${playerSign}</p> won the game!`; // display winning text
    } else {
        if(getIdVal(1) != "" && getIdVal(2) != "" && getIdVal(3) != "" && getIdVal(4) != "" && getIdVal(5) != "" && getIdVal(6) != "" && getIdVal(7) != "" && getIdVal(8) != "" && getIdVal(9) != "") {
            runBot = false; // stop bot if match is drawn
            bot(runBot); // call bot function
            setTimeout(() => {
                resultBox.classList.add("show"); // show result box after match drawn
                playBoard.classList.remove("show"); // hide playboard after match drawn
            }, 700); // 1s = 1000ms
            wonText.textContent = "Match has been drawn!"; // display draw match text
        }
    }
}

replayBtn.onclick = () => window.location.reload(); // reload the page on replay button click
```
![HTML5](https://img.shields.io/badge/html5-%23a2c4c9.svg?style=for-the-badge&logo=html5&logoColor=%23462f9c)
![CSS3](https://img.shields.io/badge/css3-%238e7cc3.svg?style=for-the-badge&logo=css3&logoColor=%235e0c1d)
![JavaScript](https://img.shields.io/badge/javascript-%23007ACC.svg?style=for-the-badge&logo=javascript&logoColor=%23F7DF1E)