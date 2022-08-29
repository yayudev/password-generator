<script lang="ts">
    import type {GeneratorOptions} from "../types/generator-options";
    import Checkbox from './checkbox.svelte';

    export let options: GeneratorOptions;
</script>

<section class="options">
    <Checkbox bind:checked={options.lowercase} label="Include lowercase letters" />
    <Checkbox bind:checked={options.uppercase} label="Include uppercase letters" />
    <Checkbox bind:checked={options.numbers} label="Include number" />
    <Checkbox bind:checked={options.symbols} label="Include special characters" />
</section>

<style>
    .options {
        padding: 0 1.5rem;
        margin: 0 1rem;
    }
</style>