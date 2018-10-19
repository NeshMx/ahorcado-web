<template>
  <div class="ahorcado">
    <b-container>
      <!-- Canvas -->
      <b-row class="text-center">
        <b-col>
          <canvas id="canvas1" width="400px" height="300px"></canvas>
        </b-col>
      </b-row>
      <!-- Lineas/Letras -->
      <b-row class="text-center">
        <b-col>
          <span>{{drawUnderscores()}}</span>
        </b-col>
      </b-row>
      <!-- Pistas -->
      <b-row class="text-center">
        <b-col>

        </b-col>
      </b-row>
      <!-- Vidas -->
      <b-row class="text-center">
        <b-col>
          <p></p>
        </b-col>
      </b-row>
      <!-- Abecedario -->
      <b-row class="text-center">
        <b-col>
          <b-button-group>
            <b-button v-for="(letra, index) in abecedario" :key="index">{{letra}}</b-button>
          </b-button-group>
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>
<script>
export default {
  name: "ahorcado",
  props: {
    vidas: Number
  },
  data: function() {
    return {
      diccionario: [
        {
          palabra: "test",
          pista: "this 'test' hint"
        },
        {
          palabra: "test2",
          pista: "this 'test2' hint"
        },
        {
          palabra: "test3",
          pista: "this 'test3' hint"
        },
        {
          palabra: "test4",
          pista: "this 'test4' hint"
        },
        {
          palabra: "test5",
          pista: "this 'test5' hint"
        }
      ],
      abecedario: [
        "a",
        "b",
        "c",
        "d",
        "e",
        "f",
        "g",
        "h",
        "i",
        "j",
        "k",
        "l",
        "m",
        "n",
        "o",
        "p",
        "q",
        "r",
        "s",
        "u",
        "v",
        "w",
        "x",
        "y",
        "z"
      ]
    };
  },
  mounted: function() {},
  methods: {
    drawVerticalLine: function() {
      var canvas = document.getElementById("canvas1");
      if (canvas.getContext("2d")) {
        // Check HTML5 canvas support
        var context = canvas.getContext("2d");
        context.beginPath();
        context.moveTo(0, 0);
        context.lineTo(0, 300); // vertical line
        context.strokeStyle = "brown";
        context.stroke();
      }
    },
    drawHorizontalLine: function() {
      var canvas = document.getElementById("canvas1");
      if (canvas.getContext("2d")) {
        // Check HTML5 canvas support
        var context = canvas.getContext("2d");
        context.beginPath();
        context.moveTo(0, 0);
        context.lineTo(280, 0); // horizontal line
        context.strokeStyle = "brown";
        context.stroke();
      }
    },
    drawDiagonalLine: function() {
      var canvas = document.getElementById("canvas1");
      if (canvas.getContext("2d")) {
        // Check HTML5 canvas support
        var context = canvas.getContext("2d");
        context.beginPath();
        context.moveTo(0, 50);
        context.lineTo(50, 0); // diagonal line
        context.strokeStyle = "brown";
        context.stroke();
      }
    },
    drawVerticalShortLine: function() {
      var canvas = document.getElementById("canvas1");
      if (canvas.getContext("2d")) {
        // Check HTML5 canvas support
        var context = canvas.getContext("2d");
        context.beginPath();
        context.moveTo(200, 0);
        context.lineTo(200, 20); // vertical short line
        context.strokeStyle = "brown";
        context.stroke();
      }
    },
    drawHead: function() {
      var canvas = document.getElementById("canvas1");
      if (canvas.getContext("2d")) {
        // Check HTML5 canvas support
        var context = canvas.getContext("2d");
        context.beginPath();
        context.fillStyle = "bisque"; // #ffe4c4
        context.arc(200, 50, 30, 0, Math.PI * 2, true); // draw circle for head
        // (x,y) center, radius, start angle, end angle, anticlockwise
        context.fill();

        // smile
        context.beginPath();
        context.strokeStyle = "red"; // color
        context.lineWidth = 3;
        context.arc(200, 50, 20, 0, Math.PI, false); // draw semicircle for smiling
        context.stroke();

        // eyes
        context.beginPath();
        context.fillStyle = "green"; // color
        context.arc(190, 45, 3, 0, Math.PI * 2, true); // draw left eye
        context.fill();
        context.arc(210, 45, 3, 0, Math.PI * 2, true); // draw right eye
        context.fill();
      }
    },
    drawBody: function() {
      var canvas = document.getElementById("canvas1");
      if (canvas.getContext("2d")) {
        // Check HTML5 canvas support
        var context = canvas.getContext("2d");
        context.beginPath();
        context.moveTo(200, 80);
        context.lineTo(200, 180);
        context.strokeStyle = "navy";
        context.stroke();
      }
    },
    drawLeftArm: function() {
      var canvas = document.getElementById("canvas1");
      if (canvas.getContext("2d")) {
        // Check HTML5 canvas support
        var context = canvas.getContext("2d");
        context.beginPath();
        context.strokeStyle = "#0000ff"; // blue
        context.moveTo(200, 80);
        context.lineTo(150, 130);
        context.stroke();
      }
    },
    drawRightArm: function() {
      var canvas = document.getElementById("canvas1");
      if (canvas.getContext("2d")) {
        // Check HTML5 canvas support
        var context = canvas.getContext("2d");
        context.beginPath();
        context.strokeStyle = "#0000ff"; // blue
        context.moveTo(200, 80);
        context.lineTo(250, 130);
        context.stroke();
      }
    },
    drawLeftFoot: function() {
      var canvas = document.getElementById("canvas1");
      if (canvas.getContext("2d")) {
        // Check HTML5 canvas support
        var context = canvas.getContext("2d");
        context.beginPath();
        context.strokeStyle = "orange";
        context.moveTo(200, 180);
        context.lineTo(150, 280);
        context.stroke();
      }
    },
    drawRightFoot: function() {
      var canvas = document.getElementById("canvas1");
      if (canvas.getContext("2d")) {
        // Check HTML5 canvas support
        var context = canvas.getContext("2d");
        context.beginPath();
        context.strokeStyle = "orange";
        context.moveTo(200, 180);
        context.lineTo(250, 280);
        context.stroke();
      }
    },
    selectRandomWord: function(diccionario) {
      var palabras = [];
      for (const palabra in diccionario) {
        palabras.push(diccionario[palabra].palabra);
      }
      var randomIndex = Math.floor(Math.random() * palabras.length);
      var palabraSeleccionada = palabras[randomIndex];
      return palabraSeleccionada;
    },
    drawUnderscores: function() {
      var palabra = this.selectRandomWord(this.diccionario);
      var guiones = [];
      for (let index = 0; index < palabra.length; index++) {
        guiones.push("_");
      }
      return guiones.join(" ");
    }
  }
};
</script>
<style scoped>
</style>
