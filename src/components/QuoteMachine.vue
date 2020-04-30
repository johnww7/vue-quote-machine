<template>
    <div id="quote-box">
        <p id="text">{{quoteMessage}}</p>
        <p id="author">{{quotesAuthor}}</p>
       
        <button id="tweet-quote">Tweet</button> 
         <button id="new-quote">New Quote</button>   
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
        background-color: yellow;
        margin: 0 auto;
        width: 40%;
        height: 30%;
    }
    #text {
        grid-column: 1/4;
    }
    #author {
        grid-column: 1/4;
    }
    #tweet-quote {
        grid-column: 1/2;
        padding: 10px;
        margin: 30px; 
    }
    #new-quote
    {
        grid-column: 3/4;
        padding: 5px;
        margin: 20px;
    }
    /*p {
        //display: inline-block;
    }
    button {
        display: inline-block;
    }*/
</style>