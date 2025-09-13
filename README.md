#<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>📃 Mon Mini Logiciel</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 20px;
      background: #f7f7f7;
    }
    h1 {
      text-align: center;
    }
    .container {
      max-width: 500px;
      margin: auto;
      padding: 20px;
      background: white;
      border-radius: 10px;
      box-shadow: 0 4px 6px rgba(0,0,0,0.1);
    }
    input, select, button {
      padding: 10px;
      margin: 5px 0;
      width: 100%;
      border: 1px solid #ddd;
      border-radius: 5px;
    }
    button {
      background: #4CAF50;
      color: white;
      cursor: pointer;
    }
    button:hover {
      background: #45a049;
    }
    #reponse {
      margin-top: 20px;
      padding: 10px;
      background: #f0f0f0;
      border-radius: 5px;
      min-height: 50px;
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>📃 Gestion de Phrases</h1>

    <select id="selectionnez">
      <option value="ajouter">Ajouter</option>
      <option value="recherche">Rechercher</option>
      <option value="retirer">Retirer</option>
    </select>

    <input type="text" id="input1" placeholder="ID (clé)">
    <input type="text" id="input2" placeholder="Phrase (valeur)">
    <button onclick="execution()">Exécuter</button>
    <button onclick="affiche()">Afficher toute la liste</button>

    <div id="reponse"></div>
  </div>

  <script>
    function execution() {
      let selection = document.getElementById('selectionnez').value;
      let id = document.getElementById('input1').value.trim();
      let phrase = document.getElementById('input2').value.trim();
      let reponses = document.getElementById('reponse');

      // Charger l'objet stocké ou créer un vide
      let list = JSON.parse(localStorage.getItem('ma_liste3')) || {};

      if (selection === "ajouter") {
        if (!id || !phrase) {
          reponses.innerHTML = "❌ Veuillez remplir ID et Phrase.";
          return;
        }
        list[id] = phrase;
        localStorage.setItem('ma_liste3', JSON.stringify(list));
        reponses.innerHTML = "✅ Phrase enregistrée avec l'id: <b>" + id + "</b>";
      }

      else if (selection === "recherche") {
        if (list[id]) {
          reponses.innerHTML = "🔎 Résultat pour <b>" + id + "</b> : " + list[id];
        } else {
          reponses.innerHTML = "❌ Aucun résultat trouvé pour l'id: " + id;
        }
      }

      else if (selection === "retirer") {
        if (list[id]) {
          delete list[id];
          localStorage.setItem('ma_liste3', JSON.stringify(list));
          reponses.innerHTML = "🗑️ Phrase supprimée pour l'id: " + id;
        } else {
          reponses.innerHTML = "❌ Impossible de supprimer, l'id n'existe pas.";
        }
      }
    }

    function affiche() {
      let reponses = document.getElementById('reponse');
      let list = JSON.parse(localStorage.getItem('ma_liste3')) || {};

      if (Object.keys(list).length === 0) {
        reponses.innerHTML = "📭 La liste est vide.";
        return;
      }

      let affichage = "<h3>📃 Liste complète :</h3>";
      for (let id in list) {
        affichage += "<p><b>" + id + "</b> ➝ " + list[id] + "</p>";
      }

      reponses.innerHTML = affichage;
    }
  </script>
</body>
</html>
