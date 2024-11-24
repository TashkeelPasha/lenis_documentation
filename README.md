# Lenis Smooth Scrolling Example

A simple project demonstrating smooth scrolling using the [Lenis](https://github.com/studio-freight/lenis) library with HTML, CSS, and JavaScript. This project includes basic smooth scrolling, a parallax effect, and element animations on scroll.

---

## **Features**

- Smooth scrolling for a seamless user experience.
- Parallax effect for enhanced visual appeal.
- Scroll-triggered animations like element fade-ins.

---

## **Demo**


---

## **Setup Instructions**

### Prerequisites
- A modern browser supporting ES6 features.
- Basic knowledge of HTML, CSS, and JavaScript.

## Code Structure

### HTML
The structure includes three main sections:

Hero Section: Contains introductory content.
Parallax Section: Implements a background parallax effect.
Footer Section: Final part of the page.
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Lenis Smooth Scrolling</title>
  <link rel="stylesheet" href="styles.css">
</head>
<body>
  <div class="container">
    <section class="hero">
      <h1>Lenis Smooth Scrolling</h1>
      <p>Scroll down to experience smooth scrolling effects.</p>
    </section>
    <section class="parallax">
      <div class="parallax-content">Parallax Effect</div>
    </section>
    <section class="footer">
      <p>Thank you for scrolling!</p>
    </section>
  </div>

  <script src="https://cdn.jsdelivr.net/npm/@studio-freight/lenis"></script>
  <script src="script.js"></script>
</body>
</html>
```
CSS
The styles.css file defines the visual styles for the page and includes the parallax setup.

```css
/* styles.css */

body {
  margin: 0;
  font-family: Arial, sans-serif;
  color: #fff;
  background-color: #000;
  overflow: hidden; /* Lenis will handle scrolling */
}

.container {
  width: 100%;
}

.hero {
  height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  background: linear-gradient(45deg, #ff6f61, #d84315);
  text-align: center;
}

.parallax {
  position: relative;
  height: 100vh;
  overflow: hidden;
  background: url('https://via.placeholder.com/1920x1080') no-repeat center center fixed;
  background-size: cover;
}

.parallax-content {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  font-size: 3rem;
  font-weight: bold;
}

.footer {
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  background: linear-gradient(45deg, #2196f3, #1e88e5);
}
JavaScript
The script.js file initializes Lenis and handles the smooth scrolling, parallax, and scroll-triggered animations.

javascript
Copy code
// script.js

// Initialize Lenis
const lenis = new Lenis({
  smooth: true,  // Enable smooth scrolling
  duration: 1.5, // Scroll duration
  easing: (t) => t * t, // Custom easing for natural feel
});

// Update Lenis on each animation frame
function raf(time) {
  lenis.raf(time);
  requestAnimationFrame(raf);
}

requestAnimationFrame(raf);

// Create parallax effect
lenis.on('scroll', ({ scroll }) => {
  const parallax = document.querySelector('.parallax');
  parallax.style.backgroundPositionY = `${scroll * 0.5}px`;
});
```


## Adding JavaScript for Lenis
The JavaScript initializes Lenis and configures its behavior.

```js
// Initialize Lenis
const lenis = new Lenis({
  smooth: true,  // Enable smooth scrolling
  duration: 1.5, // Scroll duration
  easing: (t) => t * t, // Custom easing for natural feel
});

// Update Lenis on each animation frame
function raf(time) {
  lenis.raf(time);
  requestAnimationFrame(raf);
}

requestAnimationFrame(raf);
```

## Examples of Effects
Example 1: Smooth Scrolling with Basic Setup
The above example already implements smooth scrolling for a full-page experience. Lenis automatically intercepts the scroll events and applies smooth easing, making the transitions fluid.


## Example 2: Parallax Background
For the parallax effect, Lenis can be combined with JavaScript to adjust the background position dynamically based on the scroll progress.

```js
// Create parallax effect
lenis.on('scroll', ({ scroll }) => {
  const parallax = document.querySelector('.parallax');
  parallax.style.backgroundPositionY = `${scroll * 0.5}px`;
});
```

## Example 3: Element Fade-In on Scroll
Lenis can trigger animations for elements as they appear in the viewport:

```html
<section class="fade-in">
  <p>This content fades in as you scroll!</p>
</section>
```
```css
.fade-in p {
  opacity: 0;
  transform: translateY(50px);
  transition: opacity 0.5s, transform 0.5s;
}

.fade-in p.visible {
  opacity: 1;
  transform: translateY(0);
}
```
```js
// Add scroll-based visibility effect
lenis.on('scroll', ({ scroll }) => {
  const fadeInSection = document.querySelector('.fade-in p');
  const rect = fadeInSection.getBoundingClientRect();

  if (rect.top < window.innerHeight) {
    fadeInSection.classList.add('visible');
  }
});
```


## Creating a Split Sticky Scroll Effect

This guide walks you through the logic and concepts behind building a split-sticky-scroll effect. Participants will learn how to make one section stay sticky while the adjacent section scrolls smoothly, using HTML, CSS, and JavaScript.

### 🛠️ Understanding the Concept
1. Split Layout Structure
The effect works by dividing the page into two columns:

Sticky Column: One column remains fixed (sticky) as you scroll.
Scrollable Column: The adjacent column scrolls normally.
The grid layout helps create this division, and CSS position: sticky is used to make the sticky column remain visible during the scroll.

2. Sticky Behavior
The sticky section uses the CSS property:

```css
position: sticky;
top: <value>;

position: sticky makes an element "stick" when it reaches a specified position (top, left, etc.) within its scrollable container.
top: 50px; ensures the sticky element locks 50px from the top of the viewport as the user scrolls.
```
The sticky property depends on:

The parent container having a defined height or overflow.
The sticky element being inside a scrollable container.

3. Scrollable Column
The second column holds the actual scrolling content, such as paragraphs, images, or other elements. You create spacing between content blocks using padding or margins to simulate a continuous scrolling experience.

4. Enhancing with Smooth Scrolling
To make the scrolling experience seamless:

Use Lenis for smooth scrolling effects.
The library adjusts the scroll behavior to feel fluid, improving user experience.

5. Adding Interactivity
We can add interactivity as elements come into view:

Use Intersection Observer to detect when elements scroll into or out of the viewport.
Add or remove classes dynamically based on visibility, creating subtle animations like fading in/out.

✍️ Steps to Build the Effect
Here’s how participants can implement the effect step by step:

Step 1: Create the HTML Structure
Create a section to hold the sticky and scrollable columns.
Use a grid layout to divide the content into two equal parts:
A sticky container with a heading.
A scrollable container with multiple blocks of text or content.
Logic:

Each block in the scrollable container should have ample spacing (padding/margin) to create a visual scrolling effect.
The sticky container should contain the content you want visible throughout the scroll.

Step 2: Add Basic CSS
Define a grid layout using grid-template-columns to divide the sticky and scrollable sections.
Apply position: sticky to the sticky column.

Logic:

Use grid-template-columns: 1fr 1fr; to split the container into two equal parts.
Add padding to the scrollable content blocks to ensure proper spacing and simulate the scrolling effect.
Step 3: Add Smooth Scrolling
Integrate Lenis for smooth scrolling.
Add a script to initialize the Lenis library and hook it to the browser's animation frame for smooth scroll updates.
Logic:

Lenis adjusts the browser’s native scrolling behavior, allowing smoother transitions and precise control over animations.
Step 4: Detect Viewport Visibility
Use the Intersection Observer API to detect when elements are in or out of the viewport.
Add or remove CSS classes to trigger animations or effects.
Logic:

Intersection Observer observes a target element and fires a callback when its visibility changes.
You can apply animations, such as fading in/out, scaling, or transforming elements, by toggling CSS classes.
📘 Explaining Each Component
HTML Layout
The grid container holds two children: a sticky section and a scrollable section.
The scrollable content is divided into multiple blocks, each styled individually for spacing and aesthetics.

```html

<section id="split-scroll">
  <div class="grid">
    <div class="sticky">
      <h2>Sticky Section</h2>
    </div>
    <div class="scroll">
      <div class="text-block">Content Block 1</div>
      <div class="text-block">Content Block 2</div>
      <div class="text-block">Content Block 3</div>
    </div>
  </div>
</section>
```
CSS
Use CSS Grid to align the two columns.
Add position: sticky to the sticky section with a top value for the sticky behavior.
Style the scrollable content with padding for spacing.
```css
.split-sticky-scroll .grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
}

.split-sticky-scroll .sticky h2 {
  position: sticky;
  top: 50px;
}

.split-sticky-scroll .scroll .text-block {
  padding: 200px 0;
  font-size: 32px;
}
```

Initialize Lenis for smooth scrolling.
Use Intersection Observer to monitor visibility of content blocks.
Logic Breakdown:

Lenis Smooth Scrolling:

Lenis overrides the native scroll behavior to make the scrolling effect fluid and responsive.
Hook Lenis updates to the requestAnimationFrame for continuous updates.
Intersection Observer:

Observe each content block and toggle classes based on visibility.
Use these classes for animations like scaling or fading.
```javascript
document.addEventListener('DOMContentLoaded', () => {
  const lenis = new Lenis(); // Initialize Lenis
  function raf(time) {
    lenis.raf(time);
    requestAnimationFrame(raf);
  }
  requestAnimationFrame(raf);

  // Intersection Observer for animations
  const observer = new IntersectionObserver((entries) => {
    entries.forEach((entry) => {
      if (entry.isIntersecting) {
        entry.target.classList.add('active');
      } else {
        entry.target.classList.remove('active');
      }
    });
  });

  // Apply to all text blocks
  document.querySelectorAll('.text-block').forEach((block) => observer.observe(block));
});
```
🛠️ Key Notes for Participants
The sticky column remains fixed because of position: sticky;.
Padding/margin in the scrollable column creates the space needed to simulate scrolling.
Lenis makes scrolling smooth, while Intersection Observer adds interactivity.


## Horizontal Scroll Effect with Sticky Elements
This guide helps participants create a horizontal scrolling effect where a list of items scrolls horizontally while staying visually engaging. It uses HTML, CSS, and JavaScript with smooth scrolling and sticky elements.

🛠️ Understanding the Concept
1. Horizontal Scroll Basics
Horizontal scrolling is achieved by:

Wrapping the content in a container that overflows horizontally.
Using flexbox to align items horizontally in a row.
The overflow behavior of the container allows the content to scroll horizontally while the page scrolls vertically.

2. Sticky Wrapper
The sticky wrapper:

Keeps a heading or title fixed in the center while the horizontal scroll progresses.
Uses the CSS property position: sticky to lock the element in place.
The transform: translateY(-50%); ensures the sticky element stays perfectly aligned in the viewport's center.

3. Horizontal Content Behavior
The horizontally scrollable section contains:

A flex container (display: flex) to align items in a single row.
Individual list items styled as cards with spacing and visual separation.
4. Dynamic Scrolling with Lenis and JavaScript
To make the effect interactive:

Use JavaScript to calculate the scroll position.
Adjust the transform property of items dynamically based on scroll values.
This creates an illusion of controlled motion, enhancing the user experience.

✍️ Steps to Build the Effect
Step 1: Define the HTML Structure
Create a section to hold the horizontal scroll content.
Use a sticky wrapper for the heading and a scrollable container for the items.
Logic:

The sticky wrapper locks the heading in place while content scrolls.
The container is styled for horizontal scrolling, holding items in a row.
```html
<section class="horizontal-scroll-section">
  <div class="horizontal-wrapper-sticky">
    <h2>Horizontal Scroll Section</h2>
    <ul class="card-list">
      <div class="container">
        <li>Lorem Ipsum dolor</li>
        <li>Lorem Ipsum dolor</li>
        <li>Lorem Ipsum dolor</li>
        <li>Lorem Ipsum dolor</li>
        <li>Lorem Ipsum dolor</li>
      </div>
    </ul>
  </div>
</section>
```
Step 2: Add CSS for Layout
Use flexbox for horizontal alignment.
Add sticky behavior to the heading.
Style the cards for better visual appearance.
Logic:

The flex container ensures items flow horizontally.
position: sticky on the wrapper makes the heading lock as the content scrolls.

```css
.horizontal-scroll-section {
  margin-top: 500px; /* Add vertical spacing */
}

.horizontal-wrapper-sticky {
  position: sticky;
  top: calc(100vh / 2); /* Locks the wrapper at the viewport's center */
  transform: translateY(-50%);
  overflow: hidden;
}

.card-list {
  display: flex;
  gap: 100px; /* Space between cards */
  list-style: none;
}

.container {
  display: flex; /* Align items in a row */
}

.card-list li {
  padding: 100px;
  border: 1px solid lightblue;
  position: relative;
  counter-increment: list-counter; /* Adds a number to each card */

  &:first-child {
    margin-left: 40vw; /* Adds an initial offset */
  }

  &:before {
    content: counter(list-counter); /* Displays the number */
    font-size: 32px;
    position: absolute;
    top: 10px;
    left: 10px;
  }
}
```
Step 3: Implement Smooth Scrolling
Use Lenis to ensure a smooth scrolling experience:

Initialize Lenis in your JavaScript.
Hook Lenis updates to requestAnimationFrame for smooth updates.
Logic:

Lenis smoothens the scroll, enhancing visual appeal and user interaction.
```javascript
document.addEventListener('DOMContentLoaded', () => {
  const lenis = new Lenis();

  function raf(time) {
    lenis.raf(time); // Link Lenis updates to the animation frame
    requestAnimationFrame(raf);
  }

  requestAnimationFrame(raf);
});
```
Step 4: Add Scroll-Based Motion
Use JavaScript to make the items dynamically adjust their position based on scroll progress.

Logic:

Observe the horizontal scroll section.
Calculate the container’s width and update the transform property of its children based on the scroll position.
```js
document.querySelectorAll('.horizontal-scroll-section').forEach((section) => {
  const container = section.querySelector('.container');

  // Calculate position dynamically
  window.addEventListener('scroll', () => {
    const containerWidth = container.getBoundingClientRect().width;
    const scrollPosition = window.scrollY;
    
    Array.from(container.children).forEach((item, index) => {
      item.style.transform = `translateX(${scrollPosition - containerWidth * 0.1 * index}px)`;
    });
  });
});
```
🛠️ Key Notes for Participants
Sticky Wrapper:

Use position: sticky to fix the heading in place.
Ensure the sticky element is inside a scrollable container with a height larger than the viewport.
Horizontal Scrolling:

Use display: flex for horizontal alignment.
Add spacing with gap or margins for visual clarity.
Dynamic Motion:

Use JavaScript to calculate positions dynamically.
Update each item's position using the transform property for smooth effects.
Smooth Scrolling:

Lenis adds a polished scroll experience, improving usability.


## Scale-In Text Effect
This guide explains the logic behind the Scale-In Text Effect, where text smoothly zooms in as the user scrolls down the page. It involves understanding scroll-triggered animations, sticky positioning, and dynamic transformations in CSS and JavaScript.

🛠️ Concept Breakdown
1. Sticky Container
The section uses position: sticky to keep the text element fixed in the viewport while the scroll interaction progresses. This creates the illusion that the text is zooming in dynamically during scrolling.

Key Idea:

Sticky positioning ensures the element stays in place while its parent scrolls past.
2. Scaling Text Dynamically
The scaling effect is achieved using:

The transform: scale() property, where the text starts at scale(0) and grows to scale(1) based on the scroll position.
Key Idea:

JavaScript calculates the visible percentage of the section relative to the viewport and adjusts the scale accordingly.
3. Scroll Interaction
The effect is tied to how much of the section is visible in the viewport. The JavaScript logic tracks the section's position relative to the viewport's middle point and adjusts the scaling dynamically.

Key Idea:

Smooth scaling is implemented using scroll-triggered animations controlled by the visibility percentage.
✍️ Implementation Guide
Step 1: HTML Structure
Define the section containing the scaling text.

Logic:

The .sticky-container ensures the text remains fixed as the user scrolls.
The .scale-text is the text element that scales up dynamically.
```html
<section id="el2" class="scale-in-text">
  <div class="sticky-container">
    <div class="content">
      <p class="scale-text">Zoom<br>In</p>
    </div>
  </div>
</section>
```
Step 2: CSS for Layout and Styling
Apply styles for the sticky container, full-height section, and scaling text.

Logic:

.scale-in-text: This section spans the viewport height for a smooth scroll effect.
.sticky-container: Keeps the text fixed in the center.
.scale-text: Positioned at the center and scaled dynamically using transform-origin.
```css
.scale-in-text {
  height: 1000vh; /* Long enough to allow scrolling interaction */
  position: relative; /* Ensure relative positioning for sticky container */

  .sticky-container {
    position: sticky; /* Locks the container at the viewport */
    top: 0;
    height: 100vh;
    overflow: hidden; /* Prevents overflow content */
    margin: 0 auto;

    .content {
      display: flex;
      align-items: center;
      justify-content: center;
    }
  }

  .scale-text {
    font-size: 300px; /* Large initial size */
    font-weight: 900;
    text-transform: uppercase;
    line-height: 0.8;
    text-align: center;
    position: absolute; /* Centered within the section */
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%) scale(0); /* Start at scale 0 */
    transform-origin: center; /* Center as scaling origin */
    margin: 0;
  }
}
```
Step 3: Scroll Logic with JavaScript
Use JavaScript to calculate how much of the section is visible and scale the text accordingly.

Logic:

Visibility Percentage:
Calculate the section's position relative to the viewport's middle point.
Use the getBoundingClientRect() method to determine the section's height and position.
Dynamic Scaling:
Update the text's transform property with the calculated scale value.
```javascript
document.addEventListener('DOMContentLoaded', () => {
  const scaleInTextSections = document.querySelectorAll('.scale-in-text');

  scaleInTextSections.forEach((section) => {
    const textElement = section.querySelector('.scale-text');

    window.addEventListener('scroll', () => {
      const { top, bottom } = section.getBoundingClientRect();
      const sectionHeight = bottom - top;
      const viewportMiddle = window.innerHeight / 2;
      const sectionMiddle = (top + bottom) / 2;

      let percentageVisible = 0;

      if (sectionMiddle < viewportMiddle) {
        // Section is moving above the middle
        percentageVisible = 1 - Math.max(bottom - viewportMiddle, 0) / sectionHeight;
      } else if (sectionMiddle > viewportMiddle) {
        // Section is moving below the middle
        percentageVisible = Math.max((viewportMiddle - top) / sectionHeight, 0);
      }

      // Apply the calculated scale to the text
      textElement.style.transform = `translate(-50%, -50%) scale(${percentageVisible})`;
    });
  });
});
```
🛠️ Key Points to Highlight for Participants
Sticky Positioning:

The sticky container locks the text element in place while allowing it to animate as the user scrolls.
This is achieved using position: sticky and top: 0.
Dynamic Scaling:

The transform: scale() property adjusts the size of the text smoothly based on scroll position.
The origin is set to the center using transform-origin: center.
Scroll Position Tracking:

Use JavaScript to determine the section's visibility percentage relative to the viewport.
The percentage is used as the scale factor, ensuring smooth transitions.
Enhancing User Experience:

The scaling effect adds an interactive and visually appealing element to the page.
The animation is tied to user interaction, making it intuitive and engaging.



