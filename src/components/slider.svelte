<script lang="ts">
    import {handle} from '../lib/slider';

    export let value: number = 0;
    export let min: number = 0;
    export let max: number = 100;
    let sliderBox;

    $: percentage = ((value-min)/(max-min)) * 100;

    function onClick({offsetX}) {
        if (!sliderBox) return;

        const {offsetWidth} = sliderBox;

        const percentage = offsetX / offsetWidth;
        const position = percentage * (max - min);
        const approxPosition = Math.max(1, position);
        const nextPosition = Math.ceil(approxPosition) + min;

        console.log({ approxPosition, nextPosition, value })

        if (nextPosition !== value) {
            value = nextPosition;
        }

        // Skip to prev/next possible value always, even if the diff is small.

        if (value > approxPosition) {
            value = Math.max(1, value - 1);
        }

        if (value < approxPosition) {
            value = Math.min(value + 1, max);
        }
    }

    function onDrag(event) {
        const {detail} = event;
        const position = detail * (max - min);

        value = Math.ceil(Math.max(min, position + min));
    }
</script>


<input type="range" min={min} max={max} bind:value={value} hidden />
<div class="slider-box" bind:this={sliderBox} on:click={onClick}>
    <div class="slider-progress" style:width="{percentage}%" ></div>
    <div class="slider-button"
         style:left="calc({percentage}% - 24px)"
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
        height: 16px;
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
        height: 48px;
        width: 48px;
        border-radius: 50%;
        border: 1px solid var(--inactive-color-3);
        position: absolute;
        top: -16px; /* 16px up + 16px bar + 16px down*/
        right: 0;
        cursor: grab;

        &:active {
            cursor: grabbing;
        }
    }

    @media screen and (max-width: 480px) {
        .slider-box {
          height: 12px;
          width: 75%;
        }

      .slider-button {
        height: 36px;
        width: 36px;
        top: -12px; /* 12px up + 12px bar + 12px down*/
      }
    }
</style>