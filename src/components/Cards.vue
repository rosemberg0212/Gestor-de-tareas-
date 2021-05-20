<template>
	<div class="card mb-3" style="width: 100%;" v-if="data.data.status">
		 	<div class="card-body">
			    <h5 class="card-title">{{data.data.title}}</h5>
			    <p class="card-text">{{data.data.description}}</p>
			    <p>Tecnologia:{{data.data.langs}}</p>
			    <router-link :to="`/edit/${data.id}`" class="btn btn-primary mx-2">
			    	Editar
			    </router-link>
			    <!--<button type="button" class="btn btn-primary mx-2">Editar</button>-->
			    <button 
			    	type="button" 
			    	class="btn btn-danger"
			    	@click="deleteProjec"
			    	>
			    	Eliminar
			    </button>
  			</div>
		</div>
</template>

<script>
export default {
	props:{
		data: Object,
	},
	methods:{
		async deleteProjec(){
			const user = JSON.parse(localStorage.getItem("user"))

			const id = this.data.id;

			const res = await fetch(`https://crud-vue-e5629-default-rtdb.firebaseio.com/projects/${user.localId}/${id}.json?auth=${user.idToken}`,{
				method: "PATCH",
				body: JSON.stringify({status: false})
			});
			console.log(id)

			const data = await res.json()

			this.data.data.status = data['status']
		}
	}
}
</script>

