<template>
    <div
        class="flex items-center rounded-xl border-4 border-solid py-2 xl:py-4"
    >
        <span
            class="inline-block border-r-4 border-solid border-r-inherit px-4 text-3xl text-inherit xl:px-6 xl:text-4xl"
            >{{ tierName }}</span
        >
        <div class="ml-4 inline-flex flex-wrap gap-2">
            <div v-for="item in tierList" :key="item.name">
                <TierItem :tier-item="item"></TierItem>
            </div>
        </div>
    </div>
</template>

<script setup>
    import { ref } from "vue";
    import TierItem from "./TierItem.vue";

    const props = defineProps({
        tierList: Array,
        tierName: String,
    });
</script>

<style></style>
