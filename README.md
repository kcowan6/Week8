# Project 8 - Pentesting Live Targets

Time spent: **1.5** hours spent in total

> Objective: Identify vulnerabilities in three different versions of the Globitek website: blue, green, and red.

The six possible exploits are:
* Username Enumeration
* Insecure Direct Object Reference (IDOR)
* SQL Injection (SQLi)
* Cross-Site Scripting (XSS)
* Cross-Site Request Forgery (CSRF)
* Session Hijacking/Fixation

Each version of the site has been given two of the six vulnerabilities. (In other words, all six of the exploits should be assignable to one of the sites.)

## Blue

Vulnerability #1 - SQL Injection: A lack of input sanitization allows for hackers to use SQL Injection techniques that will not be caught by the site.  If we use %27%20OR%20SLEEP(5)=0--%27 for the id field in the url, we can delay the page by forcing it to sleep for 5 seconds before it automatically resets to Daron Burke's page.

GIF Walkthrough: <img src='https://media.giphy.com/media/3o7aD8C3yG8WM8D9W8/giphy.gif' title='GIF Walkthrough Blue 1' width='' alt='GIF Walkthrough Blue 1' />

Vulnerability #2 - Session Hijacking/Fixation: With the Blue site, if one logged onto the Red site with the Red site opened in a different tab, if you clicked the "Login" menu for the Red site, the user would already be on the admin page without ever having to actually input the login credentials.

GIF Walkthrough: <img src='https://media.giphy.com/media/3ov9k8EZSdYuVWMAF2/giphy.gif' title='GIF Walkthrough Blue 2' width='' alt='GIF Walkthrough Blue 2' />


## Green

Vulnerability #1 - Username Enumeration: When a known username is used, but with an incorrect password, the failure message "Log in was unsuccessful" will show up in bold. When a username like jokie is used, the message is not bolded, meaning that the user can know if the username they are inputting is valid in the system.

GIF Walkthrough: <img src='https://media.giphy.com/media/l378alnKoX6FPrY3u/giphy.gif' title='GIF Walkthrough Green 1' width='' alt='GIF Walkthrough Green 1' />

Vulnerability #2 - Cross-Site Scripting: Under the "Contact" menu, if you input <script>alert('KC found the XSS!');</script> into the comments box and login as admin to look at the corresponding feedback, the alert message will popup.

GIF Walkthrough: <img src='https://media.giphy.com/media/xT9IgAZtNKKaI757Uc/giphy.gif' title='GIF Walkthrough Green 2' width='' alt='GIF Walkthrough Green 2' />


## Red

Vulnerability #1 - Insecure Direct Object Reference: When you look at the "Find a Salesperson" menu, you get a list of repeated employee names. In the url link, there is a field labeled id=some number, where the number represents the person.  For the list, the ID numbers are as follows:
ID 1 - Daron Burke
ID 2 - Sherry Trevino
ID 3 - Irene Boling
ID 4 - Robert Hamilton
ID 5 - Ken Barker
ID 6 - Elizabeth Olson
ID 7 - Samuel Hunter
ID 8 - Kim Stanley
ID 9 - Barbara Hinckley
On the Red site, if you change the id number to 10, you can see the non-public page for Testy McTesterton.  If the id number is 11, you see the non-public page for Lazy Lazyman.  These users were disabled on the Green and Blue sites, leaving the Red site open to an IDOR attack.

GIF Walkthrough: <img src='https://media.giphy.com/media/l378s2kAIDYvHZaa4/giphy.gif' title='GIF Walkthrough Red 1' width='' alt='GIF Walkthrough Red 1' />

Vulnerability #2 - Cross-Site Request Forgery: If a link to a malicious form is uploaded through the comments section of the Contact form, once the admin has logged in and accessed this form, the information for the user Ken Barker should be altered accordingly, exposing a major attack avenue on the page.

GIF Walkthrough: <img src='https://media.giphy.com/media/3o7aD8L8Lk0fnERwQM/giphy.gif' title='GIF Walkthrough Red 2' width='' alt='GIF Walkthrough Red 2' />


## Notes
