# OverTheWire-Natas
This repository contains a guide to completing the Natas levels in the OverTheWire wargames.  

Each level of natas consists of its own website located at http://natasX.natas.labs.overthewire.org, where X is the level number.  

To access a level, enter the username for that level (e.g. natas0 for level 0) and its password.

This repository serves as:
1) Documentation of the methods which I used and the thought process as I solve the Natas level challenges from OverTheWire wargames.
2) Revision guide based on the key takeaways from solving each challenge.

Each level of the walkthrough guide summarises the:
1) Level Goal (taken verbatim from each level's website)
2) Key Takeaways
3) Alternatives (if any)
4) Common misconceptions (if any)

# Walkthrough Guide
**Natas Level 0 → Level 1**  
You can find the password for the next level on this page.  
**Key Takeaways**: learn how to view the page source using any methods.
* Since there is no visible sign of the password on the loaded page, the page source is the next thing we look to.
* To access the page source, right-click on anywhere on the page and select "View page source".
* Tip: CTRL + U is the shortcut key for Chrome web browsers.
* Password for Level 1: gtVrDuiDfck831PqWsLEZy5gyDz1clto

**Natas Level 1 → Level 2**  
You can find the password for the next level on this page, but rightclicking has been blocked!  
**Key Takeaways**: learn how to view the page source using any methods, besides rightclicking.
* The only difference between this level and the previous one is that the right-clicking function has been disabled, i.e. the menu which you see when you right-click no longer appears, and an alert box pops up to state so.
* Method 1: The tip I mentioned in the previous level came in handy here! Find out the shortcut key to view the page source on your web browser by opening another tab/window. (CTRL + U is the shortcut key for Chrome web browsers.)
* Method 2: Find out the shortcut key to inspect elements and expand several sections of the HTML code to find the password. This is a more tedious method than Method 1, but you can play with the elements just to get a feel of how HTML elements work. (CTRL + SHIFT + I is the shortcut key for Chrome web browsers.)
* Method 3: Find a browser extension that enables right-click.
* Password for Level 2: ZluruAthQk7Q2MqmDeTiUij2ZvWy2mBi

**Natas Level 2 → Level 3**  
There is nothing on this page  
**Key Takeaways**: learn how to navigate to other files hosted on the same website, even if no direct link is given.
* Rightclicking is enabled for this level, but going to the page source yields no immediate password in our sight.
* However, we see that there is a 1 x 1 image inserted just after the HTML text. I downloaded the image and thought that the password would be found within, but the search should have been focussed back on the page source.
* We see that the image source is "files/pixel.png". This means that the image was stored in the files directory.
* We are at the parent working directory when the page is loaded, thus to navigate to the files directory, add a /files to the website link. We see that there are 2 files in the /files directory, pixel.png and users.txt.
* There are several username and password pairs found in users.txt, including the one for the next level.
* Password for Level 3: sJIJNW6ucpu6HPZ1ZAchaDtwd7oGrD14

**Natas Level 3 → Level 4**  
There is nothing on this page  
**Key Takeaways**: learn about the web crawlers and the robot.txt file of a website.
* There are no more files found from the page's source code, as stated by the creator who said that there are now "no more information leaks".
* However, the creator also said that "not even Google will find it this time". This gave a clue into where we should search next.
* Google's site crawlers index sites all over the web, and robots.txt is a text file webmasters create to instruct robots (typically search engine crawlers) how to crawl and index their page.
* We open the robots.txt file of the site, and find that there is a disallowed directory from being crawled - s3cr3t.
* Enter the s3cr3t directory and we find a users.txt file containing the password for the next level.
* Password for Level 3: Z9tkRkWmpt9Qr7XrR5jWRkgOU901swEZ
