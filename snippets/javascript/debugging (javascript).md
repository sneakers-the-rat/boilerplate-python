## Show all variables in [[scope]]

In [[Firefox]]
- List Variables: `keys(window)`

In [[Chrome]]
- List Variables: `keys(window)`
- List objects: `dir(window)`

### To show only non-standard attributes
Make a new iframe within the page to get standard variables, then find the ones that aren't in that!
[source: max-heiber](https://stackoverflow.com/a/22771158)
[source: james-morgan](https://stackoverflow.com/a/40417003)
```javascript

function getNewVariables(){
	var iframe = document.createElement('iframe');
	iframe.src = 'about:blank';
	document.body.appendChild(iframe);

	let standardGlobals = new Set(Object.keys(iframe.contentWindow))
	
	
	return  Object.entries(window).filter(k => 
			!standardGlobals.has(k[0])
		)
}

```

	