---
#
# Use the widgets beneath and the content will be
# inserted automagically in the webpage. To make
# this work, you have to use › layout: frontpage
#
 layout: frontpage
 show_logo: true
- widget1:
  title: "Getting started"
  url: '/library'
  image:
  text: 'On this website you'll find some of the most reliable and straightforward knowledge about PC optimizations. Only verified and true information makes it into our articles. Click More right below to get started with searching through our library of information!'
widget2:
  title: "Products Coming Soon!"
  url: '/shop'
  text: 'Synergy will soon offer a variety of tools such as a customized iso that can optimize your machine straight from the moment you install Windows along with soon to provide an optimization tool to easily apply a variety of optimizations that will work on any machine.'
  video: '<a href="#" data-reveal-id="videoModal"><img src="http://phlow.github.io/feeling-responsive/images/start-video-feeling-responsive-302x182.jpg" width="302" height="182" alt=""/></a>'
widget3:
  title: "About Synergy"
  url: '/info'
  image: widget-github-303x182.jpg
  text: 'Learn more about why Synergy came to be and to meet the creator.'
#
# Use the call for action to show a button on the frontpage
#
# To make internal links, just use a permalink like this
# url: /getting-started/
#
# To style the button in different colors, use no value
# to use the main color or success, alert or secondary.
# To change colors see sass/_01_settings_colors.scss
#
callforaction:
  url: https://discord.gg/QueGKynWnE
  text: Join the Khorvie Tech Community! ›
  style: alert
permalink: /index.html
#
# This is a nasty hack to make the navigation highlight
# this page as active in the topbar navigation
#
homepage: true
---

<div id="videoModal" class="reveal-modal large" data-reveal="">
  <div class="flex-video widescreen vimeo" style="display: block;">
    <iframe width="1280" height="720" src="https://www.youtube.com/embed/3b5zCFSmVvU" frameborder="0" allowfullscreen></iframe>
  </div>
  <a class="close-reveal-modal">&#215;</a>
</div>
