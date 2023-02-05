<template>
    <div class="mx-auto max-w-7xl px-4 py-8 text-white">
        <Transition>
            <GarbageBin
                @dragover.prevent
                @dragenter.prevent
                @drop="removeItem($event)"
                v-if="binVisible"
            ></GarbageBin>
        </Transition>
        <div
            class="focus-within::border-0 focus-within::outline-dashed inline-block break-words focus-within:outline-dashed"
        >
            <span
                class="focus: inline-block min-h-[1rem] min-w-[2rem] max-w-[90vw] resize-none break-words border-0 bg-transparent px-1 py-2 text-4xl leading-normal outline-none placeholder:text-white"
                max="35"
                name="Tier Title"
                placeholder="Create your tier list"
                contenteditable
                @keypress="limitHeaderLength($event)"
            >
                Click to edit your tier list name</span
            >
        </div>
        <div class="mt-4 space-y-4">
            <TierComponent
                @dragover.prevent
                @dragenter.prevent
                @drop="dropDragItem($event, 'S')"
                :tier-list="sTierItems"
                class="border-red-700 text-red-700"
                tier-name="S"
            ></TierComponent>
            <TierComponent
                @dragover.prevent
                @dragenter.prevent
                @drop="dropDragItem($event, 'A')"
                :tier-list="aTierItems"
                class="border-sky-400 text-sky-400"
                tier-name="A"
            ></TierComponent>
            <TierComponent
                @dragover.prevent
                @dragenter.prevent
                @drop="dropDragItem($event, 'B')"
                :tier-list="bTierItems"
                class="border-amber-300 text-amber-300"
                tier-name="B"
            ></TierComponent>
            <TierComponent
                @dragover.prevent
                @dragenter.prevent
                @drop="dropDragItem($event, 'C')"
                :tier-list="cTierItems"
                class="border-green-300 text-green-300"
                tier-name="C"
            ></TierComponent>
            <TierComponent
                @dragover.prevent
                @dragenter.prevent
                @drop="dropDragItem($event, 'D')"
                :tier-list="dTierItems"
                class="border-cyan-400 text-cyan-400"
                tier-name="D"
            ></TierComponent>
            <TierComponent
                @dragover.prevent
                @dragenter.prevent
                @drop="dropDragItem($event, 'E')"
                :tier-list="eTierItems"
                class="border-purple-500 text-purple-500"
                tier-name="E"
            ></TierComponent>
            <TierComponent
                @dragover.prevent
                @dragenter.prevent
                @drop="dropDragItem($event, 'F')"
                :tier-list="fTierItems"
                class="border-pink-500 text-pink-500"
                tier-name="F"
            ></TierComponent>
        </div>
        <div class="my-5 flex justify-center gap-2">
            <TierItem
                class="h-14 w-14"
                v-for="item in unsortedItems"
                :tier-item="item"
                :key="item.name"
            ></TierItem>
        </div>
        <ItemForm @create-item="refreshUnsorted"></ItemForm>
    </div>
</template>

<script setup>
    import { ref, computed, onMounted } from "vue";
    import TierComponent from "./components/TierComponent.vue";
    import ItemForm from "./components/TheItemForm.vue";
    import TierItem from "./components/TierItem.vue";
    import GarbageBin from "./components/TheGarbageBin.vue";

    const tierItems = ref([]);
    const binVisible = ref(false);

    function limitHeaderLength(e) {
        if (e.target.innerHTML.length >= e.target.getAttribute("max")) {
            e.preventDefault();
            return false;
        }
    }

    function refreshUnsorted(item) {
        tierItems.value.push(item);
    }

    const unsortedItems = computed(() => {
        return tierItems.value.filter((item) => item.tier === null);
    });
    const sTierItems = computed(() => {
        return tierItems.value.filter((item) => item.tier === "S");
    });
    const aTierItems = computed(() => {
        return tierItems.value.filter((item) => item.tier === "A");
    });
    const bTierItems = computed(() => {
        return tierItems.value.filter((item) => item.tier === "B");
    });
    const cTierItems = computed(() => {
        return tierItems.value.filter((item) => item.tier === "C");
    });
    const dTierItems = computed(() => {
        return tierItems.value.filter((item) => item.tier === "D");
    });
    const eTierItems = computed(() => {
        return tierItems.value.filter((item) => item.tier === "E");
    });
    const fTierItems = computed(() => {
        return tierItems.value.filter((item) => item.tier === "F");
    });

    function dropDragItem(event, tier) {
        const item = tierItems.value.find((elem) => {
            return elem.name === event.dataTransfer.getData("itemName");
        });
        item.tier = tier;
    }

    function removeItem(event) {
        tierItems.value = tierItems.value.filter(
            (elem) => elem.name !== event.dataTransfer.getData("itemName")
        );
    }

    onMounted(() => {
        document.addEventListener("dragstart", (event) => {
            console.log("dragstart");
            if (event.target.getAttribute("draggable")) {
                binVisible.value = true;
            }
        });

        document.addEventListener("dragend", (event) => {
            console.log("dragend");
            binVisible.value = false;
        });
        document.addEventListener("drop", (event) => {
            console.log("dragend");
            binVisible.value = false;
        });
    });
</script>

<style>
    .v-enter-from {
        opacity: 0;
    }

    .v-enter-active {
        transition: opacity 1s cubic-bezier(0.21, 1.07, 0.44, 0.93);
    }

    .v-enter-to {
        opacity: 0.9;
    }

    .v-leave-from {
        opacity: 0.9;
    }

    .v-leave-active {
        transition: opacity 1s cubic-bezier(0.21, 1.07, 0.44, 0.93);
    }

    .v-leave-to {
        opacity: 0;
    }
</style>
