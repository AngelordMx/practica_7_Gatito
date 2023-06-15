<script>
import { ref } from 'vue';

const jugadorActual = ref("X");
const tablero = ref(["", "", "", "", "", "", "", "", ""])
const ManerasGanar = [
	[0, 1, 2],
	[3, 4, 5],
	[6, 7, 8],
	[0, 3, 6],
	[1, 4, 7],
	[2, 5, 8],
	[0, 4, 8],
	[2, 4, 6],
]

function Ganador() {
	for (let i = 0; i < ManerasGanar.length; i++) {
		const [a, b, c] = ManerasGanar[i]
		if (tablero.value[a] == "") {
			continue;
		}
		if (tablero.value[a] == tablero.value[b] && tablero.value[a] == tablero.value[c]) {
			return tablero.value[a]
		}
	}
	return "";
}

function Tirar(celda) {
	if (Ganador() != "") {
		return;
	}
	if (tablero.value[celda] != "") {
		return ;
	}
	tablero.value[celda] = jugadorActual.value;
	if (jugadorActual.value=="X")
	{
		jugadorActual.value="O"
	}
	else
	{
		jugadorActual.value="X"
	}
}
</script>

<template>
	<div class="card w-96 bg-base-300 shadow-xl">
		<div class="card-body items-center">
			<h2 id="Titulo">Gatito</h2>

			<!--Celdas del juego -->
			<table class="table-auto text-5xl ">
				<tbody>
					<!-- Primer renglon-->
					<tr>
						<!-- Primera celda -->
						<td>
							<div @click="Tirar(0)" class="boton"> </div>
						</td>
						<td>
							<div @click="Tirar(1)" class="boton"> </div>
						</td>
						<td>
							<div @click="Tirar(2)"  class="boton"> </div>
						</td>
					</tr>
					<!-- Segundo Renglon-->
					<tr>
						<td>
							<div @click="Tirar(3)"  class="boton"> </div>
						</td>
						<td>
							<div @click="Tirar(4)" class="boton"> </div>
						</td>
						<td>
							<div @click="Tirar(5)" class="boton"> </div>
						</td>

					</tr>
					<!-- Tercer renglon-->
					<tr>
						<!-- Primera celda -->
						<td>
							<div @click="Tirar(6)" class="boton"> </div>
						</td>
						<td>
							<div @click="Tirar(7)" class="boton"> </div>
						</td>
						<td>
							<div @click="Tirar(8)" class="boton"> </div>
						</td>
					</tr>
				</tbody>
			</table>
			<h2 id="turnoJugador" class="card-title">Turno de X !</h2>
			<div class="alert flex justify-center">
				<span>{{ "Equipo " }}</span>
			</div>
			<button id="botonReinicio" class="btn join-item w-18">Empezar de nuevo!</button>
		</div>
	</div>
</template>

<style>
.cell {
	width: 75px;
	height: 75px;
	box-shadow: 0 0 0 2px;
	line-height: 75px;
	font-size: 50px;
	cursor: grab;
}

#Titulo {
	font-family: "Permanent Marker", cursive;
	font-size: xx-large;
}

#Contenedordeljuego {
	font-family: "Permanent Marker", cursive;
}</style>