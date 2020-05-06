<template>
    <div id="quote-box">
        <p id="text">{{quoteMessage}}</p>
        <p id="author">{{quotesAuthor}}</p>
       
        <a id="tweet-quote" 
        href="https://twitter.com/intent/tweet?text=quote+author" target="_blank">
        Tweet</a> 
        <button id="new-quote" v-on:click="onGetQuote">New Quote</button>   
    </div>
</template>

<script>
export default {
    name: 'QuoteMachine',
    /*props: {
        quoteMessage: String,
        quotesAuthor: String
    },*/
    data() {
        return {
            quoteMessage: 'Welcome to Vue js',
            quotesAuthor: 'John okay'
        }
    },
    methods: {
        onGetQuote() {
            console.log("just clicked");
            this.quoteMessage = "just clicked";
            this.fetchRandomQuoteData();
        },
        fetchRandomQuoteData() {
            //const url = 'https://api.forismatic.com/api/1.0/?method=getQuote&lang=en&format=jsonp&jsonp=?';
            const url = 'http://quotes.stormconsultancy.co.uk/random.json'
            fetch(url)
                .then(apiData => apiData.json())
                .then(data => {
                    console.log(data);
                    this.quoteMessage = data.quote;
                    this.quotesAuthor = data.author;
                })
                .catch(error => {
                    console.log('Failed to fetch: ' + error);
                });
        },
        onTweet() {

        }
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

    a{
        background-color: black;
        color: white;
        
        text-decoration: none;
    }

    a:hover {
        background-color: red;
    }
    a:active {
        background-color: blue;
    }
    /*p {
        //display: inline-block;
    }
    button {
        display: inline-block;
    }*/
</style>