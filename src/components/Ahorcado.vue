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
          <span class="categoria">La categoría es: animales</span>
        </b-col>
      </b-row>
      <!-- Lineas/Letras -->
      <b-row class="text-center">
        <b-col>
          <span class="guiones">{{guiones.join(" ")}}</span>
        </b-col>
      </b-row>
      <!-- Pistas -->
      <b-row class="text-center">
        <b-col>
          <span class="pista">Pista: {{pistaSeleccionada}}</span>
        </b-col>
      </b-row>
      <!-- Vidas -->
      <b-row class="text-center">
        <b-col>
          <span class="vidas">Te quedan {{vidas}} vidas restantes</span>
        </b-col>
      </b-row>
      <!-- Abecedario -->
      <b-row class="text-center">
        <b-col>
          <b-button-group class="flex-wrap">
            <b-button v-for="(letra, index) in abecedario" :key="index" @click="checaLetrasEnPalabra($event)">{{letra}}</b-button>
          </b-button-group>
        </b-col>
      </b-row>
      <!-- Alertas -->
      <b-row class="text-center">
        <b-col>
          <b-row align-h="center">
            <b-col cols="9">
              <div id="alerta"></div>
            </b-col>
          </b-row>
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>
<script>
export default {
  name: "ahorcado",
  data: function() {
    return {
      guiones: [],
      vidas: 10,
      palabraSeleccionada: "",
      pistaSeleccionada: "",
      diccionario: [
        {
          palabra: "perro",
          pista: "Soy el mejor amigo del hombre"
        },
        {
          palabra: "gato",
          pista: "Soy el felino más amigable"
        },
        {
          palabra: "abeja",
          pista: "Tengo alas y produzco miel"
        },
        {
          palabra: "conejo",
          pista: "Corro muy rápido y tengo grandes orejas"
        },
        {
          palabra: "caballo",
          pista: "Tengo muy buena vista y corro carreras"
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
        "ñ",
        "o",
        "p",
        "q",
        "r",
        "s",
        "t",
        "u",
        "v",
        "w",
        "x",
        "y",
        "z"
      ]
    };
  },
  computed: {
    esValido() {
      return this.valorInput.length < 2 ? true : false;
    }
  },
  mounted: function() {
    this.seleccionaPalabraPistaAleatorio(this.diccionario);
    this.dibujaGuionesBajos();
  },
  methods: {
    dibujaLineaVertical: function() {
      var canvas = document.getElementById("canvas1");
      if (canvas.getContext("2d")) {
        // Verifica soporte de canvas
        var context = canvas.getContext("2d");
        context.beginPath();
        context.moveTo(0, 0);
        context.lineTo(0, 300);
        context.strokeStyle = "brown";
        context.stroke();
      }
    },
    dibujaLineaHorizontal: function() {
      var canvas = document.getElementById("canvas1");
      if (canvas.getContext("2d")) {
        // Verifica soporte de canvas
        var context = canvas.getContext("2d");
        context.beginPath();
        context.moveTo(0, 0);
        context.lineTo(280, 0);
        context.strokeStyle = "brown";
        context.stroke();
      }
    },
    dibujaLineaDiagonal: function() {
      var canvas = document.getElementById("canvas1");
      if (canvas.getContext("2d")) {
        // Verifica soporte de canvas
        var context = canvas.getContext("2d");
        context.beginPath();
        context.moveTo(0, 50);
        context.lineTo(50, 0);
        context.strokeStyle = "brown";
        context.stroke();
      }
    },
    dibujaLineaVerticalCorta: function() {
      var canvas = document.getElementById("canvas1");
      if (canvas.getContext("2d")) {
        // Verifica soporte de canvas
        var context = canvas.getContext("2d");
        context.beginPath();
        context.moveTo(200, 0);
        context.lineTo(200, 20);
        context.strokeStyle = "brown";
        context.stroke();
      }
    },
    dibujaCabeza: function() {
      var canvas = document.getElementById("canvas1");
      if (canvas.getContext("2d")) {
        // Verifica soporte de canvas
        // Cabeza
        var context = canvas.getContext("2d");
        context.beginPath();
        context.fillStyle = "bisque";
        context.arc(200, 50, 30, 0, Math.PI * 2, true);
        context.fill();

        // Sonrisa
        context.beginPath();
        context.strokeStyle = "red";
        context.lineWidth = 3;
        context.arc(200, 50, 20, 0, Math.PI, false);
        context.stroke();

        // Ojos
        context.beginPath();
        context.fillStyle = "green";
        context.arc(190, 45, 3, 0, Math.PI * 2, true);
        context.fill();
        context.arc(210, 45, 3, 0, Math.PI * 2, true);
        context.fill();
      }
    },
    dibujaCuerpo: function() {
      var canvas = document.getElementById("canvas1");
      if (canvas.getContext("2d")) {
        // Verifica soporte de canvas
        var context = canvas.getContext("2d");
        context.beginPath();
        context.moveTo(200, 80);
        context.lineTo(200, 180);
        context.strokeStyle = "navy";
        context.stroke();
      }
    },
    dibujaBrazoIzquierdo: function() {
      var canvas = document.getElementById("canvas1");
      if (canvas.getContext("2d")) {
        // Verifica soporte de canvas
        var context = canvas.getContext("2d");
        context.beginPath();
        context.strokeStyle = "#0000ff";
        context.moveTo(200, 80);
        context.lineTo(150, 130);
        context.stroke();
      }
    },
    dibujaBrazoDerecho: function() {
      var canvas = document.getElementById("canvas1");
      if (canvas.getContext("2d")) {
        // Verifica soporte de canvas
        var context = canvas.getContext("2d");
        context.beginPath();
        context.strokeStyle = "#0000ff";
        context.moveTo(200, 80);
        context.lineTo(250, 130);
        context.stroke();
      }
    },
    dibujaPieIzquierdo: function() {
      var canvas = document.getElementById("canvas1");
      if (canvas.getContext("2d")) {
        // Verifica soporte de canvas
        var context = canvas.getContext("2d");
        context.beginPath();
        context.strokeStyle = "orange";
        context.moveTo(200, 180);
        context.lineTo(150, 280);
        context.stroke();
      }
    },
    dibujaPieDerecho: function() {
      var canvas = document.getElementById("canvas1");
      if (canvas.getContext("2d")) {
        // Verifica soporte de canvas
        var context = canvas.getContext("2d");
        context.beginPath();
        context.strokeStyle = "orange";
        context.moveTo(200, 180);
        context.lineTo(250, 280);
        context.stroke();
      }
    },
    seleccionaPalabraPistaAleatorio: function(diccionario) {
      var palabras = [];
      var pistas = [];
      for (const palabra in diccionario) {
        palabras.push(diccionario[palabra].palabra);
        pistas.push(diccionario[palabra].pista);
      }
      var randomIndex = Math.floor(Math.random() * palabras.length);
      this.palabraSeleccionada = palabras[randomIndex];
      this.pistaSeleccionada = pistas[randomIndex];
    },
    dibujaGuionesBajos: function() {
      var palabra = this.palabraSeleccionada;
      for (let index = 0; index < palabra.length; index++) {
        this.guiones.push("_");
      }
    },
    checaLetrasEnPalabra: function(e) {
      var arregloFunciones = [
        this.dibujaLineaVertical,
        this.dibujaLineaHorizontal,
        this.dibujaLineaDiagonal,
        this.dibujaLineaVerticalCorta,
        this.dibujaCabeza,
        this.dibujaCuerpo,
        this.dibujaBrazoIzquierdo,
        this.dibujaBrazoDerecho,
        this.dibujaPieIzquierdo,
        this.dibujaPieDerecho
      ];
      var valor = e.target.innerHTML;
      if (!this.palabraSeleccionada.includes(valor)) {
        arregloFunciones[arregloFunciones.length - this.vidas]();
        this.vidas--;
      } else {
        // var guiones = document
        //   .getElementsByClassName("guiones")[0]
        //   .innerText.split(" ");

        var obtenIndex = function(str, char) {
          return str
            .split("")
            .map(function(c, i) {
              if (c == char) return i;
            })
            .filter(function(v) {
              return v >= 0;
            });
        };

        var indices = obtenIndex(this.palabraSeleccionada, valor);

        console.log(this.guiones);

        console.log("posiciones a modificar", indices);

        for (let i = 0; i < indices.length; i++) {
          this.guiones.splice(indices[i], indices.length, valor);
        }

        console.log("arreglo modificado", this.guiones);
      }
    }
  }
};
</script>
<style scoped>
.ahorcado {
  padding-bottom: 100px;
}

.guiones {
  font-size: 4em;
}

.categoria {
  font-size: 2em;
}

.pista {
  font-size: 2em;
}

.vidas {
  font-size: 2em;
}

.etiqueta {
  font-size: 2em;
}
</style>
