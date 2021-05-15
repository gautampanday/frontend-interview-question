# frontend-interview-question
Frontend interview question with answer


Program for anagram?
function anagrams(stringA, stringB) {
        /*First, we remove any non-alphabet character using regex and convert
        convert the strings to lowercase. */
        stringA = stringA.replace(/[^\w]/g, "").toLowerCase()
        stringB = stringB.replace(/[^\w]/g, "").toLowerCase()

        //Get the character map of both strings
        const charMapA = getCharMap(stringA)
        const charMapB = getCharMap(stringB)

        /* Next, we loop through each character in the charMapA, 
        and check if it exists in charMapB and has the same value as
        in charMapA. If it does not, return false */
        for (let char in charMapA) {
            if (charMapA[char] !== charMapB[char]) {
                return false
            }
        }

        return true
    }

    function getCharMap(string) {
        // We define an empty object that will hold the key - value pairs.
        let charMap = {}

        /*We loop through each character in the string. if the character 
        already exists in the map, increase the value, otherwise add it 
        to the map with a value of 1 */
        for (let char of string) {
            charMap[char] = charMap[char] + 1 || 1
        }
        return charMap
    }
The runtime complexity of a for loop is linear i.e O(n). In this case, there are 3 consecutive forloops which are not nested. Ignoring constants and other factors, the time complexity is approximately linear i.e. O(n).

2. Sort Strings and check if they are the same
This is a shorter and neater way of checking if two strings are anagrams.
In this case, we convert the string to an array, use the Array.sort()
method to sort it and convert it back to a string. Then we compare both strings and check if they are the same.
    function anagrams(stringA, stringB) {
        /*First, we remove any non-alphabet character using regex and convert       
        convert the strings to lowercase. */
        stringA = stringA.replace(/[^\w]/g, '').toLowerCase()
        stringB = stringB.replace(/[^\w]/g, '').toLowerCase()

        return sortString(stringA) === sortString(stringB)
    }

    /*This function sorts the strings*/ 
    function sortString(string) {
        return string.split('').sort().join('');
    }
Array.sort uses merge sort so its time complexity is O(nlogn).
[11/03, 11:43] Gautam: Program for decimal to binary?
function convertToBinary(x) {
    let bin = 0;
    let rem, i = 1, step = 1;
    while (x != 0) {
        rem = x % 2;
        console.log(
            `Step ${step++}: ${x}/2, Remainder = ${rem}, Quotient = ${parseInt(x/2)}`
        );
        x = parseInt(x / 2);
        bin = bin + rem * i;
        i = i * 10;
    }
    console.log(`Binary: ${bin}`);
}

// take input
let number = prompt('Enter a decimal number: ');

convertToBinary(number);

Output

Step 1: 9/2, Remainder = 1, Quotient = 4
Step 2: 4/2, Remainder = 0, Quotient = 2
Step 3: 2/2, Remainder = 0, Quotient = 1
Step 4: 1/2, Remainder = 1, Quotient = 0
Binary: 1001
In the above program, the user is prompted to enter a decimal number. The number entered by the user is passed as an argument to the convertToBinary() function.

The while loop is used until the number entered by the user becomes 0.

The binary value is calculated by:

bin = bin + rem * i;
Here, rem is the modulus % value of the number when divided by 2 and i gives the place value of the binary number.
[11/03, 11:49] Gautam: Program for summation of diagonal elements
function diagonalSums(matrix) {
 
    let mainSum = 0, secondarySum = 0;
    for (let row = 0; row < matrix.length; row++) {
        mainSum += matrix[row][row];
        secondarySum += matrix[row][matrix.length - row - 1];
    }
    console.log(mainSum + ' ' + secondarySum);
}
 
diagonalSums([[20, 40], [10, 60]]);
[11/03, 11:51] Gautam: How do you improve the performance of your web application?
1. Cache in the browser
There are two options for doing this. The first is to use the JavaScript Cache API, which we can use by installing a service worker. The second is to use the HTTP protocol cache.

Scripts are often used to access a certain object. By storing a repeated access object inside a user-defined variable, as well as using a variable in subsequent references to that object, performance improvement can be achieved immediately.

2. Define the execution context
In order to effectively measure any improvements that you’re incorporating into your program, you must establish a set of well-defined environments where is possible to test the performance of the code.

Trying to do performance tests and optimizations for all versions of all Javascript engines is not feasible in practice. But, it is not a good practice to do testing in a single environment, as this can give you partial results. So, it’s important to establish multiple well-defined environments and test that the code works on them.

3. Remove unused JavaScript
This step will not only reduce transmission time, but also the time it takes for the browser to analyze and compile the code. To do this, you must take into account the following points: - If you detect a functionality that is not being used by users, it’s a good practice to remove it with all its associated JavaScript code, so the website will load faster and users will have a better experience. - It is also possible that a library was included by mistake and is not necessary, or that you have dependencies that offer some functionality that is already natively available in all browsers, without the need to use additional code

4. Avoid using too much memory
You should always try to limit memory use to what is absolutely necessary, because is not possible to know how much memory is required by the device being used to run your app. Any time your code requests that the browser reserve new memory, the browser’s garbage collector is executed, and JavaScript is stopped. If this happens frequently, the page will work slowly.

5. Defer the load of JavaScript that is not necessary
Users want to see a page load quickly, but it’s not likely that all functions need to be available for the initial load of the page. If a user must perform a certain action in order for a function to be executed (e.g. by clicking on an element, or changing tabs), it’s possible to defer loading that function until after the initial page load.

In this way you can avoid loading and compiling JavaScript code that would delay the initial display of the page. Once the page is fully loaded, we can start loading those functionalities so that they are available immediately when the user starts to interact. In the RAIL model, Google recommends that this deferred load to be done in blocks of 50ms, so that it does not influence the user's interaction with the page.

6. Avoid memory leaks
If a memory leak is ongoing, the loaded page will reserve more and more memory, eventually occupying all the available memory of the device and severely impacting performance. You’ve probably seen (and likely been frustrated by) this type of failure, likely on a page with a carousel or image slider.

In Chrome Dev Tools, you can analyze if your website has memory leaks by recording a timeline in the Performance tab. Usually, memory leaks come from pieces of the DOM that are removed from the page but have some variable that makes reference to them and, therefore, the garbage collector can not eliminate them.

7. Use web workers when you need to execute code that needs a lot of execution time
According to the Mozilla Developers Network (MDN) documentation: “Web Workers makes it possible to run a script operation in a background thread separate from the main execution thread of a web application. The advantage of this is that laborious processing can be performed in a separate thread, allowing the main (usually the UI) thread to run without being blocked/slowed down.”

Web workers allow your code to perform processor-intensive calculations without blocking the user interface thread. Web Workers allow you spawn new threads and delegate work to these threads for efficient performance. This way, long running tasks which would normally block other tasks are passed off to a worker and the main thread can run without being blocked.

8. If you access a DOM item several times, save it in a local variable
Accessing the DOM is slow. If you are going to read the content of an element several times, it's better to save it in a local variable. But it’s important to keep in mind, if you will later remove the value of the DOM, the variable should be set to "null", so it doesn’t cause any memory leaks.

9. Prioritize access to local variables
JavaScript first searches to see if a variable exists locally, then searches progressively in higher levels of scope until global variables. Saving variables in a local scope allows JavaScript to access them much faster.

Local variables are found based on the most specific scope and can pass through multiple levels of scope, the look-ups can result in generic queries. When defining the function scope, within a local variable without a preceding variable declaration, it is important to precede each variable with let or const in order to define the current scope in order to prevent the look-up and to speed up the code.

10. Avoid using global variables
Because the scripting engine needs to look through the scope when referencing global variables from within function or another scope, the variable will be destroyed when the local scope is lost. If variables in the global scope can not persist through the lifetime of the script, the performance will be improved.

11. Implement the optimizations that you would apply in any other programming language
Always use the algorithms with the least computational complexity to solve the task with the optimal data structures
Rewrite the algorithm to get the same result with fewer calculations
Avoid recursive calls
Put in variables, the calculations and calls to functions that are repeated
Factor and simplify mathematical formulas
Use search arrays: they are used to obtain a value based on another instead of using a switch/case statement
Make conditions always more likely to be true to take better advantage of the speculative execution of the processor
Use bit-level operators when you can to replace certain operations, because these operators use fewer processor cycles
[11/03, 12:02] Gautam: Explain XSRF with one good example
Cross-site request forgery attacks (CSRF or XSRF for short) are used to send malicious requests from an authenticated user to a web application. The attacker can’t see the responses to the forged requests, so CSRF attacks focus on state changes, not theft of data. Successful CSRF attacks can have serious consequences
When you are browsing a website, it is common for that website to request data from another website on your behalf. For example, in most cases, a video that is shown on a website is not typically stored on the website itself. The video appears to be on the website but is actually being embedded from a video streaming site such as YouTube. That’s the idea behind Content Delivery Networks (CDNs), which are used to deliver content faster. Many websites store scripts, images, and other bandwidth-hungry resources on CDNs, so during browsing, images and script files are downloaded from a CDN source rather than the website itself.

While this improves the browsing experience, it might also be a source of a security problem if a website asks the web browser to retrieve data from another website without the user’s consent. If such requests are not handled correctly, an attacker can launch a cross-site request forgery attack
[11/03, 12:04] Gautam: How to Prevent Cross-Site Request Forgery Attacks
An attacker can launch a CSRF attack when he knows which parameters and value combination are being used in a form. Therefore, by adding an additional parameter with a value that is unknown to the attacker and can be validated by the server, you can prevent CSRF attacks. Below is a list of some of the methods you can use to block cross-site request forgery attacks.

Implement an Anti-CSRF Token
An anti-CSRF token is a type of server-side CSRF protection. It is a random string that is only known to the user’s browser and the web application. The anti-CSRF token is usually stored inside a session variable. On a page, it is typically in a hidden field that is sent with the request.

If the values of the session variable and the hidden form field match, the web application accepts the request. If they do not match, the request is dropped. In this case, the attacker does not know the exact value of the hidden form field that is needed for the request to be accepted, so he cannot launch a CSRF attack. In fact, due to same origin policy, the attacker can’t even read the response that contains the token.
[11/03, 12:08] Gautam: Explain event propagation in JavaScript
Event propagation is a mechanism that defines how events propagate or travel through the DOM tree to arrive at its target and what happens to it afterward.

Let's understand this with the help of an example, suppose you have assigned a click event handler on a hyperlink (i.e. <a> element) which is nested inside a paragraph (i.e. <p> element). Now if you click on that link, the handler will be executed. But, instead of link, if you assign the click event handler to the paragraph containing the link, then even in this case, clicking the link will still trigger the handler. That's because events don't just affect the target element that generated the event—they travel up and down through the DOM tree to reach their target. This is known as event propagation

In modern browser event propagation proceeds in two phases: capturing, and bubbling phase.
[11/03, 12:10] Gautam: The Capturing Phase
In the capturing phase, events propagate from the Window down through the DOM tree to the target node. For example, if the user clicks a hyperlink, that click event would pass through the <html> element, the <body> element, and the <p> element containing the link.

Also if any ancestor (i.e. parent, grandparent, etc.) of the target element and the target itself has a specially registered capturing event listener for that type of event, those listeners are executed during this phase.
[11/03, 12:10] Gautam: The Bubbling Phase
In the bubbling phase, the exact opposite occurs. In this phase event propagates or bubbles back up the DOM tree, from the target element up to the Window, visiting all of the ancestors of the target element one by one. For example, if the user clicks a hyperlink, that click event would pass through the <p> element containing the link, the <body> element, the <html> element, and the document node.

Also, if any ancestor of the target element and the target itself has event handlers assigned for that type of event, those handlers are executed during this phase.
[11/03, 12:11] Gautam: Stopping the Event Propagation
You can also stop event propagation in the middle if you want to prevent any ancestor element's event handlers from being notified about the event.

For example, suppose you have nested elements and each element has onclick event handler that displays an alert dialog box. Normally, when you click on the inner element all handlers will be executed at once, since event bubble up to the DOM tree.
To prevent this situation you can stop event from bubbling up the DOM tree using the event.stopPropagation() method. In the following example click event listener on the parent elements will not execute if you click on the child elements.
[11/03, 12:15] Gautam: What are differences between $(document).ready and $(window).load?
$(window).load is an event that fires when the DOM and all the content (everything) on the page is fully loaded like CSS, images and frames. One best example is if we want to get the actual image size or to get the details of anything we use it.

$(document).ready() indicates that code in it need to be executed once the DOM got loaded and ready to be manipulated by script. It won't wait for the images to load for executing the jQuery script.
[11/03, 12:21] Gautam: Write a program to multiply two numbers with out using * symbol
function multiply(a, b){
  let answer = a
  for(var i = 0; i < b - 1; i++){
    answer += a
  }
  return answer
}

Breakdown:
We create a variable named “answer” and assign it the value of “a”. Then we create a for loop that will iterate until “i” is less than “b -1”. Why “b -1”? Because we already assigned “answer” to “a”. Every iteration we add “a” to “answer”. Once iteration is done we return “answer”.
Ex:
multiply(6, 3)           //our a is 6 and b is 3
//before iteration
answer is 6              //assign answer equal to a which is 6
//iteration begins
answer is now 12         // i is now 1 
answer is now 18         // i is now 2 which is means break loop as
                            i is no longer less than b - 1.
then we return "answer" which would be 18.
[11/03, 12:38] Gautam: difference between http1 and http2
These are the high-level differences between HTTP1 and HTTP2:

HTTP2 is binary, instead of textual
HTTP2 is fully multiplexed, instead of ordered and blocking
HTTP2 can, therefore, use one connection for parallelism
HTP2 uses header compression to reduce overhead
HTTP2 allows servers to “push” responses proactively into client caches
HTTP/2
HTTP/2 began as the SPDY protocol, developed primarily at Google with the intention of reducing web page load latency by using techniques such as compression, multiplexing, and prioritization. This protocol served as a template for HTTP/2 when the Hypertext Transfer Protocol working group httpbis of the IETF (Internet Engineering Task Force) put the standard together, culminating in the publication of HTTP/2 in May 2015. From the beginning, many browsers supported this standardization effort, including Chrome, Opera, Internet Explorer, and Safari. Due in part to this browser support, there has been a significant adoption rate of the protocol since 2015, with especially high rates among new sites.

From a technical point of view, one of the most significant features that distinguishes HTTP/1.1 and HTTP/2 is the binary framing layer, which can be thought of as a part of the application layer in the internet protocol stack. As opposed to HTTP/1.1, which keeps all requests and responses in plain text format, HTTP/2 uses the binary framing layer to encapsulate all messages in binary format, while still maintaining HTTP semantics, such as verbs, methods, and headers. An application level API would still create messages in the conventional HTTP formats, but the underlying layer would then convert these messages into binary. This ensures that web applications created before HTTP/2 can continue functioning as normal when interacting with the new protocol.

The conversion of messages into binary allows HTTP/2 to try new approaches to data delivery not available in HTTP/1.1, a contrast that is at the root of the practical differences between the two protocols.
[11/03, 12:44] Gautam: What is Service Worker:
A service worker is a script that runs independently in the browser background. On the user side, it can intercept its network requests and decide what to load (fetch).
Service workers mainly serve features like background sync, push notifications and they are commonly used for’offline first’ applications, giving the developers the opportunity to take complete control over the user experience.

Before it’s time there has been API called AppCache, which has been trying to serve the offline experience feature. However, there have been numerous problems in the interface of the AppCache API and Service Workers are here, going over them.

The service worker life cycle:
The service worker lifecycle is completely separate from the web page. It’s a programmable network proxy, which is terminated when it’s not used and restarted when it’s next needed. Service Workers heavily rely on the use of Javascript Promises , so it’s good to go over them if they are new to you.

During installation, the service worker can cache some static assets like web pages. If the browser cache the files successfully, the service worker gets installed.

Afterward, the worker needs to be activated. During activation the service worker can manage and decide what to happen to the old caches, typically they are being deleted and replaced with the new versions.



Lastly, after activation, the service worker takes control over all pages in his scope, without the page which initially registered the service worker, which needs to be refreshed. The service worker is smart in terms of memory usage and will be terminated if there is nothing to fetch and there are no message events occurring.

Prerequisites :

HTTPS unless on localhost
Service workers require the use of HTTPS connection. Before deployment, the workers does work under the localhost server but if you want to upload it to the internet you need to have the HTTPS setup on your server. One good place to host free demos are the GitHub Pages, which are server over HTTPS.
Browser support
Service Workers are highly supported over the internet by Chrome, Firefox, Opera, Safari and Edge, which makes them worthy for deployment.

Registration:
To set up a service worker it needs to be registered. This is done in your page’s Javascript. Once a service worker is registered this will cause the browser to start installing it in the background.

// Ensure that the browser supports the service worker API 
if (navigator.serviceWorker) { 
  // Start registration process on every page load 
  window.addEventListener('load', () => { 
      navigator.serviceWorker 
          // The register function takes as argument 
          // the file path to the worker's file 
          .register('/service_worker.js') 
          // Gives us registration object 
          .then(reg => console.log('Service Worker Registered')) 
          .catch(swErr => console.log( 
                `Service Worker Installation Error: ${swErr}}`)); 
    }); 
} 

Installing:
After the service worker gets registered it needs to be installed, this is done in the service worker file and where you typically want to fetch your cache assets.

The following steps need to be taken:

Open a cache
Cache the assets
Confirm if the caching is successful
var cacheName = 'geeks-cache-v1'; 
var cacheAssets = [ 
    '/assets/pages/offline-page.html', 
    '/assets/styles/offline-page.css', 
    '/assets/script/offline-page.js', 
  
]; 
  
// Call install Event 
self.addEventListener('install', e => { 
    // Wait until promise is finished  
    e.waitUntil( 
        caches.open(cacheName) 
        .then(cache => { 
            console.log(`Service Worker: Caching Files: ${cache}`); 
            cache.addAll(cacheAssets) 
                // When everything is set 
                .then(() => self.skipWaiting()) 
        }) 
    ); 
}) 


Activating:

// Call Activate Event 
self.addEventListener('activate', e => { 
    console.log('Service Worker: Activated'); 
    // Clean up old caches by looping through all of the 
    // caches and deleting any old caches or caches that 
    // are not defined in the list 
    e.waitUntil( 
        caches.keys().then(cacheNames => { 
            return Promise.all( 
                cacheNames.map( 
                    cache => { 
                        if (cache !== cacheName) { 
                            console.log('Service Worker: Clearing Old Cache'); 
                            return caches.delete(cache); 
                        } 
                    } 
                ) 
            ) 
        }) 
    ); 
}) 


Fetching event:
Once the service worker is set up, it should start to interact and use the cached responses. When a particular user navigates through the web pages, the service worker begins to receive fetch events. The following example demonstrates a case when the worker receives a fetch event and search for a matching cache if there is one, it returns the cached file/value, otherwise, it returns the default response of the call to fetch

var cacheName = 'geeks-cache-v1'; 
  
// Call Fetch Event  
self.addEventListener('fetch', e => { 
    console.log('Service Worker: Fetching'); 
    e.respondWith( 
        fetch(e.request) 
        .then(res => { 
            // The response is a stream and in order the browser  
            // to consume the response and in the same time the  
            // cache consuming the response it needs to be  
            // cloned in order to have two streams. 
            const resClone = res.clone(); 
            // Open cache 
            caches.open(cacheName) 
                .then(cache => { 
                    // Add response to cache 
                    cache.put(e.request, resClone); 
                }); 
            return res; 
        }).catch( 
            err => caches.match(e.request) 
            .then(res => res) 
        ) 
    ); 
}); 



Service Worker can’t:‘

Access the Parent Object
Access the Window Object
Access the Document Object
Access the DOM
However, the Service Worker can:

Cache Assets & API calls
Manage Push Notifications
Control the Network Traffic
Store the Application Cache
Common use cases:

Offline-optimized experience
Sending Push Notifications
Background sync
[11/03, 12:45] Gautam: Service workers have been designed to be fully asynchronous, as a consequence, APIs such as synchronous XHR and localStorage can’t be used inside a service worker. But since it is working on a different thread it doesn’t block your application in any way.
Service workers are terminated when not in use and restored when required. It acts as a programmable network proxy, allowing developers to handle how network requests from the web page is handled. So the developers can take appropriate action based on the availability of network.
[11/03, 12:46] Gautam: Service Worker v/s Web Worker
Both Service workers and Web workers are JavaScript workers with lots of similarities but there are a few difference too.
Service workers are designed to handle network requests and assist in offline first development, Push Notifications and background syncs. Communication’s with the webpage must go through service workers PostMessage method.
Web workers mimics the multi-threading model, allowing complex / data or processor intensive tasks to run in background. Ideal to keep your UI jank free when you have to deal with a lot of computations. Communication’s with the webpage must go through web workers PostMessage method.
[11/03, 12:52] Gautam: What is a JavaScript closure?
A JavaScript Closure is when an inner function has access to members of the outer function (lexical scope) even when executing outside the scope of the outer function.

Lexical Scope
JavaScript's Lexical Scope is determined during the compile phase. It sets the scope of a variable so that it may only be called/referenced from within the block of code in which it is defined.

A function declared inside a surrounding function block has access to variables in the surrounding function's lexical scope.

var initialBalance = 300 // Global Scope

function withdraw (amount) {
  /**
   * Local Scope
   * Code here has access to anything declared in the global scope
   */
  var balance = parseInt(initialBalance) - parseInt(amount)

  const actualBalance = (function () {
    const TRANSACTIONCOST = 35
    return balance - TRANSACTIONCOST /**
     * Accesses balance variable from the lexical scope
     */
  })() // Immediately Invoked Function expression. IIFE

  // console.log(TRANSACTIONCOST) // ReferenceError: Can't find variable: TRANSACTIONCOST
  return actualBalance
}
Invoking an inner function outside of its enclosing function and yet maintain access to variables in its enclosing function (lexical scope) creates a JavaScript Closure.

function person () {
  var name = 'Paul'  // Local variable

  var actions = {
    speak: function () {
    //  new function scope
      console.log('My name is ', name) /**
      * Accessing the name variable from the outer function scope (lexical scope)
      */
    }
  } // actions object with a function

  return actions /**
  * We return the actions object
  * We then can invoke the speak function outside this scope
  */
}

person().speak() // Inner function invoked outside its lexical Scope
A Closure allows us to expose a public interface while at the same time hiding and preserving execution context from the outside scope.

When we pass a function into a setTimeout or any kind of callback. The function still remembers the lexical scope because of the closure.

function foo () {
  var bar = 'bar'
  setTimeout(function () {
    console.log(bar)
  }, 1000)
}

foo() // bar
Closure and loops

for (var i = 1; i <= 5; i++) {
  (function (i) {
    setTimeout(function () {
      console.log(i)
    }, i * 1000)
  })(i)
}
/**
* Prints 1 thorugh 5 after each second
* Closure enables us to remember the variable i
* An IIFE to pass in a new value of the variable i for each iteration
* IIFE (Immediately Invoked Function expression)
*/
for (let i = 1; i <= 5; i++) {
  (function (i) {
    setTimeout(function () {
      console.log(i)
    }, i * 1000)
  })(i)
}
/**
* Prints 1 through 5 after each second
* Closure enabling us to remember the variable i
* The let keyword rebinds the value of i for each iteration
*/
[11/03, 12:59] Gautam: What is the difference between HTTP and HTTPS

HTTP is unsecured while HTTPS is secured.
HTTP sends data over port 80 while HTTPS uses port 443.
HTTP operates at application layer, while HTTPS operates at transport layer.
No SSL certificates are required for HTTP, with HTTPS it is required that you have an SSL certificate and it is signed by a CA.
HTTP doesn't require domain validation, where as HTTPS requires at least domain validation and certain certificates even require legal document validation.
No encryption in HTTP, with HTTPS the data is encrypted before sending.
[11/03, 13:04] Gautam: Working of web
The moment you enter this address in your browser and you hit ENTER, a lot of different things happen:

1.The URL gets resolved
2.A Request is sent to the server of the website
3.The response of the server is parsed
4.The page is rendered and displayed

Step 1 - URL Gets Resolved
The website code is obviously not stored on your machine and hence needs to be fetched from another computer where it is stored. This “other computer” is called a “server”. Because it serves some purpose, in our case, it serves the website.

You enter “academind.com” (that is called “a domain”) but actually, the server which hosts the source code of a website, is identified via IP (= Internet Protocol) addresses. The browser sends a “request” (see step 2) to the server with the IP address you entered (indirectly - you of course entered “academind.com”).
[11/03, 13:06] Gautam: How is the domain “academind.com” translated to its IP address?

There’s a special type of server out there in the internet - not just one but many servers of that type. A so called “name server” or “DNS server” (where DNS = “Domain Name System”).

The job of these DNS servers is to translate domains to IP addresses. You can imagine those servers as huge dictionaries that store translation tables: Domain => IP address.

When you enter “academind.com”, the browser therefore first fetches the IP address from such a DNS server.


Step 2 - Request Is Sent
With the IP address resolved, the browser goes ahead and makes a request to the server with that IP address.

“A request” is not just a term. It really is a technical thing that happens behind the scenes.

The browser bundles up a bunch of information (What’s the exact URL? Which kind of request should be made? Should metadata be attached) and sends that data package to the IP address.
The data is sent via the “HyperText Transfer Protocol” (known as “HTTP”) - a standardized protocol which defines what a request (and response) has to look like, which data may be included (and in which form) and how the request will be submitted. You can learn more about HTTP here.

Step 3 - Response Is Parsed
The browser receives the response sent by the server. This alone, doesn’t display anything on the screen though.

Instead, the next step is that the browser parses the response. Just as the server did it with the request.

Every HTML tag has some semantic meaning which the browser understands, because HTML is also standardized. Hence there is no guessing about what a <h1> tag means.

The browser knows how to parse HTML and now simply goes through the entire response data (also called “the response body”) to render the website.

Step 4 - Page Is Displayed
As mentioned, the browser goes through the HTML data returned by the server and builds a website based on that.

Though it is important to know, that HTML does not include any instructions regarding what the site should look like (i.e. how it should be styled). It really only defines the structure and tells the browser which content is a heading, which content is an image, which content is a paragraph etc. This is especially important for accessibility - screen readers get all the useful information out of the HTML structure.
[11/03, 13:13] Gautam: Webpack and it's working

Webpack is a tool that lets you compile JavaScript modules, also known as module bundler.

Given a large number of files, it generates a single file (or a few files) that run your app.

It can perform many operations:

helps you bundle your resources.
watches for changes and re-runs the tasks.
can run Babel transpilation to ES5, allowing you to use the latest JavaScript features without worrying about browser support.
can transpile CoffeeScript to JavaScript
can convert inline images to data URIs.
allows you to use require() for CSS files.
can run a development webserver.
can handle hot module replacement.
can split the output files into multiple files, to avoid having a huge js file to load in the first page hit.
can perform tree shaking.

Webpack can automatically rebuild the bundle when a change in your app happens, and keep listening for the next change.

Just add this script:

"scripts": {
  "watch": "webpack --watch"
}
and run

npm run watch
[11/03, 13:14] Gautam: Handling images
Webpack allows us to use images in a very convenient way, using the file-loader loader.

This simple configuration:

module.exports = {
  /*...*/
  module: {
    rules: [
      {
        test: /\.(png|svg|jpg|gif)$/,
        use: [
          'file-loader'
        ]
      }
    ]
  }
  /*...*/
}


Process your SASS code and transform it to CSS
Using sass-loader, css-loader and style-loader:

Generate Source Maps
Since webpack bundles the code, Source Maps are mandatory to get a reference to the original file that raised an error, for example.

You tell webpack to generate source maps using the devtool property of the configuration:

module.exports = {
  /*...*/
  devtool: 'inline-source-map',
  /*...*/
}
[11/03, 13:16] Gautam: Async/ await in es6
es6 new functionalities
Difference between for...of, for...in and simple for loop
Prototype chaining in JS
Event Loop and Message Queue in Node.js
Diff. B/w let, var and const
Diff. B/w bind, call and apply
Diff B/w map, reduce and forEach
JS Hoisting and Can functions be hoisted
Local Storage, Session Storage & cookies and diff. B/w them
Settimeout functions
Inheritance and Prototypes; Prototypes Chain
Classes and functions in JS
Async Ajax Request
Live(), bind and delegate methods
Slice vs Splice
Web Workers vs Service Workers
Async & defer Differences
How a page renders
onLoad and ready functions
Object Assign
Object Create
Object Writable and Emutable
Check if variable is Array, Number, Object
Regex
Promises and Callbacks
Block Level Elements vs Inline Elements
New Features in HTML5 - https://www.w3schools.com/html/html5_intro.asp
Box-shadow and position property css
Transitions in css
Animations in css
Server Side Rendering
Code Splitting in React
Lazy and Suspense in React
Arrow functions in JS
Spread Operator in JS
Destructuring in JS
Debouncing and Throttling in JS
Redux and its working of actions and reducers
Currying in JS
Arity in JS
Difference Between PureComponent and Component in React
Controlled and High Order Components(HOC) in React
Type Coercion, and using typeof, instanceof, and Object.prototype.toString
HTTP requests: GET and POST and their headers like Cache-Control, ETag, and Transfer-Encoding
REST vs RPC
Security: When to use CORS, JSONP, and iFrame policies
Critical rendering path
Service workers
Image optimization
Lazy loading images and video
HTTP/2
Preload, preconnect, and prefetch
Minimize browser reflows
Rendering performance
Binding: Call, Apply, and Bind & Lexical This
Execution Context: Scoping & Closures
Prototypal inheritance
Event Delegation and Bubbling
When to use function declarations and expressions
Composition and high order functions
Handling asynchronous calls with callbacks, promises, await, and async
Variable and function hoisting
Currying
Object prototypes, constructors and mixins
Dunder Properties in JS
How to create functions like map in javascript
How to create functions where it accepts array in the beginning as well as a parameter.
HTTP Get, Post, Put, Delete method and their Differences
Bubbling and Capturing and its differences and Examples
Event Loop & Call Stack & Event Queue
Modules in Node.js and exporting, importing and requiring them
Event Emitter and Event module
Two-way binding with digest cycle
Directives, Filters, Service, Factory functions
Interceptors functions
Passing Data b/w 2 controllers
https://blog.pramp.com/how-to-succeed-in-a-frontend-interview-d748cb073823
https://blog.sessionstack.com/how-javascript-works-memory-management-how-to-handle-4-common-memory-leaks-3f28b94cfbec
https://blog.sessionstack.com/how-does-javascript-actually-work-part-1-b0bacc073cf
https://blog.sessionstack.com/how-javascript-works-inside-the-v8-engine-5-tips-on-how-to-write-optimized-code-ac089e62b12e
https://medium.com/better-programming/12-useful-packages-every-node-js-developer-should-know-2746db760e
https://medium.com/better-programming/10-best-practices-for-improving-your-css-84c69aac66e
How does Browser identify JS?
6 Primitive data types in js -
1. undefined
2. null
3. boolean
4. string
5. symbol
6. Number
https://www.codementor.io/@nihantanu/21-essential-javascript-tech-interview-practice-questions-answers-du107p62z
JS objects Points -
1. Every JS object has a prototype property, due to which inheritance is possible in js.
2. Prototype property of an object consists of methods and properties of the object that other objects can inherit.
3. The constructor prototype property is not prototype of the constructor itself, its prototype of all instances that are created through it.
4. If certain method is called of an object , it first search in object itself and then it moves to the prototype. it continues until method is found - this is called prototype chain.
6. Number + Number -> Addition
7. Boolean + Number -> Addition
8. Boolean + Number -> Addition
9. Number + String -> Concatenation
10. String + Boolean -> Concatenation
11. String + String -> Concatenation
12. Boolean + Boolean -> Addition like true + true => 2 assuming true as 1 and false as 0
Two ways to setup a project -
1. Module to Language - Login ———> JS,CSS
2. Langauge to Module - JS ——> Login, CSS ———> Login
Object data type in js
Difference b/w client side rendering and server side rendering? Which one is benefinicial and why?
In which scenerios would you choose client side rendering and server side rendering?
How does Browser identify headers and cookies?
Webpack vs gulp vs grunt
React Hooks and why do we use it?
Website optimization techniques
Is there any difference b/w code conventions for web and mobile apps webview?
Websockets(How to implement instagram feed in UI)
React Lifecycle methods
Alternative Sorting in nlogn
Find the largest sum of contiguous subarray from a given array of integers
Generate a Matrix in spiral order, for a given number n.
K-reverse linked list - reverse a singly linked list for an integer k is given.
Checking for Palindrome Strings by removing special Characters and Spaces -
Solution :- var A = ‘string’;var B = A.toLowerCase().replace(/[^A-Za-z0-9]+/ig, ‘’);var C = B.split(‘’).reverse().join(‘’);return C
Write a program to find the sum of diagonal matrices.
Eg:- Input: [ 4 5 7, 8 3 2, 4 5 6 ] Output: 13, 14
Write a program to print :
*
* *
* * *
* * * *
* * * * *
Write a program to print fibonacci series using recursion?
Write a program for Anagram:Eg: FOOL & OFOL are anagram because characters and their count are same in both words.
Write a program to find whether the given point lies inside or outside of the circle.
Write a program to reverse a word in a sentence without using any inbuilt function: Eg:i/p:This is a boy.o/p:Siht si a yob.

In the LLD Interviews, they will judge you on your knowledge of creating modular, flexible, maintainable and reusable software, by applying Object-oriented Design Principles and Design Patterns. These questions (like Design a Parking Lot, Design a Chess Game etc.) are about demonstrating that you understand how to create elegant, maintainable object-oriented code. These questions are (intentionally) unstructured and open-ended and they don't have a standard answer.

How to Prepare for the LLD Interview
Learn at least one Object Oriented Language ( C++ / Java / Python or C# )
Study about the SOLID and other Object Oriented Principles
Learn all the common Design Patterns and their applications
Explore some open-source projects and try to understand the best practices
Practice common LLD interview questions
How to solve LLD problems in the Interview
Clarify the problem by asking the relevant questions. Gather the complete requirement and start with the basic features.
Define the Core Classes ( and Objects )
Establish the relationships between the classes / objects by observing the interactions among the classes / objects.
Try to fulfill all the requirements by defining the methods
Apply Object Oriented Design Principles and Design Patterns to make the system maintainable and reusable.
Write well structured clean code (if you are told to implement a function)
Resources for LLD
Books:

Head first object-oriented analysis and design http://shop.oreilly.com/product/9780596008673.do
Head first design patterns : http://shop.oreilly.com/product/9780596007126.do
Clean Code: https://www.oreilly.com/library/view/clean-code-a/9780136083238/
Clean Architecture : https://www.oreilly.com/library/view/clean-architecture-a/9780134494272/
Refactoring: Improving the Design of Existing Code
Patterns of Enterprise Application Architecture
Design Patterns: Elements of Reusable Object-Oriented Software: https://www.oreilly.com/library/view/design-patterns-elements/0201633612/
Online Live Course:

https://practice.geeksforgeeks.org/courses/design-patterns-live
Other Links:

https://refactoring.guru/design-patterns
https://sourcemaking.com/design_patterns
https://www.geeksforgeeks.org/software-design-patterns/
https://github.com/prasadgujar/low-level-design-primer
https://github.com/DovAmir/awesome-design-patterns#programming-language-design-patterns
https://www.youtube.com/watch?v=OkC7HKtiZC0&list=PLGLfVvz_LVvQ5G-LdJ8RLqe-ndo7QITYc (for UML 2.0)
[11/03, 13:19] Gautam: Async/ await in es6

async function myFirstAsyncFunction() {
  try {
    const fulfilledValue = await promise;
  }
  catch (rejectedValue) {
    // …
  }
}
If you use the async keyword before a function definition, you can then use await within the function. When you await a promise, the function is paused in a non-blocking way until the promise settles. If the promise fulfills, you get the value back. If the promise rejects, the rejected value is thrown.

Example: Logging a fetch
Say we wanted to fetch a URL and log the response as text. Here's how it looks using promises:


function logFetch(url) {
  return fetch(url)
    .then(response => response.text())
    .then(text => {
      console.log(text);
    }).catch(err => {
      console.error('fetch failed', err);
    });
}
And here's the same thing using async functions:


async function logFetch(url) {
  try {
    const response = await fetch(url);
    console.log(await response.text());
  }
  catch (err) {
    console.log('fetch failed', err);
  }
}
It's the same number of lines, but all the callbacks are gone. This makes it way easier to read, especially for those less familiar with promises.

Async functions always return a promise, whether you use await or not. That promise resolves with whatever the async function returns, or rejects with whatever the async function throws. So with:


// wait ms milliseconds
function wait(ms) {
  return new Promise(r => setTimeout(r, ms));
}

async function hello() {
  await wait(500);
  return 'world';
}
…calling hello() returns a promise that fulfills with "world".


async function foo() {
  await wait(500);
  throw Error('bar');
}
…calling foo() returns a promise that rejects with Error('bar')
[11/03, 13:21] Gautam: ES6 new feature
ECMAScript 6, also known as ECMAScript 2015, is the latest version of the ECMAScript standard. ES6 is a significant update to the language, and the first update to the language since ES5 was standardized in 2009. Implementation of these features in major JavaScript engines is underway now.

See the ES6 standard for full specification of the ECMAScript 6 language.

ES6 includes the following new features:

arrows
classes
enhanced object literals
template strings
destructuring
default + rest + spread
let + const
iterators + for..of
generators
unicode
modules
module loaders
map + set + weakmap + weakset
proxies
symbols
subclassable built-ins
promises
math + number + string + array + object APIs
binary and octal literals
reflect api
tail calls
[11/03, 13:24] Gautam: Top 10 ES6 Features
Here’s the list of the top 10 best ES6 features for a busy software engineer (in no particular order):

Default Parameters in ES6
Template Literals in ES6
Multi-line Strings in ES6
Destructuring Assignment in ES6
Enhanced Object Literals in ES6
Arrow Functions in ES6
Promises in ES6
Block-Scoped Constructs Let and Const
Classes in ES6
Modules in ES6

Disclaimer: the list if highly biased and subjective. It is in no way was intended to diminish usefulness of other ES6 features, which didn’t make it to the list simply because I had to limit the number to 10.

First, a bit of history because those who don’t know the history can’t make it. This is a brief JavaScript timeline:

1995: JavaScript is born as LiveScript
1997: ECMAScript standard is established
1999: ES3 comes out and IE5 is all the rage
2000–2005: XMLHttpRequest, a.k.a. AJAX, gains popularity in app such as Outlook Web Access (2000) and Oddpost (2002), Gmail (2004) and Google Maps (2005).
2009: ES5 comes out (this is what most of us use now) with forEach, Object.keys, Object.create (specially for Douglas Crockford), and standard JSON
2015: ES6/ECMAScript2015 comes out; it has mostly syntactic sugar, because people weren’t able to agree on anything more ground breaking (ES7?)
Enough with history, let’s get to the business of coding.

1. Default Parameters in ES6
Remember we had to do these statements to define default parameters:

var link = function (height, color, url) {
    var height = height || 50
    var color = color || 'red'
    var url = url || 'http://azat.co'
    ...
}
They were okay until the value was 0 and because 0 is falsy in JavaScript it would default to the hard-coded value instead of becoming the value itself. Of course, who needs 0 as a value (#sarcasmfont), so we just ignored this flaw and used the logic OR anyway… No more! In ES6, we can put the default values right in the signature of the functions:

var link = function(height = 50, color = 'red', url = 'http://azat.co') {
  ...
}
By the way, this syntax is similar to Ruby!

2. Template Literals in ES6
Template literals or interpolation in other languages is a way to output variables in the string. So in ES5 we had to break the string like this:

var name = 'Your name is ' + first + ' ' + last + '.'
var url = 'http://localhost:3000/api/messages/' + id
Luckily, in ES6 we can use a new syntax ${NAME} inside of the back-ticked string:

var name = `Your name is ${first} ${last}.`
var url = `http://localhost:3000/api/messages/${id}`
3. Multi-line Strings in ES6
Another yummy syntactic sugar is multi-line string. In ES5, we had to use one of these approaches:

var roadPoem = 'Then took the other, as just as fair,\n\t'
    + 'And having perhaps the better claim\n\t'
    + 'Because it was grassy and wanted wear,\n\t'
    + 'Though as for that the passing there\n\t'
    + 'Had worn them really about the same,\n\t'

var fourAgreements = 'You have the right to be you.\n\
    You can only be you when you do your best.'
While in ES6, simply utilize the backticks:

var roadPoem = `Then took the other, as just as fair,
    And having perhaps the better claim
    Because it was grassy and wanted wear,
    Though as for that the passing there
    Had worn them really about the same,`

var fourAgreements = `You have the right to be you.
    You can only be you when you do your best.`
4. Destructuring Assignment in ES6
Destructuring can be a harder concept to grasp, because there’s some magic going on… let’s say you have simple assignments where keys house and mouse are variables house and mouse:

[Sidenote]

Reading blog posts is good, but watching video courses is even better because they are more engaging.

A lot of developers complained that there is a lack of affordable quality video material on Node. It's distracting to watch to YouTube videos and insane to pay $500 for a Node video course!

Go check out Node University which has FREE video courses on Node: node.university.

[End of sidenote]

var data = $('body').data(), // data has properties house and mouse
  house = data.house,
  mouse = data.mouse
Other examples of destructuring assignments (from Node.js):

var jsonMiddleware = require('body-parser').json

var body = req.body, // body has username and password
  username = body.username,
  password = body.password  
In ES6, we can replace the ES5 code above with these statements:

var {house, mouse} = $('body').data() // we'll get house and mouse variables

var {json: jsonMiddleware} = require('body-parser')

var {username, password} = req.body
This also works with arrays. Crazy!

var [col1, col2]  = $('.column'),
  [line1, line2, line3, , line5] = file.split('\n')
It might take some time to get use to the destructuring assignment syntax, but it’s a sweet sugarcoating.

5. Enhanced Object Literals in ES6
What you can do with object literals now is mind blowing! We went from a glorified version of JSON in ES5 to something closely resembling classes in ES6.

Here’s a typical ES5 object literal with some methods and attributes/properties:

var serviceBase = {port: 3000, url: 'azat.co'},
    getAccounts = function(){return [1,2,3]}

var accountServiceES5 = {
  port: serviceBase.port,
  url: serviceBase.url,
  getAccounts: getAccounts,
  toString: function() {
    return JSON.stringify(this.valueOf())
  },
  getUrl: function() {return "http://" + this.url + ':' + this.port},
  valueOf_1_2_3: getAccounts()
}
If we want to be fancy, we can inherit from serviceBase by making it the prototype with the Object.create method:

var accountServiceES5ObjectCreate = Object.create(serviceBase)
var accountServiceES5ObjectCreate = {
  getAccounts: getAccounts,
  toString: function() {
    return JSON.stringify(this.valueOf())
  },
  getUrl: function() {return "http://" + this.url + ':' + this.port},
  valueOf_1_2_3: getAccounts()
}
I know, accountServiceES5ObjectCreate and accountServiceES5 are NOT totally identical, because one object (accountServiceES5) will have the properties in the __proto__ object as shown below:

Enhanced Object Literals in ES6
Enhanced Object Literals in ES6

But for the sake of the example, we’ll consider them similar. So in ES6 object literal, there are shorthands for assignment getAccounts: getAccounts, becomes just getAccounts,. Also, we set the prototype right there in the __proto__`` property which makes sense (not‘proto’` though:

var serviceBase = {port: 3000, url: 'azat.co'},
    getAccounts = function(){return [1,2,3]}
var accountService = {
    __proto__: serviceBase,
    getAccounts,
Also, we can invoke super and have dynamic keys (valueOf_1_2_3):

    toString() {
     return JSON.stringify((super.valueOf()))
    },
    getUrl() {return "http://" + this.url + ':' + this.port},
    [ 'valueOf_' + getAccounts().join('_') ]: getAccounts()
};
console.log(accountService)
Enhanced Object Literals in ES6 II
Enhanced Object Literals in ES6 II

This is a great enhancement to good old object literals!

6. Arrow Functions in ES6
This is probably one feature I waited the most. I love CoffeeScript for its fat arrows. Now we have them in ES6. The fat arrows are amazing because they would make your this behave properly, i.e., this will have the same value as in the context of the function—it won’t mutate. The mutation typically happens each time you create a closure.

Using arrows functions in ES6 allows us to stop using that = this or self = this or _this = this or .bind(this). For example, this code in ES5 is ugly:

var _this = this
$('.btn').click(function(event){
  _this.sendData()
})
This is the ES6 code without _this = this:

$('.btn').click((event) =>{
  this.sendData()
})
Sadly, the ES6 committee decided that having skinny arrows is too much of a good thing for us and they left us with a verbose old function instead. (Skinny arrow in CoffeeScript works like regular function in ES5 and ES6).

Here’s another example in which we use call to pass the context to the logUpperCase() function in ES5:

var logUpperCase = function() {
  var _this = this

  this.string = this.string.toUpperCase()
  return function () {
    return console.log(_this.string)
  }
}

logUpperCase.call({ string: 'es6 rocks' })()
While in ES6, we don’t need to mess around with _this:

var logUpperCase = function() {
  this.string = this.string.toUpperCase()
  return () => console.log(this.string)
}

logUpperCase.call({ string: 'es6 rocks' })()
Note that you can mix and match old function with => in ES6 as you see fit. And when an arrow function is used with one line statement, it becomes an expression, i.e,. it will implicitly return the result of that single statement. If you have more than one line, then you’ll need to use return explicitly.

This ES5 code is creating an array from the messages array:

var ids = ['5632953c4e345e145fdf2df8','563295464e345e145fdf2df9']
var messages = ids.map(function (value) {
  return "ID is " + value // explicit return
})
Will become this in ES6:

var ids = ['5632953c4e345e145fdf2df8','563295464e345e145fdf2df9']
var messages = ids.map(value => `ID is ${value}`) // implicit return
Notice that I used the string templates? Another feature from CoffeeScript… I love them!

The parenthesis () are optional for single params in an arrow function signature. You need them when you use more than one param.

In ES5 the code has function with explicit return:

var ids = ['5632953c4e345e145fdf2df8', '563295464e345e145fdf2df9'];
var messages = ids.map(function (value, index, list) {
  return 'ID of ' + index + ' element is ' + value + ' ' // explicit return
})
And more eloquent version of the code in ES6 with parenthesis around params and implicit return:

var ids = ['5632953c4e345e145fdf2df8','563295464e345e145fdf2df9']
var messages = ids.map((value, index, list) => `ID of ${index} element is ${value} `) // implicit return
7. Promises in ES6
Promises have been a controversial topic. There were a lot of promise implementations with slightly different syntax. q, bluebird, deferred.js, vow, avow, jquery deferred to name just a few. Others said we don’t need promises and can just use async, generators, callbacks, etc. Gladly, there’s a standard Promise implementation in ES6 now!

Let’s consider a rather trivial example of a delayed asynchronous execution with setTimeout():

setTimeout(function(){
  console.log('Yay!')
}, 1000)
We can re-write the code in ES6 with Promise:

var wait1000 =  new Promise(function(resolve, reject) {
  setTimeout(resolve, 1000)
}).then(function() {
  console.log('Yay!')
})
Or with ES6 arrow functions:

var wait1000 =  new Promise((resolve, reject)=> {
  setTimeout(resolve, 1000)
}).then(()=> {
  console.log('Yay!')
})
So far, we’ve increased the number of lines of code from three to five without any obvious benefit. That’s right. The benefit will come if we have more nested logic inside of the setTimeout() callback:

setTimeout(function(){
  console.log('Yay!')
  setTimeout(function(){
    console.log('Wheeyee!')
  }, 1000)
}, 1000)
Can be re-written with ES6 promises:

var wait1000 =  ()=> new Promise((resolve, reject)=> {setTimeout(resolve, 1000)})

wait1000()
  .then(function() {
    console.log('Yay!')
    return wait1000()
  })
  .then(function() {
    console.log('Wheeyee!')
  })
Still not convinced that Promises are better than regular callbacks? Me neither. I think once you got the idea of callbacks and wrap your head around them, then there’s no need for additional complexity of promises.

Nevertheless, ES6 has Promises for those of you who adore them. Promises have a fail-and-catch-all callback as well which is a nice feature. Take a look at this post for more info on promises: Introduction to ES6 Promises.

8. Block-Scoped Constructs Let and Const
You might have already seen the weird sounding let in ES6 code. I remember the first time I was in London, I was confused by all those TO LET signs. The ES6 let has nothing to do with renting. This is not a sugarcoating feature. It’s more intricate. let is a new var which allows to scope the variable to the blocks. We define blocks by the curly braces. In ES5, the blocks did NOTHING to the vars:

function calculateTotalAmount (vip) {
  var amount = 0
  if (vip) {
    var amount = 1
  }
  { // more crazy blocks!
    var amount = 100
    {
      var amount = 1000
      }
  }  
  return amount
}

console.log(calculateTotalAmount(true))
The result will be 1000. Wow! That’s a really bad bug. In ES6, we use let to restrict the scope to the blocks. Vars are function scoped.

function calculateTotalAmount (vip) {
  var amount = 0 // probably should also be let, but you can mix var and let
  if (vip) {
    let amount = 1 // first amount is still 0
  } 
  { // more crazy blocks!
    let amount = 100 // first amount is still 0
    {
      let amount = 1000 // first amount is still 0
      }
  }  
  return amount
}

console.log(calculateTotalAmount(true))
The value is 0, because the if block also has let. If it had nothing (amount=1), then the expression would have been 1.

When it comes to const, things are easier; it’s just an immutable, and it’s also block-scoped like let. Just to demonstrate, here are a bunch of constants and they all are okay because they belong to different blocks:

function calculateTotalAmount (vip) {
  const amount = 0  
  if (vip) {
    const amount = 1 
  } 
  { // more crazy blocks!
    const amount = 100 
    {
      const amount = 1000
      }
  }  
  return amount
}

console.log(calculateTotalAmount(true))
In my humble opinion, let and const overcomplicate the language. Without them we had only one behavior, now there are multiple scenarios to consider. ;-(

9. Classes in ES6
If you love object-oriented programming (OOP), then you’ll love this feature. It makes writing classes and inheriting from them as easy as liking a comment on Facebook.

Classes creation and usage in ES5 was a pain in the rear, because there wasn’t a keyword class (it was reserved but did nothing). In addition to that, lots of inheritance patterns like pseudo classical, classical, functional just added to the confusion, pouring gasoline on the fire of religious JavaScript wars.

I won’t show you how to write a class (yes, yes, there are classes, objects inherit from objects) in ES5, because there are many flavors. Let’s take a look at the ES6 example right away. I can tell you that the ES6 class will use prototypes, not the function factory approach. We have a class baseModel in which we can define a constructor and a getName() method:

class baseModel {
  constructor(options = {}, data = []) { // class constructor
    this.name = 'Base'
    this.url = 'http://azat.co/api'
    this.data = data
    this.options = options
  }

    getName() { // class method
      console.log(`Class name: ${this.name}`)
    }
}
Notice that I’m using default parameter values for options and data. Also, method names don’t need to have the word function or the colon (:) anymore. The other big difference is that you can’t assign properties this.NAME the same way as methods, i.e., you can’t say name at the same indentation level as a method. To set the value of a property, simply assign a value in the constructor.

The AccountModel inherits from baseModel with class NAME extends PARENT_NAME:

class AccountModel extends baseModel {
  constructor(options, data) {
To call the parent constructor, effortlessly invoke super() with params:

    super({private: true}, ['32113123123', '524214691']) //call the parent method with super
     this.name = 'Account Model'
     this.url +='/accounts/'
   }
If you want to be really fancy, you can set up a getter like this and accountsData will be a property:

 get accountsData() { //calculated attribute getter
    // ... make XHR
    return this.data
  }
}
So how do you actually use this abracadabra? It’s as easy as tricking a three-year old into thinking Santa Claus is real:

let accounts = new AccountModel(5)
accounts.getName()
console.log('Data is %s', accounts.accountsData)
In case you’re wondering, the output is:

Class name: Account Model
Data is %s 32113123123,524214691
10. Modules in ES6
As you might now, there were no native modules support in JavaScript before ES6. People came up with AMD, RequireJS, CommonJS and other workarounds. Now there are modules with import and export operands.

In ES5 you would use <script> tags with IIFE, or some library like AMD, while in ES6 you can expose your class with export. I am a Node.js guy, so I’ll use CommonJS which is also a Node.js syntax. It’s straightforward to use CommonJS on the browser with the Browserify bunder. Let’s say we have port variable and getAccounts method in ES5 module.js:

module.exports = {
  port: 3000,
  getAccounts: function() {
    ...
  }
}
In ES5 main.js, we would require('module') that dependency:

var service = require('module.js')
console.log(service.port) // 3000
In ES6, we would use export and import. For example, this is our library in the ES6 module.js file:

export var port = 3000
export function getAccounts(url) {
  ...
}
In the importer ES6 file main.js, we use import {name} from 'my-module' syntax. For example,

import {port, getAccounts} from 'module'
console.log(port) // 3000
Or we can import everything as a variable service in main.js:

import * as service from 'module'
console.log(service.port) // 3000
Personally, I find the ES6 modules confusing. Yes, they are more eloquent, but Node.js modules won’t change anytime soon. It’s better to have only one style for browser and server JavaScript, so I’ll stick with CommonJS/Node.js style for now.

The support for ES6 modules in the browsers are not coming anytime soon (as of this writing), so you’ll need something like jspm to use ES6 modules.

For more information and examples on ES6 modules, take a look at this text. No matter what, write modular JavaScript!

How to Use ES6 Today (Babel)
ES6 is finalized, but not fully supported by all browsers (e.g., ES6 Firefox support). To use ES6 today, get a compiler like Babel. You can run it as a standalone tool or use with your build system. There are Babel plugins for Grunt, Gulp and Webpack.

How to Use ES6 Today (Babel)
How to Use ES6 Today (Babel)

Here’s a Gulp example. Install the plugin:

$ npm install --save-dev gulp-babel
