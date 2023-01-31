<template>
    <div>
        <button @click="openForm()" class="active:scale-95 active:shadow-xl shadow-white block mx-auto bg-violet-700 rounded-full px-4 py-2 text-2xl" >Add an item</button>
        <dialog class="shadow-md backdrop-blur-lgs shadow-white border-white border-2 text-white bg-violet-800 rounded-xl backdrop:bg-[rgba(0,0,0,0.8)]" ref="modal">
            <form method="dialog" class="space-y-4">
                <button @click="closeForm()" type="button" value="cancel" class="text-xl right-4 top-3 absolute block active:scale-95">X</button>
                <div class="grid gap-y-1">
                    <label class="pointer-events-none" for="name">Item name:</label>
                    <input ref="itemName" autofocus required minlength="3" maxlength="25" class="focus:outline-white px-2 bg-gray-900 rounded-xl" type="text" name="name" id="name">
                </div>
                <div class="grid gap-y-1">
                    <label class="pointer-events-none" for="picture">Choose a profile picture:</label>
                    <input type="file" ref="itemImage"
                        id="picture" name="picture"
                        class="px-2 py-2 bg-gray-900 
                        rounded-xl file:mx-4 
                        file:py-2 file:px-4
                        file:rounded-full 
                        file:text-sm file:border-0
                        file:bg-amber-700 file:text-slate-100 file:font-semibold
                        hover:file:bg-amber-600 file:active:scale-95"
                        accept="image/png, image/jpeg">
                </div>
                <button @click="createItem()" value="confirm" class="mx-auto block px-4 py-2 bg-gray-900 rounded-full active:scale-95">Create</button>
            </form>
        </dialog>
    </div>
</template>

<script setup>
import { ref } from 'vue';

const emit = defineEmits(['create-item']);

const modal = ref(null);
const itemName = ref(null);
const itemImage = ref(null);

function openForm(){
    modal.value.showModal();
    window.document.body.style.overflow = "hidden";
}

function closeForm(){
    modal.value.close();
    itemName.value.value = "";
    itemImage.value.value = null;
    window.document.body.style.overflow = "visible";
}

function createItem(){
    window.document.body.style.overflow = "visible";
    let item = {
        name: itemName.value.value,
        image: URL.createObjectURL(itemImage.value.files[0]),
        tier: null,
    }
    console.log(item);
    emit('create-item', item);
    closeForm();
}

</script>

<style>

</style>