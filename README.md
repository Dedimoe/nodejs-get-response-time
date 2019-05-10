# nodejs-get-response-time
NodeJS get response time

//---1---
request.get({
  url : 'http://www.sample.com',
  time : true
},function(error, response){
  console.log('Request time in ms', response.elapsedTime)
})


//---2---

var begin = new Date()
request.get('http://www.sample.com', function(error, response){
    console.log('Request time plus 5 seconds', new Date() - begin)
})
require('sleep').sleep(5) // synchronous action : time need 5 seconds


//---3---

var timed_req = function(url, next) {
  var begin = new Date()
  request(url, function(error, response, body) {
    res.responseTime = new Date() - begin
    next(error, response, body);
  })
}


//---4---

var timed_req = function(url, next) {
  var tick = new t.Tick("response_time")
  tick.start()
  request(url, function(error, response, body) {
    tick.stop()
    next(error, response, body)
  })
}

// check the results :
var response_time = t.timers.response_time;
console.log(response_time.min());           // minimal response time
console.log(response_time.max());           // minimal response time
console.log(response_time.mean());          // mean response time
console.log(response_time.median());        // median response time

//---end---

