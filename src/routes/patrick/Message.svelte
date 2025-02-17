<script>
	import trash from '$lib/images/trash.png';

	let { post, deleteMe } = $props();
</script>

<!-- <link
	href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/css/bootstrap.min.css"
	rel="stylesheet"
	crossorigin="anonymous"
/> -->

<div>
	<div class="container text-center">
		<!-- Wrap the tweet content in a div with the class "tweet-container" -->
		<div class="tweet-container">
			<button id="deletePost" onclick={deleteMe} aria-label="Trash post">
				<i class="bi-trash"></i>
			</button>
			<span id="username">{post.username}</span>
			<span id="post{post.id}">{post.text}</span>
		</div>
	</div>
</div>

<!--add styles to make it prettier-->
<style>
	@import url('https://cdn.jsdelivr.net/npm/bootstrap-icons@1.11.3/font/bootstrap-icons.min.css');

	#deletePost {
		margin-right: 10px;
		opacity: 0.25;
	}

	#deletePost:hover {
		opacity: 1;
	}

	#username {
		font-weight: bold;
	}

	.tweet-container {
		border: 1px solid #e1e8ed; /* Light gray border */
		border-radius: 12px; /* Rounded corners */
		padding: 16px; /* Spacing inside the box */
		margin-bottom: 16px; /* Space between tweets */
		background-color: #ffffff; /* White background */
		max-width: 600px; /* Limit the width of the tweet box */
		margin-left: auto;
		margin-right: auto;
		box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1); /* Subtle shadow */
	}

	.tweet-container:hover {
		background-color: #f5f8fa; /* Light background on hover */
	}
</style>
