<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Responsive Image Gallery</title>
  <style>
    * {
      box-sizing: border-box;
    }

    body {
      font-family: Arial, sans-serif;
      margin: 0;
      background: #f4f4f4;
    }

    h1 {
      text-align: center;
      padding: 20px;
    }

    .filter-buttons {
      text-align: center;
      margin-bottom: 20px;
    }

    .filter-buttons button {
      padding: 10px 20px;
      margin: 5px;
      border: none;
      cursor: pointer;
      background: #333;
      color: white;
      border-radius: 5px;
      transition: background 0.3s;
    }

    .filter-buttons button:hover {
      background: #555;
    }

    .gallery {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
      gap: 15px;
      padding: 20px;
    }

    .gallery-item {
      position: relative;
      overflow: hidden;
      cursor: pointer;
    }

    .gallery-item img {
      width: 100%;
      height: auto;
      display: block;
      transition: transform 0.4s ease;
    }

    .gallery-item:hover img {
      transform: scale(1.1);
    }

    /* Lightbox */
    .lightbox {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: rgba(0,0,0,0.9);
      display: none;
      justify-content: center;
      align-items: center;
      z-index: 9999;
    }

    .lightbox img {
      max-width: 90%;
      max-height: 80vh;
    }

    .lightbox .close, .lightbox .prev, .lightbox .next {
      position: absolute;
      color: white;
      font-size: 2em;
      cursor: pointer;
      padding: 10px;
      user-select: none;
    }

    .lightbox .close {
      top: 10px;
      right: 20px;
    }

    .lightbox .prev {
      left: 20px;
      top: 50%;
      transform: translateY(-50%);
    }

    .lightbox .next {
      right: 20px;
      top: 50%;
      transform: translateY(-50%);
    }

    @media (max-width: 600px) {
      .lightbox .prev, .lightbox .next {
        font-size: 1.5em;
      }
    }
  </style>
</head>
<body>

<h1>Responsive Image Gallery</h1>

<div class="filter-buttons">
  <button onclick="filterImages('all')">All</button>
  <button onclick="filterImages('nature')">Nature</button>
  <button onclick="filterImages('city')">City</button>
</div>

<div class="gallery" id="gallery">
  <div class="gallery-item" data-category="nature"><img src="C:\Users\rohit\OneDrive\Desktop\power bi\project internpe\images (1).jpg" alt="Nature 1"></div>
  <div class="gallery-item" data-category="nature"><img src="C:\Users\rohit\OneDrive\Desktop\power bi\project internpe\download (1).jpg" alt="Nature 2"></div>
  <div class="gallery-item" data-category="city"><img src="C:\Users\rohit\OneDrive\Desktop\power bi\project internpe\pexels-peng-liu-45946-169647.jpg" alt="City 2"></div>
  <div class="gallery-item" data-category="nature"><img src="C:\Users\rohit\OneDrive\Desktop\power bi\project internpe\download (2).jpg" alt="Nature 3"></div>
  <div class="gallery-item" data-category="city"><img src="C:\Users\rohit\OneDrive\Desktop\power bi\project internpe\images.jpg" alt="City 3"></div>
</div>

<!-- Lightbox -->
<div class="lightbox" id="lightbox">
  <span class="close" onclick="closeLightbox()">×</span>
  <span class="prev" onclick="prevImage()">❮</span>
  <img id="lightbox-img" src="">
  <span class="next" onclick="nextImage()">❯</span>
</div>

<script>
  const galleryItems = document.querySelectorAll('.gallery-item');
  const lightbox = document.getElementById('lightbox');
  const lightboxImg = document.getElementById('lightbox-img');
  let currentIndex = 0;

  galleryItems.forEach((item, index) => {
    item.addEventListener('click', () => {
      currentIndex = index;
      openLightbox(item.querySelector('img').src);
    });
  });

  function openLightbox(src) {
    lightbox.style.display = 'flex';
    lightboxImg.src = src;
  }

  function closeLightbox() {
    lightbox.style.display = 'none';
  }

  function prevImage() {
    currentIndex = (currentIndex - 1 + galleryItems.length) % galleryItems.length;
    lightboxImg.src = galleryItems[currentIndex].querySelector('img').src;
  }

  function nextImage() {
    currentIndex = (currentIndex + 1) % galleryItems.length;
    lightboxImg.src = galleryItems[currentIndex].querySelector('img').src;
  }

  function filterImages(category) {
    galleryItems.forEach(item => {
      if (category === 'all' || item.dataset.category === category) {
        item.style.display = 'block';
      } else {
        item.style.display = 'none';
      }
    });
  }
</script>

</body>
</html>
