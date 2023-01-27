<template>
    <div>
        <button @click="openModal()" class="active:scale-95 active:shadow-xl shadow-white block mx-auto bg-violet-700 rounded-full px-4 py-2 text-2xl mt-10" >Add an item</button>
        <dialog class="border-white border-2 text-white bg-violet-800 rounded-xl backdrop:bg-[rgba(0,0,0,0.8)]" ref="modal">
            <form class="space-y-4" method="dialog">
                <div class="grid gap-y-1">
                    <label for="name">Item name:</label>
                    <input minlength="3" maxlength="25" class="focus:outline-white px-2 bg-gray-900 rounded-xl" type="text" name="name" id="name">
                </div>
                <div class="grid gap-y-1">
                    <label for="picture">Choose a profile picture:</label>
                    <input type="file"
                        id="picture" name="picture"
                        class="px-2 py-2 bg-gray-900 "
                        accept="image/png, image/jpeg">
                </div>
                <button class="block px-4 py-2 bg-gray-900 rounded-full mx-auto active:scale-95">Create</button>
            </form>
        </dialog>
    </div>
</template>

<script setup>
import { ref } from 'vue';

const modal = ref(null);

function openModal(){
    modal.value.showModal();
}

</script>

<style>

</style>