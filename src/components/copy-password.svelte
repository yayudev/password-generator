<script lang="ts">
    import copyIcon from '../assets/icons/copy.svg';

    export let placeholder: string = "P4$5w0rD!";
    export let password: string;

    function copyToClipboard() {
        if (!password) return;

        navigator.clipboard.writeText(password);
    }
</script>


<div class="copy-password" on:click={copyToClipboard}>
    {#if password}
        <p class="copy-password-text">{password}</p>
    {:else}
        <p class="copy-password-text placeholder">{placeholder}</p>
    {/if}

    <img class="copy-password-icon" src={copyIcon} alt="Copy password" />
</div>


<style lang="scss">
    .copy-password {
        display: flex;
        justify-content: space-between;
        align-items: center;
        padding: 0.5rem 1rem;
        cursor: pointer;

        & .copy-password-icon {
            filter: opacity(50%);
            transition: filter 150ms ease-in-out;
        }

        &:hover .copy-password-icon {
             filter: opacity(100%)
        }
    }

    .copy-password-text {
        font-size: 2rem;
        margin: 0 1rem 0 0;
        max-width: 100%;
        line-height: 1.5;
        overflow: hidden;
        white-space: nowrap;
        text-overflow: ellipsis;

        &.placeholder {
          color: var(--inactive-color);
        }
    }
</style>