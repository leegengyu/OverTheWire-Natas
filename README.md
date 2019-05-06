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
* Go to the browser's console on that page, and enter `document.cookie="loggedin=1"`. The console echoes back `loggedin=1`. Refresh the page to obtain the password.
* Alternatively, we can use a Chrome browser extension called EditThisCookie to modify the value of cookies. After changing the value, click on the green tick symbol to save it, and refresh the page to obtain the password.
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
* This challenge is similar to Level 2 where we have to access files whose links are not explictly given. However, I believe that there is a difference between these 2 levels, where the file we have to access in this level is relative to the path of the PHP file (as we will see below).
* Upon logging in, we are at a page that displays 2 links to `Home` and to `About`. Going to Home changes the weblink to `/index.php?page=home` while going to About changes the weblink to `/index.php?page=about`.
* Opening the page source of either of the 2 links, and there is a hint that says where the password for the next level is found in `/etc/natas_webpass/natas8`.
* Instead of going to home or about (which is the last parameter of the weblink), we want to go to /etc/natas_webpass/natas8, and thus, we have our password displayed.
* Password for Level 8: DBfUBfqQG69KvJvJ1iAbMoIpwSNQ9bWe

**Natas Level 8 → Level 9**  
Input secret:  
**Key Takeaways**: learn how to read PHP code and use functions such as bin2hex/hex2bin, strrev and base64_encode/base64_decode.
* This challenge is similar to Level 6 where we are required to submit the secret value before we can get the password to the next level.
* As usual, click on `View sourcecode`, and we see that the password to the next level is similarly censored.
* Our secret value is passed into the function `encodeSecret()` as a parameter, before being converted to a hexadecimal value (`bin2hex`), string reversed (`strrev`) and finally base64-encoded (`base64_encode`). The encoded value is then checked against the $encodedSecret which contains the string 3d3d516343746d4d6d6c315669563362.
* Note: bin2hex does not convert a *binary number* to a hexadecimal number. According to the PHP online documentation, it returns the hexadecimal representation of the given *string*, not a number. This is made more explicit when we go to the documentation page for hex2bin, where there is a cautionary note to highlight this point.
* To reverse-engineer the secret value out of $encodedSecret, we have to first run hex2bin against $encodedSecret. We can use an online PHP function to execute this, to get the string `==QcCtmMml1ViV3b`.
* Note: hex2bin can only be executed in an environment where the PHP version is >= 5.4.0.
* Next, reverse the string using any tool that you can get your hands on (or manually do it since the string is short), to get `b3ViV1lmMmtCcQ==`.
* Finally, do a base64-decode on the reversed string to get `oubWYf2kBq`, which is the correct $secret.
* Note: The PHP documentation page for base64_encode() states that the data is encoded with MIME base64. When using any online base64 decoder, you can choose the source character set to be UTF-8 or ASCII, and the decoding will still work successfully.
* Password for Level 9: W0mMhUcRRnG8dcghE4qvk3JA9lGt8nDl

**Natas Level 9 → Level 10**  
Find words containing:  
**Key Takeaways**: learn how unsanitised user input can be manipulated to be used as a command.
* As literal as it states, we are able to type characters into the search box, and a list of words containing the characters that we type in will be displayed as the output. We enter the word password for searching, and only 3 results appear, none of which are the passwords. Searching for natas or natas10 yields no useful results similarly.
* Head to the view the source code, and we see that the file which our characters are searched against is `dictionary.txt`. ooking into the dictionary.txt file, we do not find the password for the next level either.
* Head back to the search feature and we notice that one of the weblink's parameter changes whenever our search string changes: `?needle=<our_search_string>&submit=Search`. Given that the user input forms the request parameters, there is a chance that the user input is unsanitised, i.e. used verbatim.
* Looking at the source code, our input is assigned to $key, and the search occurs against dictionary.txt using the `grep` command. Notice that the PHP function `passthru` allows the Unix command to be executed.
* This PHP function "executes an external program and displays raw output" according to the PHP online documentation. The first warning under the Notes section tells users that user-supplied data being passed to the function must first be sanitised, to prevent the system from being tricked into executing arbitrary commands.
* On first thought, this was my crafted search string: `"0" /etc/natas_webpass/natas10"); //`. This crafted string was meant to search for a numeric character that exists within the password file, and to return the entire password that contains this character. The double slash at the end was to mark the rest of the line as a comment, so that it would not be executed.
* The result should look like this: `passthru("grep -i "0" /etc/natas_webpass/natas10"); // dictionary.txt");`.
* What I had in mind was to repeat this search a couple of times with different numbers from 0 to 9, since the password is likely to have numerical values.
* However, this method did not work (I am not sure why either).
* **To return later to investigate again.**
* Since the parameter being passed to passthru is/are command(s) being executed in a Unix environment, we can use `;` to separate the current grep command and to include our own one.
* Our additional command is `cat /etc/natas_webpass/natas10`.
* Thus, the final crafted search string is `; cat /etc/natas_webpass/natas10`, and after pressing Search, the password for the next level is found on the first line.
* We can add an additional whitespace and a `#` after the search string to mark the rest of the contents as a comment, so the dictionary.txt file would not be fully displayed as the output as well. Note: `//` is not the way to indicate comments here.
* Password for Level 10: nOpp1igQAkUzaI1GUUjzn1bFVj7xCNzu

**Natas Level 10 → Level 11**  
For security reasons, we now filter on certain characters  
Find words containing: 
**Key Takeaways**: learn how unsanitised user input can be manipulated to deviate from the intended usage of a command.
* This challenge is similar to the previous level where the exact same piece of code is used, with the exception of the checking of illegal characters in the user's input by using PHP's `preg_match()` (i.e. some form of user sanitisation).
* Characters such as `;`, `\` and `&` are checked for, and the passthru() function will not be executed if any of these characters are found. Thus the crafted search string used in the previous level cannot be used for this level because its first character is considered an illegal character in this level.
* Since the semi-colon character cannot be used, our own commands cannot be introduced, since we cannot separate our own ones (i.e. cat) from grep.
* With that, I found out that the method which did not work for me in the previous level is actually the puzzle-solver for this level.
* I modified my crafted search string to be: `"0" /etc/natas_webpass/natas11`, after getting inspiration from the previous level's working method to comment out the dictionary.txt, instead of ending the entire line by myself prematurely.
* Entering this search string does not work because there is no numberical value 0 in the password. When we change 0 to 1, the password appears because there is a numeric value 1 in the password. In unlucky cases where the numbers are bigger, we would have to attempt more guesses if we start from the number 0.
* Note: You can add a whitespace and a `#` to remove the location of the password file from the output.
* Password for Level 11: U82q5TCMMQ9xuFoI3dYX61s7OZD9JKoK
