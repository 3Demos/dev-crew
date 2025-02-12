<script>
	let name;
	let src = 'https://pngimg.com/uploads/cookie/cookie_PNG13656.png';
	let count = 0;

	function increment() {
		if (count >= 49) {
			count = 0; // Reset to 0 when it hits 100
		} else {
			count += 1;
		}
	}
</script>

<main>
	<h1>Welcome to the Cookie Clicker 2.0</h1>
	<p class="gold-text">Cookies: {count}</p>
	<!-- Displays counter -->
</main>

<div class="buttonholder">
	<button onclick={increment}>
		<img {src} alt="Cookie" class="cookie-img" />
	</button>
</div>

{#if count == 49}
	<p class="if1">You're done.</p>
{:else if count > 29}
	<p class="if1">Come on now...</p>
{:else if count > 19}
	<p class="if1">Ok, there's no way you have this many friends!</p>
{:else if count > 9}
	<p class="if1">I hope you have friends if you want {count} cookies</p>
{/if}

<style>
	.gold-text {
		text-align: center;
		padding: 0.3em;
		max-width: 1000px;
		margin: 0 auto;
		color: goldenrod;
		font-size: 1.8em;
	}

	img {
		display: block;
		padding: 1em;
		margin: auto;
		width: 300px;
		height: auto;
	}
	h1 {
		text-align: center;
		color: black;
		text-transform: uppercase;
		font-size: 2em;
		font-family: 'Gill Sans';
		font-weight: 800;
		padding: 0.01em;
	}
	.if1 {
		text-align: center;
		padding: 0.3em;
		max-width: 1000px;
		margin: 0 auto;
		color: black;
		font-size: 1.2em;
	}

	button {
		background-color: white;
		border: none;
	}

	.buttonholder {
		display: grid;
	}
</style>
