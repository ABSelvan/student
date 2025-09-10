---
toc: True
layout: post
data: tools
title: Account Creation
description: Learn how to create and manage course-required accounts, including a Portfolio Website, GitHub, Slack, and LinkedIn, while protecting your Personal Identifiable Information (PII).
categories: ['DevOps']
permalink: blogtoll
breadcrumb: True
author: John Mortensen
---
# 🖥️ My AP CSP Setup and First Canvas Project


Welcome to my **AP Computer Science Principles (CSP)** blog! 🎉  

This notebook will walk through:  
1. How I installed the tools I need (VS Code, Git, Node.js, Jupyter).  
2. How I set up my environment for coding.  
3. My first web-based project using **HTML Canvas and JavaScript**.  

## 🔧 Installing Visual Studio Code

- I went to [https://code.visualstudio.com](https://code.visualstudio.com)  
- Downloaded the version for my operating system (Windows/Mac/Linux).  
- Installed it with the default options.  
- Added extensions:  
  - **Prettier - Code Formatter** (for clean code)  
  - **Live Server** (to preview web pages in the browser)  
  - **Jupyter** (to run notebooks inside VS Code).  


## 🌐 Installing Git and Setting Up GitHub

- Installed Git from [https://git-scm.com/downloads](https://git-scm.com/downloads).  
- Opened a terminal and checked it with:  
```bash
git --version
```
- Created a free GitHub account at [https://github.com](https://github.com).  
- Set up SSH keys to connect VS Code with GitHub for pushing my code.  


---
# 🚀 First Project: Background with an Object

Now that the tools are ready, let’s build a project that displays a **background image** 
with a **sprite** (like a UFO) using JavaScript and the HTML `<canvas>` element.  


## 📝 Frontmatter (used in static site generators)

```yaml
---
layout: base
title: Background with Object
description: Use JavaScript to have an in motion background.
sprite: images/platformer/sprites/flying-ufo.png
background: images/platformer/backgrounds/alien_planet1.jpg
permalink: /background
---
```


## 🎨 Canvas Setup

```html
<canvas id="world"></canvas>
```


## 🖥️ JavaScript Code (with Comments)

Here’s the code that loads the background and sprite, making sure both are ready before drawing.

<script>
// 🎨 Get the canvas element from the page
const canvas = document.getElementById("world");
// ✏️ Set up the 2D drawing context
const ctx = canvas.getContext('2d');

// 🌌 Create an Image object for the background
const backgroundImg = new Image();
// 🛸 Create an Image object for the sprite
const spriteImg = new Image();

// 🔗 Set image sources (linked from frontmatter variables)
backgroundImg.src = '{{page.background}}'; 
spriteImg.src = '{{page.sprite}}';

// 📦 Track how many images are loaded
let imagesLoaded = 0;

// ✅ Background loaded
backgroundImg.onload = function() {
    imagesLoaded++;
    startGameWorld();
};

// ✅ Sprite loaded
spriteImg.onload = function() {
    imagesLoaded++;
    startGameWorld();
};

// 🚀 Start the game after both images load
function startGameWorld() {
    if (imagesLoaded === 2) {
        ctx.drawImage(backgroundImg, 0, 0, canvas.width, canvas.height); // Draw background
        ctx.drawImage(spriteImg, 50, 50); // Draw sprite
    }
}
</script>

## ✅ Next Steps

- Try swapping out the `background` image for a different one.  
- Replace the `sprite` with your own character or object.  
- Experiment with animation: make the background scroll or the sprite move.  

This blog shows how I set up my **AP CSP environment** and created my **first interactive project**. 🎉  
