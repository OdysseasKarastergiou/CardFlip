<template>
<div class="flip-container">
   <transition 
   :name="flipped ? 'flip-transition' : 'flip-transition-reversed'" 
   mode="out-in">
     <div 
     v-if="!flipped" 
     key="front">
       <div 
       class="front border-solid border-2 overflow-auto bg-yellow-300 rounded">
        <slot name="front"></slot>
        <button 
        class="frontFlipBtn bg-green-400 rounded text-center float-left m-2 text-white" 
        @click="freebetOffer">
        FREE BET
        </button>
      </div>
    </div>
     <div 
     v-else key="back">
       <div 
       class="back border-solid border-2 bg-white rounded">
        <slot name="back"></slot>
        <p 
        class="backFlipBtn border-3 border-solid bg-white rounded-full absolute top-0 right-5"> 
        Cancel
        </p>
        <button 
        class="backFlipBtn border-3 border-solid bg-white outline-black outline-solid rounded-full absolute top-0 right-1" 
        @click="cancelFreebet">
        X
        </button>
        <button 
        class="bg-blue-500 w-20 h-10 rounded text-white">
        FREE</button>
        <button 
        class="bg-green-400 w-20 h-10 rounded text-white">
        SUBMIT</button>
      </div>
     </div>
   </transition>
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
      this.numbersArray = this.numbersArrayB;
      this.$emit('cancelEvent');
    }

  }
};
</script>

<style type='text/css' scoped>

/*        */ 
.flip-container {
    perspective: 1000px;
    transform-style: preserve-3d;
    display: inline-block;
}
.flip-transition-enter-active,
.flip-transition-reversed-enter-active {
    transition-duration: .3s;
    transition-timing-function: ease-out;
}
.flip-transition-leave-active,
.flip-transition-reversed-leave-active {
    transition-duration: .3s;
    transition-timing-function: ease-in;
}
.flip-transition-enter,
.flip-transition-reversed-leave-to {
    transform: rotateY(-90deg);
}
.flip-transition-leave-to,
.flip-transition-reversed-enter {
    transform: rotateY(90deg);
}
  


</style>
