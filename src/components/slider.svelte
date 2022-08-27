<script lang="ts">
    import {handle} from '../lib/slider';

    export let value: number = 0;

    const STEPS = 24;
    let sliderBox;

    $: percentage = ((value-1)/(STEPS-1)) * 100;

    function onClick({offsetX}) {
        if (!sliderBox) return;

        const {offsetWidth} = sliderBox;

        const percentage = offsetX / offsetWidth;
        const position = percentage * STEPS;
        const approxPosition = Math.max(1, position);
        const nextPosition = Math.ceil(approxPosition);

        console.log({ approxPosition, nextPosition, value })

        if (nextPosition !== value) {
            value = nextPosition;
        }

        // Skip to prev/next possible value always, even if the diff is small.

        if (value > approxPosition) {
            value = Math.max(1, value - 1);
        }

        if (value < approxPosition) {
            value = Math.min(value + 1, STEPS);
        }
    }

    function onDrag(event) {
        const {detail} = event;
        const position = (detail / 1) * STEPS;

        value = Math.ceil(Math.max(1, position));
    }
</script>


<input type="range" min="1" max={STEPS} bind:value={value} hidden />
<div class="slider-box" bind:this={sliderBox} on:click={onClick}>
    <div class="slider-progress" style:width="{percentage}%" ></div>
    <div class="slider-button"
         style:left="calc({percentage}% - {STEPS}px)"
         use:handle
         on:click|stopPropagation
         on:drag={onDrag}
    ></div>
</div>


<style lang="scss">
    .slider-box {
        position: relative;
        background-color: var(--inactive-color);
        border-radius: 2px;
        height: 15px;
        width: 90%;
        margin: 1.5rem auto;
        cursor: pointer;

        &:has(.slider-button:active) {
            cursor: grabbing;
        }
    }

    .slider-progress {
        background-color: var(--inactive-color-2);
        border-radius: var(--border-radius);
        height: 100%;
    }

    .slider-button {
        background: var(--main-text-color);
        height: 45px;
        width: 45px;
        border-radius: 50%;
        border: 1px solid var(--inactive-color-3);
        position: absolute;
        top: -15px; /* 15px up + 15px bar + 15px down*/
        right: 0;
        cursor: grab;

        &:active {
            cursor: grabbing;
        }
    }
</style>