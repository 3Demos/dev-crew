<script>
	let mes = $state('');
	const username = 'ballingkitten20192984';
	let num = $state(0);
	let hasPosted = $state(false);
	let posts = $state([]);

	// $: remainingChars = charCount();
	// $: charColor = remainingChars >= 0 ? 'belowCharMax' : 'aboveCharMax';
	// $: buttonDisabled = !canPost(mes);

	// function canPost(mes) {
	//     return mes.length <= 30 && mes.length > 0;
	// }

	let remainingChars = $derived(30 - mes.length);

	let charColor = $derived(remainingChars >= 0 ? 'belowCharMax' : 'aboveCharMax');

	// function charCount() {
	//     return 30 - mes.length;
	// }

	// function handleInput(event) {
	//     // mes = event.target.value;
	//     // remainingChars = charCount();
	//     // buttonDisabled = !canPost(mes);
	// }

	function postTweet() {
		if (!hasPosted) {
			hasPosted = true;
		}

		posts.splice(0, 0, { id: num, username, text: mes });
		num++;

		// Clear the input
		mes = '';
	}
</script>

<!-- Static elements like text input for tweets -->
<input type="text" bind:value={mes} />

<br />

<span class={charColor}>{remainingChars}</span>

<button id="post_tweet" onclick={postTweet} disabled={mes.length > 30 || mes.length == 0}>
	Post Tweet
</button>

<!-- Posts listed here dynamically -->
{#if hasPosted}
	<div id="posts_header">POSTS</div>
{/if}

<div id="posts">
	{#each posts as post}
		<div>
			<span id="username">{post.username}</span>
			<span id="post{post.id}">{post.text}</span>
		</div>
		<br />
	{/each}
</div>

<style>
	.belowCharMax {
		font-weight: normal;
		color: lightgray;
	}

	.aboveCharMax {
		font-weight: normal;
		color: red;
	}

	.buttonFade {
		background-color: rgb(128, 128, 128);
	}

	#username {
		font-weight: bold;
	}

	#posts_header {
		font-weight: bold;
		font-size: large;
		font-style: italic;
	}
</style>
