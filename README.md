1. 
Explain what is meant by the stream abstraction. What is the relationship between streams and the observer pattern?  What are streams useful for modeling and when might you use them in Rich Web development?

Streams are an abstraction for some data which could be, but does not have to be present now, and could, but does not have to arrive in the future. 
Streams implement a design pattern called the observable pattern which offers a subscription model in which objects subscribe to an event and get notified when the event occurs.
Streams are used to model all application states, providing a unified abstraction of everything, we do this because callbacks and promises have drawbacks callbacks fall short when we have a ui with widgets that interact with each other or processes that consume from several downstream services. Promises fall short as they are unable to handle data sources that provide more than one value. Steams are used to resolve this synchronization problem.


2. 
Assume that you are building an interface to an API in your Rich Web App. Describe in detail how you could use the RxJS library to handle asynchronous network responses to API requests. In your opinion, what are the benefits to using a streams library for networking over, say, promises? And what do you think are the downsides?

To do asynchronous responses to api requests you could use promises or ajax
Promise:
const data = from(fetch('https:apilink.com’));
data.subscribe({
  next(response) { console.log(response); },
  error(err) { console.error('Error: ' + err); },
  complete() { console.log('Completed'); }
});
First you fetch the data with a promise and then subscribe to the data and log the response that you got to console, if theres an error log the error, and if it works perfect log that too.
Ajax:
const data = ajax('https:apilink.com’);
data.subscribe(res => console.log(res.status, res.response));
first you get the data using ajax and then it logs the status i.e. error/complete, and then the response you got from that link


A JavaScript promise is an object that produces a single value asynchronously, whereby you send a data set in, and a single value is returned and used, making it an easy, straightforward way to handle data. 
Observables take in a stream of data, and multiple pieces of data are returned over time. Observables do nothing until called upon or “subscribed” to. Once it is subscribed to it handles the data and emits the values that are returned.



Observables vs Promises: 
  1. Complexity.
  Promises come inbuilt with JavaScript, meaning you can use it the moment you get started whereas observables are inside the rxjs library meaning we have to add a third party library. Although the minified RxJS is pretty small, every byte helps with preformance.
  2. Cancelability
  Promises by default are not cancelable whereas you can unsubscribe from a rxjs observable stream.
  3. Ability to use multiple sources.
  A promise we only get one event handling to occur whereas observables can have multiple events from the same source, which could introduce the problem of if you are displaying and updating the data, you could have weird overlap problems where it swaps between sources if your displaying to the same variable on the page, but it also gives you the option to use multiple sources.

3. 
Consider three asynchronous tasks, A,B & C. What are the consequences of these functions sharing global state? What is a good practice to alleviate any problems associated with this?

Global states are easily overwritten by other scripts. Global states are not necessarily bad and not even a security concern, but it shouldn’t overwrite values of another variable, if you do modify them, you no longer can have certainty about the output you’ll get.
To alleviate the problems associated with this we should instead use local variables and wrap the code in closures. 
