<!DOCTYPE html>
<html lang="pt-br">
<head>
  <meta charset="UTF-8" />
  <title>Semeadores de Cristo</title>

  <!-- Firebase -->
  <script src="https://www.gstatic.com/firebasejs/9.6.1/firebase-app-compat.js"></script>
  <script src="https://www.gstatic.com/firebasejs/9.6.1/firebase-firestore-compat.js"></script>

  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f2f2f2;
      color: #333;
      margin: 0;
      padding: 0;
    }
    header {
      background-color: #5c9ead;
      color: white;
      padding: 20px;
      text-align: center;
    }
    main {
      max-width: 800px;
      margin: 20px auto;
      padding: 20px;
      background: white;
      border-radius: 10px;
      box-shadow: 0 0 10px #ccc;
    }
    h2 {
      color: #5c9ead;
    }
    .box {
      margin-bottom: 20px;
    }
    textarea {
      width: 100%;
      height: 100px;
      padding: 10px;
      border-radius: 5px;
      border: 1px solid #ccc;
      resize: none;
      font-size: 14px;
    }
    button {
      padding: 10px 20px;
      background: #5c9ead;
      color: white;
      border: none;
      border-radius: 5px;
      margin-top: 10px;
      cursor: pointer;
    }
    button:hover {
      background: #478ca2;
    }
    footer {
      text-align: center;
      padding: 10px;
      color: #777;
    }
  </style>
</head>

<body>
  <header>
    <h1>Semeadores de Cristo</h1>
    <p>Versículo • Reflexão • Ação • Anotações</p>
  </header>

  <main>
    <div class="box">
      <h2>📖 Versículo do Dia</h2>
      <p id="versiculo">Carregando versículo...</p>
    </div>

    <div class="box">
      <h2>🧠 Reflexão</h2>
      <p>Jesus nos ensina que promover a paz não é apenas evitar conflitos, mas agir ativamente na reconciliação. Você tem sido um instrumento de paz onde vive?</p>
    </div>

    <div class="box">
      <h2>🤝 Ação Sugerida</h2>
      <p>Hoje, tente resolver um desentendimento ou envie uma mensagem a alguém com quem não fala há muito tempo.</p>
    </div>

    <div class="box">
      <h2>✍️ Suas Anotações</h2>
      <textarea id="comentario" placeholder="Escreva aqui sua oração, sentimentos ou algo que viveu hoje..."></textarea>
      <button onclick="enviarComentario()">Enviar</button>
      <p id="mensagem-status"></p>
    </div>
  </main>

  <footer>
    <p>Projeto de Extensão • Engenharia de Software • 2025</p>
  </footer>

  <!-- SCRIPT DEPOIS DO BODY -->
  <script>
    // Firebase config
    const firebaseConfig = {
      apiKey: "AIzaSyDt0Dny4pOwJiTxKVyg5jBiOf-e1i4H-lE",
      authDomain: "semeadoresdecristo-94e33.firebaseapp.com",
      projectId: "semeadoresdecristo-94e33",
      storageBucket: "semeadoresdecristo-94e33.appspot.com",
      messagingSenderId: "620648905465",
      appId: "1:620648905465:web:c72b377ea637277ba58028"
    };

    // Inicializar Firebase
    firebase.initializeApp(firebaseConfig);
    const db = firebase.firestore();

    // Versículos
    const versiculos = [
      "Mateus 5:9 - Bem-aventurados os pacificadores...",
      "Romanos 12:18 - Se possível, tenha paz com todos.",
      "Salmo 34:14 - Afaste-se do mal e pratique o bem; busque a paz e siga-a.",
      "Provérbios 15:1 - A resposta branda desvia o furor.",
      "Tiago 3:18 - O fruto da justiça semeia-se em paz."
    ];

    // Mostrar versículo do dia
    const diaDoAno = Math.floor((new Date() - new Date(new Date().getFullYear(), 0, 0)) / 86400000);
    const versiculo = versiculos[diaDoAno % versiculos.length];
    document.getElementById("versiculo").innerText = versiculo;

    // Enviar comentário
    function enviarComentario() {
      const texto = document.getElementById("comentario").value;
      const status = document.getElementById("mensagem-status");

      if (!texto.trim()) {
        status.innerText = "Escreva algo antes de enviar.";
        return;
      }

      db.collection("comentarios").add({
        comentario: texto,
        data: new Date(),
        versiculo: versiculo
      }).then(() => {
        status.innerText = "Comentário enviado com sucesso!";
        document.getElementById("comentario").value = "";
      }).catch(error => {
        status.innerText = "Erro ao enviar: " + error;
      });
    }
  </script>
</body>
</html>
