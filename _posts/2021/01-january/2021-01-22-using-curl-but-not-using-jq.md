---
title: Using curl? But not using jq?
categories: devops
---

`jq` is command line utility, written C. That formats json and is really handy tool when working with curl

## Examples

Input: `curl https://jsonplaceholder.typicode.com/todos | jq '.[10]`

Output: 
```json
{
  "userId": 1,
  "id": 11,
  "title": "vero rerum temporibus dolor",
  "completed": true
}
``` 

Input: `curl https://jsonplaceholder.typicode.com/todos | jq '.[10].title'`

Output: `"vero rerum temporibus dolor"`

## Download jq
<https://stedolan.github.io/jq/download/>

## Official Website
<https://stedolan.github.io/jq/>