## Quick new post
(run while your server is NOT running)
`bundle exec octopress new post "My Title"``

## Drafts
To write a new post by creating a new draft (server can't be running):
`bundle exec octopress new draft "my title here"`

To preview the blog with unpublished drafts:
`bundle exec jekyll serve --config _config.yml,_config_dev.yml --drafts`

publishing later when its ready:
`bundle exec octopress publish \_drafts/my-title-here.markdown`

or you could create a post that will be instantly published next time you deploy the blog:
```
    bundle exec octopress new post "my title here"
    atom \_posts/my-title-here.markdown
```

unpublish a post:
`bundle exec octopress unpublish \_posts/my-title-here.markdown`

## Preview
Run website so it can be viewed browser at http://localhost:4000/ (bundle exec makes sure to use the gemfiles in your site instead of just the ones on your computer) -- doesn't show drafts! Type into terminal:
```
bundle exec jekyll serve --config _config.yml,_config_dev.yml
```
Need to run after editing config.yml (stop server by pressing Control+C, then arrow up to get the last line typed into terminal or retype the command)

You used to just use "jekyll serve" but now that your site is live online, everything is referencing leiahmjansen.com and when you run it locally, things are missing/won't update. So when you run locally in development, make sure to use the longer jekyll serve --config thing from above.

## To pull changes if you made some on your laptop
```
git pull
```
Then git will pull all those changes you committed to thor on your laptop.

## To scroll through the commit messages of what you changed
```
git log
```

## To check where you're at with commits
```
git status
```

## Use the command line to commit updates and push to Thor (not live yet)
1. open terminal, navigate to repository directory  
  `cd /Users/leiah/leiahmjansen.com`
  To see where you are in the file structure, type `pwd`
2. To see the status of which files I modified or added:  
  `git status`
3. If I created a new file that is untracked, I need to add it to git:  
  `git add <filename>` (btw this gives you no feedback after typing; do 'git status' again to see it)
  unless I added a bunch of stuff and I want to add all of it:  
  `git add --all`
4. Then when I am ready to commit all changes  
  `git commit --all -m "some message that describes changes (required)"`
5. Finally, push to Thor when you are on home network for syncing:
  `git push` (then type ssh password - thor's pw)

## How to publish:
OK, you're working on stuff, running server locally, etc. Make sure to test your blog post thumbnail at http://localhost:4000/blog/ . Make sure to click browser Pin button ON the blog post itself to make sure your thumbnail shows up.
Then when you're ready to publish:
1. Make sure you push all your changes to Git on Thor by using the GitHub Desktop client. Commit changes and sync it.
2. STOP the server if you're still running it.
3. DELETE .sass_cache folder.
4. Build it.
```
bundle exec jekyll build
```
5. Start the server. MAKE SURE your links (like in the top nav) are trying to reach leiahmjansen.com
```
bundle exec jekyll serve
```
6. STOP the server again. You don't want it running when you go live, because you might overlook it if your links are pulling locally.
7. Push it! Now you're ready to go public(!), run in a terminal:
```
bundle exec octopress deploy
```
This will ask for your ssh password again, twice, I believe. Type in the same pw you did for pushing to thor.

This will generate the static site files, and push it to github.io servers. It will then be live on your website, leiahmjansen.com and also leiahmjansen.github.io

*Don't skip these steps! Even if you make a small change! In the past when you skip the sass-cache deleting, skip the jekyll build... and go straight to DEPLOY, it breaks! the css is gonezo on your site.*

## After publishing:
1. Check live site to make sure it works
2. Go to permalink of your new blog post. Pin the post thumbnail to your leiahmjansen.com pinterest board
3. Pin any other relevant graphics, to "My Work" or other boards
4. Make sure this new blog post is on your google "LMJ schedule" calendar, for at-a-glance reference later

## Notes by Leiah:
- how to comment out multiple line of code: cmd + /
- blog posts use "layout: page". I know it's confusing.
- put any new images in local folder: leiahmjansen.com/images/
- except the logo, which goes in assets/img/logo.png
- in the config.yml file, there is a line that specifies what the base url is for images. It *was* Phlow's github or whatever, but i changed it to be /images so all images will read locally while i'm developing.
- tried to customize my color variable names but there were too many errors. tried to change $ci-1 to $ci-orange, but it was *not* having it.
- on the blog landing page, there was a hyphen between post category and subheader. It was annoying because if the post didn't have a category or subheader, the dash would just float there by itself. I found it specified in -includes/-pagination.html. I put a screenshot -working folder.
- also, there was a > sign between categories. Took it out in the same -pagination.html file.
- it's probably better to specify sidebar:right in the config.yml DEFAULT area rather than putting it on every single individual post's frontmatter
- How I installed/removed Disqus comments: config.yml, Line 224: put my disqus shortname here (leiahmjansen)
- I was going to repeat each blog post thumbnail image in the blog post itself (for pinterest's sake), but it appears that pinterest can pull that thumbnail image even if when it's not directly shown on the post page. I was going to put this in the img tag: data-pin-description="from @oleiah at leiahmjansen.com" PS: this image is NOT hidden in feedly subscriptions
- tiny font-based icons: See the icon-set/preview in /assets/fonts/iconfont-preview.html (open that html file in a browser to see it)

## Images
- -config.yml, line 41 has urlimg: '/images/' A path where images are to be found locally. Comment out to make the site read absolute links (like from flickr instead of locally).

## Portfolio
- where to change portfolio sidebar: /includes/-sidebar-portfolio.html
- where to change width of portfolio sidebar: layouts/portfolio.html line 58
- if you want to show a sidebar on each of the portfolio pages, change the frontmatter of each portfolio page to sidebar: left and layout: portfolio. to NOT have a sidebar, change sidebar: none and layout: page-fullwidth. i've gone back and forth with this.
- portfolio landing page: pages/portfolio.md
- Gallery / lightbox and how it appears, colors, fonts of captions, etc: -sass/foundation-components/-clearing.scss
- save thumbnails at 200px wide. append -thumb to end of filename.

## Add a new artwork to Portfolio
- resize your illustration to 600px wide. save another thumbnail as 200px wide.

## Sidebar
- sidebar: left shows the portfolio sidebar i created (sidebar-portfolio.html). sidebar: right shows the blog sidebar (-sidebar.html)

## Top navigation
- top navigation: -data/navigation.yml
- top navigation bar colors: -sass/-01_settings_colors.scss
- top nav Set the link colors and styles for top-level nav: sass/foundation components/-top-bar.scss
- top nav font case - upper or lower: -04_settings_global line 1405 $topbar-link-text-transform
- top navigation is called $topbar
- top nav font used: sass/02 search for $nav-font-family

## Header banner
- header banner heights: -sass/-07_layout.scss
- default header banner image: -config.yml
- main page header banner image: pages/pages-root-folder/index.md

## To change the header banner image:
- main page header banner image: pages/index.md (Line 9)
- default header banner image: -config.yml (Line 129) -- Need to rebuild anytime you save changes to config.
- if you want a logo to float in the banner, that goes in index.html in the frontmatter

## Frontpage
- frontpage and 3 widgets: pages/pages-root-folder/index.md

## Footer
- footer content and my social icons: includes/-footer.html
- footer links: -data/network.yml
- footer subscription links: -data/services.yml
- footer social media links: -data/socialmedia.yml
- footer colors: -sass/-01_settings_colors.scss
- footer padding and formatting: -sass/-07_layout.scss
- footer titles: -data/language.yml
- very bottom footer: includes/-footer.html

## Search
- search bar text: -data/language.yml
- what your search page says: pages/search.md

## Global
- colors: -sass/-01_settings_colors.scss
- fonts used: -sass/-02_settings_typography.scss (When you update fonts, hold down CONTROL key when you refresh the page so your updates will show)
- where to set the font icon used on tiny mobile screen: -includes/-navigation.html class="icon-heart"
- how links are displayed: i messed around a lot with this but ended up finding success in putting snippets of whatever i want to override in -sass/-leiahmods.scss

## Where to change BLOG stuff
- blog's header banner image: blog/index.html (you can no longer adjust the banner here)
- blog sidebar, whether or not to show: in -config.yml, line 150 under sidebar: (can be default, left or right)
- sidebar content: -includes/-sidebar.html
- sidebar colors: can't figure out where to change this. doing local styling on -includes/-sidebar.html instead
- default blog post template used: -config.yml under "Default" ascii art. Default applies to everything that is a post. Set your post frontmatter layout to layout: page, and it will automatically be a right-sidebar page.
- how the post snippets look on the blog landing page: -includes/-pagination.html
- "Read More" to say something else: -data/language.yml
- COMMENTS headline at the bottom of each blog post: language.yml. could change to say "let me know what you think!" or something else
- quote blockquote style: -sass/-06_typography.scss, Line 233
- how many # of blog posts show on Blog index: -config.yml line 52 "paginate"
- format of date at the top of individual blog posts: -layouts/page.html, line 11
- format of pagination (blog landing page) includes/pagination.html

## Flickr notes:
- use flickr.com/leiahmjansen for all photos related to this blog. yahoo username is leiahstevie, pw d
- actually i decided to just host all the images myself on github. because flickr is a goddamn mess and a pain in the ass to link to images. i don't have THAT many images, so i'll just put them on gitpages until git tells me to stop it.

## Search entire site:
cmd + shift + f
Will search through the entire site or every tab of pages you have open.
