<script lang="ts">
    export let value: number = 4;
</script>


<div class="bars-container" data-value={value}>
    <div class="bar"></div>
    <div class="bar"></div>
    <div class="bar"></div>
    <div class="bar"></div>
</div>


<style lang="scss">
    .bars-container {
      display: grid;
      place-items: end;
      grid-template-columns: repeat(4, 20%);
      height: 50px;
      width: 100px;
      gap: 10%;

      &[data-value="1"] {
        .bar:nth-child(1) {
          background: var(--bars-danger);
        }
      }

      &[data-value="2"] {
        .bar:nth-child(1), .bar:nth-child(2) {
          background: var(--bars-danger);
        }
      }

      &[data-value="3"] {
        .bar:nth-child(1), .bar:nth-child(2), .bar:nth-child(3) {
          background: var(--bars-warn);
        }
      }

      &[data-value="4"] {
        .bar {
          background: var(--bars-safe);
        }
      }
    }

    .bar {
        background: var(--main-text-color);
        height: 100%;
        width: 100%;

        &:nth-child(1) { height: 25%; }
        &:nth-child(2) { height: 50%; }
        &:nth-child(3) { height: 75%; }
    }

    @media screen and (max-width: 480px) {
        .bars-container {
          width: 50px;
          height: 30px;
        }
    }
</style>