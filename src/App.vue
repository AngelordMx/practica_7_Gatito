<script setup>
import 'bootstrap/dist/css/bootstrap.css';
import { ref } from 'vue';
import Nombres from './components/Nombres.vue'
// Importa las dependencias necesarias

const contx = ref(0);
const conto = ref(0);

const jugadorActual = ref("X");
const tablero = ref(["", "", "", "", "", "", "", "", ""]);
const ManerasGanar = [
  [0, 1, 2],
  [3, 4, 5],
  [6, 7, 8],
  [0, 3, 6],
  [1, 4, 7],
  [2, 5, 8],
  [0, 4, 8],
  [2, 4, 6],
];
const juegoIniciado = ref(false);
const ganador = ref("");

function ResetearContadores() {
  contx.value = 0;
  conto.value = 0;
}

function Ganador() {
  for (let i = 0; i < ManerasGanar.length; i++) {
    const [a, b, c] = ManerasGanar[i];
    if (tablero.value[a] === "") {
      continue;
    }
    if (tablero.value[a] === tablero.value[b] && tablero.value[a] === tablero.value[c]) {
      ganador.value = tablero.value[a];
      return tablero.value[a];
    }
  }
  return "";
}

function Contadores() {
  if (Ganador() === "X") {
    contx.value++;
  }
  if (Ganador() === "O") {
    conto.value++;
  }
}

function Tirar(celda) {
  if (Ganador() !== "") {
    return;
  }
  if (tablero.value[celda] !== "") {
    return;
  }
  tablero.value[celda] = jugadorActual.value;
  if (jugadorActual.value === "X") {
    jugadorActual.value = "O";
  } else {
    jugadorActual.value = "X";
  }
  Contadores();
}

function Reiniciar() {
  tablero.value = ["", "", "", "", "", "", "", "", ""];
  jugadorActual.value = "X";
  ganador.value = "";
  juegoIniciado.value = false;
}




</script>

<template>
  <div class="card w-96 bg-base-300 shadow-xl">
    <div class="card-body items-center">
      <h2 id="Titulo">Gatito</h2>

      <!-- Componente para ingresar los nombres de los jugadores -->
      <div>
		<Nombres/>
      </div>

      <!-- Celdas del juego -->
      <table class="table-auto text-5xl">
        <tbody>
          <!-- Primer renglon -->
          <tr>
            <!-- Primera celda -->
            <td>
              <div @click="Tirar(0)" class="boton"> {{ tablero[0] }}</div>
            </td>
            <td>
              <div @click="Tirar(1)" class="boton"> {{ tablero[1] }}</div>
            </td>
            <td>
              <div @click="Tirar(2)" class="boton"> {{ tablero[2] }}</div>
            </td>
          </tr>
          <!-- Segundo Renglon -->
          <tr>
            <td>
              <div @click="Tirar(3)" class="boton"> {{ tablero[3] }}</div>
            </td>
            <td>
              <div @click="Tirar(4)" class="boton">{{ tablero[4] }} </div>
            </td>
            <td>
              <div @click="Tirar(5)" class="boton">{{ tablero[5] }} </div>
            </td>
          </tr>
          <!-- Tercer renglon -->
          <tr>
            <!-- Primera celda -->
            <td>
              <div @click="Tirar(6)" class="boton"> {{ tablero[6] }}</div>
            </td>
            <td>
              <div @click="Tirar(7)" class="boton">{{ tablero[7] }} </div>
            </td>
            <td>
              <div @click="Tirar(8)" class="boton">{{ tablero[8] }} </div>
            </td>
          </tr>
        </tbody>
      </table>
      <button @click="Reiniciar" id="botonReinicio" class="border-4 border-black rounded-xl px-2">Empezar de nuevo!</button>

      <div class="flex flex-col">
        <h2 v-if="!Ganador() && !juegoIniciado" id="turnoJugador" class="card-title">Turno de {{ jugadorActual }}!</h2>

        <div v-if="Ganador()">
          <span>Ganador: {{ ganador }}</span>
        </div>

        <div>Rondas ganadas de {{ jugador1 }}: {{ contx }}</div>
        <div>Rondas ganadas de {{ jugador2 }}: {{ conto }}</div>
      </div>

      <button @click="ResetearContadores" id="botonReset" class="border-4 border-black rounded-xl px-2">Resetear Contadores</button>

    </div>
  </div>

</template>
