<script>
  import Spinner from './lib/Spinner.svelte';

  const jokeUrl = `https://icanhazdadjoke.com/`;
  const config = {
    headers: { Accept: 'application/json' },
  };

  let clicks = $state(0);

  async function fetchJoke() {
    clicks;
    try {
      const res = await fetch(jokeUrl, config);
      const data = await res.json();
      return data.joke;
    } catch (err) {
      throw new Error(err.message);
    }
  }
</script>

<div class="container">
  <h3>Don't Laugh Challenge</h3>
  {#if !clicks}{:else}
    {#await fetchJoke()}
      <Spinner />
    {:then joke}
      <div class="joke" id="joke">{joke}</div>
    {/await}
  {/if}
  <button class="btn" id="jokeBtn" onclick={() => (clicks += 1)}
    >Get Another Joke</button>
</div>

<style lang="scss">
  .container {
    background-color: white;
    border-radius: 10px;
    box-shadow:
      0 10px 20px rgba(0, 0, 0, 0.1),
      0 6px 6px rgba(0, 0, 0, 0.1);
    padding: 50px 20px;
    text-align: center;
    max-width: 100%;
    width: 800px;
  }

  h3 {
    margin: 0;
    opacity: 0.5;
    letter-spacing: 2px;
  }
  .joke {
    font-size: 30px;
    letter-spacing: 1px;
    line-height: 40px;
    margin: 50px auto;
    max-width: 600px;
  }

  .btn {
    display: block;
    margin: 2rem auto;
    background-color: #9f68e0;
    border: 0;
    border-radius: 10px;
    box-shadow:
      0 5px 15px rgba(0, 0, 0, 0.1),
      0 6px 6px rgba(0, 0, 0, 0.1);
    padding: 14px 40px;
    font-size: 16px;
    cursor: pointer;
  }
  .btn:active {
    transform: scale(0.98);
  }
  .btn:focus {
    outline: 0;
  }
</style>
