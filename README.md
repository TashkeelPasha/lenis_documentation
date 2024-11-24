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

