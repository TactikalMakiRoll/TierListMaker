<template>
    <div>
        <button
            @click="openForm()"
            class="mx-auto block rounded-full bg-violet-700 px-4 py-2 text-2xl shadow-white active:scale-95 active:shadow-xl"
        >
            Add an item
        </button>
        <dialog
            class="backdrop-blur-lgs rounded-xl border-2 border-white bg-violet-800 text-white shadow-md shadow-white backdrop:bg-[rgba(0,0,0,0.8)]"
            ref="modal"
        >
            <form method="dialog" class="space-y-4">
                <button
                    @click="closeForm()"
                    type="button"
                    value="cancel"
                    class="absolute right-4 top-3 block text-xl active:scale-95"
                >
                    X
                </button>
                <div class="grid gap-y-1">
                    <label class="pointer-events-none" for="name"
                        >Item name:</label
                    >
                    <input
                        ref="itemName"
                        autofocus
                        required
                        minlength="3"
                        maxlength="25"
                        class="rounded-xl bg-gray-900 px-2 focus:outline-white"
                        type="text"
                        name="name"
                        id="name"
                    />
                </div>
                <div class="grid gap-y-1">
                    <label class="pointer-events-none" for="picture"
                        >Choose a profile picture:</label
                    >
                    <input
                        required
                        type="file"
                        ref="itemImage"
                        id="picture"
                        name="picture"
                        class="rounded-xl bg-gray-900 px-2 py-2 file:mx-4 file:rounded-full file:border-0 file:bg-amber-700 file:py-2 file:px-4 file:text-sm file:font-semibold file:text-slate-100 hover:file:bg-amber-600 file:active:scale-95"
                        accept="image/png, image/jpeg"
                    />
                </div>
                <button
                    @click="createItem()"
                    value="confirm"
                    class="mx-auto block rounded-full bg-gray-900 px-4 py-2 active:scale-95"
                >
                    Create
                </button>
            </form>
        </dialog>
    </div>
</template>

<script setup>
    import { ref } from "vue";

    const emit = defineEmits(["create-item"]);

    const modal = ref(null);
    const itemName = ref(null);
    const itemImage = ref(null);

    function openForm() {
        modal.value.showModal();
        window.document.body.style.overflow = "hidden";
    }

    function closeForm() {
        modal.value.close();
        itemName.value.value = "";
        itemImage.value.value = null;
        window.document.body.style.overflow = "visible";
    }

    function createItem() {
        window.document.body.style.overflow = "visible";
        let item = {
            name: itemName.value.value,
            image: URL.createObjectURL(itemImage.value.files[0]),
            tier: null,
        };
        console.log(item);
        emit("create-item", item);
        closeForm();
    }
</script>

<style></style>
