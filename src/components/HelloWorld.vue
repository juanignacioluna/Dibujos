<template>
  <div id="mainDiv">

    <h1>{{ persona.nombre }}</h1>

    <br>

    <button class="button">button</button>

    <br>

    <div class="draggable"> Draggable Element </div>

    <br>

    <div class="wrapper">
      <div id="left" class="container">
        <div>Item 1.</div>
        <div>Item 2.</div>
        <div>Item 3.</div>
        <div>Item 4.</div>
      </div>
      <div id="right" class="container">
        <div>Item 5.</div>
        <div>Item 6.</div>
        <div>Item 7.</div>
      </div>
    </div>

    <br>  

    <div class="element"></div>

    <br>


    <div v-for="item in items" :key="item.id">
        {{ item.mensaje }}
    </div>

    <br>

    <div id="numero"></div>

    <br>

    <div id="draw-shapes"></div>

  </div>
</template>

<script>
  
import Typed from 'typed.js';
import { CountUp } from 'countup.js';
import * as Two from 'twojs-ts';
import * as dragula from 'dragula';
import * as interact from 'interactjs';
import $ from 'jquery';

// import html2canvas from 'html2canvas';
// import {rough} from 'roughjs';


export default {
  name: 'HelloWorld',
  data(){
    return{
      persona: {
        nombre: 'Juan',
        id: 1
      },
      items: [
        { mensaje: 'Foo', id: 1 },
        { mensaje: 'Bar', id: 2 }
      ],
    }
  },
  mounted: function () {

    var options = {
      strings: ['hola...', '...chau'],
      typeSpeed: 200,
      loop: true,
      loopCount: Infinity,
      showCursor: true,
    };

    var typed = new Typed('.element', options);

    console.log(typed);




    const optionsCountUp = {
      duration: 5000,
    };

    let demo = new CountUp('numero', 10000, optionsCountUp);

    demo.start();
    



    // Make an instance of two and place it on the page.
    let elem = document.getElementById('draw-shapes');
    var params = { width: 3000, height: 3000 };
    var two = new Two(params).appendTo(elem);

    // two has convenience methods to create shapes.
    var circle = two.makeCircle(72, 100, 50);
    var rect = two.makeRectangle(213, 100, 100, 100);
    var ellipse = two.makeEllipse(550, 100, 30, 20);
    var star = two.makeStar(850, 100, 60, 40);
    var polygon = two.makePolygon (350, 100, 20, 5);

    // The object returned has many stylable properties:
    polygon.fill = 'yellow';
    polygon.stroke = 'black';
    polygon.linewidth = 2;
    polygon.opacity = 0.15;

    // The object returned has many stylable properties:
    star.fill = 'green';
    star.stroke = 'black';
    star.linewidth = 6;
    star.opacity = 0.25;

    // The object returned has many stylable properties:
    ellipse.fill = 'black';
    ellipse.stroke = 'blue'; // Accepts all valid css color
    ellipse.linewidth = 10;

    // The object returned has many stylable properties:
    circle.fill = '#FF8000';
    circle.stroke = 'orangered'; // Accepts all valid css color
    circle.linewidth = 5;

    rect.fill = 'rgb(0, 200, 255)';
    rect.opacity = 0.75;
    rect.noStroke();

    // Don't forget to tell two to render everything
    // to the screen
    two.update();






    dragula([document.getElementById('left'), document.getElementById('right')], {
      revertOnSpill: true
    });







    let arrayXY = [];

    let arrayXY2 = [];

    for (let i = 0; i < $('path').length; i++) {

      $('path:nth-child('+(i+1)+')').addClass('draggable'+(i+1)+'');

      arrayXY.push($('path:nth-child('+(i+1)+')').position());

      console.log(arrayXY);

      arrayXY2.push({ x: (arrayXY[i].left + 30), y: 100 });

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
}
</script>


<style scoped>

  .wrapper {
      cursor: move; 
      cursor: grab;
  }

  .wrapper:active {
      cursor: grabbing;
  }

  *{
    overflow-x: hidden;
  }

  button{
    overflow-x: initial;
  }

  .draggable {
    touch-action: none;
    user-select: none;
  }

</style>
