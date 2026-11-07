---
title: "Retrieve Weather Data Based on User Geolocation"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/Weather_forcasting_based_on_geolocation"
---

This example demonstrates how to obtain weather data based on the user's geolocation.

You can obtain the user's geolocation information through the `info.geo` property of the [FetchEvent interface](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-FetchEvent). The example assumes you are retrieving weather data through https://www.example.com. You need to pass the query parameter 'city' in the request to specify the user's city.

```JavaScript
addEventListener('fetch', (event) => {
  event.respondWith(handle(event));
});

// You need to change the appsecret and appid content in apiURL to real information
const apiURL =
    'https://www.example.com/free/day?appsecret=xxxxxx&appid=xxxxxx&';

async function queryWeather(city) {
  const response = await fetch(apiURL + 'city=' + city);
  if (response.ok) {
    // Assume the returned data is in JSON format
    /*
    {
      air: '94', city: 'ExampleCity', cityid: '101190101', tem: '31', tem_day: '31',
          tem_night: '24', update_time: '14:12', wea: 'Cloudy', wea_img: 'yun',
          win: 'Southeast wind', win_meter: '9km/h', win_speed: 'Level 2'
    }
    */

    const data = await response.json();

    const weather = data.wea;
    const tempDay = data.tem_day;
    const tempNight = data.tem_night;


    return `
     Hello user from ${city}
     Your local weather is: ${weather}, daytime temperature is ${
        tempDay}, nighttime temperature is ${tempNight}
    
    `;
  } else {
    return 'The weather API is having a hiccup';
  }
}

async function handle(event) {
  // Get the client's IP city address information
  const city = event.info.geo.city;
  // Query the weather information for this user through the city
  return queryWeather(city);
}
```


<span id="related-runtime-apis"></span>
## Related runtime APIs


* [addEventListener()](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-addEventListener)

* [FetchEvent](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-FetchEvent)

* [Response](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-Response)
