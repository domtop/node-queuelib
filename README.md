QueueLib
========

Queuelib has been simplified, and now there are only two options. PushSync And PushAsync

Example
=======

    var Queuelib = require('queuelib');
    var myqueue = new Qlib(function(data,lib) {
        console.log(data*2);
        lib.done();
    });

    myqueue.pushAsync(2);
    myqueue.pushAsync(3);
    myqueue.pushAsync(4);
    myqueue.pushAsync(5);
    myqueue.pushAsync(6);
   
    // 4
    // 6
    // 8
    // 10
    // 12
    
You can advance from anywhere
=============================

    var Queuelib = require('queuelib');
    var myqueue = new Qlib(function(data) {
        console.log(data*2);
        doSomething();
    });

    var doSomething = function() {
        myqueue.done();
    };

    myqueue.pushAsync(2);
    myqueue.pushAsync(3);
    myqueue.pushAsync(4);
    myqueue.pushAsync(5);
    myqueue.pushAsync(6);
    
    // 4
    // 6
    // 8
    // 10
    // 12


You can supply your own custom work function per push
=====================================================

q is passed as the last argument, just call .done() when done

    myqueue.pushAsync({foo:42}, function(obj,q) {
        var bar = obj.foo * 2; // 84
        q.done();
    });
