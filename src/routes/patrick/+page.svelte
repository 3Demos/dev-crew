<script>
	import Message from './Message.svelte';

	let posts = $state.raw([]);
	let mes = $state('');
	let num = $state(0);

	const username = 'ballingkitten';

	let remainingChars = $derived(30 - mes.length);
	let charColor = $derived(remainingChars > 0 ? 'lightgray' : 'red');
	let buttonEnabled = $derived(mes.length <= 30 && mes.length > 0);

	function postTweet() {
		if (mes) {
			num++;
			posts = [{ id: num, username, text: mes }, ...posts];
		}

		// Clear the input
		mes = '';
	}
</script>

<div>
	<!-- Static elements like text input for tweets -->
	<input
		id="inputText"
		type="text"
		bind:value={mes}
		onkeydown={(e) => (e.key == 'Enter' ? postTweet() : null)}
		maxlength="30"
	/>

	<br />

	<span style:color={charColor}>{remainingChars}</span>

	<button id="post_tweet" onclick={postTweet} disabled={!buttonEnabled}> Post Tweet </button>
</div>

<!-- Posts listed here dynamically -->
{#if posts.length > 0}
	<div id="posts_header">POSTS</div>
{/if}

<div id="posts">
	{#each posts as post (post.id)}
		<Message {post} deleteMe={() => (posts = posts.filter((p) => p.id !== post.id))} />
	{/each}
</div>

<style>
	#posts_header {
		font-weight: bold;
		font-size: large;
		font-style: italic;
		text-align: center;
	}

	/* Styles for the tweet input field */
	input[type='text'] {
		width: 100%;
		padding: 10px;
		border: 2px solid #1da1f2;
		border-radius: 8px;
		font-size: 16px;
		outline: none;
		margin-bottom: 10px;
	}

	input[type='text']:focus {
		border-color: #1991da;
		box-shadow: 0 0 5px rgba(29, 161, 242, 0.5);
	}

	/* Styles for the Post Tweet button */
	button#post_tweet {
		background-color: #1da1f2;
		color: white;
		border: none;
		padding: 10px 20px;
		border-radius: 20px;
		font-size: 16px;
		cursor: pointer;
		transition: background-color 0.3s ease;
	}

	button#post_tweet:disabled {
		background-color: #aab8c2;
		cursor: not-allowed;
	}

	button#post_tweet:hover:not(:disabled) {
		background-color: #1991da;
	}

	/* Styles for the posts header */
	#posts_header {
		font-size: 18px;
		font-weight: bold;
		color: #14171a;
		margin: 20px 0 10px 0;
	}

	/* Styles for the posts container */
	#posts {
		display: flex;
		flex-direction: column;
		gap: 15px;
	}
</style>
