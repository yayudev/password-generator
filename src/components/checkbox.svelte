<script lang="ts">
    export let checked: boolean = false;
    export let label: string = "";

    $: checkboxId = `checkbox-${label}`;

    function toggleCheckbox() {
        checked = !checked;
    }
</script>


    <div class="checkbox-row">
        <div role="checkbox" class="checkbox-outside" on:click={toggleCheckbox}>
            <div class="checkbox-fill" class:active={checked}></div>
        </div>

        <label for={checkboxId} class="checkbox-label">{label}</label>

        <input
            type="checkbox"
            id={checkboxId}
            bind:checked={checked}
            hidden
        />
    </div>

<style lang="scss">
    .checkbox-row {
      display: flex;
      font-size: 1.2rem;
      margin: 1.5rem 0;
      align-items: center;
      width: 100%;
    }

    .checkbox-label {
      margin-left: 1.25rem;
    }

    .checkbox-outside {
      cursor: pointer;
      user-select: none;
      height: 30px;
      width: 30px;
      display: flex;
      place-items: center;
      background: var(--inactive-color);
      border-radius: var(--border-radius);
    }

    .checkbox-fill {
      background: #91CBF1;
      height: 24px;
      width: 24px;
      margin: 3px;
      border-radius: 2px;

      &.active {
        background: var(--main-text-color);
      }
    }
</style>