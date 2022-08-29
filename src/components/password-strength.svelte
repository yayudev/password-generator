<script lang="ts">
    import { passwordStrength } from 'check-password-strength';
    import StrengthBars from './strength-bars.svelte';

    const STRENGTH_VALUES = {
        "Too weak": 1,
        "Weak": 2,
        "Medium": 3,
        "Strong": 4,
    }

    export let password: string = "";

    $: strength = passwordStrength(password);
    $: value = STRENGTH_VALUES[strength.value];
</script>

<div class="strength-container">
    <p class="strength-label">Strength</p>
    <StrengthBars value={value} />
</div>

<style>
    .strength-container {
        background: var(--inactive-color);
        margin: 2rem 2rem 1rem 2rem;
        padding: .5rem 2rem;
        border-radius: 2px;
        display: flex;
        justify-content: space-between;
        align-items: center;
        font-size: 1.5rem;
    }
</style>
