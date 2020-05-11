<template>
    <div id="quote-box">
        <p id="text">{{quoteMessage}}</p>
        <p id="author">{{quotesAuthor}}</p>
       
        <a id="tweet-quote" 
        v-bind:href="tweetUrl" target="_blank">
        Tweet</a> 
        <button id="new-quote" v-on:click="onGetQuote">New Quote</button>   
    </div>
</template>

<script>
export default {
    name: 'QuoteMachine',
   
    data() {
        return {
            quoteMessage: 'Welcome to Vue js',
            quotesAuthor: 'John okay',
            tweetUrl: 'https://twitter.com/intent/tweet?text=quote+author'
        }
    },
    created() {
            console.log('At created');
            this.fetchRandomQuoteData();
    },
    methods: {
        onGetQuote() {
            console.log("just clicked");
            //this.quoteMessage = "just clicked";
            this.fetchRandomQuoteData();
            document.body.style.background = this.changeBackground();
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
                    this.onTweet(data.quote, data.author);
                })
                .catch(error => {
                    console.log('Failed to fetch: ' + error);
                });
        },
        onTweet(quote, author) {
            const baseUrl = "https://twitter.com/intent/tweet?text=";

            let formattedTweetText = this.quoteLength(quote, author);
            let newTwitterUrl = baseUrl + encodeURIComponent(formattedTweetText);
            this.tweetUrl = newTwitterUrl;
        },
        quoteLength(quote, author) {
            let quoteLength = quote.length;
            let authLength = author.length +1;
            let textTotal = 140 - authLength;

            if(quoteLength >= textTotal) {
                let newQuote = quote.slice(0, textTotal);
                let returnQuote = newQuote + '-' + author;
                return returnQuote;
            }
            else {
                let returnQuote = quote + '-' + author;
                return returnQuote;
            }
        },
        changeBackground() {
            let max = 255;
            let min = 0;
            let red = Math.floor(Math.random() * (max - min + 1)) + min;
            let green = Math.floor(Math.random() * (max - min + 1)) + min;
            let blue = Math.floor(Math.random() * (max - min + 1)) + min;
            let rgbColor = "rgb(" + red + "," + green + "," + blue + ")";
            return rgbColor;
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
        margin: 10% auto;
        width: 30%;
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
        background-color: gray;
    }
    button {
        box-shadow: 3px 4px 0px 0px #899599;
        background:linear-gradient(45deg, black, transparent);
        background-color: black;
        border-radius:15px;
        border:1px solid #593e59;
        display:inline-block;
        cursor:pointer;
        color:#3a8a9e;
        font-family:Arial;
        font-size:17px;
        padding:7px 25px;
        text-decoration:none;
        text-shadow:0px 1px 0px #e1e2ed;
    }
    button:hover {
        background:linear-gradient(to bottom, #bab1ba 5%, #ededed 100%);
        background-color:#bab1ba;
    }
    button:active {
        position:relative;
        top:1px;
    }

    a {
        box-shadow: 3px 4px 0px 0px #899599;
        
        background-color:black;
        border-radius:15px;
        border:1px solid #593e59;
        display:inline-block;
        cursor:pointer;
        color:#3a8a9e;
        font-family:Arial;
        font-size:17px;
        padding:7px 25px;
        text-decoration:none;
        text-shadow:0px 1px 0px #e1e2ed;
    }
    a:hover {
        background:linear-gradient(to bottom, #bab1ba 5%, #ededed 100%);
        background-color:#bab1ba;
    }
    a:active {
        position:relative;
        top:1px;
    }

    /*a{
        background-color: gray;
        color: white;
        
        text-decoration: none;
    }

    a:hover {
        background-color: red;
    }
    a:active {
        background-color: blue;
    }*/
    /*p {
        //display: inline-block;
    }
    button {
        display: inline-block;
    }*/
</style>