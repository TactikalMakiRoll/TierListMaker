<template>
    <div class="w-14 h-14 bg-cover bg-center" draggable="true" @dragstart="startDragItem($event, tierItem)" :style="{
          backgroundImage: 'url(' + tierItem.image + ')'
        }" @dragend="endDragItem">
    </div>
</template>

<script setup>
const emit = defineEmits(['dragStarted','dragEnded']);
const props = defineProps({
  tierItem: Object,
})

function startDragItem(event, item){
  event.dataTransfer.dropEffect = 'move';
  event.dataTransfer.effectAllowed = 'move';
  event.dataTransfer.setData('itemName', item.name);
  emit("dragStarted");
}

function endDragItem(){
  emit("dragEnded");
}

</script>

<style>

</style>