<script setup>
  import {ref,  computed } from "vue"
  // const name = 'Vue';
  // const users = [
  //   {
  //     nombre:'Julian',
  //     edad:23,
  //     ciudad:'Zipaquira'
  //   },
  //   {
  //     nombre:'Andres',
  //     edad:23,
  //     ciudad:'Bogota'
  //   },
  //   {
  //     nombre:'Juan',
  //     edad:26,
  //     ciudad:'Mosquera'
  //   }];
  const counter = ref(0);

  const incrementar =()=>{
    counter.value++;
  }
  const disminuir =()=>{
    counter.value--;
  }
  const reiniciar =()=>{
    counter.value = 0;
  }
  const computeds = computed(()=>{
    if(counter.value > 0){
      return "positivo";
    }else if(counter.value < 0){
      return "negativo";
    }else{
      return "zero";
    }
  })
 
</script>

<template>
  <ul v-for="user in users" v-bind:key="user">
    <li v-if="user.edad>23">Nombre: {{user.nombre}}</li>
    <li v-if="user.edad>23">Mas info 
    <ul>
      <li>Edad: {{user.edad}}</li>
      <li>Ciudad: {{user.ciudad}}</li>
    </ul>
  </li>
  </ul>
  <span :class="computeds">{{counter}}</span>
  <button @click='incrementar' type="button">Aumentar</button> <br>
  <button @click='disminuir' type="button">Disminuir</button> <br>
  <button @click='reiniciar' type="button">Reiniciar</button>

</template>

<style>  
  h1{
    color: brown;
  }
  .negativo{
    color: red;
  }
  .positivo{
    color: blue;
  }
  .zero{
    color: black;
  }
</style>