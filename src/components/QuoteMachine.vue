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

</style>