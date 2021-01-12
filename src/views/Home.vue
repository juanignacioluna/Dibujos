<template>
  <div class="home">


    <Navbar />

    <div class="flex six demo center">
      <div class="two-third welcome">


        <h1>Dibujos con formas :)</h1>


        <h3 class="typed"></h3>





      </div>
    </div>


  </div>
</template>

<style>
  
  .welcome{
    background: #858585;
    color: white;
    margin-top: 30px;
    border: 2px solid #363636;
    border-radius: 10px;
  }

</style>

<script>

import Typed from 'typed.js';
import Navbar from '@/components/Navbar.vue'


export default {
  name: 'Home',
  components: {
    Navbar,
  },
  mounted: function () {

    var options = {
      strings: [`Esta aplicación te ayuda a crear dibujos con formas (circulos, rectangulos, etc.)
        de una forma muy rapida y divertida :) Suerte!`],
      typeSpeed: 40,
      showCursor: false,
    };

    var typed = new Typed('.typed', options);

    console.log(typed);

  },
}
</script>
