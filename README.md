<!--
 Copyright (c) 2022 Chris Laprade (chris@rootiest.com)
 
 This software is released under the MIT License.
 https://opensource .org/licenses/MIT
-->
# This is a template for quickly and easily building multiple D1Mini-ESP32 boards in ESPHome.

As I got more into ESHome and started building more boards, I ran up against one of the best/worst parts of ESPHome, how inexpensive the boards are!

As a result, I found myself buying them in bulk. The consequence of which was a lot of repetitive code-writing for the same basic structure in each build.

So I figured I would put together a kind of template/blueprint that I could use as a base for any builds which only requires changing a few lines at the top for each board.

I'm hoping that others will find this useful as well, so I'm sharing it here.

A couple of notes before we get to the goods:

This is designed around the D1-Mini-ESP32 board (not the original D1 Mini) That said, it can be easily modified to work with other boards and may even work more less as-is with several. I've tried quite a few different boards and I really like the D1-Mini-ESP32, it has a nice compact design that has some degree of compatibility with the very popular original D1-Mini but with the much more powerful ESP32 chip. Again, you could easily modify this to work with any board, but if you are new and unsure what to go with, I highly recommend these!

Sort of 1b: This is designed for ESP32 boards. There are a few parts that will have issue with ESP82xx boards, the hall effect sensor for one. You'll need to modify/remove several parts to use this with an ESP82xx board, but it absolutely can be done. I always assumed I would have a need for Bluetooth, but I probably could have gotten away with an ESP82xx/original D1 Mini for many of my builds. The ESP82xx boards are cheaper naturally, but with how inexpensive both are, I opted for the extra oomph of an ESP32 for the majority of my boards.

This uses the !secret feature extensively. I think every use is fairly self-explanatory, but feel free to ask if any are confusing! I use this a lot, both for sensitive data like wifi passwords, and for less sensitive data, like local ip addresses, anything that's a "global variable" really. My /config/esphome/secrets.yaml file contains this one line: <<: !include ../secrets.yaml which tells it to use the Home Assistant secrets.yaml file instead. This allows me to share secrets between HA and ESPHome.

Substitutions are used even more extensively than !secret. Like they are the majority of this blueprint, and kind of the whole point of this post. This is what allows you to change just 5 lines (three of which are variations of "name") and create a whole new ESPHome device with properly ID'd and labeled entities. Combined with the global "secrets" and we've got a "blueprint"

I use 3 separate lines for variations on the "name" of the ESPHome device. There's probably a much better way to do this, but this is what I settled on until I find a better way: friendly_name is self-explanatory (it's the "label" spaces, numbers, and capitalization all allowed), device_name uses hyphens instead of spaces (ESPHome device naming guidelines) and device_entity uses underscores instead of spaces. I use this when adding the device name to an entity name, where spaces and hyphens are not allowed and underscores are the norm.

I added links to wiki sections in the comments for every relevant part of the file which makes it super convenient for looking up more information on each of the parts. Like freaking everywhere. I guess that's the other point of this post, it's pretty useful for looking up details. It's actually a little overboard so I find myself removing all the comments in my final builds, but it's still nice to have the links right there when you need them!

This is my personal template that I use myself so it's far from perfect and I know for a fact there are things that can be done better. Please feel free to tell me what you like, what you hate, and any advice/suggestions for improvement! This grew into a learning tool and I'd love to continue to develop it as such despite its actual usefulness besides!

I included a lot of extras here that many of you probably don't need/want. This is not, and nothing ever really could be, a one-size-fits-all blueprint. I imagine most people don't need every board to have access to sunrise/sunset and the suns position, the onboard LED/hall effect sensor, the web server function, using a local time server, etc. There's a lot there, feel free to trim it down in actual use. I don't often use everything in the final builds that I base off this. It's just easier to remove things than to add them, especially since I use substitutions to uniquely name the entities. The majority of this was borrowed straight out of the wiki while I was playing with features.

I hope others find this useful, and can even help make it better! Let me know what you all think!

This is a work in progress (especially this README) so it's a little rough around the edges!