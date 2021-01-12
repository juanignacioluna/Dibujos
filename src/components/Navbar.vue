<template>

  <div id="navbar">

	<div class="flex demo">
	  <div>

		<div style="overflow: hidden;height: 250px;">

		<nav class="demo">

			<router-link to="/">
				  <a class="brand">
				    <img class="logo" src="@/assets/paint01.png" />
				    <span>Dibujos con formas</span>
				  </a>
			</router-link>


			  <!-- responsive-->
			  <input id="bmenub" type="checkbox" class="show">
			  <label for="bmenub" class="burger pseudo button"><i class="fas fa-bars"></i></label>

			  <div class="menu">
			    <router-link to="/dibujar"><button class='warning'>Dibujar :)</button></router-link>
			  </div>
		</nav>

		</div>


	  </div>
	</div>

    
  </div>

</template>

<script>
  
export default {
  name: 'Navbar',
  data(){
    return{

    }
  },
	methods: {

	},


}
</script>


<style scoped>

	#navbar{
		max-height: 50px;
	}

	.brand{
		color: black;
	}

</style>
