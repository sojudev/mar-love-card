<script setup lang="ts">
import { useMouse, useWindowSize } from "@vueuse/core";
import { ref } from "vue";

const count = ref(0);
const { x, y } = useMouse({ touch: false });
const { width, height } = useWindowSize();
const memeFlag = ref(false);

const randomizePositions = () => {
    count.value++;
    const yes = document.getElementById("yes-btn");
    const no = document.getElementById("no-btn");

    // move yes button to cursor
    yes?.style.setProperty("left", `${x.value}px`, "important");
    yes?.style.setProperty("top", `${y.value}px`, "important");

    // move no button to random position on window
    const xRand = Math.round(Math.random() * width.value);
    const yRand = Math.round(Math.random() * height.value);
    no?.style.setProperty("left", `${xRand}px`, "important");
    no?.style.setProperty("top", `${yRand}px`, "important");
};

const showBowHamster = () => {
    if (!memeFlag.value) {
        memeFlag.value = true;
    }
};
</script>

<template>
    <h1>Mariam Wael Singer, do you love me?</h1>
    <div id="card" class="card">
        <div v-if="!memeFlag" class="btn-container">
            <button
                id="yes-btn"
                :class="[!count ? 'card-btn' : 'card-btn-reset']"
                type="button"
                @click="showBowHamster()"
            >
                Yes
            </button>
            <button
                id="no-btn"
                :class="[!count ? 'card-btn' : 'card-btn-reset']"
                type="button"
                @click="randomizePositions()"
            >
                No
            </button>
        </div>
        <div v-else>
            <img
                src="https://ih1.redbubble.net/image.5457619282.3746/flat,750x,075,f-pad,750x1000,f8f8f8.u1.jpg"
            />
        </div>
    </div>
</template>

<style scoped>
.card-btn {
    position: relative;
    margin: 10px;
}

.card-btn-reset {
    position: absolute;
    top: 0;
    left: 0;
}
</style>
