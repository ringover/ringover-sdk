# Ringover SDK

Import easily the **[ringover web app][0]** iframe into your own project (like your crm)

You need a **[ringover account][13]** to properly use the following features.

<br>

## Installation
  

Standalone file is available on:

[https://webcdn.ringover.com/resources/SDK/1.1.1/ringover-sdk.js](https://webcdn.ringover.com/resources/SDK/1.1.1/ringover-sdk.js)


Also the package is available on npm as _ringover-sdk_

[https://www.npmjs.com/package/ringover-sdk](https://www.npmjs.com/package/ringover-sdk)

<br>

## Setup

  

### Browser

  

```html

<script  src="ringover-sdk.js"  type="text/javascript"></script>

```

```js

const  simpleSDK = new  window.RingoverSDK();
// ...

```

  
  

### Node.js

  

```sh

npm install --save ringover-sdk

```

```js

const RingoverSDK = require("ringover-sdk");
const simpleSDK = new RingoverSDK();
// ...

```

  

### ES6 / Webpack

  

```js

import RingoverSDK from "ringover-sdk";
const simpleSDK = new RingoverSDK();

// ...
```

  
  

### AMD

  

```js

require(["ringover-sdk"], function(RingoverSDK) {
    const simpleSDK = new RingoverSDK();
    //...
});

```

<br>

## Usage

```js

// Set options
const options = {animation: false, size: "auto"};

// Create instance
const simpleSDK = new window.RingoverSDK(options);

// Generate iframe
simpleSDK.generate();

// Set event
simpleSDK.on("ringingCall", (e) => console.log("Call with from number: " + e.data.from_number);

// Check iframe status
simpleSDK.checkStatus();

```
<br>
  
## Configuration

```js

new RingoverSDK({

	// "fixed", "relative", "absolute"
	type: "fixed",
	
	// "big", "medium", "small", "auto"
	size: "medium",
	
	container: null,
	
	position: {
		top: 	null,
		bottom: "50px"
		left: 	null,
		right: 	"50px"
	},
	
	// true, false
	border: true,

	// true, false
	animation: true,

	// "rgb(0,0,0)", "#eee", "red"
	backgroundColor: "transparent",

	// true, false
	trayicon: true,

	trayposition: {
		top: 	null,
		bottom: "10px"
		left: 	null,
		right: 	"10px"
	},
});

```

### new RingoverSDK({options})

All option properties are optional.

<br>

## Options

 ###  `type`: **[string][1]**
 
 * [CSS position][2] type.  
 * Can be one of the following : `["fixed", "relative", "absolute"]`.   
  * Default is  `"fixed"`.  

 ### `size`: **[string][1]**
 
* Size of iframe.  
* Can be one of the following : `["big", "medium", "small", "auto"]`. 
* Default is `"medium"`.
	* `big`: L: 1050px, H: 750px
	* `medium`: L: 380px, H: 620px
	* `small`: L: 350px, H: 500px
	* `auto`: L: 100% of container, H: 100% of container

 ### `container`: **[string][1]** 
  * Element id of container. 
  * Default is `null`. 
  * If the container is null the **[document.body][8]** is chosen by default.

 ### `position`: **[object][3]**
  * Object of css position:
    * **[`position.top`][4]**: **[string][1]** 
    * **[`position.bottom`][5]**: **[string][1]** 
    * **[`position.left`][6]**: **[string][1]** 
    * **[`position.right`][7]**: **[string][1]** 
  * If `size` is `"auto"` or `"big"` or if `container` is filled, default position value is `{top: "0", left: "0"}`
  * If `size` is `"medium"` or `"small"`, default position value is `{bottom: "0", right: "64px"}`

 ### `backgroundcolor` : **[string][1]**
  * Choose your background iframe color (only visible if trayicon is enable)
  * Can be any [CSS background color][14] format in string
  * Default is `"transparent"`
  
 ### `border`: **[boolean][9]**
  * Choose if you want to display the border of the iframe.
  * Default is `true`.

 ### `animation`: **[boolean][9]**
  * Choose if you want to have an animation when the iframe shows and hides
  * Default is `true`.

 ### `trayicon`: **[boolean][9]**
  * Choose if you want to display a button to show and hide the iframe.
  * Default is `true`.

 ### `trayposition`: **[object][3]**
  * Object of css position:
    * **[`position.top`][4]**: **[string][1]** 
    * **[`position.bottom`][5]**: **[string][1]** 
    * **[`position.left`][6]**: **[string][1]** 
    * **[`position.right`][7]**: **[string][1]** 
  * If the container is null, default position value is `{bottom: "10px", right: "10px"}`
  * If the container is not null , default position value is `{bottom: "-42px", right: "-42px"}`

<br>

## API

```js

const simpleSDK = new RingoverSDK();

// Iframe main methods
simpleSDK.generate();			// iframe element
simpleSDK.destroy();			// boolean
simpleSDK.checkStatus();		// boolean

// Display methods
simpleSDK.show();			// boolean
simpleSDK.hide();			// boolean
simpleSDK.toggle();			// boolean
simpleSDK.isDisplay();		// boolean

// Ringover methods
simpleSDK.logout();									// boolean
simpleSDK.reload();									// boolean
simpleSDK.getCurrentPage();							// string(pageName) | boolean(false)
simpleSDK.changePage("settings");					// boolean
simpleSDK.dial("+33179757575");						// boolean
simpleSDK.sendSMS("+33610001000", "Hello");			// boolean
simpleSDK.openCallLog("616626881427127983");		// boolean

// Events

simpleSDK.on('changePage',    (e) => console.log(e.data));
simpleSDK.on('dialerReady',   (e) => console.log(e.data));
simpleSDK.on('login',         (e) => console.log(e.data));
simpleSDK.on('logout',        (e) => console.log(e.data));
simpleSDK.on('ringingCall',   (e) => console.log(e.data));
simpleSDK.on('answeredCall',  (e) => console.log(e.data));
simpleSDK.on('hangupCall',    (e) => console.log(e.data));
simpleSDK.on('smsSent',    	  (e) => console.log(e.data));
simpleSDK.on('smsReceived',   (e) => console.log(e.data));
simpleSDK.off();

```
<br>

## Methods

### `generate()`

Create an iframe, place it in the DOM and return it.

**Return: [iframe element][10]**

### `destroy()`

Remove iframe from the dom and destroy it. Return true if successful, return false if an error occurs.

**Return: [boolean][9]**

### `checkStatus()`

Returns true if the iframe can be generated or is already in the DOM, returns false if an error occurs.

**Return [boolean][9]**

### `show()` | `hide()` | `toggle()`

Show or hide the iframe (if `animation: true`, the animation is triggered).

**Return [boolean][9]**

### `isDisplay()`

Return true if the iframe is displayed, return false if the iframe is hidden.

**Return [boolean][9]**

### `logout()`

Logout the current user connected to the web app in the iframe. Return true if successful, return false if an error occurs.

**Return [boolean][9]**

### `reload()`

Reload the web app in the iframe. Return true if successful, return false if an error occurs.

**Return [boolean][9]**

### `getCurrentPage()`

Get the current web app page. Return false if an error occurs.

**Return ([string][1]|[boolean][9])**

### `changePage(pageName)`

Change the current web app page. Return true if successful, return false if an error occurs.

**Parameters:**

* `pageName`: ([string][1]). Example: "dialer", "call-logs", "sms", "settings"...

**Return [boolean][9]**

### `dial(numberE164)`

Call a specific number in the web app. Return true if successful, return false if an error occurs.

**Parameters:**

* `numberE164`: ([string][1]|[integer][11]). Example: "+16467129500", "442038906606", 33179757575...

**Return [boolean][9]**

### `sendSMS(toNumberE164, content, fromNumberE164)`

send an sms to a specific recipient from a mobile number. Return true if successful, return false if an error occurs.

**Parameters:**

* `toNumberE164`: ([string][1]|[integer][11]). Example: "+16467129500", "442038906606", 33179757575...
* `content`: ([string][1]). Example: "Hello, welcome to our service."...
* `fromNumberE164`: ([string][1]|[integer][11]). OPTIONAL Example: "+16467129500", "442038906606", 33179757575...

**Return [boolean][9]**

### `openCallLog(call_id)`

Open a specific call log by its call_id identifier. Return true if successful, return false if an error occurs.

**Parameters:**

* `call_id`: ([string][1]). Example: "616626881427127983"...

**Return [boolean][9]**

### `on(eventName, myFunction)`

Set a specific event listener to set up a function that will be called when the event is delivered. Return true if successful, return false if an error occurs.

**Parameters:**

* `eventName`: ([string][1]). Example: "login", "dialerReady", "ringingCall", "changePage"... See below.
* `myFunction`: ([function][12]).

**Return [boolean][9]**

### `off()`

Remove all event listerners previously setted. Return true if successful, return false if an error occurs.

**Return [boolean][9]**

<br>

## Events

### `changePage`

Trigger a hook when the web app changes page. Return the new page name.

**Return [object][3]:**
```js
{
	action: "changePage",
	data: {
		page: "settings"
	}
}
```
* `page`: ([string][1]). Example: "dialer", "call-logs", "sms", "settings"...

### `dialerReady`

Trigger a hook when the web app is ready to receive and make call. Return the current user id.

**Return [object][3]:**
```js
{
	action: "dialerReady",
	data: {
		userId: 123
	}
}
```
* `userId`: ([integer][11]).

### `login`

Trigger a hook when the user logs on the web app. Return the current user id.

**Return [object][3]:**
```js
{
	action: "login",
	data: {
		userId: 123
	}
}
```
* `userId`: ([integer][11]).

### `logout`

Trigger a hook when the user logs out the web app. Return the previous user id.

**Return [object][3]:**
```js
{
	action: "logout",
	data: {
		userId: 123
	}
}
```
* `userId`: ([integer][11]).


### `ringingCall`

Trigger a hook when a call is ringing or is being dialed. Automatically open the iframe. Return data call.

**Return [object][3]:**
```js
{
	action: "ringingCall",
	data: {
		direction: "out", // "in"|"out"
		from_number: "fromNumber", 
		to_number: "toNumber", 
		internal: false, // true|false 
		call_id: "123", 
		ringDuration: 0, 
		callDuration: 0
	}
}
```
* `direction`: ([string][1]). Direction (context) of the call. Value can be `"in"` or `"out"`.
* `from_number`: ([string][1]). Caller E164 number.
* `to_number`: ([string][1]). Callee E164 number.
* `internal`: ([boolean][9]). True if the call is internal of the team (inter-users), false is the call is external.
* `call_id`: ([string][1]). Identifier of the call.


### `answeredCall`

Trigger a hook when a call is ringing or is being dialed. Return data call.

**Return [object][3]:**
```js
{
	action: "answeredCall",
	data: {
		direction: "out", // "in"|"out"
		from_number: "fromNumber", 
		to_number: "toNumber", 
		internal: false, // true|false 
		call_id: "123", 
		ringDuration: 123, 
		callDuration: 0
	}
}
```
* `direction`: ([string][1]). Direction (context) of the call. Value can be `"in"` or `"out"`.
* `from_number`: ([string][1]). Caller E164 number.
* `to_number`: ([string][1]). Callee E164 number.
* `internal`: ([boolean][9]). True if the call is internal of the team (inter-users), false is the call is external.
* `call_id`: ([string][1]). Identifier of the call.
* `ringDuration`: ([integer][11]). Duration in seconds of the ringing time (before answer).

### `hangupCall`

Trigger a hook when a call is ringing or is being dialed. Return data call.

**Return [object][3]:**
```js
{
	action: "hangupCall",
	data: {
		direction: "out", // "in"|"out"
		from_number: "fromNumber", 
		to_number: "toNumber", 
		internal: false, // true|false 
		call_id: "123", 
		ringDuration: 123, 
		callDuration: 123
	}
}
```
* `direction`: ([string][1]). Direction (context) of the call. Value can be `"in"` or `"out"`.
* `from_number`: ([string][1]). Caller E164 number.
* `to_number`: ([string][1]). Callee E164 number.
* `internal`: ([boolean][9]). True if the call is internal of the team (inter-users), false is the call is external.
* `call_id`: ([string][1]). Identifier of the call.
* `ringDuration`: ([integer][11]). Duration in seconds of the ringing time (before answer).
* `callDuration`: ([integer][11]). Duration in seconds of the call time (after answer). 

### `smsSent`

Trigger a hook when a sms is sendend. Return information about the sms.

**Return [object][3]:**
```js
{
	action: "smsSent",
	data: {
		conversation_id: "123"
		to_number: "toNumber", 
		message: "Hello World",
	}
}
```
* `conversation_id`: ([string][1]). Identifier of the conversation.
* `to_number`: ([string][1]). SMS Recipient E164 number.
* `message`: ([string][1]). Content of the message.

### `smsReceived`

Trigger a hook when a sms is received. Return information about the sms.

**Return [object][3]:**
```js
{
	action: "smsReceived",
	data: {
		conversation_id: "123"
		from_number: "fromNumber", 
		message: "Hello World",
	}
}
```
* `conversation_id`: ([string][1]). Identifier of the conversation.
* `from_number`: ([string][1]). SMS Sender E164 number.
* `message`: ([string][1]). Content of the message.

<br>

## License

**[Apache-2.0](https://github.com/ringover/ringover-sdk/blob/main/LICENSE.md)**




[0]:	https://app.ringover.com/
[1]:	https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String
[2]:	https://developer.mozilla.org/docs/Web/CSS/position
[3]:	https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object
[4]:	https://developer.mozilla.org/docs/Web/CSS/top
[5]:	https://developer.mozilla.org/docs/Web/CSS/bottom
[6]:	https://developer.mozilla.org/docs/Web/CSS/left
[7]:	https://developer.mozilla.org/docs/Web/CSS/right
[8]:	https://developer.mozilla.org/docs/Web/API/Document/body
[9]:	https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Boolean
[10]:	https://developer.mozilla.org/docs/Web/HTML/Element/iframe
[11]:	https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number
[12]:	https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Function
[13]:	https://ringover.com
[14]:	https://developer.mozilla.org/en-US/docs/Web/CSS/background-color
