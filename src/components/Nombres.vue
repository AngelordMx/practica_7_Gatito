<template>
	<div>
	  <input class="form-control" placeholder="Nombre del Jugador 1" v-model="jugador1" :disabled="nombresBloqueados">
	  <input class="form-control" placeholder="Nombre del Jugador 2" v-model="jugador2" :disabled="nombresBloqueados">
  
	  <button @click="bloquearNombres" id="botonAceptar" class="border-4 border-black rounded-xl px-2">Aceptar</button>
	  <button @click="cambiarNombres" id="botonCambiar" class="border-4 border-black rounded-xl px-2" :disabled="juegoIniciado">Cambiar Nombres</button>
	</div>
  </template>
  
  <script setup>
  import { ref } from 'vue';
  
  const jugador1 = ref('');
  const jugador2 = ref('');
  
  const nombresBloqueados = ref(false);
  const juegoIniciado = ref(false);
  
  function bloquearNombres() {
	nombresBloqueados.value = true;
	juegoIniciado.value = true;
  }
  
  function cambiarNombres() {
	if (juegoIniciado.value) {
	  return;
	}
	nombresBloqueados.value = false;
  }
  </script>
  