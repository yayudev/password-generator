<script lang="ts">
    import passwordGenerator from 'secure-random-password';

    import CopyPassword from './components/copy-password.svelte';
    import CharacterLength from './components/character-length.svelte';
    import OptionsCheckboxes from './components/options-checkboxes.svelte';
    import PasswordStrength from './components/password-strength.svelte';
    import type {GeneratorOptions} from "./types/generator-options";

    const MIN_LENGTH = 6;
    const MAX_LENGTH = 32;

    let password = ""
    let options: GeneratorOptions = {
        uppercase: true,
        lowercase: true,
        numbers: true,
        symbols: true,
        length: MIN_LENGTH,
    };

    function generatePassword(opts: GeneratorOptions) {
        const characters = [];

        if (opts.uppercase) characters.push(passwordGenerator.upper);
        if (opts.lowercase) characters.push(passwordGenerator.lower);
        if (opts.numbers) characters.push(passwordGenerator.digits);
        if (opts.symbols) characters.push(passwordGenerator.symbols);

        password = passwordGenerator.randomPassword({ characters, length: opts.length });
    }

    // React to changes in options.
    $: {
        // At least one should be checked, otherwise we can't generate it
        if (!options.lowercase && !options.uppercase && !options.numbers && !options.symbols) {
            options.lowercase = true;
        }

        generatePassword(options);
    }
</script>


<div class="container">
    <h1 class="title">Password generator</h1>

    <div class="content-box">
        <CopyPassword password={password} />
    </div>

    <div class="content-box">
        <CharacterLength bind:length={options.length} minLength={MIN_LENGTH} maxLength={MAX_LENGTH} />
        <OptionsCheckboxes bind:options={options} />
        <PasswordStrength password={password} />
    </div>
</div>


<style lang="scss">
    .container {
        margin: 0 auto;
        padding: 1rem;
        width: 95%;
        max-width: 780px;
        text-align: center;
        box-sizing: border-box;
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

    @media screen and (max-width: 480px) {
        .content-box {
          padding: .25rem;
        }

      .title {
        letter-spacing: 2px;
        font-size: 1.5rem;
        margin-bottom: 2rem;
      }
    }
</style>