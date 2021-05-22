# frontend-interview-question
Frontend interview question with answer


# Program for anagram?

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

# Program for decimal to binary?

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

# Program for summation of diagonal elements

    function diagonalSums(matrix) {
 
    let mainSum = 0, secondarySum = 0;
    for (let row = 0; row < matrix.length; row++) {
        mainSum += matrix[row][row];
        secondarySum += matrix[row][matrix.length - row - 1];
    }
    console.log(mainSum + ' ' + secondarySum);
    }
 
    diagonalSums([[20, 40], [10, 60]]);


# How do you improve the performance of your web application?

# 1. Cache in the browser

There are two options for doing this. The first is to use the JavaScript Cache API, which we can use by installing a service worker. The second is to use the HTTP protocol cache.

Scripts are often used to access a certain object. By storing a repeated access object inside a user-defined variable, as well as using a variable in subsequent references to that object, performance improvement can be achieved immediately.

# 2. Define the execution context

In order to effectively measure any improvements that you’re incorporating into your program, you must establish a set of well-defined environments where is possible to test the performance of the code.

Trying to do performance tests and optimizations for all versions of all Javascript engines is not feasible in practice. But, it is not a good practice to do testing in a single environment, as this can give you partial results. So, it’s important to establish multiple well-defined environments and test that the code works on them.

# 3. Remove unused JavaScript

This step will not only reduce transmission time, but also the time it takes for the browser to analyze and compile the code. To do this, you must take into account the following points: - If you detect a functionality that is not being used by users, it’s a good practice to remove it with all its associated JavaScript code, so the website will load faster and users will have a better experience. - It is also possible that a library was included by mistake and is not necessary, or that you have dependencies that offer some functionality that is already natively available in all browsers, without the need to use additional code

# 4. Avoid using too much memory

You should always try to limit memory use to what is absolutely necessary, because is not possible to know how much memory is required by the device being used to run your app. Any time your code requests that the browser reserve new memory, the browser’s garbage collector is executed, and JavaScript is stopped. If this happens frequently, the page will work slowly.

# 5. Defer the load of JavaScript that is not necessary

Users want to see a page load quickly, but it’s not likely that all functions need to be available for the initial load of the page. If a user must perform a certain action in order for a function to be executed (e.g. by clicking on an element, or changing tabs), it’s possible to defer loading that function until after the initial page load.

In this way you can avoid loading and compiling JavaScript code that would delay the initial display of the page. Once the page is fully loaded, we can start loading those functionalities so that they are available immediately when the user starts to interact. In the RAIL model, Google recommends that this deferred load to be done in blocks of 50ms, so that it does not influence the user's interaction with the page.

# 6. Avoid memory leaks

If a memory leak is ongoing, the loaded page will reserve more and more memory, eventually occupying all the available memory of the device and severely impacting performance. You’ve probably seen (and likely been frustrated by) this type of failure, likely on a page with a carousel or image slider.

In Chrome Dev Tools, you can analyze if your website has memory leaks by recording a timeline in the Performance tab. Usually, memory leaks come from pieces of the DOM that are removed from the page but have some variable that makes reference to them and, therefore, the garbage collector can not eliminate them.

# 7. Use web workers when you need to execute code that needs a lot of execution time

According to the Mozilla Developers Network (MDN) documentation: “Web Workers makes it possible to run a script operation in a background thread separate from the main execution thread of a web application. The advantage of this is that laborious processing can be performed in a separate thread, allowing the main (usually the UI) thread to run without being blocked/slowed down.”

Web workers allow your code to perform processor-intensive calculations without blocking the user interface thread. Web Workers allow you spawn new threads and delegate work to these threads for efficient performance. This way, long running tasks which would normally block other tasks are passed off to a worker and the main thread can run without being blocked.

# 8. If you access a DOM item several times, save it in a local variable

Accessing the DOM is slow. If you are going to read the content of an element several times, it's better to save it in a local variable. But it’s important to keep in mind, if you will later remove the value of the DOM, the variable should be set to "null", so it doesn’t cause any memory leaks.

# 9. Prioritize access to local variables

JavaScript first searches to see if a variable exists locally, then searches progressively in higher levels of scope until global variables. Saving variables in a local scope allows JavaScript to access them much faster.

Local variables are found based on the most specific scope and can pass through multiple levels of scope, the look-ups can result in generic queries. When defining the function scope, within a local variable without a preceding variable declaration, it is important to precede each variable with let or const in order to define the current scope in order to prevent the look-up and to speed up the code.

# 10. Avoid using global variables

Because the scripting engine needs to look through the scope when referencing global variables from within function or another scope, the variable will be destroyed when the local scope is lost. If variables in the global scope can not persist through the lifetime of the script, the performance will be improved.

# 11. Implement the optimizations that you would apply in any other programming language

Always use the algorithms with the least computational complexity to solve the task with the optimal data structures
Rewrite the algorithm to get the same result with fewer calculations
Avoid recursive calls
Put in variables, the calculations and calls to functions that are repeated
Factor and simplify mathematical formulas
Use search arrays: they are used to obtain a value based on another instead of using a switch/case statement
Make conditions always more likely to be true to take better advantage of the speculative execution of the processor
Use bit-level operators when you can to replace certain operations, because these operators use fewer processor cycles

# Explain XSRF with one good example

Cross-site request forgery attacks (CSRF or XSRF for short) are used to send malicious requests from an authenticated user to a web application. The attacker can’t see the responses to the forged requests, so CSRF attacks focus on state changes, not theft of data. Successful CSRF attacks can have serious consequences
When you are browsing a website, it is common for that website to request data from another website on your behalf. For example, in most cases, a video that is shown on a website is not typically stored on the website itself. The video appears to be on the website but is actually being embedded from a video streaming site such as YouTube. That’s the idea behind Content Delivery Networks (CDNs), which are used to deliver content faster. Many websites store scripts, images, and other bandwidth-hungry resources on CDNs, so during browsing, images and script files are downloaded from a CDN source rather than the website itself.

While this improves the browsing experience, it might also be a source of a security problem if a website asks the web browser to retrieve data from another website without the user’s consent. If such requests are not handled correctly, an attacker can launch a cross-site request forgery attack

# How to Prevent Cross-Site Request Forgery Attacks

An attacker can launch a CSRF attack when he knows which parameters and value combination are being used in a form. Therefore, by adding an additional parameter with a value that is unknown to the attacker and can be validated by the server, you can prevent CSRF attacks. Below is a list of some of the methods you can use to block cross-site request forgery attacks.

Implement an Anti-CSRF Token

An anti-CSRF token is a type of server-side CSRF protection. It is a random string that is only known to the user’s browser and the web application. The anti-CSRF token is usually stored inside a session variable. On a page, it is typically in a hidden field that is sent with the request.

If the values of the session variable and the hidden form field match, the web application accepts the request. If they do not match, the request is dropped. In this case, the attacker does not know the exact value of the hidden form field that is needed for the request to be accepted, so he cannot launch a CSRF attack. In fact, due to same origin policy, the attacker can’t even read the response that contains the token.

# Explain event propagation in JavaScript

Event propagation is a mechanism that defines how events propagate or travel through the DOM tree to arrive at its target and what happens to it afterward.

Let's understand this with the help of an example, suppose you have assigned a click event handler on a hyperlink (i.e. <a> element) which is nested inside a paragraph (i.e. <p> element). Now if you click on that link, the handler will be executed. But, instead of link, if you assign the click event handler to the paragraph containing the link, then even in this case, clicking the link will still trigger the handler. That's because events don't just affect the target element that generated the event—they travel up and down through the DOM tree to reach their target. This is known as event propagation

In modern browser event propagation proceeds in two phases: capturing, and bubbling phase.

# The Capturing Phase
In the capturing phase, events propagate from the Window down through the DOM tree to the target node. For example, if the user clicks a hyperlink, that click event would pass through the <html> element, the <body> element, and the <p> element containing the link.

Also if any ancestor (i.e. parent, grandparent, etc.) of the target element and the target itself has a specially registered capturing event listener for that type of event, those listeners are executed during this phase.

# The Bubbling Phase

In the bubbling phase, the exact opposite occurs. In this phase event propagates or bubbles back up the DOM tree, from the target element up to the Window, visiting all of the ancestors of the target element one by one. For example, if the user clicks a hyperlink, that click event would pass through the <p> element containing the link, the <body> element, the <html> element, and the document node.

Also, if any ancestor of the target element and the target itself has event handlers assigned for that type of event, those handlers are executed during this phase.

# Stopping the Event Propagation

You can also stop event propagation in the middle if you want to prevent any ancestor element's event handlers from being notified about the event.

For example, suppose you have nested elements and each element has onclick event handler that displays an alert dialog box. Normally, when you click on the inner element all handlers will be executed at once, since event bubble up to the DOM tree.
To prevent this situation you can stop event from bubbling up the DOM tree using the event.stopPropagation() method. In the following example click event listener on the parent elements will not execute if you click on the child elements.

#  What are differences between $(document).ready and $(window).load?

$(window).load is an event that fires when the DOM and all the content (everything) on the page is fully loaded like CSS, images and frames. One best example is if we want to get the actual image size or to get the details of anything we use it.

$(document).ready() indicates that code in it need to be executed once the DOM got loaded and ready to be manipulated by script. It won't wait for the images to load for executing the jQuery script.

# Write a program to multiply two numbers with out using * symbol

         function multiply(a, b){
           let answer = a
           for(var i = 0; i < b - 1; i++){
             answer += a
           }
           return answer
         }

# Breakdown:

We create a variable named “answer” and assign it the value of “a”. 

Then we create a for loop that will iterate until “i” is less than “b -1”. 

Why “b -1”?

Because we already assigned “answer” to “a”. 

Every iteration we add “a” to “answer”. Once iteration is done we return “answer”.

         Ex:
         multiply(6, 3)           //our a is 6 and b is 3
         //before iteration
         answer is 6              //assign answer equal to a which is 6
         //iteration begins
         answer is now 12         // i is now 1 
         answer is now 18         // i is now 2 which is means break loop as
                                     i is no longer less than b - 1.
         then we return "answer" which would be 18.

# difference between http1 and http2

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

# What is Service Worker:

A service worker is a script that runs independently in the browser background. On the user side, it can intercept its network requests and decide what to load (fetch).
Service workers mainly serve features like background sync, push notifications and they are commonly used for’offline first’ applications, giving the developers the opportunity to take complete control over the user experience.

Before it’s time there has been API called AppCache, which has been trying to serve the offline experience feature. However, there have been numerous problems in the interface of the AppCache API and Service Workers are here, going over them.

# The service worker life cycle:

The service worker lifecycle is completely separate from the web page. It’s a programmable network proxy, which is terminated when it’s not used and restarted when it’s next needed. Service Workers heavily rely on the use of Javascript Promises , so it’s good to go over them if they are new to you.

During installation, the service worker can cache some static assets like web pages. If the browser cache the files successfully, the service worker gets installed.

Afterward, the worker needs to be activated. During activation the service worker can manage and decide what to happen to the old caches, typically they are being deleted and replaced with the new versions.



Lastly, after activation, the service worker takes control over all pages in his scope, without the page which initially registered the service worker, which needs to be refreshed. The service worker is smart in terms of memory usage and will be terminated if there is nothing to fetch and there are no message events occurring.

# Prerequisites :

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


# Fetching event:

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



# Service Worker can’t:‘

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

 Service workers have been designed to be fully asynchronous, as a consequence, APIs such as synchronous XHR and localStorage can’t be used inside a service worker. But since it is working on a different thread it doesn’t block your application in any way.
 
Service workers are terminated when not in use and restored when required. It acts as a programmable network proxy, allowing developers to handle how network requests from the web page is handled. So the developers can take appropriate action based on the availability of network.

# Service Worker v/s Web Worker

Both Service workers and Web workers are JavaScript workers with lots of similarities but there are a few difference too.
Service workers are designed to handle network requests and assist in offline first development, Push Notifications and background syncs. Communication’s with the webpage must go through service workers PostMessage method.
Web workers mimics the multi-threading model, allowing complex / data or processor intensive tasks to run in background. Ideal to keep your UI jank free when you have to deal with a lot of computations. Communication’s with the webpage must go through web workers PostMessage method.

# What is a JavaScript closure?

A JavaScript Closure is when an inner function has access to members of the outer function (lexical scope) even when executing outside the scope of the outer function.

# Lexical Scope

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

# What is the difference between HTTP and HTTPS

HTTP is unsecured while HTTPS is secured.
HTTP sends data over port 80 while HTTPS uses port 443.
HTTP operates at application layer, while HTTPS operates at transport layer.
No SSL certificates are required for HTTP, with HTTPS it is required that you have an SSL certificate and it is signed by a CA.
HTTP doesn't require domain validation, where as HTTPS requires at least domain validation and certain certificates even require legal document validation.
No encryption in HTTP, with HTTPS the data is encrypted before sending.

# Working of web

The moment you enter this address in your browser and you hit ENTER, a lot of different things happen:

1.The URL gets resolved
2.A Request is sent to the server of the website
3.The response of the server is parsed
4.The page is rendered and displayed

Step 1 - URL Gets Resolved

The website code is obviously not stored on your machine and hence needs to be fetched from another computer where it is stored. This “other computer” is called a “server”. Because it serves some purpose, in our case, it serves the website.

You enter “academind.com” (that is called “a domain”) but actually, the server which hosts the source code of a website, is identified via IP (= Internet Protocol) addresses. The browser sends a “request” (see step 2) to the server with the IP address you entered (indirectly - you of course entered “academind.com”).

# How is the domain “academind.com” translated to its IP address?

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

Every HTML tag has some semantic meaning which the browser understands, because HTML is also standardized. Hence there is no guessing about what a h1 tag means.

The browser knows how to parse HTML and now simply goes through the entire response data (also called “the response body”) to render the website.

Step 4 - Page Is Displayed

As mentioned, the browser goes through the HTML data returned by the server and builds a website based on that.

Though it is important to know, that HTML does not include any instructions regarding what the site should look like (i.e. how it should be styled). It really only defines the structure and tells the browser which content is a heading, which content is an image, which content is a paragraph etc. This is especially important for accessibility - screen readers get all the useful information out of the HTML structure.

# Webpack and it's working

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

# Handling images
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

# 6 Primitive data types in js -

1. undefined
2. null
3. boolean
4. string
5. symbol
6. Number


# JS objects Points -

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


# Checking for Palindrome Strings by removing special Characters and Spaces -

Solution :- 

         var A = ‘string’;
         var B = A.toLowerCase().replace(/[^A-Za-z0-9]+/ig, ‘’);
         var C = B.split(‘’).reverse().join(‘’);
         return C

# Write a program to find the sum of diagonal matrices.

         Input : 
         4
         1 2 3 4
         4 3 2 1
         7 8 9 6
         6 5 4 3
         Output :
         Principal Diagonal: 16
         Secondary Diagonal: 20

         Input :
         3
         1 1 1
         1 1 1
         1 1 1
         Output :
         Principal Diagonal: 3
         Secondary Diagonal: 3


         <script>
         // A simple Javascript program to find sum of diagonals

         const MAX = 100;

         void printDiagonalSums(mat, n)
         {
             let principal = 0, secondary = 0;
             for (let i = 0; i < n; i++) {
                 for (let j = 0; j < n; j++) {

                     // Condition for principal diagonal
                     if (i == j)
                         principal += mat[i][j];

                     // Condition for secondary diagonal
                     if ((i + j) == (n - 1))
                         secondary += mat[i][j];
                 }
             }

             document.write("Principal Diagonal:" + principal + "<br>");
             document.write("Secondary Diagonal:" + secondary + "<br>");
         }

         // Driver code
             let a = [ [ 1, 2, 3, 4 ], [ 5, 6, 7, 8 ],
                             [ 1, 2, 3, 4 ], [ 5, 6, 7, 8 ] ];
             printDiagonalSums(a, 4);

         </script>


# Async/ await in es6

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

# ES6 new feature

ECMAScript 6, also known as ECMAScript 2015, is the latest version of the ECMAScript standard. ES6 is a significant update to the language, and the first update to the language since ES5 was standardized in 2009. Implementation of these features in major JavaScript engines is underway now.


# ES6 includes the following new features:

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

# Top 10 ES6 Features
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

# 1. Default Parameters in ES6
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

# 2. Template Literals in ES6

Template literals or interpolation in other languages is a way to output variables in the string. So in ES5 we had to break the string like this:

var name = 'Your name is ' + first + ' ' + last + '.'
var url = 'http://localhost:3000/api/messages/' + id
Luckily, in ES6 we can use a new syntax ${NAME} inside of the back-ticked string:

var name = `Your name is ${first} ${last}.`
var url = `http://localhost:3000/api/messages/${id}`

# 3. Multi-line Strings in ES6

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
# 4. Destructuring Assignment in ES6

Destructuring can be a harder concept to grasp, because there’s some magic going on… let’s say you have simple assignments where keys house and mouse are variables house and mouse:

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

# 5. Enhanced Object Literals in ES6

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

# Enhanced Object Literals in ES6

Enhanced Object Literals in ES6

But for the sake of the example, we’ll consider them similar. 

So in ES6 object literal, there are shorthands for assignment getAccounts: getAccounts, becomes just getAccounts,. Also, we set the prototype right there in the 

__proto__ property which makes sense (not‘proto’ though:

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

# 6. Arrow Functions in ES6

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

Notice that I used the string templates? Another feature from CoffeeScript… 

The parenthesis () are optional for single params in an arrow function signature. You need them when you use more than one param.

In ES5 the code has function with explicit return:

         var ids = ['5632953c4e345e145fdf2df8', '563295464e345e145fdf2df9'];
         var messages = ids.map(function (value, index, list) {
           return 'ID of ' + index + ' element is ' + value + ' ' // explicit return
         })
And more eloquent version of the code in ES6 with parenthesis around params and implicit return:

         var ids = ['5632953c4e345e145fdf2df8','563295464e345e145fdf2df9']
         var messages = ids.map((value, index, list) => `ID of ${index} element is ${value} `) // implicit return
         
# 7. Promises in ES6

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

# 8. Block-Scoped Constructs Let and Const

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

# 9. Classes in ES6

ES6 class will use prototypes, not the function factory approach. We have a class baseModel in which we can define a constructor and a getName() method:

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
# 10. Modules in ES6

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


The support for ES6 modules in the browsers are not coming anytime soon (as of this writing), so you’ll need something like jspm to use ES6 modules.



# How to Use ES6 Today (Babel)

ES6 is finalized, but not fully supported by all browsers (e.g., ES6 Firefox support). To use ES6 today, get a compiler like Babel. You can run it as a standalone tool or use with your build system. There are Babel plugins for Grunt, Gulp and Webpack.


Here’s a Gulp example. Install the plugin:

$ npm install --save-dev gulp-babel

In gulpfile.js, define a task build that takes src/app.js and compiles it into the build folder:

         var gulp = require('gulp'),
           babel = require('gulp-babel')

         gulp.task('build', function () {
           return gulp.src('src/app.js')
             .pipe(babel())
             .pipe(gulp.dest('build'))
         })
Node.js and ES6
For Node.js, you can compile your Node.js files with a build tool or use a standalone Babel module babel-core. To install it,

         $ npm install --save-dev babel-core
Then in Node.js, you call this function:

         require("babel-core").transform(es5Code, options)


# Difference between for...of, for...in and simple for loop

Both for..of and for..in statements iterate over lists; the values iterated on are different though, for..in returns a list of keys on the object being iterated, whereas for..of returns a list of values of the numeric properties of the object being iterated.

Here is an example that demonstrates this distinction:

         let list = [4, 5, 6];

         for (let i in list) {
            console.log(i); // "0", "1", "2",
         }

         for (let i of list) {
            console.log(i); // "4", "5", "6"
         }
         
Another distinction is that for..in operates on any object; it serves as a way to inspect properties on this object. for..of on the other hand, is mainly interested in values of iterable objects. Built-in objects like Map and Set implement Symbol.iterator property allowing access to stored values.

         let pets = new Set(["Cat", "Dog", "Hamster"]);
         pets["species"] = "mammals";

         for (let pet in pets) {
            console.log(pet); // "species"
         }

         for (let pet of pets) {
             console.log(pet); // "Cat", "Dog", "Hamster"
         }
# Prototype chaning

What is a prototype?
What is prototype chaining?
What does hasOwnProperty do?
What is _proto_?

We'll look into it and come to know where all these methods come from. Nearly all objects in JavaScript are instances of Object. That means all the objects in JavaScript inherit the properties and methods from Object.prototype. This is called Prototype chaining. This is a very powerful and potentially dangerous mechanism to override or extend object behavior.

Objects created using the new keyword inherit from a prototype called Object.prototype.

For example: If a date object [new Date()] is created with the new keyword, then it inherits the Date.prototype.

We have Date, Array, Function, RegExp in the list for the same. All these objects inherit from the Object.prototype.

We should never alter or change the predefined methods or properties of a prototype, It may cause inappropriate failure, which may be difficult to debug.

To check whether the object has a property or not, we use hasOwnProperty() method. For example if we have the age property in any object, we can check it with the help of the hasOwnProperty() method. We will come to know more about it in this blog.

Let’s take a look at a quick example of prototype chaining.

In this example, we will create a class and add a prototype object in the same. After instantiation of the object, we will be able to use the prototype of the class. This is simply object prototype chaining.

          function Person(firstName, lastName, age){


           this.firstName = firstName;

           this.lastName = lastName;

           this.age = age;

         }
         //Person class created

         Person.prototype.getFullName = function(){

           return this.firstName + ” ” + this.lastName;

         }
         // we have added getFullName method in Person’s prototype.

          var person = new Person(“pushpendu”, “purkait”, 25);

         // It will create an instance of the Person class

          person.hasOwnProperty(“firstName”);  // true

          person.hasOwnProperty(“getFullName”);  // false

          person.getFullName(); // gautam pandey


In the above code, we used hasOwnProperty() method to check whether we have getFullName method as a property of the object. It returned false, that means there is no such property. But, when we used getFullName method, it returned the actual full name but the property was not there.

How can that be possible?

To know more we have to dig in. As the getFullName() method was not there in the object but still we were able to use it. We should not forget that we added the method in class Person’s prototype. The method went to the object through prototype chaining. It means the class had the method in its prototype, which went to its instance (person object) through prototype chaining. To prove that we will check it in the object.

Whenever we create an instance of any class, the prototype of the class is created in object as well. We have to check it in  _proto_  property. This property contains the prototype of its class. For example: Person’s getFullName() method will be created in object’s _proto_ property.

Let’s take a look into the code:

1
person._proto_.hasOwnProperty(‘getFullName’);  //true


As we can, see _proto_ has the getFullName() method, which is taken from class Person.

We can see more methods and properties like
_defineGetter, __defineSetter, __lookupGetter, __lookupSetter_, constructor etc. which are there because of prototype chaining.

# call, apply and bind

Use .bind() when you want that function to later be called with a certain context, useful in events. Use .call() or .apply() when you want to invoke the function immediately, and modify the context.

Call/apply call the function immediately, whereas bind returns a function that, when later executed, will have the correct context set for calling the original function. This way you can maintain context in async callbacks and events.



         function MyObject(element) {
             this.elm = element;

         element.addEventListener('click', this.onClick.bind(this), false);
         };

         MyObject.prototype.onClick = function(e) {
              var t=this;  //do something with [t]...
             //without bind the context of this function wouldn't be a MyObject
             //instance as you would normally expect.
         };
         
I use it extensively in Node.js for async callbacks that I want to pass a member method for, but still want the context to be the instance that started the async action.

A simple, naive implementation of bind would be like:

         Function.prototype.bind = function(ctx) {
             var fn = this;
             return function() {
                 fn.apply(ctx, arguments);
             };
         };
# Call, apply and bind


call attaches this into function and executes the function immediately:

         var person = {  
           name: "James Smith",
           hello: function(thing) {
             console.log(this.name + " says hello " + thing);
           }
         }

         person.hello("world");  // output: "James Smith says hello world"
         person.hello.call({ name: "Jim Smith" }, "world"); // output: "Jim Smith says hello world"
         bind attaches this into function and it needs to be invoked separately like this:

         var person = {  
           name: "James Smith",
           hello: function(thing) {
             console.log(this.name + " says hello " + thing);
           }
         }

         person.hello("world");  // output: "James Smith says hello world"
         var helloFunc = person.hello.bind({ name: "Jim Smith" });
         helloFunc("world");  // output: Jim Smith says hello world"
or like this:

...    
         var helloFunc = person.hello.bind({ name: "Jim Smith" }, "world");
         helloFunc();  // output: Jim Smith says hello world"
         apply is similar to call except that it takes an array-like object instead of listing the arguments out one at a time:

         function personContainer() {
           var person = {  
              name: "James Smith",
              hello: function() {
                console.log(this.name + " says hello " + arguments[1]);
              }
           }
           person.hello.apply(person, arguments);
         }
         personContainer("world", "mars"); // output: "James Smith says hello mars", note: arguments[0] = "world" , arguments[1] = "mars"
# Call, apply and bind

Call invokes the function and allows you to pass in arguments one by one.
Apply invokes the function and allows you to pass in arguments as an array.
Bind returns a new function, allowing you to pass in a this array and any number of arguments

# Call, apply and bind

Apply vs. Call vs. Bind Examples
Call

         var person1 = {firstName: 'Jon', lastName: 'Kuperman'};
         var person2 = {firstName: 'Kelly', lastName: 'King'};

         function say(greeting) {
             console.log(greeting + ' ' + this.firstName + ' ' + this.lastName);
         }

         say.call(person1, 'Hello'); // Hello Jon Kuperman
         say.call(person2, 'Hello'); // Hello Kelly King
         Apply

         var person1 = {firstName: 'Jon', lastName: 'Kuperman'};
         var person2 = {firstName: 'Kelly', lastName: 'King'};

         function say(greeting) {
             console.log(greeting + ' ' + this.firstName + ' ' + this.lastName);
         }

         say.apply(person1, ['Hello']); // Hello Jon Kuperman
         say.apply(person2, ['Hello']); // Hello Kelly King

# Bind

         var person1 = {firstName: 'Jon', lastName: 'Kuperman'};
         var person2 = {firstName: 'Kelly', lastName: 'King'};

         function say() {
             console.log('Hello ' + this.firstName + ' ' + this.lastName);
         }

         var sayHelloJon = say.bind(person1);
         var sayHelloKelly = say.bind(person2);

         sayHelloJon(); // Hello Jon Kuperman
         sayHelloKelly(); // Hello Kelly King
         
When To Use Each
         Call and apply are pretty interchangeable. Just decide whether it’s easier to send in an array or a comma separated list of arguments.

         I always remember which one is which by remembering that Call is for comma (separated list) and Apply is for Array.

         Bind is a bit different. It returns a new function. Call and Apply execute the current function immediately.

         Bind is great for a lot of things. We can use it to curry functions like in the above example. We can take a simple hello function and turn it into a helloJon or helloKelly. We can also use it for events like onClick where we don’t know when they’ll be fired but we know what context we want them to have.
# Diff B/w filter, map, reduce and forEach

1. Foreach
The easy one right ? we all know why this method is used for and even you don’t know about this method the name pretty much explains everything.
Foreach takes a callback function and run that callback function on each element of array one by one.

         var sample = [1, 2, 3];
         // es5
         sample.forEach(function (elem, index){
            console.log(elem + ' comes at ' + index);
         })
         // es6
         sample.forEach((elem, index) => `${elem} comes at ${index}`)
         /*
output
1 comes at 0
2 comes at 1
3 comes at 2
*/

For every element on the array we are calling a callback which gets element & its index provided by foreach.
Basically forEach works as a traditional for loop looping over the array and providing you array elements to do operations on them.
okay! so clear ? then let’s filter some arrays.

# 2. Filter

Whenever you have to filter an array Javascript inbuilt method to filter your array is the right choice to use. Filter let you provide a callback for every element and returns a filtered array.
The main difference between forEach and filter is that forEach just loop over the array and executes the callback but filter executes the callback and check its return value. If the value is true element remains in the resulting array but if the return value is false the element will be removed for the resulting array.

         var sample = [1, 2, 3] // yeah same array
         // es5
         var result = sample.filter(function(elem){
             return elem !== 2;
         })
         console.log(result)
         // es6
         var result = sample.filter(elem => elem !== 2)
         /* output */
         [1, 3]
See how easy it was. We passed a callback to filter which got run against every element in the array. In the callback we checked if the element !== 2 if the condition fails ( when elem was equal to 1 or 3 ) include them into the resulting array else don’t include the element in the resulting array.
Also take notice filter does not update the existing array it will return a new filtered array every time.
# 3. Map

One of my favourite and most used array method of all time. As a ReactJS developer I use map a lot inside my application UI.
Map like filter & foreach takes a callback and run it against every element on the array but whats makes it unique is it generate a new array based on your existing array.
Let’s understand map with an example

         var sample = [1, 2, 3] // i am never gonna change Boo! Yeah
         // es5
         var mapped = sample.map(function(elem) {
             return elem * 10;
         })
         // es6
         let mapped = sample.map(elem => elem * 10)
         console.log(mapped);
         /* output */
         [10, 20, 30]
         
Map ran through every element of the array, multiplied it to 10 and returned the element which will be going to store inside our resulting array.
Like filter, map also returns an array. The provided callback to map modifies the array elements and save them into the new array upon completion that array get returned as the mapped array.
And last but not least …

# 4. Reduce

As the name already suggest reduce method of the array object is used to reduce the array to one single value.
For example if you have to add all the elements of an array you can do something like this.

         var sample = [1, 2, 3] // here we meet again
         // es5
         var sum = sample.reduce(function(sum, elem){
             return sum + elem;
         })
         // es6
         var sum = sample.reduce((sum, elem) => sum + elem)
         console.log(sum)
reduce takes a callback ( like every function we talked about ). Inside this callback we get two arguments sum & elem. The sum is the last returned value of the reduce function. For example initially the sum value will be 0 then when the callback runs on the first element it will add the elem to the sum and return that value. On second iteration the sum value will be first elem + 0, on third iteration it will be 0 + first elem + second elem.
So that is how reduce works it reduces the array into one single value and returns it upon completion.

# What is Shadow DOM?

I assume you know what a DOM ( Document Object Model ) is, if you don’t you should definitely check it out. On a very high level, a DOM is a tree representation of HTML running inside the browser. The browser uses it for a lot of purpose including adding, removing nodes, changing the style of a specific component etc.
Let’s get back to the Shadow DOM. A Shadow DOM is a hidden dom which can be attached to any element inside our real DOM. It works like a normal DOM. We can use all of the DOM APIs with it but one of the coolest benefits of the Shadow DOM is that all of its markup and style will be scoped. So any CSS that we write inside it will not affect the real DOM. isn’t it cool?
Enough talk. Let’s try out Shadow DOM.

# Trying out Shadow Dom
Creating a Shadow DOM is simple as calling attachShadow on any element and this will return our Shadow DOM and then we can do anything we want with it.

If you run this HTML file in your browser you will see I am a shadow node paragraph written in your browser. What we did above is simple. We take ref of an element with id shadow-dom-container and then called attachShadow on it in return we get the Shadow DOM which we saved in the shadowDOM variable. In the next line we created a paragraph element and set it’s text to I am a shadow node paragraph and in the last line, we appended the element to our Shadow DOM.
Passing {mode: "open"} to attachShadow will allow us to access Shadow DOM anytime by using container.shadowRoot property.
No magic here. Everything is working as it works in real dom so what’s the fuss about? Let’s have a look at another example here

So everything else is the same but we also have a style element now in our code. So we basically created a style tag and inserted some style which will make p font color red but if you noticed we also have a normal p tag below the shadow-dom-container div which is not affected by our Shadow DOM.
If you run this HTML file in your browser you will get
Image for post
If you notice the style we appended to the Shadow DOM only affected the p element inside the Shadow DOM, in other words, the style of our Shadow DOM is scoped hence not affecting the real DOM.

# Throttling

Imagine yourself as a 7-year-old toddler who loves to eat chocolate cake! Today your mom has made one, but it's not for you, it's for the guests! You, being spunky, keep on asking her for the cake. Finally, she gives you the cake. But, you keep on asking her for more. Annoyed, she agrees to give you more cake with a condition that you can have the cake only after an hour. Still, you keep on asking her for the cake, but now she ignores you. Finally, after an interval of one hour, you get more cake. If you ask for more, you will get it only after an hour, no matter how many times you ask her.

This is what throttling is!

Throttling is a technique in which, no matter how many times the user fires the event, the attached function will be executed only once in a given time interval.

For instance, when a user clicks on a button, a helloWorld function is executed which prints Hello, world on the console. Now, when throttling is applied with 1000 milliseconds to this helloWorld function, no matter how many times the user clicks on the button, Hello, world will be printed only once in 1000 milliseconds. Throttling ensures that the function executes at a regular interval.

We’re going to implement throttling later in the article.

# Debouncing
Consider the same cake example. This time you kept on asking your mom for the cake so many times that she got annoyed and told you that she will give you the cake only if you remain silent for one hour. This means you won’t get the cake if you keep on asking her continuously - you will only get it one hour after last time you ask, once you stop asking for the cake. This is debouncing.

In the debouncing technique, no matter how many times the user fires the event, the attached function will be executed only after the specified time once the user stops firing the event.

For instance, suppose a user is clicking a button 5 times in 100 milliseconds. Debouncing will not let any of these clicks execute the attached function. Once the user has stopped clicking, if debouncing time is 100 milliseconds, the attached function will be executed after 100 milliseconds. Thus, to a naked eye, debouncing behaves like grouping multiple events into one single event.

When You’ll Need Them
Debouncing and throttling are recommended to use on events that a user can fire more often than you need them to.

Examples include window resizing and scrolling. The main difference between throttling and debouncing is that throttling executes the function at a regular interval, while debouncing executes the function only after some cooling period.

Debouncing and throttling are not something provided by JavaScript itself. They’re just concepts we can implement using the setTimeout web API. Some libraries like underscore.js and loadash provide these methods out of the box.

Both throttling and debouncing can be implemented with the help of the setTimeout function. So, let’s try to understand the setTimeout function.

# setTimeout

setTimeout is a scheduling function in JavaScript that can be used to schedule the execution of any function. It is a web API provided by the browsers and used to execute a function after a specified time. Here’s the basic syntax:

var timerId = setTimeout(callbackFunction, timeToDelay)

The setTimeout function takes input as a callbackFunction that is the function which will be executed after the timer expires, and timeToDelay is the time in milliseconds after which the callbackFunction will be executed.

The setTimeout function returns a timerId, which is a positive integer value to uniquely identify the timer created by the call to setTimeout; this value can be passed to clearTimeout to cancel the timeout.

Example

         function delayFuncExec() {
                  console.log("I will be called after 100 milliseconds");
         }

var timerId = setTimeout…

# Primitive data types in js -
1. undefined
2. null
3. boolean
4. string
5. symbol
6. Number


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

# JS Hoisting and Can functions be hoisted

Hoisting is a JavaScript mechanism where variables and function declarations are moved to the top of their scope before code execution.

Inevitably, this means that no matter where functions and variables are declared, they are moved to the top of their scope regardless of whether their scope is global or local.


Function expressions in JavaScript are not hoisted. Therefore, you cannot use function expressions before defining them.

how hoisting affects them.

Function Declaration
The function declaration defines a function with the specified parameters.
Syntax:

function name(param1, param2, ...) {  [statements]}
In JavaScript, function declarations hoist the function definitions.

Therefore, these functions can be used before they are declared.
Example:

hoisted() // output: "Hoisted"
function hoisted() {  console.log('Hoisted')}
Behind the scenes, this is how the JavaScript interpreter looks at the above code:

// Hoisted codefunction hoisted() {  console.log('Hoisted')}
// Rest of the codehoisted() // output: "Hoisted"
This behavior is true if you have function declarations in the Global Scope or Functional Scope (basically Local Scope in JavaScript).

This can be helpful because you can use your higher-level logic at the beginning of the code making it more readable and understandable.

Note: Never use function declarations inside if/else blocks.

# Function Expression
The function keyword can also be used to define a function inside an expression.
Syntax:

         const myFunction = function [name](param1, param2, ...) {  [statements]}
         The [name] is optional, therefore these can be anonymous functions. We can use arrow functions as well like so:

         const myFunction = (param1, param2, ...) => {  [statements]}

Function expressions in JavaScript are not hoisted.

Therefore, you cannot use function expressions before defining them.
Example:

         notHoisted() // TypeError: notHoisted is not a function
         const notHoisted = function() {  console.log('foo')}
This is all there is to be kept in mind for creating functions from a hoisting point of view.
Now on to some interview questions!

# What is the difference between localStorage, sessionStorage, session and cookies?

## LocalStorage

Pros:

Web storage can be viewed simplistically as an improvement on cookies, providing much greater storage capacity. If you look at the Mozilla source code we can see that 5120KB (5MB which equals 2.5 Million chars on Chrome) is the default storage size for an entire domain. This gives you considerably more space to work with than a typical 4KB cookie.
The data is not sent back to the server for every HTTP request (HTML, images, JavaScript, CSS, etc) - reducing the amount of traffic between client and server.
The data stored in localStorage persists until explicitly deleted. Changes made are saved and available for all current and future visits to the site.
Cons:

It works on same-origin policy. So, data stored will only be available on the same origin.
Cookies

### Pros:

Compared to others, there's nothing AFAIK.
Cons:

The 4K limit is for the entire cookie, including name, value, expiry date etc. To support most browsers, keep the name under 4000 bytes, and the overall cookie size under 4093 bytes.
The data is sent back to the server for every HTTP request (HTML, images, JavaScript, CSS, etc) - increasing the amount of traffic between client and server.

Typically, the following are allowed:

300 cookies in total
4096 bytes per cookie
20 cookies per domain
81920 bytes per domain(Given 20 cookies of max size 4096 = 81920 bytes.)

# sessionStorage

Pros:
Session storage will generally allow you to store any primitives or objects supported by your Server Side language/framework.
It is similar to localStorage.
The data is not persistent i.e. data is only available per window (or tab in browsers like Chrome and Firefox). Data is only available during the page session. Changes made are saved and available for the current page, as well as future visits to the site on the same window. Once the window is closed, the storage is deleted.
Cons:

The data is available only inside the window/tab in which it was set.
Like localStorage, it works on same-origin policy. So, data stored will only be available on the same origin.

# localStorage, sessionStorage, session and cookies?

LocalStorage
localStorage is a way to store data on the client’s computer. It allows the saving of key/value pairs in a web browser and it stores data with no expiration date. localStorage can only be accessed via JavaScript, and HTML5. However, the user has the ability to clear the browser data/cache to erase all localStorage data.

### Pros:

stores data with no expiration date
storage limit is about 5MB
data is never transferred to the server

### Cons:

plaintext, hence not secure by design
limited to string data, hence need to be serialized
can only be read on client-side
Image for post
Local Storage
So we see , we have key value storage, where we have key and value as an serialized object.
We can try localstorage api from console
and it will create a key value pair in localstorage store.


# Session storage

stores data only for a session, meaning that the data is stored until the browser (or tab) is closed
data is never transferred to the server
can only be read on client-side
storage limit is about 5-10MB
opening multiple tabs/windows with the same URL creates sessionStorage for each tab/window
Same as localstorage , we can write key-value pair in session storage as well.


# Cookie
Stores data that has to be sent back to the server with subsequent XHR requests. Its expiration varies based on the type and the expiration duration can be set from either server-side or client-side .
Cookies are primarily for server-side reading (can also be read on client-side), localStorage and sessionStorage can only be read on client-side.
Size must be less than 4KB.
Cookies can be made secure by setting the httpOnly flag as true for that cookie. This prevents client-side access to that cookie.
Image for post
Cookies can be updated , set using document.cookie object from browser window object.
Image for post
Image for post
In chrome browser, by inspect element, we can go to application tab and see values which are in localStorage, Session Storage and Cookies.
So in nutshell

# settimeout function
The JS setTimeout() method will call a function after the time specified in milliseconds (1000 ms = 1 second) has passed.
The specified function will be executed once. If you need to run a function multiple times, use the setInterval() method.
To stop the timeout and prevent the function from executing, use the clearTimeout() method.
The JavaScript setTimeout() method returns an ID which can be used in clearTimeout() method.

# What’s the Difference Between Class & Prototypal Inheritance?


Class Inheritance: A class is like a blueprint — a description of the object to be created. Classes inherit from classes and create subclass relationships: hierarchical class taxonomies.

Instances are typically instantiated via constructor functions with the `new` keyword. Class inheritance may or may not use the `class` keyword from ES6. Classes as you may know them from languages like Java don’t technically exist in JavaScript. Constructor functions are used, instead. The ES6 `class` keyword desugars to a constructor function:

class Foo {}
typeof Foo // 'function'

In JavaScript, class inheritance is implemented on top of prototypal inheritance, but that does not mean that it does the same thing:
JavaScript’s class inheritance uses the prototype chain to wire the child `Constructor.prototype` to the parent `Constructor.prototype` for delegation. Usually, the `super()` constructor is also called. Those steps form single-ancestor parent/child hierarchies and create the tightest coupling available in OO design.
“Classes inherit from classes and create subclass relationships: hierarchical class taxonomies.”

# Prototypal Inheritance: 

A prototype is a working object instance. Objects inherit directly from other objects.
Instances may be composed from many different source objects, allowing for easy selective inheritance and a flat [[Prototype]] delegation hierarchy. In other words, class taxonomies are not an automatic side-effect of prototypal OO: a critical distinction.
Instances are typically instantiated via factory functions, object literals, or `Object.create()`.
“A prototype is a working object instance. Objects inherit directly from other objects.”

Why Does this Matter?
Inheritance is fundamentally a code reuse mechanism: A way for different kinds of objects to share code. The way that you share code matters because if you get it wrong, it can create a lot of problems, specifically:
Class inheritance creates parent/child object taxonomies as a side-effect.
Those taxonomies are virtually impossible to get right for all new use cases, and widespread use of a base class leads to the fragile base class problem, which makes them difficult to fix when you get them wrong. In fact, class inheritance causes many well known problems in OO design:
The tight coupling problem (class inheritance is the tightest coupling available in oo design), which leads to the next one…
The fragile base class problem
Inflexible hierarchy problem (eventually, all evolving hierarchies are wrong for new uses)
The duplication by necessity problem (due to inflexible hierarchies, new use cases are often shoe-horned in by duplicating, rather than adapting existing code)
The Gorilla/banana problem (What you wanted was a banana, but what you got was a gorilla holding the banana, and the entire jungle)
I discuss some of the issues in more depth in my talk, “Classical Inheritance is Obsolete: How to Think in Prototypal OO”:
# Functional inheritance: 

In JavaScript, any function can create an object. When that function is not a constructor (or `class`), it’s called a factory function. Functional inheritance works by producing an object from a factory, and extending the produced object by assigning properties to it directly (using concatenative inheritance). Douglas Crockford coined the term, but functional inheritance has been in common use in JavaScript for a long time.

# JavaScript Prototypal Inheritance
In this programming paradigm, a class is a blueprint for creating objects. If you want a new class to reuse the functionality of an existing class, you can create a new class that extends the existing class. This is called classical inheritance.

JavaScript doesn’t use classical inheritance. Instead, it uses prototypal inheritance.

In prototypal inheritance, an object “inherits” properties from another object via the prototype linkage.

JavaScript prototypal inheritance and _proto_
Let’s take an example to make the concept more clear.

The following defines a person object:

         let person = {
             name: "John Doe",
             greet: function () {
                 return "Hi, I'm " + this.name;
             }
         };
Code language: JavaScript (javascript)
The person object has two properties:

name that holds a string value.
greet that holds a value that happens to be a function. The greet is known as a method of the person object.
By default, JavaScript provides you with an Object() function and a prototype object that can be accessed via the prototype property of the Object() function:

#JavaScript Prototypal Inheritance - 

person
When you use the object literal syntax to define an object, the object is an instance of the Object. Therefore, the expression person instanceof Object returns true:

         console.log(person instanceof Object)
         Code language: JavaScript (javascript)
         Output:

         true
         
Code language: JavaScript (javascript)
The person object also links to the Object.prototype via the [[prototype]] linkage.

In other words, you can access any properties of the Object.prototype object via the person object. For example:

         console.log(person.toString());
         Code language: JavaScript (javascript)
         Output:

         [object Object]
         Code language: JavaScript (javascript)
         The [object Object] is the default conversion from an object to string.

When you call toString() method on the person object, JavaScript cannot find it. So JavaScript follows the prototype chain and searches for the method on the Object.prototype object. JavaScript can find the toString() method on the Object.prototype object and executes it.

To access the prototype of the person object, you can use its _proto_ property:

         console.log(person._proto_);
         Code language: JavaScript (javascript)
         Output:

         [Object: null prototype] {}
         Code language: JavaScript (javascript)
         The following defines another object called teacher. The teacher object has the teach() method:

         let teacher = {
             teach: function (subject) {
                 return "I can teach " + subject;
             }
         };
         Code language: JavaScript (javascript)

If you want the teacher object to access all properties of the person object, you can set the prototype of teacher object to the person object:

teacher._proto_ = person;
Code language: JavaScript (javascript)

Note that you should never use the _proto_ in the production code. This is just for learning and understanding purposes.

Now, the teacher object can access the name property and greet() method from the person object via the prototype chain:

         console.log(teacher.name);
         console.log(teacher.greet());
         Code language: JavaScript (javascript)
         Output:

         John Doe
         Hi, I'm John Doe
         Code language: JavaScript (javascript)
When you call the greet() method on the teacher object, JavaScript finds it on the teacher object first.

Since JavaScript cannot find the method on the teacher object, it follows the prototype chain and searches for the method on the person object. This time, JavaScript can find the method on the person object and executes the greet() method.

In JavaScript, we say that the teacher object inherits properties of the person object. And this is prototypal inheritance.

A standard way to implement prototypal inheritance in ES5
ES5 provided a standard way to work with prototypal inheritance by using the Object.create() method.

Note that now you should use the newer ES6 class and extends keywords to implement inheritance. It’s much simpler.

The Object.create() method creates a new object and uses an existing object as a prototype of the new object:

         Object.create(proto, [propertiesObject])
         The Object.create() method accepts two arguments:

The first argument (proto) is an object used as the prototype for the new object.
The second argument (propertiesObject), if provided, is an optional object that defines additional properties for the new object.
Suppose you have a person object:

         let person = {
             name: "John Doe",
             greet: function () {
                 return "Hi, I'm " + this.name;
             }
         };
The following creates an empty teacher object with the _proto_ of the person object:

         let teacher = Object.create(person);
After that, you can define properties for the teacher object:

         teacher.name = 'Jane Doe';
         teacher.teach = function (subject) {
                 return "I can teach " + subject;
         }
Or you can do all of these steps in one statement as follows:

         let teacher = Object.create(person, {
             name: { value: 'John Doe' } ,
             teach: { value: function(subject) {
                 return "I can teach " + subject;
             }}
             
         });
ES5 also introduced the Object.getPrototypeOf() method that returns the prototype of an object. For example:

         console.log(Object.getPrototypeOf(teacher) === person);
Output:

true
Summary
Inheritance allows one object to use the properties and methods of another object.
JavaScript uses prototypal inheritance achieved via prototype linkage.

# Classes
JavaScript Classes are templates for JavaScript Objects.
Use the keyword class to create a class.

Always add a method named constructor():

Syntax

         class ClassName {
           constructor() { ... }
         }
Example

         class Car {
           constructor(name, year) {
             this.name = name;
             this.year = year;
           }
         }
The example above creates a class named "Car".

The class has two initial properties: "name" and "year".

A JavaScript class is not an object.

It is a template for JavaScript objects.


Using a Class
When you have a class, you can use the class to create objects:

Example

         let myCar1 = new Car("Ford", 2014);
         let myCar2 = new Car("Audi", 2019);

The example above uses the Car class to create two Car objects.


The constructor method is called automatically when a new object is created.

# The Constructor Method

The constructor method is a special method:

It has to have the exact name "constructor"
It is executed automatically when a new object is created
It is used to initialize object properties
If you do not define a constructor method, JavaScript will add an empty constructor method.

# Class Methods

Class methods are created with the same syntax as object methods.

Use the keyword class to create a class.

Always add a constructor() method.

Then add any number of methods.

         Syntax
         class ClassName {
           constructor() { ... }
           method_1() { ... }
           method_2() { ... }
           method_3() { ... }
         }
Create a Class method named "age", that returns the Car age:

Example
         class Car {
           constructor(name, year) {
             this.name = name;
             this.year = year;
           }
           age() {
             let date = new Date();
             return date.getFullYear() - this.year;
           }
         }

         let myCar = new Car("Ford", 2014);
         document.getElementById("demo").innerHTML =
         "My car is " + myCar.age() + " years old.";


# Sync, async, asynce/await, promise.then

# Synchronous
Imagine you make a phone call to a friend and ask him to look something up for you. Although it might take a while, you wait on the phone and stare into space, until your friend gives you the answer that you needed.

The same is happening when you make a function call containing "normal" code:

         function findItem() {
             var item;
             while(item_not_found) {
                 // search
             }
             return item;
         }

         var item = findItem();

         // Do something with item
         doSomethingElse();
Even though findItem might take a long time to execute, any code coming after var item = findItem(); has to wait until the function returns the result.

# Asynchronous
You call your friend again for the same reason. But this time you tell him that you are in a hurry and he should call you back on your mobile phone. You hang up, leave the house, and do whatever you planned to do. Once your friend calls you back, you are dealing with the information he gave to you.

That's exactly what's happening when you do an Ajax request.

         findItem(function(item) {
             // Do something with the item
         });
         doSomethingElse();
Instead of waiting for the response, the execution continues immediately and the statement after the Ajax call is executed. To get the response eventually, you provide a function to be called once the response was received, a callback (notice something? call back ?). Any statement coming after that call is executed before the callback is called.

Solution(s)
Embrace the asynchronous nature of JavaScript! While certain asynchronous operations provide synchronous counterparts (so does "Ajax"), it's generally discouraged to use them, especially in a browser context.

Why is it bad do you ask?

JavaScript runs in the UI thread of the browser and any long-running process will lock the UI, making it unresponsive. Additionally, there is an upper limit on the execution time for JavaScript and the browser will ask the user whether to continue the execution or not.

All of this is a really bad user experience. The user won't be able to tell whether everything is working fine or not. Furthermore, the effect will be worse for users with a slow connection.

In the following we will look at three different solutions that are all building on top of each other:

Promises with async/await (ES2017+, available in older browsers if you use a transpiler or regenerator)
Callbacks (popular in node)
Promises with then() (ES2015+, available in older browsers if you use one of the many promise libraries)
All three are available in current browsers, and node 7+.

# ES2017+: Promises with async/await
The ECMAScript version released in 2017 introduced syntax-level support for asynchronous functions. With the help of async and await, you can write asynchronous in a "synchronous style". The code is still asynchronous, but it's easier to read/understand.

async/await builds on top of promises: an async function always returns a promise. await "unwraps" a promise and either result in the value the promise was resolved with or throws an error if the promise was rejected.

Important: You can only use await inside an async function. Right now, top-level await isn't yet supported, so you might have to make an async IIFE (Immediately Invoked Function Expression) to start an async context.


Here is an example that builds on top of delay above:

         // Using 'superagent' which will return a promise.
         var superagent = require('superagent')

         // This is isn't declared as `async` because it already returns a promise
         function delay() {
           // `delay` returns a promise
           return new Promise(function(resolve, reject) {
             // Only `delay` is able to resolve or reject the promise
             setTimeout(function() {
               resolve(42); // After 3 seconds, resolve the promise with value 42
             }, 3000);
           });
         }


         async function getAllBooks() {
           try {
             // GET a list of book IDs of the current user
             var bookIDs = await superagent.get('/user/books');
             // wait for 3 seconds (just for the sake of this example)
             await delay();
             // GET information about each book
             return await superagent.get('/books/ids='+JSON.stringify(bookIDs));
           } catch(error) {
             // If any of the awaited promises was rejected, this catch block
             // would catch the rejection reason
             return null;
           }
         }

         // Start an IIFE to use `await` at the top level
         (async function(){
           let books = await getAllBooks();
           console.log(books);
         })();
         
Current browser and node versions support async/await. You can also support older environments by transforming your code to ES5 with the help of regenerator (or tools that use regenerator, such as Babel).

# Let functions accept callbacks

A callback is when function 1 is passed to function 2. Function 2 can call function 1 whenever it is ready. In the context of an asynchronous process, the callback will be called whenever the asynchronous process is done. Usually, the result is passed to the callback.

In the example of the question, you can make foo accept a callback and use it as success callback. So this

         var result = foo();
         // Code that depends on 'result'
         becomes

         foo(function(result) {
             // Code that depends on 'result'
         });
         Here we defined the function "inline" but you can pass any function reference:

         function myCallback(result) {
             // Code that depends on 'result'
         }

         foo(myCallback);
         foo itself is defined as follows:

         function foo(callback) {
             $.ajax({
                 // ...
                 success: callback
             });
         }
callback will refer to the function we pass to foo when we call it and we pass it on to success. I.e. once the Ajax request is successful, $.ajax will call callback and pass the response to the callback (which can be referred to with result, since this is how we defined the callback).

You can also process the response before passing it to the callback:

         function foo(callback) {
             $.ajax({
                 // ...
                 success: function(response) {
                     // For example, filter the response
                     callback(filtered_response);
                 }
             });
         }


# ES2015+: Promises with then()

The Promise API is a new feature of ECMAScript 6 (ES2015), but it has good browser support already. There are also many libraries which implement the standard Promises API and provide additional methods to ease the use and composition of asynchronous functions (e.g. bluebird).

Promises are containers for future values. When the promise receives the value (it is resolved) or when it is canceled (rejected), it notifies all of its "listeners" who want to access this value.

The advantage over plain callbacks is that they allow you to decouple your code and they are easier to compose.

Here is an example of using a promise:

         function delay() {
           // `delay` returns a promise
           return new Promise(function(resolve, reject) {
             // Only `delay` is able to resolve or reject the promise
             setTimeout(function() {
               resolve(42); // After 3 seconds, resolve the promise with value 42
             }, 3000);
           });
         }

         delay()
           .then(function(v) { // `delay` returns a promise
             console.log(v); // Log the value once it is resolved
           })
           .catch(function(v) {
             // Or do something else if it is rejected 
             // (it would not happen in this example, since `reject` is not called).
           });
         Applied to our Ajax call we could use promises like this:

         function ajax(url) {
           return new Promise(function(resolve, reject) {
             var xhr = new XMLHttpRequest();
             xhr.onload = function() {
               resolve(this.responseText);
             };
             xhr.onerror = reject;
             xhr.open('GET', url);
             xhr.send();
           });
         }

         ajax("/echo/json")
           .then(function(result) {
             // Code depending on result
           })
           .catch(function() {
             // An error occurred
           });

# Live(), bind and delegate methods
Using the Bind Method

## Pros
This methods works across various browser implementations.
It is pretty easy and quick to wire-up event handlers.
The shorthand methods (.click(), .hover(), etc...) make it even easier to wire-up event handlers.
For a simple ID selector, using .bind() not only wires-up quickly, but also when the event fires the event handler is invoked almost immediately.
## Cons
The method attaches the same event handler to every matched element in the selection.
It doesn't work for elements added dynamically that matches the same selector.
There are performance concerns when dealing with a large selection.
The attachment is done upfront which can have performance issues on page load.

## Using the Live Method

## Pros

There is only one event handler registered instead of the numerous event handlers that could have been registered with the .bind() method.
The upgrade path from .bind() to .live() is very small. All you have to do is replace "bind" to "live".
Elements dynamically added to the DOM that match the selector magically work because the real information was registered on the document.
You can wire-up event handlers before the document ready event helping you utilize possibly unused time.
## Cons

This method is deprecated as of jQuery 1.7 and you should start phasing out its use in your code.
Chaining is not properly supported using this method.
The selection that is made is basically thrown away since it is only used to register the event handler on the document.
Using event.stopPropagation() is no longer helpful because the event has already delegated all the way up to the document.
Since all selector/event information is attached to the document once an event does occur jQuery has match through its large metadata store using the matchesSelector method to determine which event handler to invoke, if any.
Your events always delegate all the way up to the document. This can affect performance if your DOM is deep.


# Using the Delegate Method

## Pros

You have the option of choosing where to attach the selector/event information.
The selection isn't actually performed up front, but is only used to register onto the root element.
Chaining is supported correctly.
jQuery still needs to iterate over the selector/event data to determine a match, but since you can choose where the root is the amount of data to sort through can be much smaller.
Since this technique uses event delegation, it can work with dynamically added elements to the DOM where the selectors match.
As long as you delegate against the document you can also wire-up event handlers before the document ready event.

## Cons

Changing from a .bind() to a .delegate() method isn't as straight forward.
There is still the concern of jQuery having to figure out, using the matchesSelector method, which event handler to invoke based on the selector/event information stored at the root element. However, the metadata stored at the root element should be considerably smaller compared to using the .live() method.
# Slice vs Splice
The splice() method returns the removed items in an array. The slice() method returns the selected element(s) in an array, as a new array object.

The splice() method changes the original array and slice() method doesn’t change the original array.

Splice() method can take n number of arguments:

Argument 1: Index, Required.

Argument 2: Optional. The number of items to be removed. If set to 0(zero), no items will be removed. And if not passed, all item(s) from provided index will be removed.

Argument 3..n: Optional. The new item(s) to be added to the array.

slice() method can take 2 arguments:

Argument 1: Required. An integer that specifies where to start the selection (The first element has an index of 0). Use negative numbers to select from the end of an array.

Argument 2: Optional. An integer that specifies where to end the selection. If omitted, all elements from the start position and to the end of the array will be selected. Use negative numbers to select from the end of an array.

Slice example:
const array = [1,2,3,4,5];

         // Remove first element
         console.log('Elements deleted:', array.splice(0, 1), 'mutated array:', array);
         // Elements deleted: [ 1 ] mutated array: [ 2, 3, 4, 5 ]

         // array = [ 2, 3, 4, 5]
         // Remove last element (start -> array.length+start = 3)
         console.log('Elements deleted:', array.splice(-1, 1), 'mutated array:', array);
         // Elements deleted: [ 5 ] mutated array: [ 2, 3, 4 ]
         
# SPlice example shared 
above slice example:
         const array = [1,2,3,4,5];

         // Extract first element
         console.log('Elements extracted:', array.slice(0, 1), 'array:', array);
         // Elements extracted: [ 1 ] array: [ 1, 2, 3, 4, 5 ]

         // Extract last element (start -> array.length+start = 4)
         console.log('Elements extracted:', array.slice(-1), 'array:', array);
         // Elements extracted: [ 5 ] array: [ 1, 2, 3, 4, 5 ]
         
# Async vs defer

With HTML5, we get two new boolean attributes for the <script> tag: async and defer. Async allows execution of scripts asynchronously and defer allows execution only after the whole document has been parsed.

These two attributes are a must for increasing speed and performance of websites. They allow the elimination of render-blocking JavaScript where the page would have to load and execute scripts before finishing to render the page. Here’s a usage example:

<script defer src="/js/jquery.min.js">
</script>


# Async vs Defer
With async, the file gets downloaded asynchronously and then executed as soon as it’s downloaded.

With defer, the file gets downloaded asynchronously, but executed only when the document parsing is completed. With defer, scripts will execute in the same order as they are called. This makes defer the attribute of choice when a script depends on another script. For example, if you’re using jQuery as well as other scripts that depend on it, you’d use defer on them (jQuery included), making sure to call jQuery before the dependent scripts.

A good strategy is to use async when possible, and then defer when async isn’t an option.

👉Note that both attributes don’t have any effect on inline scripts.

# How a page renders

When a browser sends a request to a server to fetch an HTML document, the server returns an HTML page in binary stream format which is basically a text file with the response header Content-Type set to the value text/html; charset=UTF-8.

Here text/html is a MIME Type which tells the browser that it is an HTML document and charset=UTF-8 tells the browser that it is encoded in UTF-8 character encoding. Using this information, the browser can convert the binary format into a readable text file.

If this header is missing, the browser would not understand how to process the file and it will render in plain text format. But if everything is OK, after this conversion, the browser can start reading the HTML document

If this header is missing, the browser would not understand how to process the file and it will render in plain text format. But if everything is OK, after this conversion, the browser can start reading the HTML document

A DOM tree for our earlier HTML document looks like above. A DOM tree starts from the topmost element which is html element and branches out as per the occurrence and nesting of HTML elements in the document. Whenever an HTML element is found, it creates a DOM node (Node) object from its respective class (constructor function).

# CSS Object Model (CSSOM)
After constructing the DOM, the browser reads CSS from all the sources (external, embedded, inline, user-agent, etc.) and construct a CSSOM. CSSOM stands for CSS Object Model which is a Tree Like structure just like DOM.
Each node in this tree contains CSS style information that will be applied to DOM elements that it target (specified by the selector). CSSOM, however, does not contain DOM elements which can’t be printed on the screen like <meta>, <script>, <title> etc.

# Render Tree

Render-Tree is also a tree-like structure constructed by combining DOM and CSSOM trees together. The browser has to calculate the layout of each visible element and paint them on the screen, for that browser uses this Render-Tree. Hence, unless Render-Tree isn’t constructed, nothing is going to get printed on the screen which is why we need both DOM and CSSOM trees.

When a web page is loaded, the browser first reads the HTML text and constructs DOM Tree from it. Then it processes the CSS whether that is inline, embedded, or external CSS and constructs the CSSOM Tree from it.

After these trees are constructed, then it constructs the Render-Tree from it. Once the Render-Tree is constructed, then the browser starts the printing individual elements on the screen.

# Layout operation

The first browser creates the layout of each individual Render-Tree node. The layout consists of the size of each node in pixels and where (position) it will be printed on the screen. This process is called layout since the browser is calculating the layout information of each node.

Until now we have a list of geometries that need to be printed on the screen. Since elements (or a sub-tree) in the Render-Tree can overlap each other and they can have CSS properties that make them frequently change the look, position, or geometry (such as animations), the browser creates a layer for it.

Creating layers helps the browser efficiently perform painting operations throughout the lifecycle of a web page such as while scrolling or resizing the browser window. Having layers also help the browser correctly draw elements in the stacking order (along the z-axis) as they were intended by the developer.

Now that we have layers, we can combine them and draw them on the screen. But the browser does not draw all the layers in a single go. Each layer is drawn separately first.

# Compositing operation

Until now, we haven’t drawn a single pixel on the screen. What we have are different layers (bitmap images) that should be drawn on the screen in a specific order. In compositing operations, these layers are sent to GPU to finally draw it on the screen.

Sending entire layers to draw is clearly inefficient because this has to happen every time there is a reflow (layout) or repaint. Hence, a layer is broken down into different tiles which then will be drawn on the screen. You can also visualize these tiles in Chrome’s DevTool Rendering panel.

# Object Assign

Object.assign() which is used to copy the values and properties from one or more source objects to a target object. It invokes getters and setters since it uses both [[Get]] on the source and [[Set]] on the target. It returns the target object which has properties and values copied from the target object. Object.assign() does not throw on null or undefined source values. 
Applications: 
 

Object.assign() is used for cloning an object.
Object.assign() is used to merge object with same properties.
Syntax: 
 

Object.assign(target, ...sources)

# Object Create

# difference between Object.create() and new SomeFunction()

The object used in Object.create actually forms the prototype of the new object, where as in the new Function() form the declared properties/functions do not form the prototype.

Yes, Object.create builds an object that inherits directly from the one passed as its first argument.

With constructor functions, the newly created object inherits from the constructor's prototype, e.g.:

var o = new SomeConstructor();

In the above example, o inherits directly from SomeConstructor.prototype.

There's a difference here, with Object.create you can create an object that doesn't inherit from anything, Object.create(null);, on the other hand, if you set SomeConstructor.prototype = null; the newly created object will inherit from Object.prototype.

You cannot create closures with the Object.create syntax as you would with the functional syntax. This is logical given the lexical (vs block) type scope of JavaScript.

Well, you can create closures, e.g. using property descriptors argument:

         var o = Object.create({inherited: 1}, {
           foo: {
             get: (function () { // a closure
               var closured = 'foo';
               return function () {
                 return closured+'bar';
               };
             })()
           }
         });

         o.foo; // "foobar"
# Objects — Writable, Configurable & Enumerable

So object has a config which contains four property as value, writable, enumerable and configurable.

         Object Creation
         // Each of the following options will create a new empty object:
         var newObject = {};
         // or
         var newObject = Object.create( Object.prototype );
         // or
         var newObject = new Object();
         Set Property
         var newObject = {a: 1};
         // Accessing to a property
         newObject.a; // => 1
         // Modifying the value of a property
         newObject.a = 0;
         newObject.a; // => 0;
         // Creating a new property
         newObject.b = 2;
         newObject.b; // => 2
         // Deleting a property
         delete newObject.b;
         newObject.b; // => undefined
         
but, you know that all the properties above are writable, configurable & enumerable, I mean :

# writable: 

I can modify their values, I can update a property just assigning a new value to it.Defaults to false.
enumerable: I can access to all of them using a for..in loop. Also, enumerable property keys of an object are returned using Object.keys method. Defaults to false.
# configurable:

I can modify the behavior of the property, so I can make them non-enumerable, non-writable or even non-cofigurable if I feel like doing so. Configurable properties are the only ones that can be removed using the delete operator. Defaults to false.

So Let’s take a quick look that how to use above config and how it works:
         // Set properties
         Object.defineProperty( newObject, 'a', {
            value: "some value",
            writable: true,
            enumerable: true,
            configurable: true
         });
         Object’s enumerable property
         Enumerable
         Object.defineProperty( newObject, 'a', {
            value: "some value",
            enumerable: true,
         });
         // Object {a: "some value"}
         for (var key in newObject) { console.log(key) }
         // a

         Object.keys(newObject);
         // ["a"]
         Non-Enumerable
         Object.defineProperty( newObject, 'a', {
            value: "some value",
            enumerable: false,
         });
         // Object {a: "some value"}
         for (var key in newObject) { console.log(key) }
         // undefined
         Object.keys(newObject);
         // []
         Object’s writable property
         writable
         Object.defineProperty( newObject, 'a', {
            value: "some value",
            writable: true,
         });
         // Object {a: "some value"}
         newObj.a = 'some other new value';
         // "some other new value"
         newObj
         // Object {a: "some other new value"}
         Non-writable
         Object.defineProperty( newObject, 'a', {
            value: "some value",
            writable: false,
         });
         // Object {a: "some value"}
         newObj.a = 'some other new value';
         // "some other new value"
         newObject
         // Object {a: "some value"}
         Object’s configurable property
         configurable
         Object.defineProperty( newObject, 'a', {
            value: "some value",
            configurable: true,
         });
         // Object {a: "some value"}
         delete newObject.a;
         // true
         newObject
         // Object {}
         Non-configurable
         Object.defineProperty( newObject, 'a', {
            value: "some value",
            configurable: false,
         });
         // Object {a: "some value"}
         delete newObject.a;
         // false
         newObject
         // Object {a: "some value"}
         
# verticle align middle of div

## First approch: 

         <html style="
             height: 100%;
         "><head></head><body style="
            height: 100%;
            width: 100%;
         ">
         <div style="
             width: 100%;
             height: 100%;
             display: table;
         ">
             <div style="
             display: table-cell;
             vertical-align: middle;

             "><div style="
             height: 200px;
             width: 200px;
             border: 1px solid;
             margin: 0 auto;
         "></div></div>
         </div></body></html>

## Step-2 

         <div class="container">
             <span>vertically/horizontally centered!</span>
         </div>

         <div class="container">
                  <span>I'm vertically/horizontally centered!</span>
          </div>
          
          .container {
             position: absolute;
             top: 50%;
             left: 50%;
             -moz-transform: translateX(-50%) translateY(-50%);
             -webkit-transform: translateX(-50%) translateY(-50%);
             transform: translateX(-50%) translateY(-50%);
         }

## Step-3 

html, body, .container {
    height: 100%;
}

.container {
    display: flex;
    align-items: center;
    justify-content: center;
}
         

# css if there is multiple <p> tag and i want to add third <p> element to color red
         
p:nth-of-type(2) {
  background: red;
}

Odd and even are keywords that can be used to match child elements whose index is odd or even (the index of the first child is 1).

Here, we specify two different background colors for odd and even p elements:

p:nth-of-type(odd) {
  background: red;
}

p:nth-of-type(even) {
  background: blue;
}
# Sementic and non sementic in html

Semantic HTML elements:
These elements simply mean, elements with meaning. The reason being, there definition in the code tells the browser and the developer what they are supposed to do. Framing in simpler words, these elements describe the type of content they are supposed to contain.

Following is the list of some semantic elements :

article
aside
details
figcaption
figure
footer
form
header
main
mark
nav
table
section

# Non-Semantic elements: 
Unlike, semantic elements they don’t have any meaning. They don’t tell anything about the content they contain. They can be used with different attributes to mark up semantics common to a group.



Following is the list of some non-semantic elements:

div
span

# Html5 new features

With invent of features in HTML5 it is not only possible to create better static websites but we can also create dynamic websites. Features such as audio, video, animations etc can be added to the webpage now without the use of JS.
1. Video and Audio
2. nav
The nav element is used for the part of a internet site that links to different pages at the website. The hyperlinks can be organized a number of approaches. below, the hyperlinks are displayed inside paragraph factors. An unordered list can also be used.

3. header
4. canvas
canvas is a tag of HTML which is newly introduced in HTML5. It is used to draw the images on the fly. It can be used for visual images, rendering graphs, game graphics.
5. footer
6. New types for input tags
 a.ContentEditable
It is an attribute which is used to permit the user to edit the content. It creates What You See What You Get so easy. Content will be editable by clicking on it.
 b. Progress
This tag is used to check the progress of a task during execution of that. Progress tag can used with the conjuction of JavaScript. It is like progress bar.

<progress value="22" max="100"></progress>
c.section
d.main
main is a tag which is used to contain the main content of the page. More than one main tag is not accepted in the document and this tag can not be inside in article, aside, footer, header tags. It does not include the navigation bar, header and footer.

7. Figure and Figcaption
Earlier there was no way to of figure as well as give caption to that figure. But, with the introduction of figure as well as figcaption, it has become semantically possible to insert an image in a page with its caption.
8. Placeholders
9. Required Attribute
10. Preload Videos
It is an amazing feature for uploading the videos. It specifies the way to upload the video along with the loading of the page. This helps the browser in knowing about the improvisation of the user experience of the webpage
11. Display Control
Display attribute helps in specifying the behaviour of the elements. When this property is not specified, then the default values are taken.
12. Regular Expressions
With the help of regular expression we can add the particular pattern as an input. Such as the most common pattern that is used is [A-Za-z] {5,11}. It accepts the uppercase as well as lowercase letters. Along with this it states that the minimum length of characters is 5 and the maximum length of characters that is acceptable is 11.
14. Inline elements
To keep code up to mark, semantically these inline elements help alot :

mark – It highlights the content that is marked in some or the other way.
time – This helps in adding current time as well as date to the webpage.
meter – It helps in indicating that how much space in the storage disk is still there.
progress bar – It helps in knowing the progress of the task that has been assigned for its completion.
16. Email attribute

# Javascript short and numeric array

By default, the sort() function sorts values as strings.

This works well for strings ("Apple" comes before "Banana").

However, if numbers are sorted as strings, "25" is bigger than "100", because "2" is bigger than "1".

Because of this, the sort() method will produce incorrect result when sorting numbers.

You can fix this by providing a compare function:
         var points = [40, 100, 1, 5, 25, 10];
         points.sort(function(a, b){return a - b});

         Use the same trick to sort an array descending:
          var points = [40, 100, 1, 5, 25, 10];
         points.sort(function(a, b){return b - a});
         
# Callback Functions
When a function simply accepts another function as an argument, this contained function is known as a callback function. Using callback functions is a core functional programming concept, and you can find them in most JavaScript code; either in simple functions like setInterval, event listening or when making API calls.

Callback functions are written like so:

setInterval(function() {
  console.log('hello!');
}, 1000);
setInterval accepts a callback function as its first parameter and also a time interval. Another example using .map();

const list    = ['man', 'woman', 'child']

// create a new array
// loop over the array and map the data to new content
const newList = list.map(function(val) {
  return val + " kind";
});

// newList = ['man kind', 'woman kind', 'child kind']

# Naming Callback functions

Callback functions can be named or anonymous functions. In our first examples, we used anonymous callback functions. Let’s look at a named callback function:

         function greeting(name) {
           console.log(`Hello ${name}, welcome to Scotch!`);
         }
The above function is assigned a name greeting and has an argument of name. We're also using an ES6 template string. Let’s use this function as a callback function.

         function introduction(firstName, lastName, callback) {
           const fullName = `${firstName} ${lastName}`;

           callback(fullName);
         }

introduction('Chris','Nwamba', greeting); // Hello Chris Nwamba, welcome to Scotch!
Notice the usage of the callback? 
The succeeding brackets, () after the function are not used when passing the function as a parameter.

Note: The callback function is not run unless called by its containing function, it is called back. Hence, the term call back function

Multiple functions can be created independently and used as callback functions. These create multi-level functions. When this function tree created becomes too large, the code becomes incomprehensible sometimes and is not easily refactored. This is known as callback hell. Let’s see an example:

         // a bunch of functions are defined up here

         // lets use our functions in callback hell
         function setInfo(name) {
           address(myAddress) {
             officeAddress(myOfficeAddress) {
               telephoneNumber(myTelephoneNumber) {
                 nextOfKin(myNextOfKin) {
                   console.log('done'); //let's begin to close each function! 
                 };
               };
             };
           };
         }
We are assuming these functions have been previously defined elsewhere. You can see how confusing it is to pass each function as callbacks. Callback functions are useful for short asynchronous operations. When working with large sets, this is not considered best practice. Because of this challenge, Promises were introduced to simplify deferred activities.

# Promises

I promise to do this whenever that is true. If it isn't true, then I won't.

This is a simple illustration of JavaScript Promises. Sounds like an IF statement? We’ll soon see a huge difference.

A promise is used to handle the asynchronous result of an operation. JavaScript is designed to not wait for an asynchrnous block of code to completely execute before other synchronous parts of the code can run. For instance, when making API requests to servers, we have no idea if these servers are offline or online, or how long it takes to process the server request.

With Promises, we can defer execution of a code block until an async request is completed. This way, other operations can keep running without interruption.

Promises have three states:

Pending: This is the initial state of the Promise before an operation begins
Fulfilled: This means the specified operation was completed
Rejected: The operation did not complete; an error value is usually thrown

# Creating a Promise

The Promise object is created using the new keyword and contains the promise; this is an executor function which has a resolve and a reject callback. As the names imply, each of these callbacks returns a value with the reject callback returning an error object.

         const promise = new Promise(function(resolve, reject) {
           // promise description
         })
         Let’s create a promise:

         const weather = true
         const date    = new Promise(function(resolve, reject) {
           if (weather) {
             const dateDetails = {
               name:     'Cubana Restaurant',
               location: '55th Street',
               table:    5
             };

             resolve(dateDetails)
           } else {
             reject(new Error('Bad weather, so no Date'))
           }
         });
If weather is true, resolve the promise returning the data dateDetails, else return an error object with data Bad weather, so no Date.

## Using Promises

Using a promise that has been created is relatively straightforward; we chain .then() and .catch() to our Promise like so:

         date
           .then(function(done) {
             // the content from the resolve() is here
           })
           .catch(function(error) {
             // the info from the reject() is here
           });
         Using the promise we created above, let's take this a step further:

         const myDate = function() {
           date
             .then(function(done) {
               console.log('We are going on a date!')
               console.log(done)
             })
             .catch(function(error) {
                 console.log(error.message)
             })
         }

         myDate();

Since the weather value is true, we call mydate() and our console logs read:

We are going on a date!

         {
           name: 'Cubana Restaurant',
           location: '55th Street'
           table: 5
         }
         .then() receives a function with an argument which is the resolve value of our promise. .catch returns the reject value of our promise.

Note: Promises are asynchronous. Promises in functions are placed in a micro-task queue and run when other synchronous operations complete.

# Chaining Promises

Sometimes we may need to execute two or more asynchronous operations based on the result of preceding promises. In this case, promises are chained. Still using our created promise, let’s order an uber if we are going on a date.

So we create another promise:

         const orderUber = function(dateDetails) {
           return new Promise(function(resolve, reject) {
             const message = `Get me an Uber ASAP to ${dateDetails.location}, we are going on a date!`;

             resolve(message)
           });
         }
This promise can be shortened to:

         const orderUber = function(dateDetails) {
           const message = `Get me an Uber ASAP to ${dateDetails.location}, we are going on a date!`;
           return Promise.resolve(message)
         } 
We chain this promise to our earlier date operation like so:

         const myDate = function() {
           date
             .then(orderUber)
             .then(function(done) {
               console.log(done);
             })
             .catch(function(error) {
               console.log(error.message)
             })
         }

         myDate();
Since our weather is true, the output to our console is:

Get me an Uber ASAP to 55th Street, we are going on a date!
Once the orderUber promise is chained with .then, subsequent .then utilizes data from the previous one.

# Async and Await

An async function is a modification to the syntax used in writing promises. You can call it syntactic sugar over promises. It only makes writing promises easier.

An async function returns a promise -- if the function returns a value, the promise will be resolved with the value, but if the async function throws an error, the promise is rejected with that value. Let’s see an async function:

         async function myRide() {
           return '2017 Dodge Charger';
         }
and a different function that does the same thing but in promise format:

         function yourRide() {
           return Promise.resolve('2017 Dodge Charger');
         }
From the above statements, myRide() and yourRide() are equal and will both resolve to 2017 Dodge Charger. Also when a promise is rejected, an async function is represented like this:

         function foo() {
           return Promise.reject(25)
         }

// is equal to
         async function() {
           throw 25;
         }

# Await

Await is only used with an async function. The await keyword is used in an async function to ensure that all promises returned in the async function are synchronized, ie. they wait for each other. Await eliminates the use of callbacks in .then() and .catch(). In using async and await, async is prepended when returning a promise, await is prepended when calling a promise. try and catch are also used to get the rejection value of an async function. Let's see this with our date example:

         async function myDate() {
           try {

    let dateDetails = await date;
    let message     = await orderUber(dateDetails);
    console.log(message);

           } catch(error) {
             console.log(error.message);
           }
         }
Lastly we call our async function:

         (async () => { 
           await myDate();
         })();
Note we used the ES6 arrow function syntax here.

# CSS box-shadow Property

The box-shadow CSS property adds shadow effects around an element's frame. You can set multiple effects separated by commas. A box shadow is described by X and Y offsets relative to the element, blur and spread radius, and color.

box-shadow: 10px 5px 5px red;
 box-shadow: none;

/* offset-x | offset-y | color */
box-shadow: 60px -16px teal;

/* offset-x | offset-y | blur-radius | color */
box-shadow: 10px 5px 5px black;

/* offset-x | offset-y | blur-radius | spread-radius | color */
box-shadow: 2px 2px 2px 1px rgba(0, 0, 0, 0.2);

/* inset | offset-x | offset-y | color */
box-shadow: inset 5em 1em gold;

/* Any number of shadows, separated by commas */
box-shadow: 3px 3px red, -1em 0 0.4em olive;

/* Global keywords */
box-shadow: inherit;
box-shadow: initial;
box-shadow: unset;

# CSS Layout - The position Property

The position property specifies the type of positioning method used for an element.

There are five different position values:

static
relative
fixed
absolute
sticky
position: static;
HTML elements are positioned static by default.

Static positioned elements are not affected by the top, bottom, left, and right properties.

position: relative;
An element with position: relative; is positioned relative to its normal position.

Setting the top, right, bottom, and left properties of a relatively-positioned element will cause it to be adjusted away from its normal position. Other content will not be adjusted to fit into any gap left by the element.

position: fixed;
An element with position: fixed; is positioned relative to the viewport, which means it always stays in the same place even if the page is scrolled. The top, right, bottom, and left properties are used to position the element.

A fixed element does not leave a gap in the page where it would normally have been located.
position: absolute;
An element with position: absolute; is positioned relative to the nearest positioned ancestor (instead of positioned relative to the viewport, like fixed).

However; if an absolute positioned element has no positioned ancestors, it uses the document body, and moves along with page scrolling.

Note: A "positioned" element is one whose position is anything except static.

position: sticky;
An element with position: sticky; is positioned based on the user's scroll position.

A sticky element toggles between relative and fixed, depending on the scroll position. It is positioned relative until a given offset position is met in the viewport - then it "sticks" in place (like position:fixed).

# CSS Transitions
CSS transitions allows you to change property values smoothly, over a given duration.

How to Use CSS Transitions?
To create a transition effect, you must specify two things:

the CSS property you want to add an effect to
the duration of the effect
Note: If the duration part is not specified, the transition will have no effect, because the default value is 0.

The following example shows a 100px * 100px red <div> element. The <div> element has also specified a transition effect for the width property, with a duration of 2 seconds:

Example

         div {
           width: 100px;
           height: 100px;
           background: red;
           transition: width 2s;
         }

Change Several Property Values
The following example adds a transition effect for both the width and height property, with a duration of 2 seconds for the width and 4 seconds for the height:

Example
div {
  transition: width 2s, height 4s;
}

Specify the Speed Curve of the Transition
The transition-timing-function property specifies the speed curve of the transition effect.

The transition-timing-function property can have the following values:

ease - specifies a transition effect with a slow start, then fast, then end slowly (this is default)
linear - specifies a transition effect with the same speed from start to end
ease-in - specifies a transition effect with a slow start
ease-out - specifies a transition effect with a slow end
ease-in-out - specifies a transition effect with a slow start and end
cubic-bezier(n,n,n,n) - lets you define your own values in a cubic-bezier function
The following example shows the some of the different speed curves that can be used:

Example
#div1 {transition-timing-function: linear;}
#div2 {transition-timing-function: ease;}
#div3 {transition-timing-function: ease-in;}
#div4 {transition-timing-function: ease-out;}
#div5 {transition-timing-function: ease-in-out;}

# What are CSS Animations?

An animation lets an element gradually change from one style to another.

You can change as many CSS properties you want, as many times you want.

To use CSS animation, you must first specify some keyframes for the animation.

Keyframes hold what styles the element will have at certain times.

The @keyframes Rule
When you specify CSS styles inside the @keyframes rule, the animation will gradually change from the current style to the new style at certain times.

To get an animation to work, you must bind the animation to an element.

The following example binds the "example" animation to the <div> element. The animation will last for 4 seconds, and it will gradually change the background-color of the <div> element from "red" to "yellow":

Example

         /* The animation code */
         @keyframes example {
           from {background-color: red;}
           to {background-color: yellow;}
         }

         /* The element to apply the animation to */
         div {
           width: 100px;
           height: 100px;
           background-color: red;
           animation-name: example;
           animation-duration: 4s;
         }
         
Note: The animation-duration property defines how long time an animation should take to complete. If the animation-duration property is not specified, no animation will occur, because the default value is 0s (0 seconds). 

In the example above we have specified when the style will change by using the keywords "from" and "to" (which represents 0% (start) and 100% (complete)).

It is also possible to use percent. By using percent, you can add as many style changes as you like.

The following example will change the background-color of the <div> element when the animation is 25% complete, 50% complete, and again when the animation is 100% complete:
         
# What is server-side rendering?

Server-side rendering (SSR), is the ability of an application to contribute by displaying the web-page on the server instead of rendering it in the browser. Server-side sends a fully rendered page to the client; the client’s JavaScript bundle takes over and allows the SPA framework to operate. There is also client-side rendering which slows down the procedure of viewing and interacting with the web page.

## Advantages of using server-side rendering
It enables pages to load faster which provides a better user experience.

It plays an important role in SEO (search engine optimization) and correctly indexes webpages. This happens because Google favors web pages with faster load time.

It provides body to the HTML pages for all server ships.

It assists with​ loading the page when the user has a​ slow internet connection.

It assists in loading the page when the user has an outdated device.

## Disadvantages of using server-side rendering
Although server-side rendering is an excellent concept and has a lot of advantages, it also has some disadvantages:

Server-side rendering seems to be a simple concept; however, its complexity increases as the complexity of the application increases.

Rendering a big application on the server-side can be very time consuming and it may increase the loading time due to it being a single bottleneck.

# What are Arrow functions in JS?

These are anonymous functions with their own special syntax that accept a fixed number of arguments, and operate in the context of their enclosing scope - ie the function or other code where they are defined.

Let's break down each of these pieces in turn.

Arrow Function Syntax
Arrow functions have a single overarching structure, and then an number of ways they can be simplified in special cases.

The core structure looks like this:

(argument1, argument2, ... argumentN) => {
  // function body
}
A list of arguments within parenthesis, followed by a 'fat arrow' (=>), followed by a function body.

This is very similar to traditional functions, we just leave off the function keyword and add a fat arrow after the arguments.

However, there are a number of ways to 'sugar' this up that make arrow functions dramatically more concise for simple functions.

First, if the function body is a single expression, you can leave off the brackets and put it inline. The results of the expression will be returned by the function. For example:

const add = (a, b) => a + b;
Second, if there is only a single argument, you can even leave off the parenthesis around the argument. For example:

const getFirst = array => array[0];
As you can see, this can lead to some very concise syntax, which we'll highlight more benefits of later.

(name, description) => ({name: name, description: description});
Enclosing Scope Context
Unlike every other form of function, arrow functions do not have their own execution context.

Practically, this means that both this and arguments are inherited from their parent function.

# Where You Should Not Use Arrow Functions

There are a number of situations in which arrow functions are not a good idea. Places where they will not only help, but cause you trouble.

The first is in methods on an object. This is an example where function context and this are exactly what you want.

There was a trend for a little while to use a combination of the Class Properties syntax and arrow functions as a way to create "auto-binding" methods, e.g. methods that could be used by event handlers but that stayed bound to the class.

This looked something like:

         class Counter {
           counter = 0;

           handleClick = () => {
             this.counter++;
           }
         }
In this way, even if handleClick were called with by an event handler rather than in the context of an instance of Counter, it would still have access to the instance's data.

While using this approach does give you an ergonomic-looking shortcut to having a bound function, that function behaves in a number of ways that are not intuitive, inhibiting testing and creating problems if you attempt to subclass/use this object as a prototype.

Instead, use a regular function and if necessary bind it the instance in the constructor:

         class Counter {
           counter = 0;

           handleClick() {
             this.counter++;
           }

           constructor() {
             this.handleClick = this.handleClick.bind(this);
           }
         }
         
# What is the spread operator in JavaScript?

The spread operator is a new addition to the set of operators in JavaScript ES6. It takes in an iterable (e.g an array) and expands it into individual elements.

The spread operator is commonly used to make shallow copies of JS objects. Using this operator makes the code concise and enhances its readability.

Syntax
The spread operator is denoted by three dots, ….


Example:

# 1. Copying an array
The array2 has the elements of array1 copied into it. Any changes made to array1 will not be reflected in array2 and vice versa.

If the simple assignment operator had been used then array2 would have been assigned a reference to array1 and the changes made in one array would reflect in the other array which in most cases is undesirable.
let array1 = ['h', 'e', 'y'];
let array2 = [...array1];
console.log(array2);


# 2. Inserting the elements of one array into another
It can be seen that the spread operator can be used to append one array after any element of the second array. In other words, there is no limitation that baked_desserts can only be appended at the beginning or the end of the desserts2 array.

         let baked_desserts = ['cake', 'cookie', 'donut'];
         let desserts = ['icecream', 'flan', 'frozen yoghurt', ...baked_desserts];
         console.log(desserts);
         //Appending baked_desserts after flan
         let desserts2 = ['icecream', 'flan', ...baked_desserts, 'frozen yoghurt'];
         console.log(desserts2);
         
# What is object destructuring in JavaScript?

Destructuring is a JavaScript expression that allows us to extract data from arrays, objects, and maps and set them into new, distinct variables. Destructuring allows us to extract multiple properties, or items, from an array​ at a time.

Examples
1. Assigning to existing variable names
Here’s how to destructure values from an object:

         var employee = {    // Object we want to destructure
             firstname: 'Jon',
             lastname: 'Snow',
             dateofbirth: '1990'
         };

// Destructuring the object into our variables
var { firstname, lastname, dateofbirth } = employee;
console.log( firstname, lastname, dateofbirth);

output: Jon Snow 1990


# 2. Assigning to new variable names
The following code destructures the object into variables with a different name than the object property:

         var employee = {    // Object we want to destructure
             firstname: 'Jon',
             lastname: 'Snow',
             dateofbirth: '1990'
         };

// Destructuring the object into variables with
// different names than the object variables
var { firstname: fn, lastname: ln, dateofbirth: dob } = employee;
console.log( fn, ln, dob);
output:
Jon Snow 1990

# What is currying in JavaScript?

In functional programming, currying is the process of converting a function, that takes multiple arguments at once, to a function that takes these arguments step by step.

Currying is a process in functional programming in which we can transform a function with multiple arguments into a sequence of nesting functions. It returns a new function that expects the next argument inline.
It keeps returning a new function (that expects the current argument, like we said earlier) until all the arguments are exhausted. The arguments are kept "alive"(via closure) and all are used in execution when the final function in the currying chain is returned and executed.

Note: The term arity, refers to the number of arguments a function takes. For example,
function fn(a, b) {
    //...
}
function _fn(a, b, c) {
    //...
}
function fn takes two arguments (2-arity function) and _fn takes three arguments (3-arity function).
So, currying transforms a function with multiple arguments into a sequence/series of functions each taking a single argument.
Let’s look at a simple example:
function multiply(a, b, c) {
    return a * b * c;
}
This function takes three numbers, multiplies the numbers and returns the result.
multiply(1,2,3); // 6
See, how we called the multiply function with the arguments in full. Let’s create a curried version of the function and see how we would call the same function (and get the same result) in a series of calls:
function multiply(a) {
    return (b) => {
        return (c) => {
            return a * b * c
        }
    }
}
log(multiply(1)(2)(3)) // 6
We have turned the multiply(1,2,3) function call to multiply(1)(2)(3) multiple function calls.
One single function has been turned to a series of functions. To get the result of multiplication of the three numbers 1, 2 and 3, the numbers are passed one after the other, each number prefilling the next function inline for invocation.
We could separate this multiply(1)(2)(3) to understand it better:

         const mul1 = multiply(1);
         const mul2 = mul1(2);
         const result = mul2(3);
         log(result); // 6
         Let’s take it one after the other. We passed 1 to the multiply function:
         let mul1 = multiply(1);
         It returns the function:
         return (b) => {
                 return (c) => {
                     return a * b * c
                 }
             }
Now, mul1 holds the above function definition which takes an argument b.
We called the mul1 function, passing in 2:

         let mul2 = mul1(2);
The mul1 will return the third function:

         return (c) => {
                     return a * b * c
                 }
The returned function is now stored in mul2 variable.
In essence, mul2 will be:

         mul2 = (c) => {
                     return a * b * c
                 }
When mul2 is called with 3 as the parameter,

         const result = mul2(3);
it does the calculation with the previously passed in parameters: a = 1, b = 2 and returns 6.
log(result); // 6

# Understanding RPC Vs REST

The fundamental problem with RPC is coupling. RPC clients become tightly coupled to service implementation in several ways and it becomes very hard to change service implementation without breaking clients:

Clients are required to know procedure names;
Procedure parameters order, types and count matters. It's not that easy to change procedure signatures(number of arguments, order of arguments, argument types etc...) on server side without breaking client implementations;
RPC style doesn't expose anything but procedure endpoints + procedure arguments. It's impossible for client to determine what can be done next.
On the other hand in REST style it's very easy to guide clients by including control information in representations(HTTP headers + representation). For example:

It's possible (and actually mandatory) to embed links annotated with link relation types which convey meanings of these URIs;
Client implementations do not need to depend on particular procedure names and arguments. Instead, clients depend on message formats. This creates possibility to use already implemented libraries for particular media formats (e.g. Atom, HTML, Collection+JSON, HAL etc...)
It's possible to easily change URIs without breaking clients as far as they only depend on registered (or domain specific) link relations;
It's possible to embed form-like structures in representations, giving clients the possibility to expose these descriptions as UI capabilities if the end user is human;
Support for caching is additional advantage;
Standardised status codes;
There are many more differences and advantages on the REST side.

RPC-based APIs are great for actions (that is, procedures or commands).

REST-based APIs are great for modeling your domain (that is, resources or entities), making CRUD (create, read, update, delete) available for all of your data.

REST is not only CRUD, but things are done through mainly CRUD-based operations. REST will use HTTP methods such as GET, POST, PUT, DELETE, OPTIONS and, hopefully, PATCH to provide semantic meaning for the intention of the action being taken.

RPC, however, would not do that. Most use only GET and POST, with GET being used to fetch information and POST being used for everything else. It is common to see RPC APIs using something like POST /deleteFoo, with a body of { “id”: 1 }, instead of the REST approach, which would be DELETE /foos/1.

This is not an important difference; it’s simply an implementation detail. The biggest difference in my opinion is in how actions are handled. In RPC, you just have POST /doWhateverThingNow, and that’s rather clear. But with REST, using these CRUD-like operations can make you feel like REST is no good at handling anything other than CRUD.

Well, that is not entirely the case. Triggering actions can be done with either approach; but, in REST, that trigger can be thought of more like an aftereffect. For example, if you want to “Send a message” to a user, RPC would be this:

POST /SendUserMessage HTTP/1.1
Host: api.example.com
Content-Type: application/json

{"userId": 501, "message": "Hello!"}
Copy
But in REST, the same action would be this:

POST /users/501/messages HTTP/1.1
Host: api.example.com
Content-Type: application/json

{"message": "Hello!"}
Copy
There’s quite a conceptual difference here, even if they look rather similar:

RPC. We are sending a message, and that might end up storing something in the database to keep a history, which might be another RPC call with possibly the same field names — who knows?
REST. We are creating a message resource in the user’s messages collection. We can see a history of these easily by doing a GET on the same URL, and the message will be sent in the background.

# what is Cache-Control

Cache-control is an HTTP header used to specify browser caching policies in both client requests and server responses. Policies include how a resource is cached, where it’s cached and its maximum age before expiring (i.e., time to live).

## Cache-Control: Max-Age

The max-age request directive defines, in seconds, the amount of time it takes for a cached copy of a resource to expire. After expiring, a browser must refresh its version of the resource by sending another request to a server.

For example, cache-control: max-age=120 means that the returned resource is valid for 120 seconds, after which the browser has to request a newer version.

Cache-Control: No-Cache
The no-cache directive means that a browser may cache a response, but must first submit a validation request to an origin server.

Cache-Control: No-Store
The no-store directive means browsers aren’t allowed to cache a response and must pull it from the server each time it’s requested. This setting is usually used for sensitive data, such as personal banking details.

Cache-Control: Public
The public response directive indicates that a resource can be cached by any cache.

Cache-Control: Private
The private response directive indicates that a resource is user specific—it can still be cached, but only on a client device. For example, a web page response marked as private can be cached by a desktop browser, but not a content delivery network (CDN).

## Additional HTTP Cache Headers
In addition to cache-control, notable HTTP cache headers include:

Expires – This header specifies a fixed date/time for the expiration of a cached resource. For example, Expires: Sat, 13 May 2017 07:00:00 GMT signals that the cached resource expires on May 13, 2017 at 7:00 am GMT. The expires header is ignored when a cache-control header containing a max-age directive is present.

ETag – A response header that identifies the version of served content according to a token – a string of characters in quotes, e.g., "675af34563dc-tr34" – that changes after a resource is modified. If a token is unchanged before a request is made, the browser continues to use its local version.

Vary – A header that determines the responses that must match a cached resource for it to be considered valid. For example, the header Vary: Accept-Language, User-Agent specifies that a cached version must exist for each combination of user agent and language.

# What is JSONP, and why was it created?

ay you're on domain example.com, and you want to make a request to domain example.net. To do so, you need to cross domain boundaries, a no-no in most of browserland.

The one item that bypasses this limitation is <script> tags. When you use a script tag, the domain limitation is ignored, but under normal circumstances, you can't really do anything with the results, the script just gets evaluated.

Enter JSONP. When you make your request to a server that is JSONP enabled, you pass a special parameter that tells the server a little bit about your page. That way, the server is able to nicely wrap up its response in a way that your page can handle.

For example, say the server expects a parameter called callback to enable its JSONP capabilities. Then your request would look like:

http://www.example.net/sample.aspx?callback=mycallback
Without JSONP, this might return some basic JavaScript object, like so:

{ foo: 'bar' }
However, with JSONP, when the server receives the "callback" parameter, it wraps up the result a little differently, returning something like this:

mycallback({ foo: 'bar' });
As you can see, it will now invoke the method you specified. So, in your page, you define the callback function:

mycallback = function(data){
  alert(data.foo);
};
And now, when the script is loaded, it'll be evaluated, and your function will be executed. Voila, cross-domain requests!

It's also worth noting the one major issue with JSONP: you lose a lot of control of the request. For example, there is no "nice" way to get proper failure codes back. As a result, you end up using timers to monitor the request, etc, which is always a bit suspect. The proposition for JSONRequest is a great solution to allowing cross domain scripting, maintaining security, and allowing proper control of the request.

These days (2015), CORS is the recommended approach vs. JSONRequest. JSONP is still useful for older browser support, but given the security implications, unless you have no choice CORS is the better choice.
# What are the differences between JSON and JSONP?


JSONP is JSON with padding. That is, you put a string at the beginning and a pair of parentheses around it. For example:

//JSON
{"name":"stackoverflow","id":5}
//JSONP
func({"name":"stackoverflow","id":5});

The result is that you can load the JSON as a script file. If you previously set up a function called func, then that function will be called with one argument, which is the JSON data, when the script file is done loading. This is usually used to allow for cross-site AJAX with JSON data. If you know that example.com is serving JSON files that look like the JSONP example given above, then you can use code like this to retrieve it, even if you are not on the example.com domain:

         function func(json){
           alert(json.name);
         }
         var elm = document.createElement("script");
         elm.setAttribute("type", "text/javascript");
         elm.src = "http://example.com/jsonp";
         document.body.appendChild(elm);

Basically, you're not allowed to request JSON data from another domain via AJAX due to same-origin policy. AJAX allows you to fetch data after a page has already loaded, and then execute some code/call a function once it returns. We can't use AJAX but we are allowed to inject <script> tags into our own page and those are allowed to reference scripts hosted at other domains.

Usually you would use this to include libraries from a CDN such as jQuery. However, we can abuse this and use it to fetch data instead! JSON is already valid JavaScript (for the most part), but we can't just return JSON in our script file, because we have no way of knowing when the script/data has finished loading and we have no way of accessing it unless it's assigned to a variable or passed to a function. So what we do instead is tell the web service to call a function on our behalf when it's ready.

For example, we might request some data from a stock exchange API, and along with our usual API parameters, we give it a callback, like ?callback=callThisWhenReady. The web service then wraps the data with our function and returns it like this: callThisWhenReady({...data...}). Now as soon as the script loads, your browser will try to execute it (as normal), which in turns calls our arbitrary function and feeds us the data we wanted.

It works much like a normal AJAX request except instead of calling an anonymous function, we have to use named functions.

jQuery actually supports this seamlessly for you by creating a uniquely named function for you and passing that off, which will then in turn run the code you wanted.

# What is critical rendering path?

The Critical Rendering Path is the sequence of steps the browser goes through to convert the HTML, CSS, and JavaScript into pixels on the screen. Optimizing the critical render path improves render performance.The critical rendering path includes the Document Object Model (DOM), CSS Object Model (CSSOM), render tree and layout.

The document object model is created as the HTML is parsed. The HTML may request JavaScript, which may, in turn, alter the DOM. The HTML includes or makes requests for styles, which in turn builds the CSS object model. The browser engine combines the two to create the Render Tree. Layout determines the size and location of everything on the page. Once layout is determined, pixels are painted to the screen.

Optimizing the critical rendering path improves the time to first render. Understanding and optimizing the critical rendering path is important to ensure reflows and repaints can happen at 60 frames per second, to ensure performant user interactions and avoid jank.


## Optimizing for CRP
Improve page load speed by prioritizing which resources get loaded, controlling the order in which they are loaded, and reducing the file sizes of those resources. Performance tips include 1) minimizing the number of critical resources by deferring their download, marking them as async, or eliminating them altogether, 2) optimizing the number of requests required along with the file size of each request, and 3) optimizing the order in which critical resources are loaded by prioritizing the downloading critical assets, shorten the critical path length.

# How to compress an image via Javascript in the browser?

Read the files using the HTML5 FileReader API with .readAsArrayBuffer

Create a Blob with the file data and get its url with window.URL.createObjectURL(blob)

Create new Image element and set it's src to the file blob url

Send the image to the canvas. The canvas size is set to desired output size

Get the scaled-down data back from canvas via canvas.toDataURL("image/jpeg",0.7) (set your own output format and quality)
Attach new hidden inputs to the original form and transfer the dataURI images basically as normal text

On backend, read the dataURI, decode from Base64, and save it
# What Is Lazy Loading?
Lazy loading images means loading images on websites asynchronously — that is, after the above-the-fold content is fully loaded, or even conditionally, only when they appear in the browser’s viewport. This means that if users don’t scroll all the way down, images placed at the bottom of the page won’t even be loaded.

Lazy Loading with Blurred Image Effect
You can lazy load images with this interesting blurring effect in a number of ways.

Native lazy loading of images and iframes is super cool. Nothing could be more straightforward than the markup below:

<img src="myimage.jpg" loading="lazy" alt="..." />
<iframe src="content.html" loading="lazy"></iframe>
As you can see, no JavaScript, no dynamic swapping of the src attribute’s value, just plain old HTML.

The loading attribute gives us the option to delay off-screen images and iframes until users scroll to their location on the page. loading can take any of these three values:

lazy: works great for lazy loading
eager: instructs the browser to load the specified content right away
auto: leaves the option to lazy load or not to lazy load up to the browser.
This method has no rivals: it has zero overhead, it’s clean and simple. However, although at the time of writing most major browsers have good support for the loading attribute, not all browsers are on board yet.

# Why Lazy Load at All?

## Performance Gains
The obvious benefit is that we get smaller web pages that load faster. Lazy loading reduces the number of images that need to be loaded on a page up front. Fewer image requests mean fewer bytes to download. And fewer bytes to download means the page renders faster than if those bytes and requests were being made.

## Cost reduction
The second benefit is for you as a website administrator. Cloud hosting services, like Content Delivery Networks (CDNs) or web servers or storages, deliver images (or any asset for that matter) at a cost based on the number of bytes transferred. A lazy loaded image may never get loaded if the user never reaches it. Thus, you may reduce the total bytes delivered on the page and ultimately save yourself a few pennies in the process. This is especially true for users that instantly bounce off a page or interact only with the top portion of the content.

Method 1: Trigger the image load using Javascript events
This technique uses event listeners on the scroll, resize and orientationChange events in the browser. The scroll event is pretty clear cut because it watches where the user is on a page as scrolling occurs. The resize and orientationChange events are equally important. The resize event occurs when the browser window size changes, whereas orientationChange gets triggered when the device is rotated from landscape to portrait, or vice versa.

We can use these three events to recognize a change in the screen and determine the number of images that become visible on the screen and trigger them to load accordingly.

When any of these events occur, we find all the images on the page that are deferred and, from these images, we check which ones are currently in the viewport. This is done using an image’s top offset, the current document top position, and window height. If an image has entered the viewport, we pick the URL from the data-src attribute and move it to the src attribute and the image will load as a result.

Note that we will ask JavaScript to select images that contain a lazy class. Once the image has loaded, we’ll remove the class because it no longer needs to trigger an event. And, once all the images are loaded, we remove the event listeners as well.

Method 2: Trigger the image load using the Intersection Observer API
The Intersection Observer API is relatively new. It makes it simple to detect when an element enters the viewport and take an action when it does. In the previous method, we had to bind events, keep performance in mind and implement a way to calculate if the element was in the viewport or not. The Intersection Observer API removes all that overhead by avoiding the math and delivering great performance out of the box.

# What is Preload, Prefetch, and Preconnect?

preload is a new web standard that offers more control on how particular resources are fetched for current navigation. This is the updated version of subresource prefetching which was deprecated in January 2016. This directive can be defined within a <link> element for example as <link rel="preload">. Generally it is best to preload your most important resources such as images, CSS, JavaScript, and font files. This is not to be confused with browser preloading in which only resources declared in HTML are preloaded. The preload directive actually overcomes this limitation and allows resources which are initiated via CSS and JavaScript to be preloaded and define when each resource should be applied.

Here is a very basic example of preloading an image.

<link rel="preload" href="image.png">
Here is an example of preloading fonts. If you are preloading links with CORS enabled resources you must also include the crossorigin attribute.

<link rel="preload" href="https://example.com/fonts/font.woff" as="font" crossorigin>

prefetch#
prefetch is a low priority resource hint that allows the browser to fetch resources in the background (idle time) that might be needed later, and store them in the browser's cache. Once a page has finished loading it begins downloading additional resources and if a user then clicks on a prefetched link, it will load the content instantly. There are three different types of prefetching, link, DNS, and prerendering which we will go into more below.

1. Link prefetching#
As mentioned above, link prefetching allows the browser to fetch resources, store them in cache, assuming that the user will request them. The browser looks for prefetch in the <link> HTML element or the Link HTTP header such as:

HTML: <link rel="prefetch" href="/uploads/images/pic.png">
HTTP header: Link: </uploads/images/pic.png>; rel=prefetch


3. Prerendering#
Prerendering is very similar to prefetching in that it gathers resources that the user may navigate to next. The difference is that prerendering actually renders the entire page in the background, all the assets of a document. Below is an example.

<link rel="prerender" href="https://www.keycdn.com">
The prerender hint can be used by the application to indicate the next likely HTML navigation target: the user agent will fetch and process the specified resource as an HTML response. To fetch other content-types with appropriate request headers, or if HTML preprocessing is not desired, the application can use the prefetch hint.

# rendering optimize

Optimizing your JavaScript
JavaScript often triggers visual changes in the browser. All the more so when building an SPA.
Here are a few tips on which parts of your JavaScript you can optimize to improve rendering:
Avoid setTimeout or setInterval for visual updates. These will invoke the callback at some point in the frame, possible right at the end. What we want to do is trigger the visual change right at the start of the frame not to miss it.

Move long-running JavaScript computations to Web Workers as we have previously discussed.
Use micro-tasks to introduce DOM changes over several frames. This is in case the tasks need access to the DOM, which is not accessible by Web Workers. This basically means that you’d break up a big task into smaller ones and run them inside requestAnimationFrame , setTimeout, setInterval depending on the nature of the task.

Optimize your CSS

Modifying the DOM through adding and removing elements, changing attributes, etc. will make the browser recalculate element styles and, in many cases, the layout of the entire page or at least parts of it.

To optimize the rendering, consider the following:

Reduce the complexity of your selectors. Selector complexity can take more than 50% of the time needed to calculate the styles for an element, compared to the rest of the work which is constructing the style itself.
Reduce the number of elements on which style calculation must happen. In essence, make style changes to a few elements directly rather than invalidating the page as a whole.

## Optimize the layout

Layout re-calculations can be very heavy for the browser. Consider the following optimizations:
Reduce the number of layouts whenever possible. When you change styles the browser checks to see if any of the changes require the layout to be re-calculated. Changes to properties such as width, height, left, top, and in general, properties related to geometry, require layout. So, avoid changing them as much as possible.

Use flexbox over older layout models whenever possible. It works faster and can create a huge performance advantage for your app.
Avoid forced synchronous layouts. The thing to keep in mind is that while JavaScript runs, all the old layout values from the previous frame are known and available for you to query. If you access box.offsetHeight it won’t be an issue. If you, however, change the styles of the box before it’s accessed (e.g. by dynamically adding some CSS class to the element), the browser will have to first apply the style change and then run the layout. This can be very time-consuming and resource-intensive, so avoid it whenever possible.

## Optimize the paint
This often is the longest-running of all the tasks so it’s important to avoid it as much as possible. Here is what we can do:

Changing any property other than transforms or opacity triggers a paint. Use it sparingly.
If you trigger a layout, you will also trigger a paint, since changing the geometry results in a visual change of the element.
Reduce paint areas through layer promotion and orchestration of animations.
Rendering is a vital aspect of how SessionStack functions. SessionStack has to recreate as a video everything that happened to your users at the time they experienced an issue while browsing your web app.
To do this, SessionStack leverages only the data that was collected by our library: user events, DOM changes, network requests, exceptions, debug messages, etc. Our player is highly optimized to properly render and make use of all the collected data in order to offer a pixel-perfect simulation of your users’ browser and everything that happened in it, both visually and technically.

# Optimizing the rendering performance
If you’d like to optimize your app, there are five major areas that you need to focus on. These are the areas over which you have control:
JavaScript — in previous posts we covered the topic of writing optimized code that doesn’t block the UI, is memory efficient, etc. When it comes to rendering, we need to think about the way your JavaScript code will interact with the DOM elements on the page. JavaScript can create lots of changes in the UI, especially in SPAs.

## Style calculations — 
this is the process of determining which CSS rule applies to which element based on matching selectors. Once the rules are defined, they are applied and the final styles for each element are calculated.

## Layout — 
once the browser knows which rules apply to an element, it can begin to calculate how much space the latter takes up and where it is located on the browser screen. The web’s layout model defines that one element can affect others. For example, the width of the <body> can affect the width of its children and so on. This all means that the layout process is computationally intensive. The drawing is done in multiple layers.
         
## Paint — 
this is where the actual pixels are being filled. The process includes drawing out text, colors, images, borders, shadows, etc. — every visual part of each element.
## Compositing — 
since the page parts were drawn into potentially multiple layers they need to be drawn onto the screen in the correct order so that the page renders properly. This is very important, especially for overlapping elements.

# What is lexical 'this'?

As you probably know, when you define a function and use a variable inside of it, it checks if the variable has been defined in its scope. If it is, it uses it! If not, it checks the enclosing scope for that variable definition. 
It keeps checking enclosing scopes until it finds the variable or reaches global scope. Now, function definitions that are not arrow functions define this for you, implicitly. 
Thus, they will never check an enclosing scope when you try to use this in their scope (because they find it in their own scope!). Arrow functions do NOT define their own this, so they go to the enclosing scope and look for it just as they would with any variable you try to use in their scope.

# When to use function declarations and expressions

use function declarations when you want to create a function on the global scope and make it available throughout your code. Use function expressions to limit where the function is available, keep your global scope light, and maintain clean syntax.

Function declarations are hoisted but function expressions are not.

# Higher-Order Functions

Higher order functions are functions that operate on other functions, either by taking them as arguments or by returning them. In simple words, A Higher-Order function is a function that receives a function as an argument or returns the function as output.
For example, Array.prototype.map, Array.prototype.filter and Array.prototype.reduce are some of the Higher-Order functions built into the language.

# Array.prototype.map
The map() method creates a new array by calling the callback function provided as an argument on every element in the input array. The map() method will take every returned value from the callback function and creates a new array using those values.

Example 1#
         Let’s say we have an array of numbers and we want to create a new array which contains double of each value of the first array. Let’s see how we can solve the problem with and without Higher-Order Function.
         Without Higher-order function
         const arr1 = [1, 2, 3];
         const arr2 = [];
         for(let i = 0; i < arr1.length; i++) {
           arr2.push(arr1[i] * 2);
         }
         // prints [ 2, 4, 6 ]
         console.log(arr2);
         With Higher-order function map
         const arr1 = [1, 2, 3];
         const arr2 = arr1.map(function(item) {
           return item * 2;
         });
         console.log(arr2);
         We can make this even shorter using the arrow function syntax:
         const arr1 = [1, 2, 3];
         const arr2 = arr1.map(item => item * 2);
         console.log(arr2);

## Array.prototype.filter

The filter() method creates a new array with all elements that pass the test provided by the callback function. The callback function passed to the filter() method accepts 3 arguments: element, index, and array.

## Array.prototype.reduce

The reduce method executes the callback function on each member of the calling array which results in a single output value. The reduce method accepts two parameters: 
1) The reducer function (callback), 
2) 2) and an optional initialValue.

Creating Our own Higher-Order Function
Up until this point, we saw various Higher-order functions built into the language. Now let’s create our own Higher-order function.
Let’s imagine JavaScript didn’t have the native map method. We could build it ourselves thus creating our own Higher-Order Function.
Let’s say, we have an array of strings and we want to convert this array to an array of integers, where each element represent the length of the string in the original array.
const strArray = ['JavaScript', 'Python', 'PHP', 'Java', 'C'];
function mapForEach(arr, fn) {
  const newArray = [];
  for(let i = 0; i < arr.length; i++) {
    newArray.push(
      fn(arr[i])
    );
  }
  return newArray;
}
const lenArray = mapForEach(strArray, function(item) {
  return item.length;
});
// prints [ 10, 6, 3, 4, 1 ]
console.log(lenArray);

In the above example, we created an Higher-order function mapForEach which accepts an array and a callback function fn. This function loops over the provided array and calls the callback function fn inside the newArray.push function call on each iteration.
The callback function fn receives the current element of array and returns the length of that element, which is stored inside the newArray. After the for loop has finished, the newArray is returned and assigned to the lenArray.

# how to create our own map function.

Create an empty array mapArr.
Loop through array elements.
Call function mapFunc with the current element as the argument.
Push the result of the mapFunc function to the mapArr array.
Return the mapArr array after going through all the elements.
Now let’s write our implementation of the map()

         // map takes an array and function as 
         argumentfunction map(arr, mapFunc) {    
         const mapArr = []; // empty array       
         // loop though array   
         for(let i=0;i<arr.length;i++) {        
         const result = mapFunc(arr[i], i, arr);
         mapArr.push(result);    
         }    
         return mapArr;
         }
Now if you call the new map() in the previous example code,

         const squareArr2 = map(arr, num => num ** 2);
         console.log(squareArr2); // prints [1, 4, 9, 16, 25]
         
# What is client-side rendering?

Client-side rendering means that a website’s JavaScript is rendered in your browser, rather than on the website’s server. 

According to Google’s Martin Splitt, “If you use a JavaScript framework, the default is client-side rendering. This means you send the bare-bones HTML over and then a piece of JavaScript, and the JavaScript fetches and assembles the content in the browser.” 


# What are the benefits of client-side rendering?

Because all the burden of rendering content is on the client (i.e. person or bot trying to view your page), client-side rendering is the cheaper option for the website owner because it reduces the load on their own servers. 

It’s also the default state for JavaScript websites, making client-side rendering easier than server-side rendering for the website owner. 

# What are the risks of client-side rendering?

Client-side rendering has two main downsides. 

For one, client-side rendering can increase the likelihood of a poor user experience. JavaScript can add seconds of load time to a page, and if that burden is fully on the client (website visitor), then they could get frustrated and leave your site.

he second big downside of client-side rendering is its effect on search engine bots. For example, Googlebot has something called a second wave of indexing. In this process, they crawl and index the HTML of a page first, then come back to render the JavaScript when resources become available. This two-phased approach means that sometimes, JavaScript content might be missed, and not included in Google’s index

# What is server-side rendering?

Server-side rendering means that a website’s JavaScript is rendered on the website’s server. To use the furniture example again, this would be like ordering furniture that arrives at your house fully assembled.  

# What are the benefits of server-side rendering?

Because JavaScript is rendered on the website’s server, both search engine bots and humans get a faster page experience. This not only means a better UX (which is also part of Google’s ranking algorithm), but it also eliminates speed-related crawl budget issues.

Sending fully-rendered pages to search engine bots also means that you’re not risking the “partial indexing” that can happen with client-side rendered content. When Google and other search engine bots try to access your page, instead of having to wait for rendering resources to become available before seeing your full page, they’ll get the fully-rendered page right from the get-go. 

# What are the risks of server-side rendering?

Server-side rendering can be expensive and resource-intensive. It can be expensive because the full burden of rendering your content for bots and human website visitors is on your servers. It can be resource-intensive to implement, since it’s not the default for JavaScript websites and will require work from your engineering team to execute. 

Server-side rendering also tends not to work with third-party JavaScript. So, if you use services like Bazaarvoice to pull in reviews on your website, they won’t be rendered with server-side rendering.

# Which is better for SEO, client-side or server-side rendering?
Between the two options, server-side rendering is better for SEO than client-side rendering. This is because server-side rendering can speed up page load times, which not only improves the user experience, but can help your site rank better in Google search results. 

Server-side rendering is also better for SEO because it removes the burden of rendering JavaScript off of search engine bots, solving speed-related crawl budget issues and partial indexing.

# HTTP cookies

An HTTP cookie (web cookie, browser cookie) is a small piece of data that a server sends to the user's web browser. The browser may store it and send it back with later requests to the same server. Typically, it's used to tell if two requests came from the same browser — keeping a user logged-in, for example. It remembers stateful information for the stateless HTTP protocol.

Cookies are mainly used for three purposes:

# Session management

Logins, shopping carts, game scores, or anything else the server should remember
Personalization
User preferences, themes, and other settings
Tracking
Recording and analyzing user behavior
Cookies were once used for general client-side storage. While this was legitimate when they were the only way to store data on the client, it is now recommended to use modern storage APIs. Cookies are sent with every request, so they can worsen performance (especially for mobile data connections). Modern APIs for client storage are the Web Storage API (localStorage and sessionStorage) and IndexedDB.

# Creating cookies
After receiving an HTTP request, a server can send one or more Set-Cookie headers with the response. The cookie is usually stored by the browser, and then the cookie is sent with requests made to the same server inside a Cookie HTTP header. An expiration date or duration can be specified, after which the cookie is no longer sent. Additional restrictions to a specific domain and path can be set, limiting where the cookie is sent. For details about the header attributes mentioned below, refer to the Set-Cookie reference article.

The Set-Cookie and Cookie headers
The Set-Cookie HTTP response header sends cookies from the server to the user agent. A simple cookie is set like this:

Set-Cookie: <cookie-name>=<cookie-value>
This shows the server sending headers to tell the client to store a pair of cookies
         
# what is mobile first approach

Mobile First Design/Development refers to the practice of designing for mobile, well, first. Essentially, the aim of mobile first is to switch the workflow from tackling desktop designs first and addressing the mobile design head on, working towards the desktop version as the project evolves.

With Mobile First, developers have the flexibility to scale up rather than scale down. For example, when you start designing for a desktop platform, there is a lot more real estate to take advantage of. The core design elements may be incredible on a desktop platform, providing a really great user experience. However, when this design needs to be adapted for mobile, you realize that none of the technology that makes the desktop user experience so great can scale down well to mobile devices. Which then leads to a sub-par mobile experience in comparison to the desktop version, and for some consumers it may feel like more of an afterthought than an actual finished product.

Scaling up designs on the other hand, presents a lot more freedom in the way you’re able to adapt your designs. With a well-functioning mobile product, you’ve already prioritized features and capabilities and identified the essential elements of your platform. Progressively enhancing the mobile platform to fit the requirements for desktop becomes a series of decisions on how to add rather than cut elements of your platform, which gives you another opportunity to be creative about how to engage users.

## Why Does Mobile Matter?

Whether it’s browsing the internet on the train in the morning, checking your emails while waiting for an appointment, or listening to music at the gym, cell phones are deeply embedded in our daily routines. Each speck of downtime is one we can use to update ourselves with our network and the news, or even order that one thing from Amazon that we keep forgetting to buy. It’s no surprise that our mobile devices take up almost 5 hours of our day, mainly attributed to application use. Mobile application usage grew 6% last year, with interesting shifts in how people are using the time spent on their phones.

# gulp vs grunt vs webpack

Grunt and Gulp are task runners, while Webpack is a module bundler. Task runners are basically used to automate tasks in a development process. Some of these tasks include compressing JS files, compiling Sass files, watching out for file changes, minifying files and auto-prefixing

Gulp and Grunt offer features like code minification, CSS preprocessing, unit testing and a list of others.

Gulp is based on Node streams, allowing for pipelining. Grunt, on the other hand, relies on data configuring files where every source and destination file must be declared. As the project gets larger, Grunt becomes even more cumbersome to manage.

For Gulp and Grunt, there is a high dependence on the plugin author to maintain the plugins, and sometimes, there is little or no documentation to fall back on when an issue is being faced. The result is usually to wait for these authors to make updates or resolve to fix them yourself. However, most Webpack plugins are maintained by Webpack’s core team while the rest are managed by Webpack’s community; and this makes it more reliable.

Gulp uses plugins that each perform a single task as opposed to Grunt where one plugin can perform multiple tasks.

Webpack can be extended even beyond its core functionality with the aid of plugins and loaders, the only issue being the complications that may arise while configuring it.

# display none and visibility hidden difference

display:none removes the element from the normal flow of the page, allowing other elements to fill in.

visibility:hidden leaves the element in the normal flow of the page such that is still occupies space.

 if we use id and class on same div then add color to both id and class then which color get reflected
Id color get reflected
 doesn't matter of order of css line
 If more than one rule applies to an element and specifies the same property, then CSS gives priority to the rule that has the more specific selector. An ID selector is more specific than a class selector, which in turn is more specific than a tag selector.
 if u want to work css class then what u will do 
Ans => #color {
  color: white;
}
#color.color{
color: red
}
use this type of css
