+++
date = "2015-06-17T00:29:19+05:30"
title = "Bulk Download Facebook Photos"
tags = ["Facebook photo download" , "Bulk download"]

+++

Occasionally we download a lot of photos from Facebook. Downloading photos is really simple too : Just right click the mouse and select save image as. But what if you want to download bulk images, like 50 or 100 (for instance, you are into this girl and you want to save all the best albums of your crush) ?  Will you select each and every pic and do the same process?

Some months back I faced the same problem when I wanted to download a hundred to two hundred photos from Facebook 😉 . I searched for tools and scripts and since I could not find any (either no one really faced that problem, or they were content with the present method), I ended up in writing a script. I completed the script in 1 hour and Yeah, it worked!

If you are curious enough or if you have the same problem, please follow the given steps.

**Step 1**

Launch Google Chrome, go to Facebook and open the album you want to download. Scroll down till all the thumbnails of the photos are loaded.

![fb1][1]

**Step 2**

Go to JavaScript console by:

Google Chrome controls -> More Tools -> JavaScript Console

![fb5][2]

**Step 3**

Chrome will warn you about hacking. Dont worry, I am not gonna hack anyone's account.:) Please copy paste the script into the console.

```javascript
var divs = document.getElementsByClassName('_53s');
for(var i=0;i<divs.length;i++)
{
  console.log(divs[i].getAttribute("data-starred-src"));
  var save = document.createElement('a');
  save.href = divs[i].getAttribute("data-starred-src");
  save.target = '_blank';
  save.download = 'Image '+i+'.jpg';
 
  var event = document.createEvent('Event');
  event.initEvent('click', true, true);
  save.dispatchEvent(event);
  (window.URL || window.webkitURL).revokeObjectURL(save.href);
 
  (function myLoop (i) {          
  setTimeout(function () {
     if (--i) myLoop(i);      
  }, 3000)
})(10);    
 
}
```

![fb2][3]

**Step 4**

After copying the script, press Enter. You will get a question from Chrome to allow Facebook to download multiple images. Click on Allow.

![fb3][4]

**Step 5**

Now all you have to do is wait for all the images to download.

![fb4][5]

Oh, by the way, you can use this until Facebook discovers this and blocks it. :) :) :)

[1]: /img/fb1.jpg
[2]: /img/fb5.jpg
[3]: /img/fb2.jpg
[4]: /img/fb3.jpg
[5]: /img/fb4.jpg
