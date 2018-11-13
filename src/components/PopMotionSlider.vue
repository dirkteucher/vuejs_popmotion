<template>
    <div class="popMotionSlider" >
        <Box class="box" :pose="isVisible ? 'visible' : 'hidden'" />
        <Box class="box"  />
        <Box class="box3"  />
        <Box class="box3"  />
        <button v-on:click="moveBox()">Move box {{windowWidth}}</button>
    </div>
</template>

<script>
  import posed from "vue-pose";
  import { tween, styler, pointer } from 'popmotion';
  import { listen } from 'popmotion';


  export default {
    name: "popMotionSlider",
    data: function () {
      return {
        isVisible: false,
        windowWidth: ''
      }
    },
    mounted: function(stuff){
      pointer()
        .start(({ x, y }) => {
          console.log(x, y);
          this.windowWidth = x;
        });

      listen(document, 'mousedown')
        .start((e) => console.log("tatata"));

      setInterval(() => {
        this.isVisible = !this.isVisible;
      }, 1000);

      console.log(posed);

    },

    methods: {
      boxClicked: function (event) {
            alert("cds");
        },
      moveBox : function() {

        const element = document.querySelector('.box3');
        const ball = styler(element);

        tween({ to: 300, duration: 500,   flip: 1, })
          .start(v => ball.set('x', v));

      }
    },

    components: {
      Box: posed.div({
        visible: { opacity: 1 },
        hidden: { opacity: 0 },
        draggable: 'x',
        dragBounds: { left: '-1000%', right: '1000%' },
        init: { scale: 1, boxShadow: '0px 0px 0px rgba(0,0,0,0)' },
        drag: { scale: 1.2, boxShadow: '5px 5px 10px rgba(0,0,0,0.5)',  },
        dragEnd: {
          x: 0,
          y: 0,
          transition: { type: 'spring' }
        }
      })
    }
  }
</script>

<style>
    .popMotionSlider {
        background-color: azure;
    }
    .box {
        background-color: blue;
        width: 100px;
        height:100px;
        position: relative;
        left: 20%;
    }

    .box3 {
        background-color: blue;
        width: 100px;
        height:100px;
        position: relative;
        left: 20%;
    }
</style>
