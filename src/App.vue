<template>
  <div class="text-white px-4 py-8">
    <div class="inline-block focus-within::border-0 focus-within::outline-dashed 
    focus-within:outline-dashed break-words">
      <span class="inline-block break-words px-1 py-2 border-0 bg-transparent 
      focus: text-4xl outline-none placeholder:text-white resize-none
      min-h-[1rem] leading-normal max-w-[90vw]" max=35 name="Tier Title" 
      placeholder="Create your tier list" contenteditable
      @keypress="limitHeaderLength($event)" @keyup="fillEmptyHeader($event)">
      Create your tier list</span>
    </div>
    <div class="mt-4 space-y-4">
      <div class="py-5 border-solid border-4 rounded-full border-red-700">
        <span class="px-4 border-solid border-r-red-700 border-r-4 text-3xl text-red-700">S</span>
      </div>
      <div class="py-5 border-solid border-4 rounded-full border-sky-400">
        <span class="px-4 border-solid border-r-sky-400 border-r-4 text-3xl text-sky-400 ">A</span>
      </div>
      <div class="py-5 border-solid border-4 rounded-full border-amber-300">
        <span class="px-4 border-solid border-r-amber-300 border-r-4 text-3xl text-amber-300">B</span>
      </div>
      <div class="py-5 border-solid border-4 rounded-full border-green-300">
        <span class="px-4 border-solid border-r-green-300 border-r-4 text-3xl text-green-300">C</span>
      </div>
      <div class="py-5 border-solid border-4 rounded-full border-sky-400">
        <span class="px-4 border-solid border-r-sky-400 border-r-4 text-3xl text-sky-400">D</span>
      </div>
      <div class="py-5 border-solid border-4 rounded-full border-purple-500">
        <span class="px-4 border-solid border-r-purple-500 border-r-4 text-3xl text-purple-500">E</span>
      </div>
      <div class="py-5 border-solid border-4 rounded-full border-pink-500">
        <span class="px-4 border-solid border-r-pink-500 border-r-4 text-3xl text-pink-500">F</span>
      </div>
    </div>
    <ItemForm ref="itemModal"></ItemForm>
  </div>
</template>

<script setup>
import {ref} from 'vue';
import TierComponent from './components/TierComponent.vue'
import ItemForm from './components/ItemForm.vue';

const itemModal = ref(null);

function openModal(){
  console.log("fjsdklafj");
  itemModal.value.openModal();
}

function limitHeaderLength(e){
  if(e.target.innerHTML.length >= e.target.getAttribute("max")){
    e.preventDefault();
    return false;
  }
}
function fillEmptyHeader(e){
  if(e.target.textContent.length===0){
    e.target.textContent = "Input title";
  }
}
</script>


<style>

</style>
