<script setup>


import { ref } from 'vue'
const TouchArray=[7,8,9,'+',4,5,6,"-",1,2,3,"/",".",0,"C","*","%"]
const specialOperator=["+/-","(",")","x²"]
let current=ref(0||"")

let operator=null
let previousValue=""
const action=(touch)=>{
  if(!isNaN(touch)||touch==='.'||['(',')'].includes(touch)){

    current.value+=touch
  }
  if(touch==='C'){
    current.value=""
  }

  if (['+','/','*','-'].includes(touch)){
    operator=touch
    previousValue=current.value 
    current.value=""
    
  }
  if (touch==='%'){
    current.value=current.value/100+""
    
  }
  if (touch==='x²'){
    current.value=current.value*current.value
    
    
  }
  if (touch==='+/-'){
    current.value="-"+current.value
    
    
  }


}



const calc=()=>{
  if (isNaN(previousValue) || isNaN(current.value)){
    current.value="Error"
  }
  else{

    current.value=eval(previousValue+operator+current.value)
    previousValue=""
  }
  
}



</script>

<template>

  <h1 class="title">Ma calculatrice avec VueJS</h1>
  <div class="box column is-3-desktop">
    <div class="field">
      <input type="text"   class="input is-success has-text-right" v-model="current">
    </div>
    <ul class="grid">
      <li class="button is-info" v-for="special in specialOperator" @click="action(special)">{{ special }}</li>

      <li class="button"
      :class="{'is-warning':['C','+','/','*','-'].includes(touch)}"
       v-for="touch in TouchArray" @click="action(touch)">{{ touch }} </li>
       <li class="is-success button equal" @click="calc">=</li>
       
    </ul>
  </div>
</template>

<style scoped>
@import "https://cdn.jsdelivr.net/npm/bulma@0.9.4/css/bulma.min.css";

@import url('https://fonts.googleapis.com/css2? family=Montserrat:ital,wght@0,100;0,200;0,400;1,100;1,200&family=Poppins:ital,wght@0,100;0,200;0,300;0,400;0,800;1,400&display=swap');

*{
  font-family:'Poppins';
}
.grid{
  display: grid;
  grid-template-columns:repeat(4,auto);
  gap:3px;
}

.equal{
  grid-column:span 2
}
</style>
