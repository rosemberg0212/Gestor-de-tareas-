<template>
	<div>
		<h1 class="text-center">Iniciar Sesion</h1>
		<hr>
		<div 
			class="alert alert-danger" 
			role="alert"
			v-if="errores"
			>
 			<h5>Email o password Invalidos</h5>
		</div>
		<form @submit.prevent="validarUser">
		  <div class="mb-3">
		    <label for="exampleInputEmail1" class="form-label">Email</label>
		    <input 
		    	type="email" 
		    	class="form-control" 
		    	id="exampleInputEmail1" 
		    	aria-describedby="emailHelp"
		    	v-model="email">
		  </div>

		  <div class="mb-3">
		    <label for="exampleInputPassword1" class="form-label">Password</label>
		    <input 
		    	type="password" 
		    	class="form-control" 
		    	id="exampleInputPassword1"
		    	v-model="password"
		    	>
		  </div>
		  
		  <button type="submit" class="btn btn-primary">Iniciar</button>
		</form>
	</div>
</template>

<script>
	import router from '../router/index.js'
export default {
	data: ()=>({
		email:'',
		password: '',
		errores: false
	}),
	methods:{
		async validarUser(){
			if(this.password.length >= 6 && this.email != "")
			{
				const API_KEY = "AIzaSyCqzToNa2r6OQcaql9koxhwzzeTVk6V0h0"

				try{
					const res = await fetch(`https://identitytoolkit.googleapis.com/v1/accounts:signInWithPassword?key=${API_KEY}`,{
					method: 'POST',
					body: JSON.stringify({
							email: this.email,
							password: this.password,
							returnSecureToken: true
						})
					})
					const data = await res.json()
					if(data.error){
						this.errores = true
					}else
					{
						this.errores = false
						console.log(data)
						localStorage.setItem("user", JSON.stringify(data))
						router.push("/proyectos")
					}
				}catch(error){}
				
				}else{
				return;
			}
		}
	}
}
</script>