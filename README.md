
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Système Économique - Royaume-Uni</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 0;
      background-color: #f5f5f5;
    }
    .container {
      max-width: 600px;
      margin: 20px auto;
      padding: 20px;
      background-color: #fff;
      border-radius: 8px;
      box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    }
    h1, h2 {
      color: #333;
    }
    .section {
      margin-bottom: 20px;
    }
    button {
      margin-top: 10px;
      padding: 10px 15px;
      background-color: #007bff;
      color: #fff;
      border: none;
      border-radius: 4px;
      cursor: pointer;
    }
    button:hover {
      background-color: #0056b3;
    }
    ul {
      padding-left: 20px;
      list-style-type: disc;
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>Système Économique - Royaume-Uni</h1>

    <section class="section resources" aria-labelledby="resources-title">
      <h2 id="resources-title">Ressources</h2>
      <p>Minerais/Roche: <span id="minerals">150</span></p>
      <p>Ressources Alimentaires: <span id="food">100</span></p>
      <p>Ressources Luxueuses: <span id="luxury">80</span></p>
    </section>

    <section class="section buildings" aria-labelledby="buildings-title">
      <h2 id="buildings-title">Bâtiments</h2>
      <p>Mines: <span id="mines">15</span></p>
      <p>Champs: <span id="fields">10</span></p>
      <p>Industries Légères: <span id="industries">8</span></p>
      <p>Infrastructures: <span id="infrastructures">0</span></p>
      <button id="increase-infrastructure">Augmenter</button>
    </section>

    <section class="section queue" aria-labelledby="queue-title">
      <h2 id="queue-title">File de Construction</h2>
      <ul id="constructionQueue" aria-live="polite"></ul>
      <button id="validate-construction">Valider la première construction</button>
    </section>

    <section class="section build-options" aria-labelledby="build-options-title">
      <h2 id="build-options-title">Construire</h2>
      <button data-building="mine">Ajouter une Mine à la file (Gratuit)</button>
      <button data-building="field">Ajouter un Champ à la file (Gratuit)</button>
      <button data-building="industry">Ajouter une Industrie Légère à la file (Coût: 5 minerais)</button>
    </section>
  </div>

  <script>
    document.addEventListener('DOMContentLoaded', () => {
      let minerals = 150;
      let food = 100;
      let luxury = 80;
      let mines = 15;
      let fields = 10;
      let industries = 8;
      let infrastructures = 0;
      const constructionQueue = [];

      const updateResources = () => {
        document.getElementById('minerals').textContent = minerals;
        document.getElementById('food').textContent = food;
        document.getElementById('luxury').textContent = luxury;
        document.getElementById('mines').textContent = mines;
        document.getElementById('fields').textContent = fields;
        document.getElementById('industries').textContent = industries;
        document.getElementById('infrastructures').textContent = infrastructures;
      };

      const updateQueueDisplay = () => {
        const queueElement = document.getElementById('constructionQueue');
        queueElement.innerHTML = '';
        constructionQueue.forEach((building, index) => {
          const li = document.createElement('li');
          li.textContent = building;
          queueElement.appendChild(li);
        });
      };

      const validateConstruction = () => {
        if (constructionQueue.length > 0) {
          const building = constructionQueue.shift();
          switch (building) {
            case 'mine':
              minerals += 150;
              mines++;
              break;
            case 'field':
              food += 100;
              fields++;
              break;
            case 'industry':
              if (minerals >= 5) {
                minerals -= 5;
                luxury += 10;
                industries++;
              } else {
                alert('Pas assez de ressources pour construire une Industrie Légère !');
                constructionQueue.unshift(building);
                return;
              }
              break;
          }
          updateResources();
          updateQueueDisplay();
        }
      };

      const increaseInfrastructure = () => {
        infrastructures++;
        updateResources();
      };

      const queueBuilding = (type) => {
        constructionQueue.push(type);
        updateQueueDisplay();
      };

      document.getElementById('increase-infrastructure').addEventListener('click', increaseInfrastructure);
      document.getElementById('validate-construction').addEventListener('click', validateConstruction);

      document.querySelectorAll('[data-building]').forEach(button => {
        button.addEventListener('click', () => queueBuilding(button.getAttribute('data-building')));
      });

      updateResources();
    });
  </script>
</body>
</html>
Ajout du fichier index.html
