<template>
	<div>
		<nav class="navbar navbar-expand-lg navbar-dark" style="background-color: #E5097F">
		  <div class="container-fluid">
		    <!--<a class="navbar-brand" href="#">Navbar</a>-->
		    <router-link to="/" class="navbar-brand">Gestor de proyectos</router-link>
		    <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
		      <span class="navbar-toggler-icon"></span>
		    </button>
		    <div class="collapse navbar-collapse" id="navbarSupportedContent">
		      <ul class="navbar-nav me-auto mb-2 mb-lg-0 my-md-0">
		        <li class="nav-item">
		        	<router-link v-if="!sesion" to="/" class="nav-link active">Registro</router-link>
		        </li>
		        <li class="nav-item">
		        	<router-link v-if="!sesion" to="/login" class="nav-link">Login</router-link>
		        </li>
		        <li>
		        	<router-link v-if="sesion" to="/proyectos" class="btn btn-success">
		        		Proyectos
		        	</router-link>
		        </li>
		        <li>
		        	<router-link 
		        		v-if="sesion" 
		        		to="/login" 
		        		class="btn btn-danger" 
		        		style="background-color: #8b0000"
		        		@click="cerrarSesion">
		        		Cerrar Sesion
		        	</router-link>
		        </li>
		      </ul>
		    </div>
		  </div>
		</nav>
	</div>
</template>

<script>
export default {
	methods:{
		cerrarSesion(){
			localStorage.removeItem("user")
		}
	},
	computed:{
		sesion(){
			const user = localStorage.getItem("user")
			if(user)
			{
				return true
			}
			return false
		}
	}
}
</script>

