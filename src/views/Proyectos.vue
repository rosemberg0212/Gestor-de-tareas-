<template>
	<div class="container">
		<h1 class="text-center">Proyectos</h1>
		<hr>
		<router-link to="/create" class="btn btn-warning mb-2">Nuevo</router-link>
		<ContenedorProyec/>
	</div>
	
</template>

<script>
	import ContenedorProyec from '../components/ContenedorProyec'
export default {
	components:{
		ContenedorProyec,
	}
}
</script>

