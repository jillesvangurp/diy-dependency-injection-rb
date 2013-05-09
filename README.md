# diy-dependency-injection-rb


Simple [http://misko.hevery.com/2010/05/26/do-it-yourself-dependency-injection/](DIY dependency injection) framework for Ruby that 

* allows you to register any Ruby object with an application context and then refer to it by name 
* can integrate a Java Spring Context as well. This is particularly useful if you have mixed Java and Jruby code and want to expose your Spring beans to a JRuby application.
* integrates a solution for setting and reading feature flags

# Usage

Simply copy app_context into your project. There is no gem currently and the version I have here is a simplified version of what I use in my applications. The code is simple enough that you may want to tweak it anyway.

Create an application definition module where you wire up all your Ruby objects:

    require 'app_context'
    
    module ApplicationDefinition  
      @@initialized=false
      @@ctx=AppContext.instance  
      # make sure we only do this once
      if !@@initialized
        @@ctx.register(:myname, someobject)
        @@ctx.flags[:myflag]=true
        
        @@initialized=true
      end
    end

Then whenever you need to inject a dependency, simply refer to it like this:

    AppContext.instance.myname
    
    if AppContext.instance.flags[:myflag] 
        # do stuff
    end

# License

This code is licensed under the expat license. See the LICENSE file for details.
