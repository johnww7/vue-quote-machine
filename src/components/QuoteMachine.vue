<template>
    <div v-if="quoteMessage !== ''" id="quote-box">
        <p id="text">{{quoteMessage}}</p>
        
        <p id="author">-{{quotesAuthor}}</p>

        <a id="tweet-quote" class="button-sizing"
        v-bind:href="tweetUrl" target="_blank">
        Tweet</a> 
        <button id="new-quote" class="button-sizing" v-on:click="onGetQuote">New Quote</button>   
    </div>

    <div v-else id="quote-box">
        <p id="text">Error fetching quotes from API</p>
        
        <p id="author">-Error message</p>

        <a id="tweet-quote" class="button-sizing"
        v-bind:href="tweetUrl" target="_blank">
        Tweet</a> 
        <button id="new-quote" class="button-sizing" v-on:click="onGetQuote">New Quote</button>   
    </div>
</template>

<script>
export default {
    name: 'QuoteMachine',
   
    data() {
        return {
            quoteMessage: '',
            quotesAuthor: '',
            tweetUrl: 'https://twitter.com/intent/tweet?text=quote+author'
        }
    },
    created() {
            this.fetchRandomQuoteData();
            document.body.style.background = this.changeBackground();
    },
    methods: {
        onGetQuote() {
            this.fetchRandomQuoteData();
            document.body.style.background = this.changeBackground();
        },
        
        fetchRandomQuoteData() {
            const url = 'http://quotes.stormconsultancy.co.uk/random.json';            //const url = 'https://api.forismatic.com/api/1.0/?method=getQuote&lang=en&format=jsonp&jsonp=?';
            
            fetch(url)
                .then(apiData => apiData.json())
                .then(data => {
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
        grid-template-rows: minmax(125px, auto);
        grid-template-columns: 2fr 2fr 2fr;
        grid-gap: 5px;
        background-color: rgb(194, 194, 182);
        margin: 10% auto;
        width: 30%;
        height: 35%;
        border: 3px solid #5b52a5;
        border-radius: 20px;
        box-shadow: 3px 4px 0px 0px #899599;
    }
    #text {
        grid-column: 1/4;
        padding: 5px 5px 5px 5px;
        margin: 30px 10px 10px 10px;
        font-family: 'Atma';
        font-size: 20px;
        text-align: center;
    }
    #author {
        grid-column: 1/4;
        padding: 10px;
        margin: 30px 5px 5px 5px;
        font-family: 'Atma';
    }
    #tweet-quote {
        grid-column: 1/2;

    }
    #new-quote{
        grid-column: 3/4;

    }

    .button-sizing {
        padding: 20px 10px 20px 10px;
        margin: 20px 15px 20px 15px;
    }

    button {
        box-shadow: 3px 4px 0px 0px #899599;
        background:linear-gradient(60deg, black, transparent);
        background-color: black;
        border-radius:15px;
        border:1px solid #593e59;
        display:inline-block;
        cursor:pointer;
        color:#3a8a9e;
        font-family:Arial;
        font-size:17px;
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
        background: linear-gradient(60deg, black, transparent);
        background-color:black;
        border-radius:15px;
        border:1px solid #593e59;
        display:inline-block;
        cursor:pointer;
        color:#3a8a9e;
        font-family:Arial;
        font-size:17px;
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

</style>