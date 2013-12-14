# Diet: Dictionary
With the dictionary module you can translate your app into any language using the `echo()` function and the `dictionary` table inside your mysql database.

### Install
If you have `dietjs` then it's already installed.
```
npm install diet-dictionary
```

### Prerequsitions
1. Make sure you have `mysql` installed
2. Make sure you have `dietjs` installed
3. Make sure you have correct `mysql configuration` when you initialize your `dietjs` app
4. Create a `dictionary` table inside your mysql database

### Example `dictionary` table
If you want to support more languages just create a new `column` for it and restart the server.

English | Hungarian | Spanish
---|---|---
Hello | Szia | Hola
How are you? | Hogy vagy? | ¿Cómo estás?
 
### Example Backend Usage 
```javascript
var app = new Application(options);

app.get('/', function(request, response, mysql){
	// DEFINE language
	response.head.language = 'Hungarian';
	
	// Translate string
	response.head.title = message = response.head.echo('Hello World');
	
	// End HTTP Response
	response.end(response.head.title); // -> outputs "Üdv Világ!"
	mysql.end();
});
```

### Example Usage in HTML
```html
<!DOCTYPE html/>
<html>
	<head>
		<title>{{-echo @title}}</title><!-- outputs: "Üdv Világ" -->
	</head> 
	<body>
		<h1>{{-echo @title}}</h1> <!-- outputs: "Üdv Világ" -->
		<p>{{-echo 'How are you?'}}</p> <!-- outputs: "Hogy vagy?" -->
	</body>
</html>
```
### Example Usage in Client Side JS
You will need to include the `dictionary.js` files which is autogenerated for you in:
```
/your_app/resources/scripts/dictionary.js
```
This is how it looks like:
```html
<!DOCTYPE html/>
<html>
	<head>
		<title>Piece of Cake</title>
		<!-- Just Include the Auto Generated dictionary.js file -->
		<script src="/scripts/dictionary.js"></script>
		
		<!-- Then start using the echo function to translate things -->
		<script>
			var message = echo('Hello World');
			alert(message); // alerts: "Üdv Világ"
		</script>
	</head>
	<body>diet is awesome</body>
</html>
```
You can see what's the current language in `window.language` set within `dictionary.js`. You can change the language by changing `response.head.language` in html and `response.cookies.set('language', 'yourLanguage')` for client side javacsript.
