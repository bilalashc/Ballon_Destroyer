# Balloon Destroyer - Typing Game

[Ballon Destroyer](https://bilalashc.github.io/Ballon_Destroyer/) is a web browser game that helps users test and improve their typing skills by popping all the ballons before they exit the screen.

The link to the live site for the game can be found [here](https://bilalashc.github.io/Ballon_Destroyer/)

## Game Description

Characters from the alphabet are presented on a balloon in random locations on the screen. As the balloon with a character is visible on the canvas, the user can press the character value on the keyboard and the balloon with the corresponding character is destroyed. For each balloon that is destroyed, the user gains 5 points. The user has five lives, but will lose a life for each balloon that escapes. Lives are the number of chances a user has to destroy the balloons before it escapes. The user can have varying difficulty levels, to set the speed of the balloons. The difficulties are: Easy, Medium, and Hard. In addition, the user will be able to track their highest score.  


## Tech Stack

This app was developed using `HTML`, `CSS` and `JavaScript`. In addition, `Webpack` was used to bundle the source code and generate a static page. 

## Features

### 1) Balloons Animation

To animate the balloons as they are dropping from the atmosphere in the canvas involves generating a sequence of images that depict a group of balloons floating or falling through the sky. The image sequence of drawing balloons and text inside the canvas is used to create the animation effect on the canvas by utilizing JavaScript. It gives the illusion that the ballons are dropping from the atmosphere. The animated balloons can be customized according to speed, color, size, direction, and the distance on the canvas.

#### Challenge

The animation sequence feature was a challenge because it required creating a series of different images of balloons that had to be manipulated and combined to create a smooth animation on the canvas. It was also challenging to figure out the optimal way to manipulate the size, color, direction, and speed of the balloons to create an immersive and realistic experience for the user. In addition, it was a challenge to figure out the most efficient manner to render the animation on canvas without compromising the performance. 

#### Solution

The balloon class was created to store the state of each balloon in the game run time. In addition, it stores the balloon's `[x, y]` position, the corresponding character value inside the balloon, and the balloon's visible or escaped status. The JavaScript code for the balloon class is showcased below:

```javascript
import { BALLOON_RADIUS } from './constants';

export class Balloon {
  constructor(value, x, y, id) {
    this.id = id + value;
    this.value = value;
    this.x = x;
    this.y = y;
    this.visible = false;
  }

  isVisible() {
    return this.visible;
  }

  getYPosition() {
    return this.y;
  }

  getPosition() {
    return [this.x, this.y];
  }

  getValue() {
    return this.value;
  }

  isEscaped(canvasHeight) {
    return this.y > canvasHeight + BALLOON_RADIUS;
  }

  drop(step, canvasHeight = 0) {
    this.y += step;
    this.visible = this.y >= BALLOON_RADIUS && this.y <= canvasHeight;
  }
}
```

### 2) Game Background & Game Hero

The game offers a feature to change the game background and game hero from the availaible options in game control. It allows users to customize their experience by personalizing their gaming envioronment. This customization includes selecting from a variety of pre-designed backgrounds and game heros for the game screen.

#### Challenge

The challenge of implementing this feature was to ensure that changing the background or hero would not effect the state of the game. It should update the game background and hero upon selection without intervening with the game logic.

#### Solution

The background and the game hero drawn on the canvas are placed into the DOM with an id to be manipulated. A click event listener using Javascript was used to change the styling exclusively. A snippet of the code that showcases the implemenation can be seen below:

```javascript
function setCanvasBackground(image) {
  const canvasContainer = document.getElementById('canvas_container');
  canvasContainer.setAttribute('class', `container-right ${image}`);
}

function setGameHero(image) {
  const characterImage = document.getElementById('characterImg');
  characterImage.setAttribute('src', './dist/images/' + image + '.png');
}
```

### 3) Destroying balloon if a character is entered from keyboard

The feature in a game of destroying a balloon inside with text when the same key value is entered from keyboard would allow the player to enter a specific key into their keyboard which, when pressed, will destroy the balloon in the canvas. This feature adds an element of interactivity to the game and it is the core feature of the game that challenges the user where user is required to enter the keyboard characters as fast as possible and collect more scores. Additionally, it can also add another layer of challenge as the player may have to enter the correct key in order to progress.

#### Challenge

The challenge with this feature is that it requires the player to be very precise and to enter the key as quickly as possible. This can be difficult for some players and may require practice in order to improve their scores. Additionally, the key value needs to be chosen carefully to ensure that it does not overlap with other commands and does not prevent the player from continuing the game. Finally, there may be necessary constraints for the game such as difficulty levels that need to be considered to provide an enjoyable gaming experience.

#### Solution

The user waits for the ballons enter to atmospher and becomes visible. Then, I added event listner to the game body to listen for the key entered. When the user enters the matching key, I delete the respective ballon from array of ballons created and the change is reflected in the canvas. In addition, a user can choose from levels of difficulties from game control `EASY`, `MEDIUM` and `HARD` and challenge them selves with the balloon step shift. Below is the snippet of the code that controls how these levels affect the step each balloon moves down at each frame.

```javascript
export const DIFFICULTIES = {
  EASY: 20,
  MEDIUM: 40,
  HARD: 60,
};
```
