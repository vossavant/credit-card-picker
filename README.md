# Credit Card Picker

I wrote this simple Vue.js app as part of an interview process with a well-known financial services company. It pulls credit card information from a JSON file and allows users to filter down to one or two cards by selecting a card type and a credit score. The app originally pulled data from an API, but I localized the data so the app can work if the API changes in the future.


## Installation

1. Open your terminal and navigate to the app's root folder. 
2. If needed, modify the `vue.config.js` file to set your **publicPath**. In most cases, you can leave this as the default `/`, which assumes this app will be running in the root directory of your server. More information in the [Vue CLI docs](https://cli.vuejs.org/config/#publicpath).
3. Type `npm run build`
4. Upload the **dist** folder to your web server
5. Enter the appropriate URL and the app should load.


## Design Rationale

* For optimum speed, I elected to load credit card data from the API once the app is loaded, rather than when the user first interacts with the app controls. My rationale here is that the user would have a better experience if the card picker had either zero delay or told the user ahead of time that it wasn't working (i.e., couldn't fetch results). Snappiness was priority #1!

* I decided to require both the **card type** and **credit rating** options to be selected before showing any card offers, since this returns the best results for that user. No sense in showing cash back cards if the user won't qualify for some of them.

* For card ratings, I decided that numbers (e.g., *4/5*) had less cognitive load than stars or progress indicators, so I kept the same convention currently used on the financial institution's website.

* I placed the CTA button at the bottom of each offer because I feel it is more logical for the user to learn about the card before taking action. On mobile (screens at and below 480px), I added a second CTA near the top to account for the additional scrolling distance.


## Ephemera

* Tested in the latest versions of Chrome, Firefox, Safari, and Edge
* Bonus: Tested in IE11
* You should see a message if the API call throws an error
* Optimized for mobile devices down to 320px
