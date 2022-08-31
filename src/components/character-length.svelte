<script lang="ts">
    import Slider from './slider.svelte';

    export let length: number = 8;
    export let minLength: number = 6;
    export let maxLength: number = 100;
</script>

<section class="length-section">
    <div class="length-info">
        <span class="length-label">Character length</span>
        <span class="length-value">{length}</span>
    </div>

    <Slider bind:value={length} min={minLength} max={maxLength} />
</section>

<style>
    .length-section {
        margin-bottom: 3rem;
    }

     .length-info {
         display: flex;
         justify-content: space-between;
         align-items: center;
         padding: 1rem .5rem;
     }

     .length-label {
         font-size: 2rem;
     }

     .length-value {
         font-size: 3rem;
     }

     @media screen and (max-width: 480px) {
         .length-section {
             margin-bottom: 2rem;
         }

         .length-info {
             padding-bottom: 0;
         }

         .length-label {
             font-size: 1.25rem;
             margin: .5em;
             text-align: start;
         }

         .length-value {
             font-size: 2rem;
         }
     }
 </style>