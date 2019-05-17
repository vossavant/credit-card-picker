# Credit Card Picker

This simple Vue.js app pulls credit card information from The Ascent's API and allows users to filter down to one or two cards by selecting a card type and a credit score.


## Installation

1. Open your terminal and navigate to the app's root folder. 
2. If needed, modify the `vue.config.js` file to set your **publicPath**. In most cases, you can leave this as the default `/`, which assumes this app will be running in the root directory of your server. More information in the [Vue CLI docs](https://cli.vuejs.org/config/#publicpath).
3. Type `npm run build`
4. Upload the **dist** folder to your web server
5. Enter the appropriate URL and the app should load.


## Design Rationale

* I decided to request data from the API as soon as the app is loaded, primarily because I assume the component has a high likelihood of being used wherever it is placed, and because I wanted the most optimal user experience. The API request is small and shouldn't block the user, but I wanted to avoid any potential frustration on the user's part (i.e., seeing a faillure after they make selections, or having to wait after making selections). Snappiness was priority #1!

* It would be possible to show results if the user only chose one option (that is, either **card type** or **credit rating**) but these results wouldn't be as useful, so I decided to require both options to be selected before showing any card offers.

* Each card has some ratings (out of a possible high of 5). I played around with showing progress-style indicators and using stars, but ultimately felt that numbers had the lowest cognitive load. In other words, I personally found numbers like **4/5** to be easier to understand at a glance. I also see this is how cards are currently scored on the [Ascent's website](https://www.fool.com/the-ascent/api/creditcardrecommendations/).

* CTA buttons are placed at the bottom of each card offer (except on mobile at 480px and below) because I think the logical flow for a user is to learn about the card and *then* want to apply, vs. being given the option to apply too early. I show an additional button near the top on mobile because more scrolling is required on smaller screens to see the CTA. I figured more conversion options on mobile would make more business sense since mobile users are less likely to find the "apply" button.


## Ephemera

* Tested in latest versions of Chrome, Firefox, Safari, and Edge
* Bonus! Tested in IE11
* You should see a message if the API call throws an error
* Optimized for mobile devices down to 320px


**Thanks so much for this opportunity!**


<!-- Docs to Markdown version 1.0β17 -->
