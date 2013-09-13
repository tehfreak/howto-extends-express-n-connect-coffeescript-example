# Extends Connect/Express Application]()

    {assert}= require 'chai'




## Extends Connect

    connect= require 'connect'


    class ConnectApp extends connect

        constructor: () ->
            app= super
            @constructor.prototype.__proto__= app.__proto__
            app.__proto__= @constructor.prototype
            return app

        method1: () ->
            return @

        @staticMethod1: () ->
            return @


    app= new ConnectApp


    assert.instanceOf app, Function, 'should be an instance of Function'
    assert.instanceOf app, ConnectApp, 'should be an instance of ConnectApp'

    assert.strictEqual app.constructor.version, connect.version, 'constructor should be extended'

    assert.isDefined app.method1, 'prototype method should be defined'
    assert.isDefined app.constructor.staticMethod1, 'constructor method should be defined'





## Extends Express

    express= require 'express'


    class ExpressApp extends express

        constructor: () ->
            app= super
            @constructor.prototype.__proto__= app.__proto__
            app.__proto__= ExpressApp.prototype
            return app

        method1: () ->
            return @

        @staticMethod1: () ->
            return @


    app= new ExpressApp


    assert.instanceOf app, Function, 'should be an instance of Function'
    assert.instanceOf app, ExpressApp, 'should be an instance of ExpressApp'

    assert.strictEqual app.constructor.application, express.application, 'constructor should be extended'

    assert.isDefined app.method1, 'prototype method should be defined'
    assert.isDefined app.constructor.staticMethod1, 'constructor method should be defined'





## Moar

Extends...

    class App extends ExpressApp

        constructor: () ->
            app= super
            @constructor.prototype.__proto__= app.__proto__
            app.__proto__= App.prototype
            return app

        method2: () ->
            return @

        @staticMethod2: () ->
            return @


    app= new App


    assert.instanceOf app, Function, 'should be an instance of Function'
    assert.instanceOf app, App, 'should be an instance of App'
    assert.instanceOf app, ExpressApp, 'should be an instance of ExpressApp'

    assert.isDefined app.method1, 'prototype method should be defined'
    assert.isDefined app.method2, 'prototype method should be defined'

    assert.isDefined app.constructor.staticMethod1, 'constructor method should be defined'
    assert.isDefined app.constructor.staticMethod2, 'constructor method should be defined'

And run...

    app.listen port= 1337, () ->
        console.log 'listening on port - %d', port

    app.use (req, res, next) ->
        res.end 'Hello World'
