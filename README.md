<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Galerie des Dessinateurs</title>
  <style>
    body {
      font-family: sans-serif;
      background: #f0f0f0;
      margin: 0;
      padding: 20px;
    }
    h1 {
      text-align: center;
    }
    form {
      background: white;
      padding: 20px;
      border-radius: 8px;
      max-width: 500px;
      margin: 0 auto 30px;
      box-shadow: 0 2px 5px rgba(0,0,0,0.1);
    }
    input, button {
      display: block;
      width: 100%;
      margin: 10px 0;
      padding: 10px;
      font-size: 16px;
    }
    .gallery {
      display: flex;
      flex-wrap: wrap;
      gap: 20px;
      justify-content: center;
    }
    .drawing {
      background: white;
      padding: 10px;
      border-radius: 8px;
      box-shadow: 0 2px 5px rgba(0,0,0,0.1);
      width: 250px;
      text-align: center;
    }
    .drawing img {
      max-width: 100%;
      border-radius: 4px;
    }
    .drawing h3 {
      margin: 10px 0 0;
    }
  </style>
</head>
<body>
  <h1>Galerie des Dessinateurs</h1>
  <form id="uploadForm">
    <label for="title">Titre du dessin (obligatoire) :</label>
    <input type="text" id="title" required placeholder="Ex : Mon dragon stylisé">

    <label for="image">Choisis une image :</label>
    <input type="file" id="image" accept="image/*" required>

    <button type="submit">Publier le dessin</button>
  </form>

  <section class="gallery" id="gallery"></section>

  <script>
    const form = document.getElementById('uploadForm');
    const gallery = document.getElementById('gallery');

    form.addEventListener('submit', (e) => {
      e.preventDefault();

      const title = document.getElementById('title').value.trim();
      const fileInput = document.getElementById('image');
      const file = fileInput.files[0];

      if (!title || !file) {
        alert('Merci de remplir tous les champs.');
        return;
      }

      const reader = new FileReader();
      reader.onload = function(event) {
        const drawing = document.createElement('div');
        drawing.className = 'drawing';

        const img = document.createElement('img');
        img.src = event.target.result;

        const caption = document.createElement('h3');
        caption.textContent = title;

        drawing.appendChild(img);
        drawing.appendChild(caption);

        gallery.prepend(drawing);

        // Reset form
        form.reset();
      };
      reader.readAsDataURL(file);
    });
  </script>
</body>
</html>
