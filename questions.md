1.  What is XSS, CORS,CSRF?
    ans: XSS, CORS, and CSRF are all security vulnerabilities that can affect web applications.

          XSS (Cross-Site Scripting) is a type of vulnerability that allows an attacker to inject malicious scripts into a web page viewed by other users. This can allow the attacker to steal sensitive data or perform actions on behalf of the user.

          CORS (Cross-Origin Resource Sharing) is a security feature implemented by browsers that restricts web pages from making requests to a different origin than the one that served the page. This helps prevent malicious scripts from accessing data on other sites.

          CSRF (Cross-Site Request Forgery) is a type of vulnerability that allows an attacker to execute unauthorized actions on behalf of a user who is logged in to a web application. This can happen when a user visits a malicious website that contains a script that performs a request to the vulnerable application, allowing the attacker to perform actions on the user's behalf.

          It's important for web developers to understand these vulnerabilities and take appropriate measures to prevent them, such as input validation, proper use of HTTP headers, and using CSRF tokens.

2.  Difference between useMemo, useCallback?
    ans: memo remembers a value and vaue is recalculated based on the dependecy variable.
    callback remembers a function, and recreated when the dependency variable changes

    useMemo and useCallback are both hooks in React that can help optimize performance by memoizing (caching) the results of a function, and preventing unnecessary re-rendering of components.

    useMemo is used to memoize the result of a function or expression, and returns a memoized value. It takes two arguments: the first is a function that returns the value to be memoized, and the second is an array of dependencies that trigger the memoization when they change. useMemo is useful for expensive computations or functions that need to be called repeatedly but don't depend on props or state.

    `const memoizedValue = useMemo(() => expensiveFunction(arg), [arg]);`

    useCallback is used to memoize a function itself, and returns a memoized callback function. It takes two arguments: the first is a function that needs to be memoized, and the second is an array of dependencies that trigger the memoization when they change. useCallback is useful for preventing unnecessary re-renders of child components that rely on a function passed down from the parent component.

    `const memoizedCallback = useCallback(() => {
  doSomethingWithArg(arg);
}, [arg]);`

    The main difference between useMemo and useCallback is the type of value they memoize. useMemo memoizes a value, while useCallback memoizes a function. useCallback is often used in conjunction with React.memo to memoize a component and prevent unnecessary re-renders.

3.  What is event-delegation?
    Event delegation is a technique used in web development to handle events on a large number of child elements using only a single event listener on a parent element.

    Instead of adding an event listener to each child element individually, event delegation takes advantage of event bubbling, where an event that occurs on a child element will also be triggered on its parent elements up to the document root. By attaching an event listener to the parent element, it can catch and handle the events triggered by its child elements.

    For example, consider a list of items where each item has a button to delete it. Rather than adding an event listener to each button, we can add a single event listener to the list container element and use event delegation to handle button clicks.

    `<ul id="myList">
      <li>Item 1 <button>Delete</button></li>
      <li>Item 2 <button>Delete</button></li>
      <li>Item 3 <button>Delete</button></li>
    </ul>`

    `const list = document.getElementById('myList');

    list.addEventListener('click', (event) => {
    if (event.target.nodeName === 'BUTTON') {
    const listItem = event.target.parentNode;
    listItem.parentNode.removeChild(listItem);
    }
    });`
    In the example above, we attach a click event listener to the ul element and check if the event target is a button. If it is, we retrieve the parent li element and remove it from the list.

    Event delegation can make our code more efficient, especially when dealing with large numbers of child elements, since we only need a single event listener instead of many. It can also simplify our code by avoiding the need to add and remove event listeners dynamically as elements are added or removed from the DOM.
    ans: keeping the handler function on the parent than on each child, so event propagation can still trigger the call.

4.  what is critical rendering path?
    The critical rendering path is the sequence of steps that a browser takes to render a web page on the screen. It includes the loading and rendering of the HTML, CSS, and JavaScript resources required by the page.

    The critical rendering path is critical because it determines how quickly a web page appears on the user's screen, and how smoothly it interacts with the user. The faster a page loads and renders, the better the user experience, and the higher the chances that the user will stay on the site.

    The critical rendering path consists of several steps:

    HTML parsing: The browser fetches the HTML document and parses it to construct the Document Object Model (DOM) tree.
    CSS parsing and styling: The browser fetches the CSS resources and constructs the CSS Object Model (CSSOM) tree. It then combines the DOM and CSSOM to generate the Render Tree, which represents the content that will be displayed on the screen.
    Layout: The browser calculates the layout of each element in the Render Tree, determining its size, position, and other properties.
    Paint: The browser paints the pixels on the screen based on the layout and styling information.
    To optimize the critical rendering path, web developers can take several steps, such as minimizing the size and number of resources, using asynchronous loading of resources, and optimizing the CSS and JavaScript code. They can also use tools like Lighthouse, Google PageSpeed Insights, and WebPageTest to analyze and optimize the critical rendering path of their web pages.

5.  What is service worker?
    A service worker is a type of web worker that runs in the background of a web application, separate from the web page, intercepting network requests and enabling advanced features such as offline support, push notifications, and background sync.

    Service workers are event-driven, meaning they respond to events such as network requests, push notifications, and updates to cached resources. They run in a separate thread from the main JavaScript execution context, allowing them to perform tasks without blocking the user interface or other JavaScript code.

    Service workers use the Cache API to store resources, such as HTML, CSS, JavaScript, images, and other assets, in the browser cache. By caching resources, service workers can make web applications load faster, even when the user is offline or has a slow network connection.

    In addition to caching resources, service workers can also intercept network requests and serve cached responses, allowing web applications to work offline or in limited connectivity environments. Service workers can also respond to push notifications, allowing web applications to send messages and alerts to users, even when the web page is not open.

    To use a service worker, a web developer must first register it with the browser by including a link to the service worker JavaScript file in the web page, and then install it. Once installed, the service worker can control certain aspects of the web application, such as caching and network requests.

    Service workers are supported in modern web browsers, including Google Chrome, Mozilla Firefox, and Microsoft Edge. They can significantly enhance the user experience of web applications by enabling advanced features that were previously only available in native mobile apps.

6.  what is web worker?
    Web workers are a type of JavaScript API that enable running JavaScript code in a separate background thread, allowing long-running or CPU-intensive tasks to be performed without blocking the user interface or other scripts running on the main thread.

        Web workers enable concurrent processing by allowing scripts to be executed in parallel with the main thread. This improves the overall performance of the application and the user experience, as it allows the application to remain responsive even when performing complex or time-consuming tasks.

        There are two types of web workers: Dedicated workers and Shared workers.

        A dedicated worker is a worker that is associated with a specific script file and can only be accessed by that script. Dedicated workers are ideal for tasks that require high performance or are long-running, such as data processing or computations.

        A shared worker is a worker that can be accessed by multiple scripts running on different web pages, allowing multiple web pages to communicate and share data with the same worker. Shared workers are ideal for tasks that require interactivity or real-time updates, such as chat applications or multi-player games.

        Web workers communicate with the main thread using message passing, which allows them to exchange data and work together without interfering with each other or blocking the user interface.

        Web workers are supported in modern web browsers, including Google Chrome, Mozilla Firefox, and Microsoft Edge. They are a powerful tool for building high-performance web applications that require complex calculations or real-time updates.

7.  Explain webpack?
    Webpack is a popular open-source module bundler for modern web applications. It allows developers to bundle JavaScript files and other assets, such as CSS, images, and fonts, into a single file that can be served to the browser.

        Webpack works by analyzing a JavaScript file's dependencies and creating a dependency graph, which includes all of the modules that the file depends on. It then uses loaders to transform the modules into a format that can be included in the final bundle.

        Loaders are plugins that allow developers to transform files, such as transpiling ES6 to ES5, or minifying CSS and JavaScript files. Webpack also supports plugins that can perform tasks such as code splitting, caching, and optimization.

        Webpack has several core concepts, including entry points, output, loaders, and plugins.

        Entry points: An entry point is the starting point for Webpack to build its dependency graph. Typically, an application will have one or more entry points, which are usually JavaScript files.

        Output: The output is the location where Webpack will output the final bundled file. It includes the filename and the location of the file, and can be customized using Webpack configuration.

        Loaders: Loaders are used to transform files before they are included in the bundle. Loaders can be used for tasks such as transpiling, linting, and minifying.

        Plugins: Plugins are used to perform additional tasks, such as code splitting, optimization, and caching.

        Webpack can be configured using a JavaScript configuration file, which includes the entry points, output, loaders, and plugins. The configuration file can also include other options, such as optimization settings, dev server settings, and performance metrics.

        Webpack is widely used in modern web development and is supported by most major web development frameworks, such as React, Vue.js, and Angular. It provides a powerful and flexible toolset for bundling assets and optimizing the performance of web applications.

8.  explain BABEL?
9.  Expalin OOPS in JS?
10. what is react-scripts used in package.json?
11. What is web-scokets?
12. what is lexical scope?
13. What is React.memo?
14. How to do deep copying of object in JS?
15. Methods to delete array elements?
    ans: splice, pop, shift, delete, and set length to 0
16. What is side effects in react and how to handle them?
17. What is pure functions?
18. What are advantages of semntic tags?
19. Explain border-box.
20. How Promises are handled in event-loop?
