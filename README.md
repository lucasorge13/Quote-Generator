## Random Quote Generator

This is a simple web-based application that fetches and displays random quotes. The project includes functionality for speaking the quote, copying the quote to the clipboard, and sharing the quote on Twitter.

### Project Files

1. `index.html`
2. `style.css`
3. `script.js`

### Features

- Fetches a random quote from an API.
- Displays the quote and author on the webpage.
- Allows the quote to be spoken aloud.
- Copies the quote to the clipboard.
- Shares the quote on Twitter.

### Installation

No installation is necessary. Simply open the `index.html` file in a web browser.

### Usage

- **New Quote**: Click the "New Quote" button to fetch and display a new random quote.
- **Speak Quote**: Click the speaker icon to hear the quote read aloud.
- **Copy Quote**: Click the copy icon to copy the quote text to the clipboard.
- **Tweet Quote**: Click the Twitter icon to share the quote on Twitter.

### File Descriptions

#### index.html
```html
<!DOCTYPE html>
<html lang="en" dir="ltr">
  <head>
    <meta charset="utf-8">  
    <title>Random Quote Generator</title>
    <link rel="stylesheet" href="style.css">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.3/css/all.min.css"/>
  </head>
  <body>
    <div class="wrapper">
      <header>Quote of the Day</header>
      <div class="content">
        <div class="quote-area">
          <i class="fas fa-quote-left"></i>
          <p class="quote">Never give up because you never know if the next try is going to be the one that works.</p>
          <i class="fas fa-quote-right"></i>
        </div>
        <div class="author">
          <span>__</span>
          <span class="name">Mary Kay Ash</span>
        </div>
      </div>
      <div class="buttons">
        <div class="features">
          <ul>
            <li class="speech"><i class="fas fa-volume-up"></i></li>
            <li class="copy"><i class="fas fa-copy"></i></li>
            <li class="twitter"><i class="fab fa-twitter"></i></li>
          </ul>
          <button>New Quote</button>
        </div>
      </div>
    </div>
    <script src="script.js"></script>
  </body>
</html>
```

#### style.css
```css
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@400;500;600;700&display=swap');

*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Poppins', sans-serif;
}
body{
  display: flex;
  align-items: center;
  justify-content: center;
  min-height: 100vh;
  background: #5372f0;
}
.wrapper{
  width: 605px;
  background: #fff;
  border-radius: 15px;
  padding: 30px 30px 25px;
}

.wrapper header{
  font-size: 35px;
  font-weight: 600;
  text-align: center;
}

.wrapper .content{
  margin: 35px
}

.content .quote-area{
  display: flex;
  justify-content: center;
}

.quote-area{
  font-size: 15px;
}

.quote-area i:first-child{
  margin: 3px 10px 0 0;
}

.quote-area i:last-child{
  display: flex;
  align-items: flex-end;
  margin: 0 0 3px 10px;
}

.quote-area .quote{
  font-size: 22px;
  text-align: center;
  word-break: break-all;
}

.content .author{
  display: flex;
  margin-top: 20px;
  font-style: italic;
  font-size: 18px;
  justify-content: flex-end;
}

.author span:first-child{
  margin: -7px 5px 0 0;
  font-family: monospace;
}

.wrapper .buttons{
  border-top: 1px solid #ccc ;
}

.buttons .features{
  display: flex;
  align-items: center;
  margin-top: 20px;
  justify-content: space-between;
}

.features ul{
  display: flex;
}

.features ul li{
  list-style: none;
  margin: 0 5px;
  height: 47px;
  width: 47px;
  display: flex;
  color: #5372f0;
  align-items: center;
  justify-content: center;
  border-radius: 50%;
  border: 2px solid #5372f0;
  cursor: pointer;
  transition: all 0.3s ease;
}

.features ul li:hover{
  color:#fff;
  background: #5372f0;
}

.features button{
  border: none;
  outline: none;
  color: #fff;
  cursor: pointer;
  font-style: 16px;
  padding: 13px 22px;
  border-radius: 30px;
  background: #5372f0;
}

button.loading{
  opacity: 0.7;
  pointer-events: none;
}
```

#### script.js
```javascript
const quoteText = document.querySelector(".quote"),
quoteBtn = document.querySelector("button"),
authorName = document.querySelector(".name"),
speechBtn = document.querySelector(".speech"),
copyBtn = document.querySelector(".copy"),
twitterBtn = document.querySelector(".twitter"),
synth = speechSynthesis;

function randomQuote(){
    quoteBtn.classList.add("loading");
    quoteBtn.innerText = "Loading Quote...";
    fetch("http://api.quotable.io/random").then(response => response.json()).then(result => {
        quoteText.innerText = result.content;
        authorName.innerText = result.author;
        quoteBtn.classList.remove("loading");
        quoteBtn.innerText = "New Quote";
    });
}

speechBtn.addEventListener("click", ()=>{
    if(!quoteBtn.classList.contains("loading")){
        let utterance = new SpeechSynthesisUtterance(`${quoteText.innerText} by ${authorName.innerText}`);
        synth.speak(utterance);
        setInterval(()=>{
            !synth.speaking ? speechBtn.classList.remove("active") : speechBtn.classList.add("active");
        }, 10);
    }
});

copyBtn.addEventListener("click", ()=>{
    navigator.clipboard.writeText(quoteText.innerText);
});

twitterBtn.addEventListener("click", ()=>{
    let tweetUrl = `https://twitter.com/intent/tweet?url=${quoteText.innerText}`;
    window.open(tweetUrl, "_blank");
});

quoteBtn.addEventListener("click", randomQuote);
```

### Credits

- Quotes API: [Quotable](http://api.quotable.io/)
- Icons: [Font Awesome](https://fontawesome.com/)
- Font: [Google Fonts - Poppins](https://fonts.google.com/specimen/Poppins)
