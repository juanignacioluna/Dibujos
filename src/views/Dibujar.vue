<template>
  <div class="dibujar">


    <Navbar />

    <div class="flex demo center">
      <div class="two-third main">


        <h1>Dibuje aquí:</h1>

        <h2>Empiece creando una forma de las <span id="numero"></span> posibles.</h2>

        <h4>El color de relleno debe ser un color en hexadecimal (ej: #333333), la opacidad un valor entre 0 y 1 (ej: 0.7),
        el color del borde un hexadecimal como el color de relleno, el tamaño del borde debe ser un valor entre 0 y 10.</h4>

		<select name="select" @change="onChangeSelect($event)">
		  <option value="Circulo" selected>Circulo</option> 
		  <option value="Poligono">Poligono</option>
		  <option value="Rectangulo">Rectangulo</option>
		  <option value="Estrella">Estrella</option>
		  <option value="Elipse">Elipse</option>
		</select>


		<div class="flex demo center three">
			<label><input v-model="colorDeRelleno" type="text" placeholder="color de relleno"></label>
			<label><input v-model="opacidad" type="text" placeholder="opacidad"></label>
			<label><input v-model="colorDelBorde" type="text" placeholder="color del borde"></label>
			<label><input v-model="tamanoDelBorde" type="text" placeholder="tamaño del borde"></label>
		    <div v-for="ajuste in ajustes" :key="ajuste.id">
		        <label><input :id="ajuste.tipoMin" type="text" :placeholder="ajuste.tipo"></label>
		    </div>
		</div>


		<button class="agregar" v-on:click="agregar">Agregar</button>

		<div id="draw-shapes"></div>


      </div>
    </div>


  </div>
</template>

<style>

	.main{
	   margin-top: 10px;
	}

	.dibujar{
	  overflow-x: hidden;
	}

	select{
		width: 25%;
		margin-bottom: 10px;
	}

	.agregar{
		width: 25%;
	}

</style>

<script>

import Navbar from '@/components/Navbar.vue'
import { CountUp } from 'countup.js';
import * as Two from 'twojs-ts';
import * as interact from 'interactjs';
import $ from 'jquery';



export default {
  name: 'Dibujar',
  data(){

    return{
      ajustes: [
        { tipo: 'radio', id: 1, tipoMin: 'radio' }
      ],
      two: "",
      colorDeRelleno: "",
      opacidad: "",
      colorDelBorde: "",
      tamanoDelBorde: "",
    }
  },
  components: {
    Navbar,
  },
  mounted: function () {

    const optionsCountUp = {
      duration: 10,
    };

    let demo = new CountUp('numero', 5, optionsCountUp);

    demo.start();


    let elem = document.getElementById('draw-shapes');
    var params = { width: 3000, height: 500 };
    this.two = new Two(params).appendTo(elem);



  },
   methods: {

   		dragg(){

		    let arrayXY = [];

		    let arrayXY2 = [];

		    for (let i = 0; i < $('path').length; i++) {

		      $('path:nth-child('+(i+1)+')').addClass('draggable'+(i+1)+'');

		      arrayXY.push($('path:nth-child('+(i+1)+')').position());

		      console.log(arrayXY);

		      arrayXY2.push({ x: (arrayXY[i].left + 30), y: arrayXY[i].top - 400 });

		      interact('.draggable'+(i+1)+'').draggable({
		        listeners: {
		          start (event) {
		            console.log(event.type, event.target)
		          },
		          move (event) {
		            arrayXY2[i].x += event.dx
		            arrayXY2[i].y += event.dy

		            event.target.style.transform =
		              `translate(${arrayXY2[i].x}px, ${arrayXY2[i].y}px)`
		          },
		        }
		      })

		    }

   		},

	   	agregar(event){



			switch ($("select").val()) {
			  case 'Circulo':

				    var circle = this.two.makeCircle(72, 100, parseInt($("#radio").val()));

				    circle.fill = this.colorDeRelleno;
				    circle.stroke = this.colorDelBorde; 
				    circle.linewidth = this.tamanoDelBorde;
					circle.opacity = this.opacidad;

			    break;
			  case 'Poligono':

				    var polygon = this.two.makePolygon(72, 100, parseInt($("#radio").val()), parseInt($("#lados").val()));

				    polygon.fill = this.colorDeRelleno;
				    polygon.stroke = this.colorDelBorde; 
				    polygon.linewidth = this.tamanoDelBorde;
					polygon.opacity = this.opacidad;

			    break;
			  case 'Rectangulo':

				    var rectangle = this.two.makeRectangle(72, 100, parseInt($("#ancho").val()), parseInt($("#alto").val()));

				    rectangle.fill = this.colorDeRelleno;
				    rectangle.stroke = this.colorDelBorde; 
				    rectangle.linewidth = this.tamanoDelBorde;
					rectangle.opacity = this.opacidad;

			    break;
			  case 'Estrella':

				    var star = this.two.makeStar(72, 100, parseInt($("#radioExterno").val()), parseInt($("#radioInterno").val()), parseInt($("#puntosDeLaEstrella").val()));

				    star.fill = this.colorDeRelleno;
				    star.stroke = this.colorDelBorde; 
				    star.linewidth = this.tamanoDelBorde;
					star.opacity = this.opacidad;

			    break;
			  case 'Elipse':

				    var ellipse = this.two.makeEllipse(72, 100, parseInt($("#ancho").val()), parseInt($("#alto").val()));

				    ellipse.fill = this.colorDeRelleno;
				    ellipse.stroke = this.colorDelBorde; 
				    ellipse.linewidth = this.tamanoDelBorde;
					ellipse.opacity = this.opacidad;

			    break;
			}


		    this.two.update();

		    this.dragg();

			$("input").val('');

		    this.colorDeRelleno = "";
		    this.opacidad = "";
		    this.colorDelBorde = "";
		    this.tamanoDelBorde = "";


	   	},

        onChangeSelect(event) {

			switch (event.target.value) {
			  case 'Circulo':
			    this.ajustes = [];
			    this.ajustes[0] = { tipo: 'radio', id: 1, tipoMin: 'radio' };
			    break;
			  case 'Poligono':
			    this.ajustes = [];
			    this.ajustes[0] = { tipo: 'radio', id: 1, tipoMin: 'radio' };
			    this.ajustes[1] = { tipo: 'lados', id: 2, tipoMin: 'lados' };
			    break;
			  case 'Rectangulo':
			    this.ajustes = [];
			    this.ajustes[0] = { tipo: 'ancho', id: 1, tipoMin: 'ancho' };
			    this.ajustes[1] = { tipo: 'alto', id: 2, tipoMin: 'alto' };
			    break;
			  case 'Estrella':
			    this.ajustes = [];
			    this.ajustes[0] = { tipo: 'radio externo', id: 1, tipoMin: 'radioExterno' };
			    this.ajustes[1] = { tipo: 'radio interno', id: 2, tipoMin: 'radioInterno' };
			    this.ajustes[2] = { tipo: 'puntos de la estrella', id: 3, tipoMin: 'puntosDeLaEstrella' };
			    break;
			  case 'Elipse':
			    this.ajustes = [];
			    this.ajustes[0] = { tipo: 'ancho', id: 1, tipoMin: 'ancho' };
			    this.ajustes[1] = { tipo: 'alto', id: 2, tipoMin: 'alto' };
			    break;
			}

			$("input").val('');

		    this.colorDeRelleno = "";
		    this.opacidad = "";
		    this.colorDelBorde = "";
		    this.tamanoDelBorde = "";

        }

   }

}
</script>
