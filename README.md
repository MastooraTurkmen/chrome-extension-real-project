# Chrome-extension-real-project

A wonderful Chrome Extension Personal Dashboard project which you can add to you chrome and get lots of
random background images :)

![Alt text](./images/image.png)
![Alt text](./images/image-1.png)


## Cloning the project 🪛🔨

```
# Clone this repository
$ git clone https://github.com/MastooraTurkmen/chrome-extension-real-project.git


# Go inside the repository
$ cd chrome-extension-real-project
```


----

## Languages and Tools are used 🗣️🔧

1. **Languages** 🗣️

    + [HTML](https://github.com/topics/html)
    + [HTML5](https://github.com/topics/html5)
    + [CSS](https://github.com/topics/css)
    + [CSS3](https://github.com/topics/css3)
    + [JavaScript](https://github.com/topics/javascript)


2. **Tools** 🔧

    + [Chrome](https://github.com/topics/chrome)
    + [Figma](https://github.com/topics/figma)
    + [VSCode](https://github.com/topics/vscode)
    + [Netlify](https://github.com/topics/netlify)


-----


## Deployment 📥

1. How to deploy our project to the ***Netlify*** site?
2. I use [Netlify App](https://app.netlify.com/) for deploying my projects.
4. From there select **_Deploy with Github_**.
5. Then write your project name and select it.
6. After selecting here you can see that the project **_Review configuration for chrome-extension-real-project_** and then select the **_Deploy chrome-extension-real-project_** Button.
7. Now your project is Live.

------


## Author 👩🏻‍💻

**Mastoora Turkmen**

[LinkedIn](https://www.linkedin.com/in/mastoora-turkmen/) 
<br>
[Github](https://github.com/MastooraTurkmen/) 
<br>
[Twitter](https://twitter.com/MastooraJ22)


# Codes are used in Project

1. ***Index HTML***
2. ***Index CSS***
3. ***Index JS***
4. ***manifest json***


## ***Index HTML***

```html

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <link rel="icon" type="image/svg+xml" href="./images/icon.png" />
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/normalize/8.0.1/normalize.css">
  <link rel="stylesheet" href="index.css">
  <title>Personal Dashboard</title>
</head>
<body>
  <main>    
    <div class="top">
      <div id="crypto">
        <div id="crypto-top"></div>
           </div>
        <div id="weather"></div>
      </div>
        
    <h1 id="time" class="time"></h1>
    <p id="author"></p>
  </main>
<script src="index.js"></script>
</body>
</html>

```


## ***Index CSS***

```css

* {
    box-sizing: border-box;
}    

body {
    margin: 0;
    background: no-repeat center center fixed; 
    background-size: cover;
    color: white;
    font-family: Arial, Helvetica, sans-serif;
    text-shadow: 0px 0px 20px #242424;
}

main {
    padding: 15px;
    height: 100vh;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
}

div.top {
    display: flex;
    justify-content: space-between;
}

h1.time {
    text-align: center;
    font-size: 5rem;
}

div#crypto {
    font-size: 1.3rem;
}

div#crypto > p {
    margin: 0;
}

div#crypto-top {
    display: flex;
    align-items: center;
    margin-bottom: 5px;
}

div#crypto-top > span {
    margin-left: 10px;
}

div#weather {
    display: flex;
    align-items: center;
    flex-wrap: wrap;
    justify-content: flex-end;
    align-self: flex-start;
    margin-top: -20px;
}

div#weather > img {
    width: 70px;
}

p.weather-city {
    width: 100%;
    text-align: right;
    margin: 0;
    margin-top: -10px;
    font-size: 1.2rem;
}

p.weather-temp {
    margin: 0;
    font-size: 1.7rem;
    margin-left: -10px;
}

p#author {
    font-size: 1rem;
}
```

## ***Index JS***

```js

fetch("https://apis.scrimba.com/unsplash/photos/random?orientation=landscape&query=nature")
    .then(res => res.json())
    .then(data => {
        document.body.style.backgroundImage = `url(${data.urls.regular})`
		document.getElementById("author").textContent = `By: ${data.user.name}`
    })
    .catch(err => {
        // Use a default background image/author
        document.body.style.backgroundImage = `url(https://images.unsplash.com/photo-1560008511-11c63416e52d?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&ixid=MnwyMTEwMjl8MHwxfHJhbmRvbXx8fHx8fHx8fDE2MjI4NDIxMTc&ixlib=rb-1.2.1&q=80&w=1080
)`
		document.getElementById("author").textContent = `By: Dodi Achmad`
    })

fetch("https://api.coingecko.com/api/v3/coins/dogecoin")
    .then(res => {
        if (!res.ok) {
            throw Error("Something went wrong")
        }
        return res.json()
    })
    .then(data => {
        document.getElementById("crypto-top").innerHTML = `
            <img src=${data.image.small} />
            <span>${data.name}</span>
        `
        document.getElementById("crypto").innerHTML += `
            <p>🎯: $${data.market_data.current_price.usd}</p>
            <p>👆: $${data.market_data.high_24h.usd}</p>
            <p>👇: $${data.market_data.low_24h.usd}</p>
        `
    })
    .catch(err => console.error(err))

function getCurrentTime() {
    const date = new Date()
    document.getElementById("time").textContent = date.toLocaleTimeString("en-us", {timeStyle: "short"})
}

setInterval(getCurrentTime, 1000)

navigator.geolocation.getCurrentPosition(position => {
    fetch(`https://apis.scrimba.com/openweathermap/data/2.5/weather?lat=${position.coords.latitude}&lon=${position.coords.longitude}&units=imperial`)
        .then(res => {
            if (!res.ok) {
                throw Error("Weather data not available")
            }
            return res.json()
        })
        .then(data => {
            const iconUrl = `http://openweathermap.org/img/wn/${data.weather[0].icon}@2x.png`
            document.getElementById("weather").innerHTML = `
                <img src=${iconUrl} />
                <p class="weather-temp">${Math.round(data.main.temp)}º</p>
                <p class="weather-city">${data.name}</p>
            `
        })
        .catch(err => console.error(err))
});

```


## ***manifest json***