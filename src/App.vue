<template>
  <div class="text-white px-4 py-8">
    <div class="inline-block focus-within::border-0 focus-within::outline-dashed 
    focus-within:outline-dashed break-words">
      <span class="inline-block break-words px-1 py-2 border-0 bg-transparent 
      focus: text-4xl outline-none placeholder:text-white resize-none
      min-h-[1rem] min-w-[2rem] leading-normal max-w-[90vw]" max=35 name="Tier Title" 
      placeholder="Create your tier list" contenteditable
      @keypress="limitHeaderLength($event)">
      Click to edit your tier list name</span>
    </div>
    <div class="mt-4 space-y-4">
      <div class="flex items-center py-2 border-solid border-4 rounded-full border-red-700">
        <span class="px-4 border-solid border-r-red-700 border-r-4 text-3xl text-red-700">S</span>

        <div @dragover.prevent
             @dragenter.prevent 
             @drop="dropDragItem($event, 'S')" class="ml-4 w-full h-14 inline-flex gap-2">
          <div class="w-14 h-14" v-for="item in listTierS" :key="item.name" draggable @dragstart="startDragItem($event, item)">
          <img class="w-full h-full object-fill" :src="item.image" :alt="item.name">
          </div>
        </div>
      
      </div>
      <div class="flex items-center py-5 border-solid border-4 rounded-full border-sky-400">
        <span class="px-4 border-solid border-r-sky-400 border-r-4 text-3xl text-sky-400 ">A</span>
      </div>
      <div class="flex items-center py-5 border-solid border-4 rounded-full border-amber-300">
        <span class="px-4 border-solid border-r-amber-300 border-r-4 text-3xl text-amber-300">B</span>
      </div>
      <div class="flex items-center py-5 border-solid border-4 rounded-full border-green-300">
        <span class="px-4 border-solid border-r-green-300 border-r-4 text-3xl text-green-300">C</span>
      </div>
      <div class="flex items-center py-5 border-solid border-4 rounded-full border-sky-400">
        <span class="px-4 border-solid border-r-sky-400 border-r-4 text-3xl text-sky-400">D</span>
      </div>
      <div class="flex items-center py-5 border-solid border-4 rounded-full border-purple-500">
        <span class="px-4 border-solid border-r-purple-500 border-r-4 text-3xl text-purple-500">E</span>
      </div>
      <div class="flex items-center py-5 border-solid border-4 rounded-full border-pink-500">
        <span class="px-4 border-solid border-r-pink-500 border-r-4 text-3xl text-pink-500">F</span>
      </div>
    </div>
    <div class="my-5 flex justify-center gap-2">
      <div class="w-14 h-14" v-for="item in tierItems" :key="item.name" draggable @dragstart="startDragItem($event, item)">
        <img class="w-full h-full object-fill" :src="item.image" :alt="item.name">
      </div>
    </div>
    <ItemForm class="" @create-item="refreshUnsorted"></ItemForm>
  </div>
</template>

<script setup>
import {ref, computed} from 'vue';
import TierComponent from './components/TierComponent.vue'
import ItemForm from './components/TheItemForm.vue';

const tierItems = ref([]);

function limitHeaderLength(e){
  if(e.target.innerHTML.length >= e.target.getAttribute("max")){
    e.preventDefault();
    return false;
  }
}

function refreshUnsorted(item){
  console.log(item);
  tierItems.value.push(item);
  console.log(tierItems.value);
}

function startDragItem(event, item){
  event.dataTransfer.dropEffect = 'move';
  event.dataTransfer.effectAllowed = 'move';
  event.dataTransfer.setData('itemName', item.name);
}

function dropDragItem(event, tier){
  const itemName = event.dataTransfer.getData('itemName');
  const item = tierItems.value.find((item) => item.name === itemName);
  item.tier = tier;
  console.log(item);
}

const listTierS = computed(() => {
  return tierItems.value.filter((item)=> item.tier==='S');
})

</script>


<style>

</style>
