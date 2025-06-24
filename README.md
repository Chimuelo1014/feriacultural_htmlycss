// Estado global del juego
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
