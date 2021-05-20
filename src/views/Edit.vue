<template>
	<div class="container border mt-3">
		<h2 class="text-center">Editar Proyecto</h2>
		<hr>
		<router-link to="/proyectos" 
			class="btn btn-success mb-2"
			style="width: 100%"
			>
		    Regresar a Proyectos
		</router-link>
		<hr>
		<form @submit.prevent = "UpdateProjects">
		  <div class="mb-3">
		    <label for="nombreProject" class="form-label">Nombre del Proyecto</label>
		    <input 
		    	type="text" 
		    	class="form-control" 
		    	id="nombreProject" 
		    	aria-describedby="emailHelp" 
		    	placeholder="ingrese nombre del preyecto"
		    	v-model="project.title"
		    	>
		  </div>

		  <div class="mb-3">
		    <label for="descriptionProject" class="form-label">Descripción</label>
		    <input
		     	type="text" 
		     	class="form-control" 
		     	id="descriptionProject" 
		     	placeholder="ingrese descripcion"
		     	v-model="project.description"
		     	>
		  </div>

		   <div class="mb-3 form-check">
			    <input 
			    	type="checkbox" 
			    	class="form-check-input" 
			    	id="exampleCheck1"
			    	v-model="project.langs"
			    	value="html" 
			    	>
			    <label class="form-check-label" for="exampleCheck1">HTML</label>
 			</div>

 			<div class="mb-3 form-check">
			    <input 
			    	type="checkbox" 
			    	class="form-check-input" 
			    	id="exampleCheck1"
			    	v-model="project.langs"
			    	value="css"
			    	>
			    <label class="form-check-label" for="exampleCheck1">CSS</label>
 			 </div>

 			 <div class="mb-3 form-check">
			    <input 
			    	type="checkbox" 
			    	class="form-check-input" 
			    	id="exampleCheck1"
			    	v-model="project.langs"
			    	value="JavaScript"
			    	>
			    <label class="form-check-label" for="exampleCheck1">JavaScript</label>
 			 </div>

 			 <div class="mb-3 form-check">
			    <input 
			    	type="checkbox" 
			    	class="form-check-input" 
			    	id="exampleCheck1"
			    	v-model="project.langs"
			    	value="Vue"
			    	>
			    <label class="form-check-label" for="exampleCheck1">Vue</label>
 			 </div>

		  <button type="submit" class="btn btn-primary mb-2">Guardar</button>
		</form>
	</div>
	
</template>

<script>
	import router from '../router/index.js'
export default {
	data:()=>({
		project:{},
		id: Object
	}),
	mounted()
	{
		this.getProject();
	},
	methods:{
		async getProject(){
			const user = JSON.parse(localStorage.getItem("user"))
			
			const para = this.$route.params.id;

			this.id = para

			const res = await fetch(`https://crud-vue-e5629-default-rtdb.firebaseio.com/projects/${user.localId}/${this.id}.json?auth=${user.idToken}`)
			const data = await res.json();

			this.project = data;
			//console.log(data)

		},
		async UpdateProjects(){
			const user = JSON.parse(localStorage.getItem("user"))

			await fetch(`https://crud-vue-e5629-default-rtdb.firebaseio.com/projects/${user.localId}/${this.id}.json?auth=${user.idToken}`,{
				method: "PATCH",
				body: JSON.stringify(this.project),
			});
			router.push("/proyectos")
		}
	}
}
</script>