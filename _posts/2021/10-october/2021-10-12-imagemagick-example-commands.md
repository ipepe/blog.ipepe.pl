---
title: ImageMagick example commands
categories: programming
---

 * `convert IMG_0761.HEIC -resize 50% IMG_0761.png`
 * `convert image.png -fuzz 10% -transparent white image_new.png`
 * `convert image.png -strip -resize 1024x1024 image_new.jpg`
 * `convert background.png logo.png -geometry +0+1000 -composite -crop 5600x5600+0+0 -strip -resize 40% splash.png`