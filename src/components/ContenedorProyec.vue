<template>
	<div class="row">
		<div class="col">
			<Cards 
			v-for="(project, i) in projects" 
			:key="i"
			:data="project"
			/>
		</div>
	</div>

</template>

<script>
	import Cards from '../components/Cards'
export default {
	data:()=>({
		projects: [],
	}),
	components:{
		Cards,
	},
	mounted(){
		this.getProjects()
	},
	methods:{
		async getProjects(){
			const user = JSON.parse(localStorage.getItem("user"))

			console.log(user)
			const res = await fetch(`https://crud-vue-e5629-default-rtdb.firebaseio.com/projects/${user.localId}.json?auth=${user.idToken}`);

			const data = await res.json();
			for(let i in data)
			{
				this.projects.push({
					id: i,
					data: data[i]
				})
			}

			//console.log(data)
		}
	}
}
</script>

