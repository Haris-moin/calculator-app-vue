<template>
  <div id="app" class="calculator">
   
      <input v-if="isLoading" class="result-container" placeholder="loading....." type="text" />
      <input v-else class="result-container" placeholder="0" type="text" v-model="currentValue" />
   <div class="calculator-buttons">
      <div class="number-buttons">
      <div v-for="(text , index) of numberButtons" :key="index" class="numbers">
        <button v-on:click="onclick(text)" class="numbers">{{text}}</button>
      </div>
    </div>
    <div class="operator-buttons">
      <div v-for="(text , index) of operatorButtons" :key="index" class="numbers">
        <button v-on:click="onclick(text)" class="operators">{{text}}</button>
      </div>
    </div>
   </div>
  </div>
</template>

<script>

export default {
  name: 'App',
  updated : function(){
    if(this.isLoading){
setTimeout(()=>{ this.isLoading=false }, 2000);
    }
    
  },
  data() {
    return {
      isLoading:false,
      currentValue:'',
      prevValue:'',
      opertor:'',
      numberButtons:['c','/','*','1','2','3','4','5','6','7','8','9','0','00','.'],
      operatorButtons:['-','+','%','=']
      }
  },
  methods:{
    onclick(value){
      if(!isNaN(value)|| value==='.'){
        this.currentValue +=value+'';
      }
     else if(value==='%'){
        this.currentValue = this.currentValue / 100 + '';
      }
      else if(value==='c'){
        this.currentValue=""
      }
      else if(['/','*','+','-'].includes(value)){
        this.opertor= value;
        this.prevValue= this.currentValue;
        this.currentValue=''
      }
      else if(value=== '='){
        this.currentValue = eval(
          this.prevValue + this.opertor + this.currentValue
          
        )
        this.isLoading=true
      }
    }
  }
}
</script>

<style>

.calculator {
  max-width: 400px;
  margin: 40px auto;
  background: #2c3e50;
  border-radius: 10px ;
  padding: 5px;
}
.calculator-buttons{
  display: flex;
}
.result-container {
  font-weight: bold;
  color:black;
  width: 90%;
  font-size: 32px;
  padding: 10px;
  background:rgb(255, 255, 255);
  border-radius: 10px ;
  margin: 5px 10px;
 
}
.number-buttons {
  width: 100%;
  display: flex;
  justify-content: space-around;
  flex-wrap: wrap;
}
button {
  width:80px;
  height: 70px;
  border: none;
  margin: 5px;
  font-size: 25px;
  border-radius: 5px;
  background: rgb(171, 182, 190);
}
.numbers:hover, .operators:hover{
  background: rgb(50, 161, 252);
  border-radius: 10px;
}
</style>
