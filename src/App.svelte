<script lang="ts">
  import copyIcon from './assets/icons/copy.svg';
  import Checkbox from './components/checkbox.svelte';

  let password = "P4$5w0rD!"
  let options = {
    uppercase: true,
    lowercase: true,
    numbers: true,
    symbol: true,
  };
</script>


<div class="container">
  <h1 class="title">Password generator</h1>

  <div class="content-box">
    <div class="password">
      <p class="password-text">{password}</p>
      <img class="password-copy-icon" src={copyIcon} alt="Copy password" />
    </div>
  </div>

  <div class="content-box">
<!--    <div>-->
<!--      <span>Character length</span>-->
<!--      <span>9</span>-->
<!--    </div>-->
    <div class="options">
      <Checkbox bind:checked={options.uppercase} label="Include uppercase letters" />
      <Checkbox bind:checked={options.lowercase} label="Include lowercase letters" />
      <Checkbox bind:checked={options.numbers} label="Include number" />
      <Checkbox bind:checked={options.symbol} label="Include special characters" />
    </div>

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
  }

  .content-box {
    background: rgba(255, 255, 255, 0.3);
    border-radius: var(--border-radius);
    margin: 1.5rem 0;
    padding: 1rem;
  }

  .options {
    margin: 0 1rem;
  }

  .password {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 0.5rem 1rem;
    cursor: pointer;

    .password-copy-icon {
      filter: opacity(50%);
    }

    &:hover .password-copy-icon {
      filter: opacity(100%);
    }
  }

  .password-text {
    font-size: 2rem;
    margin: 0;
  }
</style>