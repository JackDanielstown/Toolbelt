# Toolbelt
An extensible minimalist set of .Net utilities you can pick and mix as you need them, with "contracts" based on Fascias

The idea behind this project is that it gives you a set of small, almost self-contained utilities in a "toolbox".  When you start a project that uses some of these utilities, you create a toolbelt by picking exactly the utilities you need from your toolbox.

Why this approach?
------------------
When writing a utility library, there is an urge to make it into a "swiss army knife", containing everything you could possibly want.  This inevitable leads to bloat.  
An alternative approach is to split your library into many small sub-libraries.  However if you deliver your utilities as a set of compiled DLLs, you find the number of DLLs growing quickly, and this soon becomes unmanigable.
I have tried both of these approaches in the past and was never happy with either of them.

This project takes a slightly different approach.  It provides a set of utilities that can be put together in different configurations depending on the needs of the application, and then lets you build into a single Toolbelt DLL at application compile time with as little bloat as possible, as you have explicitly chosen what you want included.

The minimalist utilities
------------------------
I have attempted to ensure that, where possible, the utilities in the Toolbox require no third party DLLs.  Certainly that is the case with all Fallback implementations.  Where non-Fallback implementations are available and require third party software, this is made clear in their descriptions.  Obviously if you create your own implementations or extensions you can include whatever you like - but I would suggest keeping to thye spirit of this wherever possible

A note on the Fascias
---------------------
Fascias are one way of separating "contract" from "implementation".  Rather than use an interface for the contract, however, it uses an abstract static class: the "Fascia".  Fascia classes are defined to have an associated Interface and an associated Fallback implementation.  Calls to the Fascias methods are passed to an instance of the Interface contained in the Fascia to do the actual work.  By default, the implementation instance is an instance of the Fallback class, but the implementing instance can be changed to any class that implements the associated Interface.

All patterns have advantages and disadvantages.  A Fascia only permits one implementation of a contract at any one time.  This makes it much less flexible and powerful than approaches with interfaces and factories, or approaches involving Dependecy Injection (also know as Inversion of Control).  Personally, I like Dependency Injection for all sorts of reasons (it can be invaluable in unit testing for example, or when implementaions need to change on the fly) but Fascias have the redeeming feature that they are simple (though a bit tedious to code...).  This simplicity was what I was after.
