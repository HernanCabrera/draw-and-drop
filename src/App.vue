<template lang="pug">
  #app
    .contenedor-remera(
                      @mousemove="moverImg"
                      @touchmove="moverImg"
    )
      figure.remera
        img.imagen(src="src/assets/remera.png")
      .contenedor-icon
        .icon-actual(
              @mousedown="escucharClick"
              @mouseup="escucharSalidaDelClick"
              @touchstart="escucharClick"
              @touchend="escucharSalidaDelClick"
              :class="iconoActual" 
              :style="{ color: colorActual, fontSize: tamanoActual + 'px', left: posicionX, top: posicionY }"
        )

    .opciones
      .contenedor-color
        span.titulo Color
        input.color(
              type="color"
              v-model="colorActual"
        )
      .contenedor-tamano
        span.titulo Tamaño
        input.tamano(
              type="number"
              min="20"
              max="200"
              step="5"
              v-model="tamanoActual"
        )

    ul.menu
      li.item(v-for="i in items")
        button.icon(
                    :for="i.id"  
                    :class="i.src"
                    @click="devolverIconoActual(i.src)"
        )
</template>
<script>
export default {
  name: 'app',
  data () {
    return {
      items: [
        { src: 'icon-droplet', id: 1 },
        { src: 'icon-play', id: 2 },
        { src: 'icon-pacman', id: 3 },
        { src: 'icon-spades', id: 4 },
        { src: 'icon-clubs', id: 5 },
        { src: 'icon-diamonds', id: 6 },
        { src: 'icon-bullhorn', id: 7 },
        { src: 'icon-connection', id: 8 },
        { src: 'icon-fire', id: 9 },
        { src: 'icon-lab', id: 10 },
        { src: 'icon-magnet', id: 11 },
        { src: 'icon-bin', id: 12 },
        { src: 'icon-bin2', id: 13 },
        { src: 'icon-briefcase', id: 14 },
        { src: 'icon-airplane', id: 15 },
        { src: 'icon-truck', id: 16 },
        { src: 'icon-road', id: 17 },
        { src: 'icon-accessibility', id: 18 },
        { src: 'icon-target', id: 19 }
      ],

      iconoActual: '',
      colorActual: '#DD1C1A',
      tamanoActual: '50',
      posicionX: '50% - 50px',
      posicionY: '50% - 50px',
      auxPosicionX: 0,
      auxPosicionY: 0,
      estaActivo: false
    }
  },
  methods: {
    devolverIconoActual (iconoActual) {
      this.iconoActual = iconoActual
    },
    moverImg (ev) {
      if (this.estaActivo) {
        this.posicionX = (ev.pageX - this.auxPosicionX) + 'px'
        this.posicionY = (ev.pageY - this.auxPosicionY) + 'px'
      }
    },
    escucharClick (ev) {
      this.estaActivo = true
      this.auxPosicionX = ev.offsetX
      this.auxPosicionY = ev.offsetY
    },
    escucharSalidaDelClick () {
      this.estaActivo = false
    }
  }
}
</script>

<style lang="scss">
ul{
  margin: 0;
  padding: 0;
}
figure{
  margin: 0;
}

.contenedor-remera{
  margin-bottom: 50px;
  position: relative;
  .remera{
    margin: 0 auto;
    max-width: 400px;
    .imagen{
      width: 100%;
      height: auto;
    }
  }
  .contenedor-icon{
    position: absolute;
    top: 0;
    left: 0;
    height: 100%;
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
    overflow: hidden;
    .icon-actual{
      border: 0;
      display: inline-block;
      position: absolute;
      cursor: pointer;
    }
  }
}
.opciones{
  margin: 0 auto 20px auto;
  max-width: 700px;
  text-align: center;
  .titulo{
    display: block;
    font-size: 24px;
    font-family: sans-serif;
    color: #161612;
    font-weight: 700;
  }
  .contenedor-color{
    display: inline-block;
    .color{
      display: inline-block;
      width: 100px;
      height: 20px;
    }
  }
  .contenedor-tamano{
    display: inline-block;
    .tamano{
      display: inline-block;
      width: 100px;
      height: 20px;
      padding: 0;
      text-align: center;
      font-weight: 700;
      font-size: 16px;
      color: #161612;
    }
  }
}
.menu{
  display: flex;
  list-style: none;
  max-width: 700px;
  background: #fcfcfc;
  overflow: auto;
  margin: 0 auto;
  .item{
    margin: 10px 20px;
    .icon{
      color: #5e5e5e;
      border: 0;
      background: none;
      display: inline-block;
      font-size: 80px;
      cursor: pointer;
      transition: .3s;
    }
    .icon:hover{
      transform: scale(1.2);
    }
  }
}

@media screen and (max-width: 600px){
  .opciones{
    .titulo{
      font-size: 24px;
    }
    .contenedor-color{
      .color{
        width: 100px;
        height: 20px;
      }
    }
    .contenedor-tamano{
      .tamano{
        width: 100px;
        height: 20px;
        font-size: 16px;
      }
    }
  }
  .menu{
    .item{
      .icon{
        font-size: 64px;
      }
    }
  }
}
@media screen and (max-width: 400px){
  .menu{
    .item{
      .icon{
        font-size: 51.2px;
      }
    }
  }
}


</style>
