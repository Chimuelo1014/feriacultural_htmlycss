<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>CRUDY - Juego Lógico</title>
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bulma@1.0.4/css/bulma.min.css">
  <style>
    body {
      background-color: #121212;
      color: white;
      font-family: 'Courier New', Courier, monospace;
    }
    html {
      scroll-behavior: smooth;
    }
    .hero.is-fullheight {
      background-image: url("https://media.istockphoto.com/id/1732963074/es/foto/cielo-nocturno-estrellado-en-el-espacio.jpg");
      background-size: cover;
      background-position: center;
      color: white;
    }
    .hero .title, .hero .subtitle {
      text-shadow: 1px 1px 4px rgba(0,0,0,0.6);
      margin: auto;
    }
    .hero .subtitle {
      margin-top: 50px;
    }
    .hero .button {
      margin-top: 50px;
      background-color: #00f7ff;
      color: black;
      padding: 10px 20px;
      font-size: 16px;
    }
    .card {
      display: flex;
      flex-direction: column;
      height: 100%;
    }
    .card-content {
      flex-grow: 1;
      display: flex;
      flex-direction: column;
      justify-content: space-between;
    }
    .nivel {
      background-size: cover;
      background-position: center;
      min-height: 100vh;
      display: flex;
      justify-content: center;
      align-items: center;
      flex-direction: column;
      text-align: center;
      padding: 2rem;
    }
    .contenido-nivel {
      opacity: 0;
      transition: opacity 1s ease;
    }
    .contenido-nivel.visible {
      opacity: 1;
    }
  </style>
</head>
<body>
  <section class="hero is-fullheight">
    <div class="hero-body">
      <div class="container has-text-centered">
        <h1 class="title is-1">Crudy</h1>
        <h2 class="subtitle is-3">Bienvenido a nuestro juego de <strong>supervivencia</strong> donde explorarás diferentes <strong>aventuras</strong></h2>
        <a href="#cartas" class="button is-primary is-medium">Ver Secciones</a>
      </div>
    </div>
  </section>

  <section class="section" id="cartas">
    <div class="container has-text-centered">
      <h2 class="title is-2">Sección de Opciones</h2>
      <p class="subtitle is-5">Selecciona una de las siguientes funcionalidades</p>
      <div class="columns is-multiline is-centered mt-5">

        <div class="column is-4">
          <div class="card">
            <div class="card-image">
              <figure class="image is-4by3">
                <img src="https://picsum.photos/id/1011/600/400" alt="Carta 1">
              </figure>
            </div>
            <div class="card-content">
              <p class="title is-5">Núcleo Lógico</p>
              <p class="content">Accede al sistema central para decisiones importantes.</p>
            </div>
            <footer class="card-footer">
              <a href="#" class="card-footer-item button is-info is-light" onclick="iniciarJuego('logico')">Opción 1</a>
            </footer>
          </div>
        </div>

        <div class="column is-4">
          <div class="card">
            <div class="card-image">
              <figure class="image is-4by3">
                <img src="https://picsum.photos/id/1012/600/400" alt="Carta 2">
              </figure>
            </div>
            <div class="card-content">
              <p class="title is-5">Entorno Simulado</p>
              <p class="content">Explora una simulación de entrenamiento avanzada.</p>
            </div>
            <footer class="card-footer">
              <a href="#" class="card-footer-item button is-info is-light" onclick="iniciarJuego('simulado')">Opción 2</a>
            </footer>
          </div>
        </div>

        <div class="column is-4">
          <div class="card">
            <div class="card-image">
              <figure class="image is-4by3">
                <img src="https://picsum.photos/id/1013/600/400" alt="Carta 3">
              </figure>
            </div>
            <div class="card-content">
              <p class="title is-5">Trampa Activada</p>
              <p class="content">La ruta peligrosa puede llevar a fallos del sistema.</p>
            </div>
            <footer class="card-footer">
              <a href="#" class="card-footer-item button is-danger is-light" onclick="iniciarJuego('trampa')">Opción 3</a>
            </footer>
          </div>
        </div>

      </div>
    </div>
  </section>

  <div id="juego"></div>

  <script>
    let estado = {
      nivel: 1,
      decisiones: [],
      puntaje: 0
    };

    function iniciarJuego(opcionInicial) {
      estado.nivel = 1;
      estado.decisiones = [opcionInicial];
      mostrarNivel2();
    }

    function mostrarNivel2() {
      const ruta = estado.decisiones[0];
      const mensaje = ruta === 'logico' ? 'Módulo de decisiones activado.' :
                      ruta === 'simulado' ? 'Entorno simulado iniciado.' :
                      'Has caído en una trampa. Precaución.';

      document.getElementById('juego').innerHTML = `
        <section class="nivel" style="background-image: url('https://picsum.photos/id/1020/1200/800');">
          <div class="contenido-nivel visible">
            <h2 class="title is-2">Nivel 2: Laberinto de Decisión</h2>
            <p class="subtitle is-5">${mensaje}</p>
            <div class="buttons is-centered">
              <button class="button is-link" onclick="guardarYMostrar(3, 'puerta-condicional')">Puerta Condicional</button>
              <button class="button is-link" onclick="guardarYMostrar(3, 'acceso-directo')">Acceso Directo</button>
              <button class="button is-link" onclick="guardarYMostrar(3, 'puerta-codigo')">Puerta de Código</button>
            </div>
          </div>
        </section>
      `;
    }

    function guardarYMostrar(siguienteNivel, decision) {
      estado.nivel = siguienteNivel;
      estado.decisiones.push(decision);
      if (siguienteNivel === 3) mostrarNivel3();
      if (siguienteNivel === 4) mostrarNivel4();
      if (siguienteNivel === 5) mostrarNivel5();
    }

    function mostrarNivel3() {
      const patron = ['🟩', '🟦', '🟥'];
      document.getElementById('juego').innerHTML = `
        <section class="nivel">
          <div class="contenido-nivel" id="contenido-nivel">
            <h2 class="title is-2">Nivel 3: Desafío de Reconstrucción</h2>
            <div id="patron" style="font-size: 3rem;"></div>
            <div id="respuestas" style="margin-top: 2rem; display: none;">
              <button class="button" onclick="verificarRespuesta('🟥')">🟥</button>
              <button class="button" onclick="verificarRespuesta('🟩')">🟩</button>
              <button class="button" onclick="verificarRespuesta('🟦')">🟦</button>
            </div>
          </div>
        </section>
      `;
      const div = document.getElementById("patron");
      let i = 0;
      const mostrar = setInterval(() => {
        div.textContent = patron[i];
        i++;
        if (i >= patron.length) {
          clearInterval(mostrar);
          div.textContent = "";
          document.getElementById("respuestas").style.display = "block";
        }
      }, 1000);
      setTimeout(() => document.getElementById("contenido-nivel").classList.add("visible"), 3000);
    }

    function verificarRespuesta(resp) {
      if (resp === '🟥') estado.puntaje++;
      guardarYMostrar(4, resp);
    }

    function mostrarNivel4() {
      document.getElementById('juego').innerHTML = `
        <section class="nivel">
          <div class="contenido-nivel visible">
            <h2 class="title is-2">Nivel 4: Lógica Fractal</h2>
            <p>Si A entonces B. Si B entonces C. ¿Qué ocurre si A?</p>
            <div class="buttons is-centered">
              <button class="button" onclick="guardarYMostrar(5, 'C')">C</button>
              <button class="button" onclick="guardarYMostrar(5, 'A')">A</button>
              <button class="button" onclick="guardarYMostrar(5, 'ninguna')">Ninguna</button>
            </div>
          </div>
        </section>
      `;
    }

    function mostrarNivel5() {
      document.getElementById('juego').innerHTML = `
        <section class="nivel">
          <div class="contenido-nivel visible">
            <h2 class="title is-2">Nivel 5: Juicio del Núcleo</h2>
            <p>¿Cuál es el resultado de typeof null en JavaScript?</p>
            <div class="buttons is-centered">
              <button class="button" onclick="finalizar('object')">object</button>
              <button class="button" onclick="finalizar('null')">null</button>
              <button class="button" onclick="finalizar('undefined')">undefined</button>
            </div>
          </div>
        </section>
      `;
    }

    function finalizar(resp) {
      if (resp === 'object') estado.puntaje++;
      const finalText = estado.puntaje >= 2 ? '¡Has liberado a CRUDY!' : 'CRUDY te ha rechazado. Reinicia.';
      document.getElementById('juego').innerHTML = `
        <section class="nivel">
          <div class="contenido-nivel visible">
            <h2 class="title is-1">Resultado</h2>
            <p class="subtitle is-4">${finalText}</p>
            <p>Decisiones tomadas: ${estado.decisiones.join(', ')}</p>
            <p>Puntaje: ${estado.puntaje}</p>
            <button class="button mt-5" onclick="location.reload()">Reiniciar</button>
          </div>
        </section>
      `;
    }
  </script>
</body>
</html>
