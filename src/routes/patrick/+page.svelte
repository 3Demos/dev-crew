


<script>
    import Message from "./Message.svelte";
    import { globalPosts } from './posts.svelte.js';
    

    let mes = $state('');
    let username = 'ballingkitten';
    let num = $derived(globalPosts.posts.length);
    let hasPosted = $state(false);



    let remainingChars = $derived(30 - mes.length);
    let charColor = $derived(remainingChars >= 0 ? 'belowCharMax' : 'aboveCharMax');
    let buttonEnabled=  $derived(mes.length <= 30 && mes.length > 0);


    // function canPost(mes) {
    //     return mes.length <= 30 && mes.length > 0;
    // }

    // function charCount() {
    //     return 30 - mes.length;
    // }

    // function handleInput(event) {
    //     mes = event.target.value;

    //     remainingChars = charCount();
    //     charColor = remainingChars >= 0 ? 'belowCharMax' : 'aboveCharMax';
    //     buttonDisabled = !canPost(mes);
    // }

    function postTweet() {

        if (!hasPosted) {
            hasPosted = true;
        }

      
        globalPosts.posts.splice(0,0, {id: num, username, text: mes })
        // num += 1;

        // Clear the input
        mes = '';
        
    }


</script>

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

    #posts_header {
        font-weight: bold;
        font-size: large;
        font-style: italic;
        text-align:center;
    }


    /* Styles for the tweet input field */
input[type="text"] {
    width: 100%;
    padding: 10px;
    border: 2px solid #1DA1F2;
    border-radius: 8px;
    font-size: 16px;
    outline: none;
    margin-bottom: 10px;
}

input[type="text"]:focus {
    border-color: #1991DA;
    box-shadow: 0 0 5px rgba(29, 161, 242, 0.5);
}

/* Styles for the character counter */
span.charColor {
    font-size: 14px;
    color: #657786;
    margin-right: 10px;
}

/* Styles for the Post Tweet button */
button#post_tweet {
    background-color: #1DA1F2;
    color: white;
    border: none;
    padding: 10px 20px;
    border-radius: 20px;
    font-size: 16px;
    cursor: pointer;
    transition: background-color 0.3s ease;
}

button#post_tweet:disabled {
    background-color: #AAB8C2;
    cursor: not-allowed;
}

button#post_tweet:hover:not(:disabled) {
    background-color: #1991DA;
}

/* Styles for the posts header */
#posts_header {
    font-size: 18px;
    font-weight: bold;
    color: #14171A;
    margin: 20px 0 10px 0;
}

/* Styles for the posts container */
#posts {
    display: flex;
    flex-direction: column;
    gap: 15px;
}
    
</style>

<!-- Static elements like text input for tweets -->
<input id="inputText" type="text" bind:value={mes} onkeydown={(e) => (e.keyCode == 13 ? postTweet(mes) : {})}/>

<br />

<span class={charColor}>{remainingChars}</span>

<button id="post_tweet" onclick={postTweet} disabled={!buttonEnabled}>
    Post Tweet
</button>


<!-- Posts listed here dynamically -->
{#if hasPosted}
    <div id="posts_header">POSTS</div>
{/if}

<div id="posts">
    {#each globalPosts.posts as post}
        <Message 
        post = {post}
        />
        
    {/each}
</div>