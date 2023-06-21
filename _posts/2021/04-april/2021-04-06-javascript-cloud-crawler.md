---
title: Building a Powerful Crawler using Javascrit in the Cloud
categories: programming, web scraping

Introduction:
Web crawling and data extraction from websites are essential tasks in today's data-driven world. JavaScript cloud crawlers offer a convenient and scalable solution for efficiently collecting and processing data from the web. In this blog post, we will explore an example of a JavaScript cloud crawler using the popular GSM Arena website.

Using 80legs for Cloud Crawling:
When it comes to cloud crawling solutions, one of my favorites is 80legs (available at [80legs.com](http://80legs.com/)). This powerful platform provides the necessary infrastructure and tools to crawl websites at scale, making it an excellent choice for various web scraping projects.

GSM Arena Crawler Code:
Now, let's take a closer look at a JavaScript cloud crawler that extracts data from GSM Arena, a well-known website specializing in mobile phone specifications. Below is an example code snippet that demonstrates how to use the 80legs crawler to retrieve phone specifications from GSM Arena.

```javascript
const EightyApp = require('eighty-app');
const app = new EightyApp();

app.processDocument = function (html, url, headers, status, $) {
    const $html = this.parseHtml(html, $);

    return { specs_list: $html.find('#specs-list table').html() };
};

app.parseLinks = function (html, url, headers, status, $) {
    const $html = this.parseHtml(html, $);
    return $html.find('.module-phones-link').toArray().map(function(a){
        return app.makeLink(url, a.attribs.href);
    });
};

module.exports = function () {
    return app;
};
```

Explanation of the Code:
1. The code begins by importing the `EightyApp` module, which provides the necessary functionality for building an 80legs crawler.

2. An instance of the `EightyApp` class is created using the `new` keyword.

3. The `processDocument` function is defined within the `app` object. This function is responsible for processing the HTML content of a specific page and extracting the desired data. In this case, it finds the HTML of the specifications table (`#specs-list table`) on the page and returns it.

4. The `parseLinks` function is also defined within the `app` object. It is used to identify and extract links from the HTML of a page. In this example, it searches for elements with the class `.module-phones-link` and creates links using the `makeLink` method provided by the `app` object.

5. Finally, the module exports a function that returns the `app` object, making it available for use in the 80legs crawler.

Conclusion:
JavaScript cloud crawlers, such as the one demonstrated in this blog post, offer a powerful solution for web scraping tasks. By leveraging platforms like 80legs, developers can easily build scalable and efficient crawlers to extract data from websites. Whether it's gathering product information, monitoring competitors, or conducting market research, JavaScript cloud crawlers are a valuable tool in the data professional's arsenal.

Remember to always abide by the terms of service and the legal and ethical guidelines when scraping websites. Happy crawling!
---