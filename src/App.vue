<script setup>
import {ref, computed} from 'vue'
  const name = "Carlos";
  //
  let counter = ref(0);
  const arrayFavoritos = ref([])
  //
  
  //metodo para incrementar
  const increment = () =>{
    console.log('aumentar contador')
    counter.value++
  }

  const decrement = () =>{
    console.log('disminuir contador')
    counter.value--
  }
  const reset = () =>{
    console.log('reseteo a 0')
    counter.value = 0;
  }
  const classCounter  = computed(() =>{
    if(counter.value === 0){
      return 'zero'
    }
    if(counter.value > 0){
      return 'positive'
    }
    if(counter.value < 0){
      return 'negative'
    }
  })
  
  const add = () =>{
    arrayFavoritos.value.push(counter.value)
  }

  const bloquearBtnAdd = computed(() => {
    const numSearch = arrayFavoritos.value.find(num => num === counter.value)
    console.log(numSearch)
    if(numSearch === 0) return true
    return numSearch ? true : false;
  })
</script>

<template>
  <div class="container text-center mt-2">
    <h1>Bienvenido {{ name }}</h1>
    <h2 :class="classCounter"> {{ counter }}</h2>
    <div class="btn-group">
      <button  @click="increment" class="btn btn-success">Aumentar</button>
    <button  @click="decrement" class="btn btn-danger">Disminuir</button>
    <button  @click="reset" class="btn btn-secondary">Reset</button>
    <button  @click="add" :disabled="bloquearBtnAdd" class="btn btn-primary">Add</button>
    </div>
    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="(num,index) in arrayFavoritos" :key="index">
        {{ num }}
      </li>
    </ul>
  </div>
</template>

<style>
  h1{
    color: rgb(64, 19, 107);
  }

  .positive{
    color:green
  }
  .negative {
    color: red;
  }
  .zero{
    color: peru;
  }
</style>