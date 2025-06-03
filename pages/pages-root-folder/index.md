---
#
# Use the widgets beneath and the content will be
# inserted automagically in the webpage. To make
# this work, you have to use › layout: frontpage
layout: frontpage
header:
  image_fullwidth: header_unsplash_12.jpg
widget1:
  title: "Get Started"
  url: '/library'
  image: widget-1-302x182.jpg
  text: 'Click More to be taken to the Library in its entirety. This website was made with the intents of providing accurate and easily accessible pc optimization knowledge. '
widget2:
  title: "Why use this theme?"
  url: 'http://phlow.github.io/feeling-responsive/info/'
  text: '<em>Feeling Responsive</em> is heavily customizable.<br/>1. Language-Support :)<br/>2. Optimized for speed and it&#39;s responsive.<br/>3. Built on <a href="http://foundation.zurb.com/">Foundation Framework</a>.<br/>4. Seven different Headers.<br/>5. Customizable navigation, footer,...'
  video: '<a href="#" data-reveal-id="videoModal"><img src="http://phlow.github.io/feeling-responsive/images/start-video-feeling-responsive-302x182.jpg" width="302" height="182" alt=""/></a>'
widget3:
  title: "Join the Community"
  url: 'https://discord.com/invite/QueGKynWnE'
  image: widget-github-303x182.jpg
  text: 'Talk with other members of the Khorvie Tech community or to get in touch with me too!'
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
# note to khorvie; remove these for a cool looking popup
 callforaction:
  url: https://tinyletter.com/feeling-responsive
  text: Inform me about new updates and features ›
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
