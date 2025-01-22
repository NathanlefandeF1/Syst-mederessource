# Syst-mederessource
Systeme de ressource RP
<!DOCTYPE html>
<html lang="fr">
<head>
 <meta charset="UTF-8">
 <meta name="viewport" content="width=device-width, initial-scale=1.0">
 <title>Système Économique - Royaume-Uni</title>
 <style>
 body { font-family: Arial, sans-serif; }
 .container { max-width: 600; margin: auto; padding: 20px; }
 .resources, .buildings, .queue { margin-bottom: 20px; }
 button { margin-top: 10px; display: block; }
 </style>
</head>
<body>
 <div class="container">
 <h1>Système Économique - Royaume-Uni</h1>

 <div class="resources">
 <h2>Ressources</h2>
 <p>Minerais/Roche: <span id="minerals">150</span></p>
 <p>Ressources Alimentaires: <span id="food">100</span></p>
 <p>Ressources Luxueuses: <span id="luxury">80</span></p>
 </div>

 <div class="buildings">
 <h2>Bâtiments</h2>
 <p>Mines: <span id="mines">15</span></p>
 <p>Champs: <span id="fields">10</span></p>
 <p>Industries Légères: <span id="industries">8</span></p>
 <p>Infrastructures: <span id="infrastructures">0</span> <button onclick="increaseInfrastructure()">Augmenter</button></p>
 </div>

 <div class="queue">
 <h2>File de Construction</h2>
 <ul id="constructionQueue"></ul>
 <button onclick="validateConstruction()">Valider la première construction</button>
 </div>

 <div class="buildings">
 <h2>Construire</h2>
 <button onclick="queueBuilding('mine')">Ajouter une Mine à la file (Gratuit)</button>
 <button onclick="queueBuilding('field')">Ajouter un Champ à la file (Gratuit)</button>
 <button onclick="queueBuilding('industry')">Ajouter une Industrie Légère à la file (Coût: 5 minerais)</button>
 </div>
 </div>
 <script>
 let minerals = 150; // 150 minerais initialement
 let food = 100; // 100 ressources alimentaires initiales
 let luxury = 80; // 80 ressources luxueuses initiales
 let mines = 15; // 15 mines
 let fields = 10; // 10 champs
 let industries = 8; // 8 industries légères
 let infrastructures = 0;
 let constructionQueue = [];

 function updateResources() {
 document.getElementById('minerals').textContent = minerals;
 document.getElementById('food').textContent = food;
 document.getElementById('luxury').textContent = luxury;
 document.getElementById('mines').textContent = mines;
 document.getElementById('fields').textContent = fields;
 document.getElementById('industries').textContent = industries;
 document.getElementById('infrastructures').textContent = infrastructures;
 }
 function queueBuilding(type) {
 constructionQueue.push(type);
 updateQueueDisplay();
 }
 function updateQueueDisplay() {
 let queueElement = document.getElementById('constructionQueue');
 queueElement.innerHTML = "";
 constructionQueue.forEach((building, index) => {
 let li = document.createElement('li');
 li.textContent = building;
 queueElement.appendChild(li);
 });
 }
 function validateConstruction() {
 if (constructionQueue.length > 0) {
 let building = constructionQueue.shift();
 if (building === 'mine') {
 minerals += 150; // Chaque mine produit 150 minerais
 mines += 1;
 } else if (building === 'field') {
 food += 100; // Chaque champ produit 100 ressources alimentaires
 fields += 1;
 } else if (building === 'industry') {
 if (minerals >= 5) {
 minerals -= 5;
 luxury += 10;
 industries += 1;
 } else {
 alert("Pas assez de ressources pour construire une Industrie Légère !");
 constructionQueue.unshift(building);
 return;
 }
 }
 updateResources();
 updateQueueDisplay();
 }
 }
 function increaseInfrastructure() {
 infrastructures += 1;
 updateResources();
 }
 </script>
</body>
</html>
