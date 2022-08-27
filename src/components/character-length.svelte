<script lang="ts">
    import Slider from './slider.svelte';

    export let length: number = 8;
</script>

<section class="length-section">
    <div class="length-info">
        <span class="length-label">Character length</span>
        <span class="length-value">{length}</span>
    </div>

    <Slider bind:value={length} />
</section>

<style>
    .length-section {
        margin-bottom: 3rem;
    }

     .length-info {
         display: flex;
         justify-content: space-between;
         padding: 1rem .5rem;
     }

     .length-label {
         font-size: 2rem;
     }

     .length-value {
         font-size: 3rem;
     }
 </style>