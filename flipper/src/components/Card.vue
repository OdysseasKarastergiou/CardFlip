<template>
  <div v-bind:class="flipped ? 'flip-container flipped': 'flip-container'">
    <div class="flipper">
      <div class="front border-solid border-2 overflow-auto bg-yellow-300 rounded">
        <slot name="front"></slot>
        <button class="frontFlipBtn bg-green-400 rounded text-center float-left m-2 text-white" 
            v-on:click="freebetOffer">
            FREE BET
        </button>
      </div>
      <div class="back border-solid border-2 bg-white rounded">
        <slot name="back"></slot>
        <p class="backFlipBtn border-3 border-solid bg-white rounded-full absolute top-0 right-5"> Cancel</p>
        <button class="backFlipBtn border-3 border-solid bg-white outline-black outline-solid rounded-full absolute top-0 right-1" 
            v-on:click="cancelFreebet"> 
            X
        </button>
        <button class="bg-blue-500 w-20 h-10 rounded text-white">FREE</button>
        <button class="bg-green-400 w-20 h-10 rounded text-white">SUBMIT</button>
      </div>
    </div>
  </div>

</template>

<script> 

export default {
  name: 'Card',
  props:{
    flippedF:{
      type:Boolean
    },
    flippedB:{
      type:Boolean
    },
    numbersArrayF:{
      type:Array
    }
  },
  data(){
    return {
        flipped:"",
        numbersArray:[]
    }
  },
  methods:{
    freebetOffer(){
      this.flipped = this.flippedF;
      this.numbersArray = this.numbersArrayF;
      this.$emit('freebetEvent');
    },
    cancelFreebet(){
      this.flipped = this.flippedB;
      this.numbersArray = this.numbersArrayF;
      this.$emit('cancelEvent');
    }

  }
};
</script>

<style type='text/css' scoped>
i.frontFlipBtn,
i.backFlipBtn {
    position:absolute; 
    right: 20px; 
    top: 20px;
    color:#FFFFFF;
}
i.backFlipBtn {
    -webkit-transform: rotateY(-180deg);
    -moz-transform: rotateY(-180deg);
    -o-transform: rotateY(-180deg);
    -ms-transform: rotateY(-180deg);
    transform: rotateY(-180deg);
}
.flip-container {
  -webkit-perspective: 1000;
  -moz-perspective: 1000;
  -o-perspective: 1000;
  perspective: 1000;
}
.flip-container {
  position: relative;
  max-width:100%;
  max-height:100%;
  overflow:auto;
}
.flipper {
  -moz-transform: perspective(1000px);
  -moz-transform-style: preserve-3d;
  position: relative;
  max-width:100%;
  max-height:100%;
  overflow:auto;

}

.front,
.back {
  -webkit-backface-visibility: hidden;
  -moz-backface-visibility: hidden;
  -o-backface-visibility: hidden;
  backface-visibility: hidden;
  -webkit-transition: 0.6s;
  -webkit-transform-style: preserve-3d;
  -moz-transition: 0.6s;
  -moz-transform-style: preserve-3d;
  -o-transition: 0.6s;
  -o-transform-style: preserve-3d;
  -ms-transition: 0.6s;
  -ms-transform-style: preserve-3d;
  transition: 0.6s;
  transform-style: preserve-3d;
  top: 0;
  left: 0;
  width: 100%;
}
.back {
  -webkit-transform: rotateY(-180deg);
  -moz-transform: rotateY(-180deg);
  -o-transform: rotateY(-180deg);
  -ms-transform: rotateY(-180deg);
  transform: rotateY(-180deg);
  position: relative;

}
.flip-container.flipped .back {
  -webkit-transform: rotateY(0deg);
  -moz-transform: rotateY(0deg);
  -o-transform: rotateY(0deg);
  -ms-transform: rotateY(0deg);
  transform: rotateY(0deg);
}
.flip-container.flipped .front {
  -webkit-transform: rotateY(180deg);
  -moz-transform: rotateY(180deg);
  -o-transform: rotateY(180deg);
  -ms-transform: rotateY(180deg);
  transform: rotateY(180deg);
  
}
.front {
  z-index: 2;
  
}


  


</style>
