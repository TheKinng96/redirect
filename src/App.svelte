<script>
  import { onMount } from 'svelte';

  let defaultUrl = "http://localhost:8080";
  let redirectUrl = defaultUrl;

  onMount(() => {
    const params = new URLSearchParams(window.location.search);
    if (params.toString()) {
      redirectUrl = `${defaultUrl}?${params.toString()}`;
    }
  });


  const copyToClipboard = () => {
    navigator.clipboard.writeText(redirectUrl).then(() => {
      alert("URL copied to clipboard!");
    });
  };

  const goToUrl = () => {
		window.open(redirectUrl, '_blank');
  };
</script>

<main>
  <h1>Redirection Hub</h1>
  <input type="text" bind:value={redirectUrl} />

	<div>
		<button on:click={copyToClipboard}>Copy URL</button>
		<button on:click={goToUrl}>Go To URL</button>
	</div>
</main>

<style>
  main {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: start;
    height: 100vh;
		margin-top: 4rem;
    font-family: Arial, sans-serif;
  }

  input {
    width: 80%;
    padding: 10px;
    margin: 10px 0;
    font-size: 1.2rem;
  }

	div {
		display: flex;
		gap: 2rem;
	}

  div > button {
    padding: 10px 20px;
    margin: 5px;
    font-size: 1rem;
    cursor: pointer;
  }
</style>
