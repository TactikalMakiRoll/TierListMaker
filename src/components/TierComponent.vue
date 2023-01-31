<template>
    <div class="flex items-center py-2 border-solid border-4 rounded-xl">
        <span class="inline-block px-4 border-solid border-r-inherit border-r-4 text-3xl text-inherit">{{tierName}}</span>
        <div class="ml-4 inline-flex gap-2 flex-wrap">
            <div v-for="item in tierList" :key="item.name">
                <TierItem :tier-item="item"></TierItem>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref } from 'vue';
import TierItem from './TierItem.vue';

const props = defineProps({
    tierList: Array,
    tierName: String,
});

</script>


<style>
</style>
