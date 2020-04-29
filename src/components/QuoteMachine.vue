<template>
    <div id="quote-box">
        <p id="text">{{quoteMessage}}</p>
        <p id="author">{{quotesAuthor}}</p>
        <button id="new-quote">New Quote</button>
        <button id="tweet-quote">Tweet</button>    
    </div>
</template>

<script>
export default {
    name: 'QuoteMachine',
    props: {
        quoteMessage: String,
        quotesAuthor: String
    }
}
</script>

<style scoped>
    #quote-box {
        display: grid;
        grid-template-rows: minmax(40px, auto);
        grid-template-columns: 2fr 2fr 2fr;
        grid-gap: 10px;
    }
    #text {
        grid-column: 1/4;
    }
    #author {
        grid-column: 1/4;
    }
    #new-quote {
        grid-column: 1/2;
    }

    #tweet-quote {
        grid-column: 3/4;
    }
</style>