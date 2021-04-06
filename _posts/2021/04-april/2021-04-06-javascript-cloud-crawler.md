---
title: Javascript Cloud Crawler
categories: programming
---

One of my favorite cloud crawling soltuions is <http://80legs.com/>

GSM Arena crawler:

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
    })
};

module.exports = function () {
    return app;
};
```
