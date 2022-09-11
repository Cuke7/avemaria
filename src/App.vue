<template>
    <div data-theme="forest" class="flex-col flex h-screen">
        <div class="flex justify-center items-center p-4 font-mono font-bold text-xl mx-8 text-justify rounded-lg">Neuvaine à Marie qui défait les noeuds</div>
        <div style="overflow: scroll" class="flex-1 flex">
            <div class="flex pl-6">
                <ul class="steps steps-vertical">
                    <li v-for="(step, index) in Object.keys(prayer).length" :key="index" :class="index <= stepIndex ? 'step step-primary' : 'step'"></li>
                </ul>
            </div>
            <div class="p-4 pr-6 flex justify-between flex-col">
                <div v-if="step.length != 1" class="w-full flex justify-between mb-4">
                    <div v-for="index in 9" :key="index">
                        <button v-if="day == index - 1" class="px-2 rounded-lg bg-primary">{{ index }}</button>
                        <button @click="click(index)" v-else class="px-2 rounded-lg">{{ index }}</button>
                    </div>
                </div>
                <div style="overflow: scroll">
                    <div v-if="step.length == 1">
                        <div class="text-primary font-bold text-xl mb-8">{{ step[0].title }}</div>
                        <div class="text-white" style="white-space: pre-line">{{ step[0].text }}</div>
                    </div>
                    <div v-else>
                        <div class="text-primary font-bold text-xl mb-8">{{ step[day].title }}</div>
                        <div class="text-white" style="white-space: pre-line">{{ step[day].text }}</div>
                    </div>
                </div>
                <div class="flex justify-around mt-4">
                    <button :disabled="stepIndex == 0" @click="changeStep(false)" class="bg-accent p-2 rounded-lg px-4 font-bold disabled:opacity-50">Précedent</button>
                    <button :disabled="stepIndex == Object.keys(prayer).length - 1" @click="changeStep(true)" class="bg-accent p-2 rounded-lg px-4 font-bold disabled:opacity-50">Suivant</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup lang="ts">
import data from "./assets/text.js";
import { ref, computed } from "vue";

const prayer = data;
const stepIndex = ref(0);
const day = ref(0);
const step = computed(() => {
    return prayer[stepIndex.value];
});

function click(index) {
    day.value = index - 1;
}

function changeStep(next) {
    if (next) {
        stepIndex.value++;
    } else {
        stepIndex.value--;
    }
}
</script>
