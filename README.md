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
**Key Takeaways**: learn how to view the page source using any methods.
* Since there is no visible sign of the password on the loaded page, the page source is the next thing we look to.
* To access the page source, right-click on anywhere on the page and select "View page source".
* Tip: CTRL + U is the shortcut key for Chrome web browsers.
* Password for Level 1: gtVrDuiDfck831PqWsLEZy5gyDz1clto

**Natas Level 1 → Level 2**  
**Key Takeaways**: learn how to view the page source using any methods, besides rightclicking.
* The only difference between this level and the previous one is that the right-clicking function has been disabled, i.e. the menu which you see when you right-click no longer appears, and an alert box pops up to state so.
* Method 1: The tip I mentioned in the previous level came in handy here! Find out the shortcut key to view the page source on your web browser by opening another tab/window. (CTRL + U is the shortcut key for Chrome web browsers.)
* Method 2: Find out the shortcut key to inspect elements and expand several sections of the HTML code to find the password. This is a more tedious method than Method 1, but you can play with the elements just to get a feel of how HTML elements work. (CTRL + SHIFT + I is the shortcut key for Chrome web browsers.)
* Method 3: Find a browser extension that enables right-click.
* Password for Level 2: ZluruAthQk7Q2MqmDeTiUij2ZvWy2mBi

**Natas Level 2 → Level 3**    
**Key Takeaways**: learn how to navigate to other files hosted on the same website, even if no direct link is given.
* Rightclicking is enabled for this level, but going to the page source yields no immediate password in our sight.
* However, we see that there is a 1 x 1 image inserted just after the HTML text. I downloaded the image and thought that the password would be found within, but the search should have been focussed back on the page source.
* We see that the image source is "files/pixel.png". This means that the image was stored in the files directory.
* We are at the parent working directory when the page is loaded, thus to navigate to the files directory, add a /files to the website link. We see that there are 2 files in the /files directory, pixel.png and users.txt.
* There are several username and password pairs found in users.txt, including the one for the next level.
* Password for Level 3: sJIJNW6ucpu6HPZ1ZAchaDtwd7oGrD14

**Natas Level 3 → Level 4**  
**Key Takeaways**: learn about the web crawlers and the robot.txt file of a website.
* There are no more files found from the page's source code, as stated by the creator who said that there are now "no more information leaks".
* However, the creator also said that "not even Google will find it this time". This gave a clue into where we should search next.
* Google's site crawlers index sites all over the web, and robots.txt is a text file webmasters create to instruct robots (typically search engine crawlers) how to crawl and index their page.
* We open the robots.txt file of the site, and find that there is a disallowed directory from being crawled - s3cr3t.
* Enter the s3cr3t directory and we find a users.txt file containing the password for the next level.
* Password for Level 4: Z9tkRkWmpt9Qr7XrR5jWRkgOU901swEZ

**Natas Level 4 → Level 5**  
**Key Takeaways**: learn how to modify elements of a website or use Burp Suite Intercept.
**Method 1: Modifying elements of a website**
* When the page is first loaded, the page says that access is disallowed because we did not come from "http://natas5.natas.labs.overthewire.org/". Having the login credentials to the level itself did not allow us to be "authorized users".
* Clicking on the "Refresh page" link on the same page (which is found just below the message) results in a change in the part which states where we visited the page *from*. Clicking it again changes the link again, because the displayed message takes reference from the previous link which we were at, before we visit the natas4 page.
* Since we have to come from the natas5 site in order to be considered an authorized user, we head to the site (albeit with no valid credentials). We do not have to successfully login, just escape the login pop-up box by pressing the Cancel button. A page with the title Unauthorized is displayed.
* We have to visit natas4 from the natas5 site, and since the page (with the title Unauthorized) that is displayed does not have the link to natas4, we have to manually insert it into the page.
* Open up the Developer Tools (CTRL + SHIFT + I for Chrome web browser users) and head to the Elements tab. Here, I will be replacing the `<address>Apache/2.4.10 ...</address>` with the address to natas4.
* Right-click on the part which we will be replacing and select Edit as HTML. We can copy and paste the Refresh link from natas4 to natas5, using it as a template. The code from natas4 is `<a href="index.php">Refresh page</a>`.
* Let us modify it to be `<a href="http://natas4.natas.labs.overthewire.org/">Refresh page</a>`, since we have to visit natas5 from natas4.
* Close the Developer Tools after this is done and click on Refresh page on natas5 Unauthorized site. The password is now shown on the natas4 page.
**Method 2: Use Burp Suite Intercept**
* This method is much shorter in my opinion, but might require some set-up for those who are unfamiliar with Burp Suite. Some might consider that the time in setting up Burp Suite being the same as the time used in editing the webpage in method 1.
* After ensuring that our web browser uses a proxy where Burp Suite is able to intercept requests, we modify the `Referer` part of the HTTP request from `natas4` to `natas5`, since the loading of the natas4 page is requested to be from natas5:
![](/screenshots/natas4.jpg)
* After modifying the one numerical figure, forward the HTTP request, and the password for the next stage is displayed.
* Password for Level 5: iX6IOfmpN7AYOQGPwtn3fXpbaJVJcHfq

**Natas Level 5 → Level 6**  
**Key Takeaways**: learn how to modify a browser cookie's value.
* There are no obvious hints of how we should proceed besides the generic message that we are not logged in. The previous level gave the clue that we were unauthorized because we did not come from a specific page previously, but there was no such hint in this level.
* However, looking at the other tabs on the Developer Tools, we see that there is an Application tab (for Chrome web browser users) with the cookie 'loggedin', whose value is set to 0.
* Using the Chrome web browser, double-clicking on the value allows us to change the value. However, on some occasions, the modified value is not actually retained, i.e. refreshing the page results in the cookie value being set back to 0. Not entirely sure why, but this method did not work when I first attempted this level, but it worked when I came back months later.
* A guaranteed way would be to go to the browser's console on that page, and enter `document.cookie="loggedin=1"`. The console echoes back `loggedin=1`. Refresh the page to obtain the password.
* Alternatively, we can use a Chrome browser extension called EditThisCookie to modify the value of cookies. After changing the value, click on the green tick symbol to save it, and refresh the page to obtain the password.
* Password for Level 6: aGoY4q2Dc6MgDq4oL4YtoKtyAg9PeHa1

**Natas Level 6 → Level 7**  
**Key Takeaways**: learn to read PHP code.
* There is a text field box on the page that allows us to submit the secret value. For a start, by entering random values into the textbox and submitting it, we get the same error message "Wrong secret".
* Next, click on the "View sourecode" to be taken to index-source.html, where we see that there is an if-else statement that gives us our password for the next level if the secret value is correct. We also see that the print statement has the password censored.
* Notice that there is a file that is located at the includes directory, titled secret.inc, that is included at the start of the PHP source code just before the if-else statement.
* We do not have permissions granted to us to see what is in the includes directory, but we are able to access the file `secret.inc` within it:
![](/screenshots/natas6.jpg)
* Submit the string value that was assigned to the secret variable, i.e. `FOEIUWGHFEEUHOFUOIU`, where we will satisfy the `if` condition  and get the password for the next level.
* Password for Level 7: 7z3hEENjQtflzgnT29q7wAvMNfZdh0i9

**Natas Level 7 → Level 8**  
**Key Takeaways**: learn about file path traversal **(not sure if this counts as local file inclusion)**, i.e. how to navigate to other files hosted on the same website, even if no direct link is given.
* This challenge is similar to Level 2 where we have to access files whose links are not explictly given. However, I believe that there is a difference between these 2 levels, where the file we have to access in this level is relative to the path of the PHP file (as we will see below).
* Upon logging in, we are at a page that displays 2 links to `Home` and to `About`. Going to Home changes the weblink to `/index.php?page=home` while going to About changes the weblink to `/index.php?page=about`.
* Opening the page source in any page of this level gives us a hint into the location of the password for the next level, which is `/etc/natas_webpass/natas8`.
* Loading `/index.php?page=/etc/natas_webpass/natas8` solves this level's challenge.
* Password for Level 8: DBfUBfqQG69KvJvJ1iAbMoIpwSNQ9bWe

**Natas Level 8 → Level 9**  
**Key Takeaways**: learn about various forms of encoding such as hexadecimal and base-64 representation.
* This challenge is similar to Level 6 where we are required to submit the secret value before we can get the password to the next level.
* As usual, click on `View sourcecode`, and we see that the password to the next level is similarly censored.
* Our secret value is passed into the function `encodeSecret()` as a parameter, before being converted to a hexadecimal value (`bin2hex`), string reversed (`strrev`) and finally base64-encoded (`base64_encode`). The encoded value is then checked against the $encodedSecret which contains the string 3d3d516343746d4d6d6c315669563362.
* Note: `bin2hex` does not convert a string from binary to hexadecimal form. Reading up the PHP documentation tells us that it returns the hexadecimal representation of a given string. This is made more explicit when we go to the documentation page for `hex2bin`, where there is a cautionary note to highlight this point.
* To reverse-engineer the secret value out of $encodedSecret, we have to first run hex2bin against $encodedSecret. We can use an online PHP function to execute this, to get the string `==QcCtmMml1ViV3b`.
* Note: hex2bin can only be executed in an environment where the PHP version is >= 5.4.0.
* Next, reverse the string using any tool that you can get your hands on (or manually do it since the string is short), to get `b3ViV1lmMmtCcQ==`.
* Finally, do a base64-decode on the reversed string to get `oubWYf2kBq`, which is the correct $secret.
* Note: The PHP documentation page for base64_encode() states that the data is encoded with MIME base64. When using any online base64 decoder, you can choose the source character set to be UTF-8 or ASCII, and the decoding will still work successfully.
* Password for Level 9: W0mMhUcRRnG8dcghE4qvk3JA9lGt8nDl

**Natas Level 9 → Level 10**  
**Key Takeaways**: learn how unsanitised user input can result in OS command injection.
* As literal as it states, we are able to type characters into the search box, and a list of words containing the characters that we type in will be displayed as the output. We enter the word password for searching, and only 3 results appear, none of which are the passwords. Searching for natas or natas10 yields no useful results similarly.
* Head to the view the source code, and we see that the file which our characters are searched against is `dictionary.txt`. Looking into the dictionary.txt file, we do not find the password for the next level either.
* Head back to the search feature and we notice that one of the weblink's parameter changes whenever our search string changes: `?needle=<our_search_string>&submit=Search`. Given that the user input forms the request parameters, there is a chance that the user input is unsanitised, i.e. used verbatim.
* Looking at the source code, our input is assigned to $key, and the search occurs against dictionary.txt using the `grep` command. Notice that the PHP function `passthru` allows the Unix command to be executed.
* This PHP function "executes an external program and displays raw output" according to the PHP online documentation. The first warning under the Notes section tells users that user-supplied data being passed to the function must first be sanitised, to prevent the system from being tricked into executing arbitrary commands.
**Method 1: Using grep**
* This is our crafted search string: `"0" /etc/natas_webpass/natas10`, which is meant to search for a numeric character that exists within the natas10 password file, and a hit would return the entire password that contains this character.
* The source code would look like this after inserting our crafted string: `passthru("grep -i "0" /etc/natas_webpass/natas10 dictionary.txt")`. While we were searching for characters within the password file, search matching was also done with the dictionary text file. This is fine.
* We did not have to make too many attempts at this (2 attempts in total only) because the password contained the numeric value `1`, and we started at `0`. In the event where there are no numbers in the password, we would have to try entering both upper and lower-case alphabets till we get a hit.
**Method 2: Using cat**
* Since the parameter being passed to passthru is/are command(s) being executed in a Unix environment, we can use `;` to truncate the grep command and add our own ones after it.
* Our additional command is `cat /etc/natas_webpass/natas10`, where I guess the password would be stored, since this was the location previously given in level 7.
* Thus, our specially crafted search string is `; cat /etc/natas_webpass/natas10`.
* This is what the source code would look like with our search string in it: `passthru("grep -i ; cat /etc/natas_webpass/natas10 dictionary.txt")`. The `grep` command would result in an error because no file was specified, and our `cat` command would be successfully executed.
* After pressing Search, the password for the next level is found on the first line of the output, and the entire dictionary text file is displayed because 2 file names were specified after `cat`.
* I thought of method 1 first, but did not manage to get it working for a long while because I was wrongly focussing on trying to make the rest of the command after our string into a comment.
* *Fun-fact*: We can add an additional whitespace and a `#` after the search string for both methods 1 and 2, so that only our password file is loaded. The `#` character marks the rest of the string after it as being a comment. The whitespace is also required, or the `#` character would have a different effect and be interpreted as being part of the file name. Note: `//` does not work here.
* Password for Level 10: nOpp1igQAkUzaI1GUUjzn1bFVj7xCNzu

**Natas Level 10 → Level 11**  
**Key Takeaways**: very similar to previous level, involving OS command injection.
* The exact same piece of code is used here when we compare it with the previous level's, with the exception of the checking of illegal characters in the user's input by using PHP's `preg_match()` (i.e. some form of user sanitisation).
* 3 characters such as `;`, `|` and `&` are checked for (not a lot at all), and the passthru() function will not be executed if any of these characters are found.
* Since the semi-colon character cannot be used, method 2 from the previous level would not work. However, method 1 still works here because its use of `"` characters is not prohibited here.
* Similarly, we only have to make 2 attempts because there is a numeric character `1` in the password: `"1" /etc/natas_webpass/natas11`.
* Password for Level 11: U82q5TCMMQ9xuFoI3dYX61s7OZD9JKoK
