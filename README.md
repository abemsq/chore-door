# Mini Web Javascript Game: Chore Bot

# Instructions
1. Hiding behind one of these doors is the ChoreBot.
2. Your mission is to open all of the doors without running into the ChoreBot.
3. If you manage to avoid the ChoreBot until you open the very last door, you win!
4. See if you can score a winning streak!

[!image]()

## Javascript
```
let doorImage1 = document.getElementById("door1");
let doorImage2 = document.getElementById("door2");
let doorImage3 = document.getElementById("door3");

const botDoorPath = "https://content.codecademy.com/projects/chore-door/images/robot.svg";
const beachDoorPath = "https://content.codecademy.com/projects/chore-door/images/beach.svg";
const spaceDoorPath = "https://content.codecademy.com/projects/chore-door/images/space.svg";

let startButton = document.getElementById("start");
let numClosedDoors = 3;

let openDoor1;
let openDoor2;
let openDoor3;

let currentPlaying = true;

const isBot = (door) => {
    if (door.src === botDoorPath) {
        return true;
    } else {
        return false;
    }
};

const isClicked = door => {
    if (door.src === closedDoorPath) {
        return false;
    } else {
        return true;
    }
};

const playDoor = (door) => {
    numClosedDoors--;
    if (numClosedDoors === 0) {
        gameOver('win');
    }
    else if (isBot(door) === true) {
        return gameOver();
    }
};

let randomChoreDoorGenerator = () => {
  let choreDoor = Math.floor(Math.random() * numClosedDoors);
  if (choreDoor === 0) {
    openDoor1 = botDoorPath;
    openDoor2 = beachDoorPath;
    openDoor3 = spaceDoorPath;
  } else if (choreDoor === 1) {
    openDoor2 = botDoorPath;
    openDoor1 = spaceDoorPath;
    openDoor3 = beachDoorPath;
  } else {
    openDoor3 = botDoorPath;
    openDoor2 = beachDoorPath;
    openDoor1 = spaceDoorPath;
  }
} 

doorImage1.onclick = () => {
    if (!isClicked(doorImage1) && currentPlaying) {
        doorImage1.src = openDoor1;
        playDoor(doorImage1);
    }
};

doorImage2.onclick = () => {
    if (!isClicked(doorImage2) && currentPlaying) {
        doorImage2.src = openDoor2;
        playDoor(doorImage2);
    }
};

doorImage3.onclick = () => {
    if (!isClicked(doorImage3) && currentPlaying) {
        doorImage3.src = openDoor3;
        playDoor(doorImage3);
    }
};

const startRound = () => {
    doorImage1.src = closedDoorPath;
    doorImage2.src = closedDoorPath;
    doorImage3.src = closedDoorPath;
    numClosedDoors = 3;
    startButton.innerHTML = "Good luck!";
    currentPlaying = true;
    randomChoreGenerator();
};

startButton.onclick = () => {
    if (!currentPlaying) {
        startRound();
    }
};

const gameOver = (status) => {
    if (status === 'win') {
        startButton.innerHTML = "You win! Play again?";
    } else {
        startButton.innerHTML = "Game over! Play again?"
    }
    currentPlaying = false;
};
```

## HTML
```
<!DOCTYPE html>
<html>
  <head>
    <title>Chore Door!</title>
    <link href="./style.css" rel="stylesheet" type="text/css">
    <script type="text/javascript" src="./script.js"></script>
    <link href="https://fonts.googleapis.com/css?family=Work+Sans"
    rel="stylesheet" type="text/css">
  </head>
  <body>
    <div class="header">
      <img src="https://content.codecademy.com/projects/chore-door/images/logo.svg">
    </div>
    <div class="title-row">
      <img src="https://content.codecademy.com/projects/chore-door/images/star.svg">
      <p class="instructions-title">Instructions</p>
      <img src="https://content.codecademy.com/projects/chore-door/images/star.svg">
    </div>
    <table class="instructions-row">
      <tr>
        <td class="instructions-number">1</td>
        <td class="instructions-text">Hiding behind one of these doors is the ChoreBot.</td>
      </tr>
      <tr>
        <td class="instructions-number">2</td>
        <td class="instructions-text">Your mission is to open all of the doors without running into the ChoreBot.</td>
      </tr>
      <tr>
        <td class="instructions-number">3</td>
        <td class="instructions-text">If you manage to avoid the ChoreBot until you open the very last door, you win!</td>
      </tr>
      <tr>
        <td class="instructions-number">4</td>
        <td class="instructions-text">See if you can score a winning streak!</td>
      </tr>
    </table>
    <div class="door-row">
      <img id="door1" class= "door-frame" src="https://content.codecademy.com/projects/chore-door/images/closed_door.svg">
      <img id="door2" class= "door-frame" src="https://content.codecademy.com/projects/chore-door/images/closed_door.svg">
      <img id="door3" class= "door-frame" src="https://content.codecademy.com/projects/chore-door/images/closed_door.svg">
    </div>
    <div id="start" class="start-row">
      Good luck!
    </div>
    <script type="text/javascript" src="script.js"></script>
  </body>
</html>
```

## CSS
```
body {
    background-color: #010165;
    margin: 0px;
  }
  
  .header {
    background-color: #00ffff;
    text-align: center;
  }
  
  .title-row {
    margin-top: 42px;
    margin-bottom: 21px;
    text-align: center;
  }
  
  .instructions-title {
    display: inline;
    font-size: 18px;
    color: #00ffff;
    font-family: 'Work Sans';
  }
  
  .instructions-row {
    margin: 0 auto;
    width: 400px;
  }
  
  .instructions-number {
    padding-right: 25px;
    font-family: 'Work Sans';
    font-size: 36px;
    color: #00ffff;
  }
  
  .instructions-text {
    padding: 10px;
    font-family: 'Work Sans'
    font-size: 14px;
    color: #ffffff;
  }
  
  .door-row {
    text-align: center;
  }
  
  .door-frame {
    cursor: pointer;
    padding: 10px;
  }
  
  .start-row {
    margin: auto;
    width: 120px;
    height: 43px;
    font-family: 'Work Sans';
    background-color: #eb6536;
    padding-top: 18px;
    font-size: 18px;
    text-align: center;
    color: #010165;
    margin-bottom: 21px;
    cursor: pointer;
  }
```