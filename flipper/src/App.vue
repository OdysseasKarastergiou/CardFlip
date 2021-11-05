<template>
  <div id="app">
    <header>
      <h1>FlipCard App</h1>
    </header>
    <transition-group 
    name="list-complete">
      <Card 
      class="list-complete-item" 
      :flippedF="flippedF" 
      @freebetEvent="offeredFreebet" 
      @cancelEvent="freebetCanceled" 
      v-for="card in cards" 
      :key="card">
        <template slot="front">
          <div 
          class="list-complete-item grid grid-cols-2">
            <div>
              <div 
              class="flex text-purple-500 text-3xl font-bold">
                <img 
                src="https://pm.ua/content/uploads/Free_Bet_10_UAH_2_1_23c98cc95d.png" 
                class="w-12">
                FREEBET OFFER
              </div>
                <div 
                class="  m-2 flex text-purple-500 text-xl font-semibold">
                one freebet (5+1) is waiting for you!
                </div>
                <div 
                class="bg-red-700 m-3 text-white flex  ">
                Exp.Date 15/05/2022
                </div>
            </div>
            <div 
            class="m-10 text-purple-500 font-bold text-3xl">
            FREE <br />
            COLUMN
            </div>
          </div>
        </template>
        <template slot="back">
          <div 
          class="list-complete-item divide-y-2 divide-black md:divide-solid">
            <div>
              <div 
              class="m-6">
                <span 
                class="flex text-black text-2xl font-bold">
                Freebet with Quick Pick</span><br />
              </div>
            <div 
            class="flex border-solid  border-4 border-gray-200 bg-gray-200">
              <div 
              class="inline-flex m-3 h-8 font-bold text-2xl text-white" 
              v-for="(number,i) in numbersArrayF" 
              :key="i">
                <div 
                class="rounded-full h-10 w-10 text-center" 
                :class="{luckyN:i===5,unluckyN:i!==5}">
                {{ number }}
                </div>    
                </div><br />               
            </div>
              <div 
              class="m-6">
                <div 
                class="text-xl flex font-bold">
                Consecutive draws:
                </div>
                <div 
                class="text-l flex">
                Click on "Submit" button to redeem your free bet and <br /> 
                participate in the next draw with the above randomly <br /> 
                selected numbers!
                </div>
              </div>
            </div>
          </div>
        </template>
      </Card>
    </transition-group>
  </div>
</template>

<script>
import Card from './components/Card.vue';

export default {
  name:"App",
  components:{
    Card
  },
  data(){
    return{
      flippedF:true,
      flippedB:false,
      numbersArrayF:[],
      cards:5
    }
  },
  methods:{
    offeredFreebet(){
      this.flippedF = true;
      for(var i=0;i<6;i++){
            let num = Math.floor(Math.random() * (40 - 1 + 1)) + 1;
            for(let check of this.numbersArrayF){
                while(check === num){
                  num = Math.floor(Math.random() * (40 - 1 + 1)) + 1;
                }
            }
        this.numbersArrayF.push(num);
      }

    },
    freebetCanceled(){
      this.flippedB = false;
      this.numbersArrayF.splice(0);
    },
     randomIndex: function () {
      return Math.floor(Math.random() * this.items.length)
    },
    add: function () {
      this.items.splice(this.randomIndex(), 0, this.nextNum++)
    },
    remove: function () {
      this.items.splice(this.randomIndex(), 1)
    },
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;

}
.luckyN{
  --tw-text-opacity: 1;
  color: rgba(59, 130, 246, var(--tw-text-opacity));
  font-weight: 700;
  --tw-bg-opacity: 1;
  background-color: rgba(252, 211, 77, var(--tw-bg-opacity));
}
.unluckyN{
  --tw-text-opacity: 1;
  color: rgba(255, 255, 255, var(--tw-text-opacity));
  --tw-bg-opacity: 1;
  background-color: rgba(59, 130, 246, var(--tw-bg-opacity));
}


.list-complete-item {
  transition: all 2s;
  display: inline-block;
  margin-right: 2px;  
  position: relative;
  
}
.list-complete-enter, .list-complete-leave-to
/* .list-complete-leave-active below version 2.1.8 */ {
  opacity: 0;
  transform: translateY(20px);
  position: absolute;
}
.list-complete-leave-active {
  position: absolute;
}



</style>

