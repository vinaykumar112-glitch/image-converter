<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Image Sketch &amp; Colorizer</title>
<style>
  /* Reset and base */
  * {
    box-sizing: border-box;
  }
  body {
    margin: 0;
    background: #181818;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    color: #eee;
    min-height: 100vh;
    display: flex;
    flex-direction: column;
  }
  header {
    background-color: #222;
    padding: 12px 24px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    box-shadow: 0 2px 6px rgba(25,150,250,0.6);
  }
  nav {
    display: flex;
    gap: 20px;
  }
  nav a {
    color: #a9d6e5;
    text-decoration: none;
    font-weight: 600;
    padding: 4px 8px;
    border-radius: 6px;
    transition: background-color 0.3s ease;
    cursor: pointer;
  }
  nav a:hover, nav a.active {
    background-color: #40c4ff;
    color: #222;
  }
  .logo {
    font-weight: 700;
    font-size: 1.3rem;
    color: #40c4ff;
    letter-spacing: 1.5px;
  }
  main {
    flex-grow: 1;
    display: flex;
    justify-content: center;
  }
  /* Container for dynamic content sections */
  .content-container {
    max-width: 900px;
    width: 100%;
    background: #222;
    border-radius: 12px;
    padding: 20px;
    box-shadow: 0 0 16px #40c4ffaa;
    margin: 24px;
    color: #eee;
  }

  /* Styles for Home section */
  #homeSection #controls, #homeSection #colorAreaControls {
    display: flex;
    flex-wrap: wrap;
    gap: 12px;
    align-items: center;
    justify-content: flex-start;
  }
  #homeSection label {
    font-weight: 600;
    user-select: none;
  }
  #homeSection input[type="file"], #homeSection input[type="number"] {
    background: #333;
    border-radius: 8px;
    border: none;
    color: #eee;
    font-size: 1rem;
    padding: 6px 12px;
    width: 90px;
  }
  #homeSection input[type="number"] {
    appearance: textfield;
    -moz-appearance: textfield;
  }
  #homeSection input[type="number"]::-webkit-inner-spin-button, 
  #homeSection input[type="number"]::-webkit-outer-spin-button { 
    -webkit-appearance: none; 
    margin: 0; 
  }
  #homeSection select, #homeSection input[type="color"] {
    padding: 8px 12px;
    border-radius: 8px;
    border: none;
    background: #333;
    color: #eee;
    font-size: 1rem;
    cursor: pointer;
    transition: background 0.3s ease;
  }
  #homeSection select:hover, #homeSection input[type="color"]:hover {
    background: #555;
  }
  #homeSection button {
    background: #40c4ff;
    border: none;
    color: #222;
    font-weight: 700;
    padding: 10px 20px;
    border-radius: 10px;
    cursor: pointer;
    transition: background 0.3s ease;
    user-select: none;
    flex-shrink: 0;
  }
  #homeSection button:hover {
    background: #00a1ff;
  }
  #homeSection #canvasContainer {
    position: relative;
    background: #111;
    border-radius: 12px;
    overflow: hidden;
    align-self: center;
    box-shadow: 0 0 20px #1696ffaa;
  }
  #homeSection canvas {
    display: block;
    max-width: 100%;
    height: auto;
    border-radius: 12px;
    cursor: crosshair;
  }
  #homeSection #instructions {
    font-size: 0.9rem;
    color: #a0a0a0;
    margin-top: 8px;
  }

  /* Styles for About section */
  #aboutSection {
    font-size: 1.1rem;
    line-height: 1.5;
  }

  /* Styles for Login section */
  #loginSection {
    max-width: 400px;
    margin: 0 auto;
  }
  #loginSection h2 {
    color: #40c4ff;
    margin-bottom: 16px;
    font-weight: 700;
  }
  #loginSection form {
    display: flex;
    flex-direction: column;
    gap: 14px;
  }
  #loginSection label {
    font-weight: 600;
  }
  #loginSection input[type="text"], #loginSection input[type="password"] {
    padding: 10px 12px;
    font-size: 1rem;
    border-radius: 8px;
    border: none;
    background: #333;
    color: #eee;
  }
  #loginSection input[type="text"]:focus, #loginSection input[type="password"]:focus {
    outline: 2px solid #40c4ff;
  }
  #loginSection button {
    background: #40c4ff;
    border: none;
    color: #222;
    font-weight: 700;
    padding: 12px 20px;
    border-radius: 10px;
    cursor: pointer;
    transition: background 0.3s ease;
    user-select: none;
  }
  #loginSection button:hover {
    background: #00a1ff;
  }
  #loginSection .message {
    margin-top: 12px;
    font-size: 0.95rem;
    color: #ff7070;
    min-height: 20px;
  }

  /* Styles for Registration section */
  #registerSection {
    max-width: 400px;
    margin: 0 auto;
  }
  #registerSection h2 {
    color: #40c4ff;
    margin-bottom: 16px;
    font-weight: 700;
  }
  #registerSection form {
    display: flex;
    flex-direction: column;
    gap: 14px;
  }
  #registerSection label {
    font-weight: 600;
  }
  #registerSection input[type="text"], #registerSection input[type="password"] {
    padding: 10px 12px;
    font-size: 1rem;
    border-radius: 8px;
    border: none;
    background: #333;
    color: #eee;
  }
  #registerSection button {
    background: #40c4ff;
    border: none;
    color: #222;
    font-weight: 700;
    padding: 12px 20px;
    border-radius: 10px;
    cursor: pointer;
    transition: background 0.3s ease;
    user-select: none;
  }
  #registerSection button:hover {
    background: #00a1ff;
  }
  #registerSection .message {
    margin-top: 12px;
    font-size: 0.95rem;
    color: #ff7070;
    min-height: 20px;
  }
</style>
</head>
<body>
  <header>
    <div class="logo">SketchColorizer</div>
    <nav>
      <a href="#" class="active" id="loginNav">Login</a>
      <a href="#" id="registerNav">Register</a>
      <a href="#" id="aboutNav" style="display:none;">About</a>
      <a href="#" id="homeNav" style="display:none;">Home</a>
    </nav>
  </header>
  <main>
    <!-- Login Section -->
    <section id="loginSection" class="content-container">
      <h2>Login</h2>
      <form id="loginForm" autocomplete="off">
        <label for="username">Username</label>
        <input type="text" id="username" name="username" placeholder="Enter username" required autocomplete="username">
        
        <label for="password">Password</label>
        <input type="password" id="password" name="password" placeholder="Enter password" required autocomplete="current-password">
        
        <button type="submit">Login</button>
        <div class="message" id="loginMessage"></div>
      </form>
    </section>

    <!-- Registration Section -->
    <section id="registerSection" class="content-container" style="display:none;">
      <h2>Register</h2>
      <form id="registerForm" autocomplete="off">
        <label for="regUsername">Username</label>
        <input type="text" id="regUsername" name="regUsername" placeholder="Choose a username" required>
        
        <label for="regPassword">Password</label>
        <input type="password" id="regPassword" name="regPassword" placeholder="Choose a password" required>
        
        <button type="submit">Register</button>
        <div class="message" id="registerMessage"></div>
      </form>
    </section>

    <!-- About Section -->
    <section id="aboutSection" class="content-container" style="display:none;">
      <h2>About SketchColorizer</h2>
      <p>SketchColorizer is a client-side web application that converts your images into beautiful pencil sketches using advanced canvas image processing techniques. Beyond just sketching, this app lets you selectively color parts of your sketch by providing coordinate inputs, creating artistic hybrid images.</p>
      <p>This app uses pure HTML, CSS, and JavaScript — you don’t need to upload your images to any server; everything happens in your browser, keeping your images private and safe.</p>
      <p>Use SketchColorizer to create unique artwork, shareable sketches, and have fun exploring creative effects on your photos.</p>      
    </section>

    <!-- Home Section -->
    <section id="homeSection" class="content-container" style="display:none;">
      <div id="controls">
        <label for="uploadImage">Upload Image:
          <input type="file" id="uploadImage" accept="image/*" />
        </label>

        <label for="modeSelect">Effect Mode:
          <select id="modeSelect" disabled>
            <option value="none">None</option>
            <option value="grayscale">Grayscale</option>
            <option value="blackwhite">Black &amp; White</option>
            <option value="pencil">Pencil Sketch</option>
            <option value="sketch">Sketch</option>
            <option value="softblur">Soft Blur</option>
            <option value="dotted">Dotted Sketch</option>
          </select>
        </label>

        <button id="resetBtn" disabled>Reset</button>
        <button id="downloadBtn" disabled>Download Image</button>
      </div>

      <div id="colorAreaControls" style="margin-top:10px;">
        <label>X Start:
          <input type="number" id="xStart" min="0" step="1" disabled />
        </label>
        <label>Y Start:
          <input type="number" id="yStart" min="0" step="1" disabled />
        </label>
        <label>X End:
          <input type="number" id="xEnd" min="0" step="1" disabled />
        </label>
        <label>Y End:
          <input type="number" id="yEnd" min="0" step="1" disabled />
        </label>
        <button id="applyColorBtn" disabled>Apply Color to Area</button>
        <button id="clearColorBtn" disabled>Clear Colored Area</button>
      </div>

      <div id="canvasContainer">
        <canvas id="canvas"></canvas>
      </div>
      <div id="instructions">Upload an image, select an effect, then optionally input coordinates to color that part of the image selectively on the sketch.</div>
    </section>
  </main>

<script>
(() => {
  const uploadImage = document.getElementById('uploadImage');
  const modeSelect = document.getElementById('modeSelect');
  const resetBtn = document.getElementById('resetBtn');
  const downloadBtn = document.getElementById('downloadBtn');

  const xStartInput = document.getElementById('xStart');
  const yStartInput = document.getElementById('yStart');
  const xEndInput = document.getElementById('xEnd');
  const yEndInput = document.getElementById('yEnd');
  const applyColorBtn = document.getElementById('applyColorBtn');
  const clearColorBtn = document.getElementById('clearColorBtn');

  const homeNav = document.getElementById('homeNav');
  const aboutNav = document.getElementById('aboutNav');
  const loginNav = document.getElementById('loginNav');
  const registerNav = document.getElementById('registerNav');
  const homeSection = document.getElementById('homeSection');
  const aboutSection = document.getElementById('aboutSection');
  const loginSection = document.getElementById('loginSection');
  const registerSection = document.getElementById('registerSection');
  const loginForm = document.getElementById('loginForm');
  const loginMessage = document.getElementById('loginMessage');
  const registerForm = document.getElementById('registerForm');
  const registerMessage = document.getElementById('registerMessage');

  const canvas = document.getElementById('canvas');
  const ctx = canvas.getContext('2d');

  let originalImage = null;
  let imageDataOriginal = null;
  let currentEffect = 'none';

  let imageDataSketch = null;
  let colorAreaApplied = false;

  // Simple in-memory "database" for registered users
  // Stored in localStorage for persistence
  function getUsers() {
    const users = localStorage.getItem('sc_users');
    return users ? JSON.parse(users) : {};
  }
  function saveUsers(users) {
    localStorage.setItem('sc_users', JSON.stringify(users));
  }

  // Navigation content control
  function showSection(section) {
    homeSection.style.display = 'none';
    aboutSection.style.display = 'none';
    loginSection.style.display = 'none';
    registerSection.style.display = 'none';

    // Hide or show nav links depending on login status
    const loggedIn = isLoggedIn();
    loginNav.style.display = loggedIn ? 'none' : 'inline';
    registerNav.style.display = loggedIn ? 'none' : 'inline';
    homeNav.style.display = loggedIn ? 'inline' : 'none';
    aboutNav.style.display = loggedIn ? 'inline' : 'none';

    homeNav.classList.remove('active');
    aboutNav.classList.remove('active');
    loginNav.classList.remove('active');
    registerNav.classList.remove('active');

    switch(section) {
      case 'home':
        if (!loggedIn) {
          showSection('login');
          return;
        }
        homeSection.style.display = 'block';
        homeNav.classList.add('active');
        break;
      case 'about':
        if (!loggedIn) {
          showSection('login');
          return;
        }
        aboutSection.style.display = 'block';
        aboutNav.classList.add('active');
        break;
      case 'login':
        loginSection.style.display = 'block';
        loginNav.classList.add('active');
        break;
      case 'register':
        registerSection.style.display = 'block';
        registerNav.classList.add('active');
        break;
    }
    // Clear messages on navigation
    loginMessage.textContent = '';
    registerMessage.textContent = '';
    // Reset forms when switching away
    if (section !== 'login') loginForm.reset();
    if (section !== 'register') registerForm.reset();
  }

  loginNav.addEventListener('click', e => {
    e.preventDefault();
    showSection('login');
  });
  registerNav.addEventListener('click', e => {
    e.preventDefault();
    showSection('register');
  });
  aboutNav.addEventListener('click', e => {
    e.preventDefault();
    showSection('about');
  });
  homeNav.addEventListener('click', e => {
    e.preventDefault();
    showSection('home');
  });

  function isLoggedIn() {
    return !!localStorage.getItem('sc_loggedInUser');
  }
  function setLoggedInUser(username) {
    localStorage.setItem('sc_loggedInUser', username);
  }
  function clearLoggedInUser() {
    localStorage.removeItem('sc_loggedInUser');
  }

  // Login form logic
  loginForm.addEventListener('submit', e => {
    e.preventDefault();
    const username = loginForm.username.value.trim();
    const password = loginForm.password.value;
    const users = getUsers();

    if (users[username] && users[username] === password) {
      setLoggedInUser(username);
      loginMessage.style.color = '#8FEE98';  // success green
      loginMessage.textContent = 'Login successful! Welcome, ' + username + '.';
      setTimeout(() => {
        showSection('home');
      }, 1000);
    } else {
      loginMessage.style.color = '#ff7070';
      loginMessage.textContent = 'Invalid username or password.';
    }
  });

  // Registration form logic
  registerForm.addEventListener('submit', e => {
    e.preventDefault();
    const username = registerForm.regUsername.value.trim();
    const password = registerForm.regPassword.value;
    const users = getUsers();

    if (!username || !password) {
      registerMessage.style.color = '#ff7070';
      registerMessage.textContent = 'Please enter username and password.';
      return;
    }
    if (users[username]) {
      registerMessage.style.color = '#ff7070';
      registerMessage.textContent = 'Username already taken.';
      return;
    }
    users[username] = password;
    saveUsers(users);
    registerMessage.style.color = '#8FEE98';
    registerMessage.textContent = 'Registration successful! You can now log in.';
    setTimeout(() => {
      showSection('login');
    }, 1500);
  });

  // Image and canvas handling code below

  function loadImageFromFile(file) {
    return new Promise((resolve, reject) => {
      const img = new Image();
      img.onload = () => resolve(img);
      img.onerror = e => reject(e);
      img.src = URL.createObjectURL(file);
    });
  }

  function resizeCanvas(img) {
    const maxDim = 800;
    let w = img.width;
    let h = img.height;
    if (w > maxDim || h > maxDim) {
      let ratio = Math.min(maxDim / w, maxDim / h);
      w = Math.round(w * ratio);
      h = Math.round(h * ratio);
    }
    canvas.width = w;
    canvas.height = h;
  }

  function blurImage(imageData, radius=5) {
    const w = imageData.width;
    const h = imageData.height;
    const data = imageData.data;
    const temp = new Uint8ClampedArray(data.length);
    temp.set(data);
    const r = radius;

    for(let y=0; y<h; y++) {
      for(let x=0; x<w; x++) {
        let rSum=0,gSum=0,bSum=0,aSum=0;
        let count=0;
        for(let dy=-r; dy<=r; dy++) {
          let ny = y + dy;
          if(ny>=0 && ny<h) {
            for(let dx=-r; dx<=r; dx++) {
              let nx = x + dx;
              if(nx>=0 && nx<w) {
                const idx = (ny*w + nx)*4;
                rSum += temp[idx];
                gSum += temp[idx+1];
                bSum += temp[idx+2];
                aSum += temp[idx+3];
                count++;
              }
            }
          }
        }
        const idx = (y*w + x)*4;
        data[idx] = rSum/count;
        data[idx+1] = gSum/count;
        data[idx+2] = bSum/count;
        data[idx+3] = aSum/count;
      }
    }
  }

  function colorDodge(base, blend) {
    return blend === 255 ? blend : Math.min(255, (base << 8 ) / (255 - blend));
  }

  function pencilSketch(imgCtx, width, height) {
    const imgData = imgCtx.getImageData(0, 0, width, height);
    const grayData = new ImageData(width, height);
    const sketchData = new ImageData(width, height);

    for(let i=0; i<imgData.data.length; i+=4) {
      const avg = 0.299*imgData.data[i] + 0.587*imgData.data[i+1] + 0.114*imgData.data[i+2];
      grayData.data[i] = grayData.data[i+1] = grayData.data[i+2] = avg;
      grayData.data[i+3] = imgData.data[i+3];
    }

    const invData = new Uint8ClampedArray(grayData.data);
    for(let i=0; i<invData.length; i+=4) {
      invData[i] = 255 - invData[i];
      invData[i+1] = 255 - invData[i+1];
      invData[i+2] = 255 - invData[i+2];
      invData[i+3] = invData[i+3];
    }

    const tempCanvas = document.createElement('canvas');
    tempCanvas.width = width;
    tempCanvas.height = height;
    const tempCtx = tempCanvas.getContext('2d');
    tempCtx.putImageData(new ImageData(invData, width, height), 0, 0);

    let blurred = tempCtx.getImageData(0, 0, width, height);
    for(let i=0; i<3; i++) {
      blurImage(blurred, 5);
    }
    tempCtx.putImageData(blurred, 0, 0);
    blurred = tempCtx.getImageData(0,0,width,height);

    for(let i=0; i<sketchData.data.length; i+=4) {
      sketchData.data[i] = colorDodge(grayData.data[i], blurred.data[i]);
      sketchData.data[i+1] = colorDodge(grayData.data[i+1], blurred.data[i+1]);
      sketchData.data[i+2] = colorDodge(grayData.data[i+2], blurred.data[i+2]);
      sketchData.data[i+3] = grayData.data[i+3];
    }
    return sketchData;
  }

  function sketchEffect(imgCtx, width, height) {
    const imgData = imgCtx.getImageData(0, 0, width, height);
    const output = imgCtx.createImageData(width, height);
    const gray = new Uint8ClampedArray(width * height);
    for(let i=0; i<width*height; i++) {
      const idx = i*4;
      const val = 0.299*imgData.data[idx] + 0.587*imgData.data[idx +1] + 0.114*imgData.data[idx +2];
      gray[i] = val;
    }
    const kernelX = [-1,0,1,-2,0,2,-1,0,1];
    const kernelY = [-1,-2,-1,0,0,0,1,2,1];
    for(let y=1; y<height-1; y++) {
      for(let x=1; x<width-1; x++) {
        let gx=0, gy=0;
        for(let ky=-1; ky<=1; ky++) {
          for(let kx=-1; kx<=1; kx++) {
            const px = x + kx;
            const py = y + ky;
            const val = gray[py*width + px];
            const kIdx = (ky+1)*3 + (kx+1);
            gx += val * kernelX[kIdx];
            gy += val * kernelY[kIdx];
          }
        }
        let g = Math.sqrt(gx*gx + gy*gy);
        g = Math.min(255, g*2);
        const idx = (y*width + x)*4;
        output.data[idx] = output.data[idx+1] = output.data[idx+2] = 255 - g;
        output.data[idx+3] = 255;
      }
    }
    return output;
  }

  function dottedSketch(imgCtx, width, height) {
    const sketch = sketchEffect(imgCtx, width, height);
    const data = sketch.data;
    const output = imgCtx.createImageData(width, height);
    for(let i=0; i<data.length; i+=4) {
      const v = data[i];
      if (v < 100 && Math.random() < 0.08) {
        output.data[i] = output.data[i+1] = output.data[i+2] = 0;
        output.data[i+3] = 255;
      } else {
        output.data[i] = output.data[i+1] = output.data[i+2] = 255;
        output.data[i+3] = 255;
      }
    }
    return output;
  }

  function softBlurEffect(imgCtx, width, height) {
    const imgData = imgCtx.getImageData(0,0,width,height);
    for(let i=0; i<2; i++) {
      blurImage(imgData, 8);
    }
    return imgData;
  }

  function applyGrayscale(imgCtx, width, height) {
    const imgData = imgCtx.getImageData(0, 0, width, height);
    const data = imgData.data;
    for(let i = 0; i < data.length; i += 4) {
      const avg = 0.299 * data[i] + 0.587 * data[i + 1] + 0.114 * data[i + 2];
      data[i] = data[i + 1] = data[i + 2] = avg;
    }
    return imgData;
  }

  function applyBlackWhite(imgCtx, width, height) {
    const imgData = imgCtx.getImageData(0, 0, width, height);
    const data = imgData.data;
    for(let i = 0; i < data.length; i += 4) {
      const avg = 0.299 * data[i] + 0.587 * data[i + 1] + 0.114 * data[i + 2];
      const bw = avg > 128 ? 255 : 0; // Threshold at mid-level
      data[i] = data[i + 1] = data[i + 2] = bw;
    }
    return imgData;
  }

  function drawOriginalImage(image) {
    resizeCanvas(image);
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    ctx.filter = 'none';
    ctx.globalAlpha = 1.0;
    ctx.drawImage(image, 0, 0, canvas.width, canvas.height);
    imageDataOriginal = ctx.getImageData(0, 0, canvas.width, canvas.height);
  }

  function drawCoordinateGrid() {
    if(!imageDataSketch) return;
    const w = canvas.width;
    const h = canvas.height;
    ctx.save();
    ctx.strokeStyle = 'rgba(25, 150, 250, 0.6)';
    ctx.lineWidth = 1.5;
    ctx.fillStyle = 'rgba(25, 150, 250, 0.8)';
    ctx.font = '13px Segoe UI, Tahoma, Geneva, Verdana, sans-serif';
    ctx.textBaseline = 'top';

    const gridSpacing = 100;
    for(let x=0; x<=w; x += gridSpacing) {
      ctx.beginPath();
      ctx.moveTo(x,0);
      ctx.lineTo(x,h);
      ctx.stroke();
      ctx.fillText(($x, 0), x+4, h-18);
    }
    for(let y=0; y<=h; y += gridSpacing) {
      ctx.beginPath();
      ctx.moveTo(0,y);
      ctx.lineTo(w,y);
      ctx.stroke();
      ctx.fillText((0, $y), 4, y+4);
    }
    ctx.restore();
  }

  function applyEffect(effect) {
    if (!imageDataOriginal) return;
    ctx.putImageData(imageDataOriginal, 0, 0);
    const width = canvas.width;
    const height = canvas.height;
    let resultImageData;

    switch(effect) {
      case 'grayscale': resultImageData = applyGrayscale(ctx, width, height); break;
      case 'blackwhite': resultImageData = applyBlackWhite(ctx, width, height); break;
      case 'pencil': resultImageData = pencilSketch(ctx, width, height); break;
      case 'sketch': resultImageData = sketchEffect(ctx, width, height); break;
      case 'softblur': resultImageData = softBlurEffect(ctx, width, height); break;
      case 'dotted': resultImageData = dottedSketch(ctx, width, height); break;
      case 'none':
      default: resultImageData = imageDataOriginal; break;
    }
    ctx.putImageData(resultImageData, 0, 0);
    imageDataSketch = resultImageData;
    drawCoordinateGrid();
    colorAreaApplied = false;
    clearColorBtn.disabled = true;
  }

  function applyColorToArea() {
    if(!originalImage || !imageDataSketch) return;

    clearColorBtn.disabled = false;

    const xs = parseInt(xStartInput.value);
    const ys = parseInt(yStartInput.value);
    const xe = parseInt(xEndInput.value);
    const ye = parseInt(yEndInput.value);

    if(isNaN(xs) || isNaN(ys) || isNaN(xe) || isNaN(ye)) {
      alert('Please enter valid numeric coordinates.');
      return;
    }
    if(xs < 0 || ys < 0 || xe > canvas.width || ye > canvas.height || xs >= xe || ys >= ye) {
      alert('Coordinates out of bounds or invalid (start must be less than end).');
      return;
    }

    // Draw the sketch first
    ctx.putImageData(imageDataSketch, 0, 0);

    // Draw coordinate grid on top
    drawCoordinateGrid();

    // Draw the original colored area from original image for the coordinates
    const tempCanvas = document.createElement('canvas');
    tempCanvas.width = canvas.width;
    tempCanvas.height = canvas.height;
    const tempCtx = tempCanvas.getContext('2d');
    tempCtx.drawImage(originalImage, 0, 0, canvas.width, canvas.height);
    const originalData = tempCtx.getImageData(xs, ys, xe - xs, ye - ys);
    ctx.putImageData(originalData, xs, ys);
    colorAreaApplied = true;
  }

  function clearColoredArea() {
    if(!imageDataSketch) return;
    ctx.putImageData(imageDataSketch, 0, 0);
    drawCoordinateGrid();
    colorAreaApplied = false;
    clearColorBtn.disabled = true;
  }

  async function handleImageChange(e) {
    if (!e.target.files || e.target.files.length === 0) return;
    try {
      const img = await loadImageFromFile(e.target.files[0]);
      originalImage = img;

      modeSelect.disabled = false;
      resetBtn.disabled = false;
      downloadBtn.disabled = false;
      xStartInput.disabled = false;
      yStartInput.disabled = false;
      xEndInput.disabled = false;
      yEndInput.disabled = false;
      applyColorBtn.disabled = false;
      clearColorBtn.disabled = true;

      currentEffect = 'none';
      modeSelect.value = 'none';

      drawOriginalImage(img);
      imageDataSketch = ctx.getImageData(0, 0, canvas.width, canvas.height);

      drawCoordinateGrid();

      colorAreaApplied = false;
    } catch(err) {
      alert('Error loading image: ' + err.message);
    }
  }

  function downloadImage() {
    if (!canvas) return;
    canvas.toBlob(blob => {
      const url = URL.createObjectURL(blob);
      const a = document.createElement('a');
      a.href = url;
      a.download = 'sketch_colored_image.png';
      document.body.appendChild(a);
      a.click();
      setTimeout(() => {
        document.body.removeChild(a);
        URL.revokeObjectURL(url);
      }, 0);
    });
  }

  // On page load: check if logged in and set view
  document.addEventListener('DOMContentLoaded', () => {
    if (isLoggedIn()) {
      showSection('home');
    } else {
      showSection('login');
    }
  });

  uploadImage.addEventListener('change', handleImageChange);
  modeSelect.addEventListener('change', e => {
    currentEffect = e.target.value;
    applyEffect(currentEffect);
  });
  resetBtn.addEventListener('click', () => {
    if (!originalImage) return;
    currentEffect = 'none';
    modeSelect.value = 'none';
    drawOriginalImage(originalImage);
    imageDataSketch = ctx.getImageData(0, 0, canvas.width, canvas.height);
    drawCoordinateGrid();
    colorAreaApplied = false;
    clearColorBtn.disabled = true;
    xStartInput.value = '';
    yStartInput.value = '';
    xEndInput.value = '';
    yEndInput.value = '';
  });
  applyColorBtn.addEventListener('click', applyColorToArea);
  clearColorBtn.addEventListener('click', clearColoredArea);
  downloadBtn.addEventListener('click', downloadImage);

})();
</script>
</body>
</html>
