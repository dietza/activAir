# ActivAir
###### Find fresh air for your outdoor activities.
---
## Table of Contents
* [Introduction](#Introduction)
* [Technologies](#Technologies)
* [Deployment](#Deployment)
* [Features](#Features)
* [Learning Process](#Learning-Process)
* [Authors](#Authors)

## Introduction
Last summer, as wildfires were raging across the western United States, residents who live and recreate nearby were often faced with the decision of whether to be active outdoors in the first place, and if so, where to go. Hikers, runners, cyclists, dog walkers, and more could have used an app that brings in up-to-date weather and air quality information by location to help make that decision.

[ActivAir](https://github.com/alia-peterson/ActivAir) solves this problem by tapping into data from the [IQAir AirVisual API](https://www.iqair.com/us/). Users can view data for their current location, add and remove other locations, get advice on whether it's safe to recreate outdoors given the AQI for that area, and click to view trail recommendations for each location on [AllTrails](https://www.alltrails.com/). The project specifications can be found [here](https://frontend.turing.io/projects/module-3/stretch.html).

### Motivation & Goals
* Learn a new "stretch" technology independently. After learning React last month, we chose to dive into Vue.js to deepen our understanding of frameworks. We had 9 days to self-teach Vue.js and create our app.
* Create an MVP that solves a problem for users
* Gain more experience using external APIs

---

## Technologies
JavaScript, Vue, RESTful APIs, Cypress, Local Storage, HTML, CSS

---

## Deployment
[Deployment Link](https://activ-air-alia-peterson.vercel.app/)

**To run locally:**
1. Clone down this repo
2. `npm install`
3. `npm run start`

---

## Features
* [Display Current Location](#Display-Current-Location)
* [Display Other Locations](#Display-Other-Locations)
* [Activity Recommendations](#Activity-Recommendations)
* [View Trails](#View-Trails)


#### Display Current Location
When the site loads, the you'll see a form with options to get info for your current location or to choose a location from a dropdown list of available cities and states. If you click "Nearest Location," a card will show up and persist on refresh with the latest data so you can stay up to date with the AQI and weather for where you are.
<p align = "center">
<img width="1440" alt="Display Current Location" src="https://user-images.githubusercontent.com/66852774/109685355-6a819c80-7b3e-11eb-8dc5-f1c338256855.png">
</p>
  <details>
    <summary>Under the Hood</summary>
    The current location card data comes from our <code>fetch</code> to the AirVisual API IP geolocation endpoint. Conditional rendering in Vue.js allowed us to include "Current Location" copy at the top of the card without the delete button. We used <code>unshift</code> to ensure that the current location card always shows up first in the render even as other location cards are added. Once a current location card has been added from the form, it is also added to <code>localStorage</code> and will show up on refresh with data from the latest timestamp.
  </details>

#### Display Other Locations
To see what the AQI and weather looks like in other areas, you can choose supported cities and states from the dropdown menus in the form. Once a new location has been added, it's automatically saved so that you can come back to it later on. You can also delete a location if you no longer want to view it. Each card can be individually refreshed to view the latest weather and AQI data.
<p align = "center">
<img width="1440" alt="Display Other Locations" src="https://user-images.githubusercontent.com/66852774/109685516-913fd300-7b3e-11eb-92f5-4607540fe329.png">
</p>
  <details>
    <summary>Under the Hood</summary>
    On load, the state form dropdown menu is populated with a <code>fetch</code> to AirVisual's "List supported states in a country" endpoint. Once a state has been selected, the cities dropdown is populated with a <code>fetch</code> to AirVisual's "List supported cities in a state" endpoint for the selected state. On submit, another <code>fetch</code> to their "Get specified city data" endpoint interpolating both state and city dropdown values provides the data needed to render a new card for that location. Error handling was used to disable the cities dropdown and submit button until the form has met certain conditions, and to display a server error message to the UI when the calls/minute limit has been reached. Locations are saved to <code>localStorage</code> and can also be deleted.
  </details>

#### Activity Recommendations
To make the app directly relevant to our active/outdoorsy target audience, messages are displayed with specific recommendations for outdoor activity based on a location's given AQI and what [AirNow.gov](https://www.airnow.gov/) suggests is safe.
<p align = "center">
<img width="1440" alt="AQI Activity Recommendations" src="https://user-images.githubusercontent.com/66852774/109685668-b59baf80-7b3e-11eb-8d0e-95bcda281302.png">
</p>
  <details>
    <summary>Under the Hood</summary>
    Conditional rendering in Vue.js allowed us to render colors, recommendation messages, and more based on where a location's AQI falls within a range of numbers on the scale.
  </details>

#### View Trails
Taking the activity recommendations a step further, we added a button to each location card that sends users to the trails page for that location on AllTrails.
<p align = "center">
<img width="1440" alt="AllTrails" src="https://user-images.githubusercontent.com/66852774/109685890-f09de300-7b3e-11eb-9c12-cbb088d2fea4.png">
</p>
  <details>
    <summary>Under the Hood</summary>
    By formatting the city and state inputs from the form to match the AllTrails URL format, we were able to interpolate the link for each individual card so that the user lands on that particular location page.
  </details>

### Accessibility
This app was built with all users in mind. We used Lighthouse and [WAVE](https://wave.webaim.org/) to work towards including as broad of an audience as we could. Of course, as we are committed to including all users, we are ready to make future edits to address any areas that we may have missed.

### Future Improvements
- Allow a user to login to see their saved locations (rather than using local storage). We'd love to dive into Firebase for this as another new "stretch" technology for us.
- Implement (and learn) Vue Router so that we can include an FAQ page about AQI and how it can impact your health when being active outdoors.
- Bring in AQI rankings, interactive maps, or other data visualizations
- Use a different API? (See notes in "Learning Process" below)

---

## Learning Process
This is the first time we've had to learn a new technology without the help of Turing's lesson plans and instructor knowledge. The 3 of us in our group had 9 days total to learn Vue.js and create our application.

We started out by choosing an API, discussing our MVP, wireframing, and creating a project board. Then, we independently taught ourselves Vue.js for the first 2 days of the project. We had some context for how Vue.js should work because we had just learned React. Because we all loved Scrimba's React course, we started out by diving into their Vue.js course, which we all agreed was unfortunately not up to the same standard. So we switched gears and went directly to the Vue.js docs and video courses, which turned out to be very useful!

Similar to `Create React App`, we discovered that you can easily spin up a Vue.js app in the CLI. So once we all felt like we had a good foundation in Vue.js, we started out by doing some paired programming to make sure we were all on the same page with our learning goals and understanding the code together. Once we felt comfortable with that, we were able to split up tasks to make sure we were on track to meet our deadline.

### Challenges
While we were pleased that learning Vue.js from scratch in such a short amount of time was actually quite manageable, most of the issues we ran into were with the API. We used the free version from IQAir AirVisual, which has call limits by the minute, day, month, and year. This made building the app and QA testing new functionality more difficult because if we tried to interact with our form too quickly/too often, the API would throw an error in the console.

We got around this by either waiting it out for a minute and, if the daily limit had been reached, getting a new API key. We did our best to mitigate the poor user experience this can cause with error handling, but this may be better managed if we were able to gain unlimited access to the necessary data. The biggest change we'd make to our app without these call limits would be to refresh the timestamp (make a new API call) for each card in local storage on load, rather than just the current location card. For now, the user is only able to refresh location cards manually in order to reduce the number of calls made.

We had decided to bring in our data from the API calls early on in the process because we weren't sure how long it would take us to figure it out in the new framework. But in the future, we would likely try to hold out on implementing the API calls for as long as possible and bring in our data from our mock data file to speed up our development & QA testing process.

---

## Authors
<table>
    <tr>
        <td> Alia Peterson <a href="https://github.com/alia-peterson">GH</td>
        <td> Tashia Davis <a href="https://github.com/tashiad">GH</td>
        <td> Allison Dietz <a href="https://github.com/dietza">GH</td>
    </tr>
<td><img src="https://avatars.githubusercontent.com/u/70297733?s=460&u=f7e7c3682b498a90f005565b56b38a8ac985b053&v=4" alt="Ms. Peterson"
 width="150" height="auto" /></td>
 <td><img src="https://avatars3.githubusercontent.com/u/66852774?s=400&v=4" alt="Ms. Davis"
 width="150" height="auto" /></td>
 <td><img src="https://avatars.githubusercontent.com/u/64617223?s=460&u=8f5b1a393d777e490de0367a2ddb5f236bbdef75&v=4" alt="Ms. Dietz"
 width="150" height="auto" /></td>
</table>
