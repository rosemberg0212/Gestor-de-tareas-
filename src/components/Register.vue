<template>
	<div>
		<h1 class="text-center">Crea tu Cuenta</h1>
		<hr>
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
		  
		  <div class="mb-3">
		    <label for="password2" class="form-label">Confirm Password</label>
		    <input 
		    	type="password" 
		    	class="form-control" 
		    	id="password2"
		    	v-model="password2"
		    	>
		  </div>
		  <button type="submit" class="btn btn-primary">Registro</button>
		</form>
	</div>
</template>

<script>
	import router from '../router/index.js'
export default {
	data: ()=>({
		email:'',
		password: '',
		password2: ''
	}),
	methods:{
		async validarUser(){
			if(this.password === this.password2 && this.password.length >= 6 && this.email != "")
			{
				const API_KEY = "AIzaSyCqzToNa2r6OQcaql9koxhwzzeTVk6V0h0"
				const res = await fetch(`https://identitytoolkit.googleapis.com/v1/accounts:signUp?key=${API_KEY}`,{
					method: 'POST',
					body: JSON.stringify({
						email: this.email,
						password: this.password,
						returnSecureToken: true
					})
				})

				const data = await res.json()
				localStorage.setItem("user", JSON.stringify(data));
				router.push("/proyectos")
			}else{
				return;
			}
		}
	}
}
</script>

