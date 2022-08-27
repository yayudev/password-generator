<script lang="ts">
    import CopyPassword from './components/copy-password.svelte';
    import CharacterLength from './components/character-length.svelte';
    import OptionsCheckboxes from './components/options-checkboxes.svelte';
    import type {GeneratorOptions} from "./types/generator-options";

    let password = ""
    let options: GeneratorOptions = {
        uppercase: true,
        lowercase: true,
        numbers: true,
        symbols: true,
        length: 9,
    };
</script>


<div class="container">
    <h1 class="title">Password generator</h1>

    <div class="content-box">
        <CopyPassword password={password} />
    </div>

    <div class="content-box">
        <CharacterLength bind:length={options.length} />
        <OptionsCheckboxes bind:options={options} />

        {JSON.stringify(options)}
    </div>
</div>


<style lang="scss">
    .container {
        margin: 0 auto;
        padding: 1rem;
        width: 95%;
        max-width: 780px;
        text-align: center;
    }

    .title {
        letter-spacing: 2px;
         margin-bottom: 3rem;
    }

    .content-box {
        background: rgba(255, 255, 255, 0.3);
        border-radius: var(--border-radius);
        margin: 1.5rem 0;
        padding: 1rem;
    }
</style>