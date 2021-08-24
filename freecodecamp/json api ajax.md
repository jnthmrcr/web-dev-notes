# Handle Click Events with JavaScript using the onclick property

You want your code to execute only once your page has finished loading. For that purpose, you can attach a JavaScript event to the document called `DOMContentLoaded`
```js
document.addEventListener('DOMContentLoaded', function() { });
```

You can implement event handlers that go inside of the `DOMContentLoaded` function. You can implement an `onclick` event handler which triggers when the user clicks on the element with id `getMessage`, by adding the following code:
```js
document.getElementById('getMessage').onclick = function(){ };
```

# Change Text with click Events
When the click event happens, you can use JavaScript to update an HTML element.
```js
document.addEventListener('DOMContentLoaded', function(){
	document.getElementById('getMessage').onclick = function(){
		document.getElementsByClassName('message')[0].textContent="Here is the message"
	}
});
```
# Get JSON with the JavaScript XMLHttpRequest Method
You can also request data from an external source. This is where APIs come into play.

Most web APIs transfer data in a format called JSON.

JSON transmitted by APIs are sent as `bytes`, and your application receives it as a `string`. These can be converted into JavaScript objects, but they are not JavaScript objects by default. The `JSON.parse` method parses the string and constructs the JavaScript object described by it.

You can request the JSON from freeCodeCamp's Cat Photo API:
```js
const req = new XMLHttpRequest();
req.open("GET",'/json/cats.json',true);
req.send();
req.onload = function(){
  const json = JSON.parse(req.responseText);
  document.getElementsByClassName('message')[0].innerHTML = JSON.stringify(json);
};
```
The JavaScript `XMLHttpRequest` object has a number of properties and methods that are used to transfer data. First, an instance of the `XMLHttpRequest` object is created and saved in the `req` variable.

Next, the `open` method initializes a request - this example is requesting data from an API, therefore is a `GET` request. The second argument for `open` is the URL of the API you are requesting data from. The third argument is a Boolean value where `true` makes it an asynchronous request. 

The `send` method sends the request.

Finally, the `onload` event handler parses the returned data and applies the `JSON.stringify` method to convert the JavaScript object into a string. This string is then inserted as the message text.

# Get JSON with the JavaScript fetch method
`fetch()` is equivalent to `XMLHttpRequest`, but the syntax is considered easier to understand.

Here is the code for making a GET request to `/json/cats.json`

```js
fetch('/json/cats.json')
	.then(response => response.json())
	.then(data => {
		document.getElementById('message').innerHTML = JSON.stringify(data);
	})
```
The first line is the one that makes the request. So, `fetch(URL)` makes a `GET` request to the URL specified. The method returns a Promise.

After a Promise is returned, if the request was successful, the `then` method is executed, which takes the response and converts it to JSON format.

The `then` method also returns a Promise, which is handled by the next `then` method. The argument in the second `then` is the JSON object you are looking for!

Now, it selects the element that will receive the data by using `document.getElementById()`. Then it modifies the HTML code of the element by inserting a string created from the JSON object returned from the request.

# Access the JSON Data from an API
>gonna hit you with a big "its not that hard bro" ¯\\_(ツ)_/¯
```js
document.addEventListener('DOMContentLoaded', function(){
	document.getElementById('getMessage').onclick = function(){
	const req = new XMLHttpRequest();
	req.open("GET",'/json/cats.json', true);
	req.send();
	req.onload=function(){
		const json = JSON.parse(req.responseText);
		document.getElementsByClassName('message')[0].innerHTML = 
		// Add your code below this line
		json[2].codeNames[1];
		// Add your code above this line
		};
	};
});
```

# Convert JSON Data to HTML
you can loop over json? i didn't know what this lesson wanted but it makes sense??
```js
<script >
  document.addEventListener('DOMContentLoaded', function() {
    document.getElementById('getMessage').onclick = function() {
      req = new XMLHttpRequest();
      req.open("GET", '/json/cats.json', true);
      req.send();
      req.onload = function() {
        json = JSON.parse(req.responseText);
        var html = "";
        // Add your code below this line

        json.forEach(function(val) {

          // Adding each object keys
          var keys = Object.keys(val);
          // Generating new html
          html += "<div class = 'cat'>";
          // Adding the custom html to each key
          keys.map(function(key) {

            html += "<strong>" + key + "</strong>: " + val[key] + "<br>";

          });

          html += "</div><br>";

        });

        // Add your code above this line
        document.getElementsByClassName('message')[0].innerHTML = html;
      };
    };
  });
</script>
```

# Render Images from Data Sources
When you're looping through these objects, you can use this `imageLink` property to display this image in an `img` element.
> this is specific to this example API
```js
html += "<img src = '" + val.imageLink + "' " + "alt='" + val.altText + "'>";
```
> again, lot of 'no duh' shit

# Pre-filter JSON to Get the Data You Need
Given that the JSON data is stored in an array, you can use the `filter` method to filter out the cat whose `id` key has a value of `1`.
```js
json = json.filter(function(val) {
  return (val.id !== 1);
});

// or

json = json.filter((x)=>{return (x.id != 1);});
```

# Get Geolocation Data to Find A User's GPS Coordinates

Every browser has a built in navigator that can give you your user's current location. The navigator will get the user's current longitude and latitude.
```js
if (navigator.geolocation) {
  navigator.geolocation.getCurrentPosition(function(position) {
    $("#data").html("latitude: " + position.coords.latitude + "<br>longitude: " + position.coords.longitude);
  });
}
```

# Post Data with the JavaScript XMLHttpRequest Method

You can also send data to an external resource, as long as that resource supports AJAX requests and you know the URL.

JavaScript's `XMLHttpRequest` method is also used to post data to a server. Here's an example:
```js
const xhr = new XMLHttpRequest();
xhr.open('POST', url, true);
xhr.setRequestHeader('Content-Type', 'application/json; charset=UTF-8');
xhr.onreadystatechange = function () {
  if (xhr.readyState === 4 && xhr.status === 201){
    const serverResponse = JSON.parse(xhr.response);
    document.getElementsByClassName('message')[0].textContent = serverResponse.userName + serverResponse.suffix;
  }
};
const body = JSON.stringify({ userName: userName, suffix: ' loves cats!' });
xhr.send(body);
```

the `open` method initializes the request as a `POST` to the given URL of the external resource, and uses the `true` Boolean to make it asynchronous.

The `setRequestHeader` method sets the value of an HTTP request header, which contains information about the sender and the request. It must be called after the `open` method, but before the `send` method. The two parameters are the name of the header and the value to set as the body of that header.

Next, the `onreadystatechange` event listener handles a change in the state of the request. A `readyState` of 4 means the operation is complete, and a `status` of `201` means it was a successful request. The document's HTML can be updated.

Finally, the `send` method sends the request with the body value, which the `userName` key was given by the user in the `input` field.

>idk u say these things as if i understand any of them
