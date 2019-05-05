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
* Password for Level 0: natas0  

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
* Password for Level 4: Z9tkRkWmpt9Qr7XrR5jWRkgOU901swEZ

**Natas Level 4 → Level 5**  
Access disallowed. You are visiting from "" while authorized users should come only from "http://natas5.natas.labs.overthewire.org/"  
**Key Takeaways**: learn how to modify elements of a website.
* When the page is first loaded, the page says that access is disallowed because we did not come from "http://natas5.natas.labs.overthewire.org/". Having the login credentials to the level itself did not allow us to be "authorized users".
* Clicking on the "Refresh page" link on the same page (which is found just below the message) results in a change in the part which states where we visited the page *from*. Clicking it again changes the link again, because the displayed message takes reference from the previous link which we were at, before we visit the natas4 page.
* Since we have to come from the natas5 site in order to be considered an authorized user, we head to the site (albeit with no valid credentials). We do not have to successfully login, just escape the login pop-up box by pressing the Cancel button. A page with the title Unauthorized is displayed.
* We have to visit natas4 from the natas5 site, and since the page (with the title Unauthorized) that is displayed does not have the link to natas4, we have to manually insert it into the page.
* Open up the Developer Tools (CTRL + SHIFT + I for Chrome web browser users) and head to the Elements tab. Here, I will be replacing the `<address>Apache/2.4.10 ...</address>` with the address to natas4.
* Right-click on the part which we will be replacing and select Edit as HTML. We can copy and paste the Refresh link from natas4 to natas5, using it as a template. The code from natas4 is `<a href="index.php">Refresh page</a>`.
* Let us modify it to be `<a href="http://natas4.natas.labs.overthewire.org/">Refresh page</a>`, since we have to visit natas5 from natas4.
* Close the Developer Tools after this is done and click on Refresh page on natas5 Unauthorized site. The password is now shown on the natas4 page.
* Password for Level 5: iX6IOfmpN7AYOQGPwtn3fXpbaJVJcHfq

**Natas Level 5 → Level 6**  
Access disallowed. You are not logged in  
**Key Takeaways**: learn how to modify a cookie's value.
* There are no obvious hints of how we should proceed besides the generic message that we are not logged in. The previous level gave the clue that we were unauthorized because we did not come from a specific page previously, but there was no such hint in this level.
* However, looking at the other tabs on the Developer Tools, we see that there is an Application tab (for Chrome web browser users) with the cookie 'loggedin', whose value is set to 0.
* Using the chrome web browser, double-clicking on the value allows us to change the value, but the modified value is not actually retained, i.e. refreshing the page results in the cookie value being set back to 0. I think that this is a security measure by the Chrome developers.
* I used a Chrome browser extension called EditThisCookie to modify the value of the cookie 'loggedin' to 1. After changing the value, click on the green tick symbol to save it, and refresh the page to obtain the password.
* Password for Level 6: aGoY4q2Dc6MgDq4oL4YtoKtyAg9PeHa1

**Natas Level 6 → Level 7**  
Input secret:  
**Key Takeaways**: learn how to read PHP code.
* There is a text field box on the page that allows us to submit the secret value. For a start, by entering random values into the textbox and submitting it, we get the same error message "Wrong secret".
* Next, click on the "View sourecode" to be taken to index-source.html, where we see that there is an if-else statement that gives us our password for the next level if the secret value is correct. We also see that the print statement has the password censored.
* Notice that there is a file that is located at the includes directory, titled secret.inc, that is included at the start of the PHP source code just before the if-else statement.
* We do not have permissions granted to us to see what is in the includes directory, but we are able to get the secret value ($secret) by accessing the file, by adding /includes/secret.inc to the original link.
* `$secret = "FOEIUWGHFEEUHOFUOIU";`
* Submit the secret value and we get the password for the next level.
* Password for Level 7: 7z3hEENjQtflzgnT29q7wAvMNfZdh0i9

**Natas Level 7 → Level 8**  
Home About  
**Key Takeaways**: learn how to navigate to other files hosted on the same website, even if no direct link is given.
* This challenge is similar to that of Level 2 where we have to access files whose links are not explictly given. However, I believe that there is a difference between these 2 levels, where the file we have to access in this level is relative to the path of the PHP file (as we will see below).
* Upon logging in, we are at a page that displays 2 links to `Home` and to `About`. Going to Home changes the weblink to `/index.php?page=home` while going to About changes the weblink to `/index.php?page=about`.
* Opening the page source of either of the 2 links, and there is a hint that says where the password for the next level is found in `/etc/natas_webpass/natas8`.
* Instead of going to home or about (which is the last parameter of the weblink), we want to go to /etc/natas_webpass/natas8, and thus, we have our password displayed.
* Password for Level 8: DBfUBfqQG69KvJvJ1iAbMoIpwSNQ9bWe
