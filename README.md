# Timer Diffusion

## Objective

The Timer Diffusion project aims to simulate the diffusion process using random movement of circles within a confined area. The project visually demonstrates how particles spread over time and calculates the variance of their positions from the center, providing insights into diffusion patterns.

### Skills Learned

- Understanding of basic simulation concepts.
- Proficiency in JavaScript for animation and event handling.
- Knowledge of HTML and CSS for structuring and styling the web page.
- Ability to calculate statistical measures like variance.
- Development of problem-solving skills through implementation of random movement algorithms.

### Tools Used

- HTML for structuring the web page.
- CSS for styling and layout.
- JavaScript for implementing the simulation logic and user interactions.

## Steps

### Initial Setup

The project consists of a simple HTML page with embedded CSS and JavaScript. The HTML structure includes a table with a cell for displaying the circles, buttons for controlling the simulation, and a textarea for outputting the variance values.

### Simulation Process

1. **HTML Structure:**
    - A `<table>` element contains a cell (`<td>`) for displaying the circles.
    - Control buttons (`Start`, `Pause`, `Continue`) to manage the simulation.
    - A `<textarea>` for displaying the variance values at each step.

2. **CSS Styling:**
    - Defines the appearance of the web page, including the background color, text color, and styles for the circles.

3. **JavaScript Implementation:**
    - Handles the movement of the circles within the cell.
    - Calculates and displays the variance of the circle positions from the center.
    - Manages the start, pause, and continue functionality of the simulation.

### Running the Simulation

- **Start Button:** Initializes the positions of the circles and starts the simulation timer.
- **Pause Button:** Stops the simulation timer.
- **Continue Button:** Resumes the simulation timer from where it was paused.


## Code

The complete code for the Timer Diffusion project is as follows:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Timer Diffusion</title>
    <style>
      body {
        color: #000000;
        background-color: #3d863d;
      }
      #top-cell {
        width: 500px;
        height: 500px;
        position: relative;
        border: 1px solid black;
      }
      .circle_green {
        position: absolute;
        top: 250px;
        left: 250px;
        width: 10px;
        height: 10px;
      }
      textarea {
        width: 100%;
        height: 400px; /* Adjust the height as needed */
        resize: none;
      }
    </style>
  </head>
  <body>
    <h1>Timer Diffusion</h1>

    <table>
      <tr>
        <td id="top-cell">
          <img src="circle_green.png" class="circle_green" />
          <img src="circle_green.png" class="circle_green" />
          <img src="circle_green.png" class="circle_green" />
          <img src="circle_green.png" class="circle_green" />
          <img src="circle_green.png" class="circle_green" />
          <img src="circle_green.png" class="circle_green" />
          <img src="circle_green.png" class="circle_green" />
          <img src="circle_green.png" class="circle_green" />
          <img src="circle_green.png" class="circle_green" />
          <img src="circle_green.png" class="circle_green" />
          <img src="circle_green.png" class="circle_green" />
          <img src="circle_green.png" class="circle_green" />
          <img src="circle_green.png" class="circle_green" />
          <img src="circle_green.png" class="circle_green" />
          <img src="circle_green.png" class="circle_green" />
          <img src="circle_green.png" class="circle_green" />
          <img src="circle_green.png" class="circle_green" />
          <img src="circle_green.png" class="circle_green" />
          <img src="circle_green.png" class="circle_green" />
          <img src="circle_green.png" class="circle_green" />
        </td>
      </tr>
      <tr>
        <td>
          <button id="start-btn">Start</button>
          <button id="pause-btn" disabled>Pause</button>
          <button id="continue-btn" disabled>Continue</button>
        </td>
      </tr>
      <tr>
        <td>
          <textarea id="output" rows="60"></textarea>
        </td>
      </tr>
    </table>
    <script>
      let dot = document.getElementsByTagName("img");

      var variances = [];

      var x = new Array(20).fill(250);
      var y = new Array(20).fill(250);

      var t = 0;

      document
        .getElementById("start-btn")
        .addEventListener("click", function () {
          x.fill(250);
          y.fill(250);
          document.getElementById("output").value = "";
          timer = setInterval(moveCircles, 100);
          document.getElementById("pause-btn").removeAttribute("disabled");
          this.setAttribute("disabled", true);
        });

      document
        .getElementById("pause-btn")
        .addEventListener("click", function () {
          clearInterval(timer);
          document.getElementById("start-btn").removeAttribute("disabled");
          document.getElementById("continue-btn").removeAttribute("disabled");
          this.setAttribute("disabled", true);
        });

      document
        .getElementById("continue-btn")
        .addEventListener("click", function () {
          timer = setInterval(moveCircles, 100);
          this.setAttribute("disabled", true);
          document.getElementById("start-btn").setAttribute("disabled", true);
          document.getElementById("pause-btn").removeAttribute("disabled");
        });

      function moveCircles() {
        for (let i = 0; i < x.length; i++) {
          x[i] += Math.floor(Math.random() * 3 - 1);
          y[i] += Math.floor(Math.random() * 3 - 1);

          dot[i].style.left = x[i] + "px";
          dot[i].style.top = y[i] + "px";
        }
        calculateVariance();
      }

      function calculateVariance() {
        const sum = x.reduce((acc, xPos, i) => {
          return acc + Math.pow(xPos - 250, 2) + Math.pow(y[i] - 250, 2);
        }, 0);
        const variance = sum / 20;
        variances.push(variance);
        document.getElementById("output").value += `Step ${
          t + 1
        }: Variance ${variance}\n`;
        t++;
      }
    </script>
  </body>
</html>
