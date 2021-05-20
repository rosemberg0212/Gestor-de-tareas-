<template>
  <div class="container">
  	<Register/>
  </div>
  
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'
import Register from '../components/Register'
export default {
  name: 'Home',
  components: {
    HelloWorld,
    Register,
  }
}
</script>
