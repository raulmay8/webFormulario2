<script setup lang="ts">
import { ref } from 'vue';
import  ItemsVue from './Items.vue';
import Skills  from "@/data/Skills";
import type { ISkill } from './interface/ISkill';
 const skillInput = ref('');
 const skillReactivo = ref(Skills);
const order = ref('asc')
const Ordernar =()=>{
  if (order.value == "asc") {
    skillReactivo.value.sort((a, b) => a.id - b.id);
  } else {
    skillReactivo.value.sort((a, b) => b.id - a.id);
    console.log(skillReactivo)
  }
}
const save = () =>{
  const nextId = skillReactivo.value.length + 1;
  if(skillInput.value.length == 0){
    return alert('La habilidad no puede estar vacia')
  }
  const findSkills =   skillReactivo.value.find(i =>i.name.toLowerCase() == skillInput.value.toLowerCase());
  if(findSkills != null){
   return alert('Ya existe esta habilidad intente con otra')
  }
  skillReactivo.value.push(
    {
      id:nextId,
      name: skillInput.value
    }
  )
  skillInput.value= ''
  Ordernar()
}
</script>

<template>
  <div class="caja">
    <input class="input" type="text" placeholder="Agrega nueva habilidad" v-model="skillInput"   @keyup.enter="save"/>
    <select placeholder="Ordenar Lista" v-model="order" @change="Ordernar">
      <option value="asc">Ascendente</option>
      <option value="desc">Descendente</option>
    </select>
    <ItemsVue v-bind="skill"  v-for="(skill, index) in skillReactivo" :key="index"/>
  </div>
</template>
