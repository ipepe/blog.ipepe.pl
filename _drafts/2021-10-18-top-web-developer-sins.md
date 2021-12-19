---
title: TOP Web Developer sins
categories: programming
---

## 1. Render buttons based on permissions and dont check permissions on backend
This is bad because permissions might change in time, and if someone was revoked permissions but still has browser window open, it will give them ability to make operations they should have permissions for.

This is also bad for batch actions where You select multiple objects to perform batch action on, and one of objects changes in the meantime of rendering the page and submitting the batch action.

## 2. Double click = double ajax = double action


## 3. Race conditions

