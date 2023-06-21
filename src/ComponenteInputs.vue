<template>
	<div>
	  <input class="form-control" placeholder="Nombre del Jugador 1" :disabled="nombresBloqueados">
	  <input class="form-control" placeholder="Nombre del Jugador 2" :disabled="nombresBloqueados">
	</div>
  </template>
  
  <script>
  export default {
	props: {
	  nombresBloqueados: Boolean
	}
  }
  </script>
  
  <style>
  /* Estilos opcionales para los inputs */
  </style>
  