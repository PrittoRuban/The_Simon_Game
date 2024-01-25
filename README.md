<h1  align="center"> Hello there 👋, This is the Simon game project created during my web development bootcamp. </h1>

<details>
<p align="center">Explore the captivating world of the Simon game, crafted with passion during a dynamic web development bootcamp. Immerse yourself in this classic memory challenge, where vibrant colors and crisp sounds harmonize to test your recall prowess. Dive into a seamless user experience, meticulously designed with HTML, CSS, and JavaScript, as you engage in a nostalgic journey of patterns and precision. Elevate your cognitive skills while enjoying the sleek, responsive interface of this project, a testament to your journey in mastering the art of web development.</p> 
</details> 

<h2>You can try it yourself ⬇️</h2>

- File Name: Index.html
```html
<!DOCTYPE html>
<html lang="en" dir="ltr">
  <head>
    <meta charset="utf-8" />
    <title>Simon</title>
    <link rel="stylesheet" href="styles.css" />
    <link
      href="https://fonts.googleapis.com/css?family=Press+Start+2P"
      rel="stylesheet"
    />
  </head>

  <body>
    <h1 id="level-title">Press A Key to Start</h1>
    <div class="container">
      <div lass="row">
        <div type="button" id="green" class="btn green"></div>

        <div type="button" id="red" class="btn red"></div>
      </div>

      <div class="row">
        <div type="button" id="yellow" class="btn yellow"></div>
        <div type="button" id="blue" class="btn blue"></div>
      </div>
    </div>
    <footer class="footer">
      <p>
        Designed by
        <a style="color: plum;"
          href="https://www.linkedin.com/in/pritto-ruban-0b1290289?utm_source=share&utm_campaign=share_via&utm_content=profile&utm_medium=android_app"
          >Pritto Ruban</a
        >
      </p>
    </footer>
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.4.1/jquery.min.js"></script>
    <script src="game.js" charset="utf-8"></script>
  </body>
</html>
```

- File name: Style.css

```css
body {
  text-align: center;
  background-color: #011F3F;
}

#level-title {
  font-family: 'Press Start 2P', cursive;
  font-size: 3rem;
  margin:  5%;
  color: #FEF2BF;
}

.container {
  display: block;
  width: 50%;
  margin: auto;

}

.btn {
  margin: 25px;
  display: inline-block;
  height: 200px;
  width: 200px;
  border: 10px solid black;
  border-radius: 20%;
}

.game-over {
  background-color: red;
  opacity: 0.8;
}

.red {
  background-color: red;
}

.green {
  background-color: green;
}

.blue {
  background-color: blue;
}

.yellow {
  background-color: yellow;
}

.pressed {
  box-shadow: 0 0 20px white;
  background-color: grey;
}

.footer {
  font-size: 2rem;
  padding: 0%;
  margin: 0%;
  color: #FEF2BF;
}
```

- File name: game.js

```js
var buttonColours = ["red", "blue", "green", "yellow"];

var gamePattern = [];
var userClickedPattern = [];

var started = false;
var level = 0;

$(document).keypress(function() {
  if (!started) {
    $("#level-title").text("Level " + level);
    nextSequence();
    started = true;
  }
});

$(".btn").click(function() {

  var userChosenColour = $(this).attr("id");
  userClickedPattern.push(userChosenColour);

  playSound(userChosenColour);
  animatePress(userChosenColour);

  checkAnswer(userClickedPattern.length-1);
});

function checkAnswer(currentLevel) {

    if (gamePattern[currentLevel] === userClickedPattern[currentLevel]) {
      if (userClickedPattern.length === gamePattern.length){
        setTimeout(function () {
          nextSequence();
        }, 1000);
      }
    } else {
      playSound("wrong");
      $("body").addClass("game-over");
      $("#level-title").text("Game Over, Press Any Key to Restart");

      setTimeout(function () {
        $("body").removeClass("game-over");
      }, 200);

      startOver();
    }
}


function nextSequence() {
  userClickedPattern = [];
  level++;
  $("#level-title").text("Level " + level);
  var randomNumber = Math.floor(Math.random() * 4);
  var randomChosenColour = buttonColours[randomNumber];
  gamePattern.push(randomChosenColour);

  $("#" + randomChosenColour).fadeIn(100).fadeOut(100).fadeIn(100);
  playSound(randomChosenColour);
}

function animatePress(currentColor) {
  $("#" + currentColor).addClass("pressed");
  setTimeout(function () {
    $("#" + currentColor).removeClass("pressed");
  }, 100);
}

function playSound(name) {
  var audio = new Audio("sounds/" + name + ".mp3");
  audio.play();
}

function startOver() {
  level = 0;
  gamePattern = [];
  started = false;
}
```
