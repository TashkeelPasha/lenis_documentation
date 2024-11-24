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
```js
Initialize Lenis for smooth scrolling.
Use Intersection Observer to monitor visibility of content blocks.
Logic Breakdown:

Lenis Smooth Scrolling:

Lenis overrides the native scroll behavior to make the scrolling effect fluid and responsive.
Hook Lenis updates to the requestAnimationFrame for continuous updates.
Intersection Observer:

Observe each content block and toggle classes based on visibility.
Use these classes for animations like scaling or fading.
javascript
Copy code
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

