# Balloon Destroyer - Typing Game

[Ballon Destroyer](https://bilalashc.github.io/Ballon_Destroyer/) is a web browser game that helps users test and improve their typing skills by popping all the ballons before they exit the screen.

[Click here to view the project](https://bilalashc.github.io/Ballon_Destroyer/)

# Table of Contents
### 1) Game Description
### 2) Tech Stack 
### 3) Features

## Game Description

Characters from the alphabet are presented on a balloon in random locations on the screen. As the balloon with a character is visible on the canvas, the user can press the character value on the keyboard and the balloon with the corresponding character is destroyed. For each balloon that is destroyed, the user gains 5 points. The user has five lives, but will lose a life for each balloon that escapes. Lives are the number of chances a user has to destroy the balloons before it escapes. The user can have varying difficulty levels, to set the speed of the balloons. The difficulties are: Easy, Medium, and Hard. In addition, the user will be able to track their highest score.  


## Tech Stack

This app was developed using `HTML`, `CSS` and `JavaScript`. In addition, `Webpack` was used to bundle the source code and generate a static page. 

## Features

### 1) Balloons Animation

To animate the balloons as they are dropping from the atmosphere in the canvas involves generating a sequence of images that depict a group of balloons floating or falling through the sky. The image sequence of drawing balloons and text inside the canvas is used to create the animation effect on the canvas by utilizing JavaScript. It gives the illusion that the ballons are dropping from the atmosphere. The animated balloons can be customized according to speed, color, size, direction, and distance on the canvas.

![BalloonCharacters](https://github.com/bilalashc/Ballon_Destroyer/assets/122466002/1c82708a-13db-4691-9688-b44da8b77396)

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

The game offers a feature to change the game background and game hero from the available options in game control. It allows users to customize their experience by personalizing their gaming environment. This customization includes selecting from a variety of pre-designed backgrounds and game heroes for the game screen.

![GameControls](https://github.com/bilalashc/Ballon_Destroyer/assets/122466002/b1455b41-5cbf-4cbe-a850-b1d4fc8a50da)

#### Challenge

The challenge of implementing this feature was to ensure that changing the background or hero would not affect the state of the game. It should update the game background and hero upon selection without intervening with the game logic.

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

### 3) Destroying balloons by pressing the corresponding character on the keyboard

The balloon is destroyed when the character inside the balloon and the corresponding character are entered from the keyboard by the user. This is the core feature of the game and adds an element of interactivity. The user is challenged to enter the keyboard characters as fast as possible to increase his score and not lose any lives. In addition, the user is able to select difficulty based on their typing proficiency. 

![Recording 2023-06-22 at 16 54 23](https://github.com/bilalashc/Ballon_Destroyer/assets/122466002/1cbd9818-a2c6-4d55-9704-f2e935a27741)

#### Challenge

The challenge with this feature was that it requires the player to be precise and enter the character on the keyboard as quickly as possible. In addition, the key value needs to be picked carefully to ensure that it does not overlap with other commands and does not prevent the player from continuing the game. There was an additional challenge to place the necessary constraints such as different difficulty levels to provide the user with an enjoyable gaming experience. 

#### Solution

The user waits for the balloon to enter the atmosphere as it becomes visible. An event listener was added to the game to listen for the key entered. When the user enters the matching key, the respective balloon from the array of balloons created is deleted. This change is reflected on the canvas. Additionally, a user can choose from different levels of difficulty under game control. These include: `Easy`, `Medium`, and `Hard`. A snippet of the code that controls the difficulty levels based on the step the balloons move down at each frame is showcased below:


```javascript
export const DIFFICULTIES = {
  EASY: 20,
  MEDIUM: 40,
  HARD: 60,
};
```

