---
title: Actions Pattern
date: "2014-11-19"
template: "post"
draft: false
slug: "/posts/2014/actions-pattern/"

tags:
- "c-sharp"
- "programming"
- "development"
description: "It's a terrible name, but maybe one day I'll figure a better one.  Either way..."
---
It's a terrible name, but maybe one day I'll figure a better one.  Either way...

Recently we started a new large scale project that is being built in ASP.NET MVC working side-by-side with an Umbraco installation.  It got me thinking about the best way to approach the back-end code structure.

Initially we decided on a modular approach, but "modular" is a pretty vague term and wasn't very easy to clearly define.  So it soon ended up with some God-classes full of various functions that did a whole lot of things and no clear separation.  It was clear to see that this was going to get out of hand very quickly.

The problem brought me back a method I described in a [previous post](/blog/2013/04/alternative-to-entity-framework-and-the-repository-pattern/).  It basically involves having a base designator that defines a class as one that does something, one thing, it has a specific purpose.  The class is given a logical name that simply defines its purpose.  These classes only require one thing, an `Execute` method.  That's all that it must have, the parameters and return types can vary as need-be.

In this current project I have called this pattern the Actions Pattern.  There is a base interface `IAction` that has no fields or method descriptors, it's just a basic designator.  I then use a DI container (Autofac in this instance) to find all classes that implement `IAction` and register them.

From there throughout the system I can get an action and execute it.

It's a fairly loose pattern in that the `Execute` function can be defined as needed, but I feel it allows for the greatest flexibility, but still gives a basic outline on how things should be done.

There are instances where one class may contain multiple `Execute` methods, but the only viable case for this is when the two (or more) methods do the same thing but with varying parameters.

Now for an example...

    namespace MyApp
    {
        public interface IAction { }
    }

    namespace MyApp.Authentication
    {
        public class AuthenticateUser : IAction
        {
            #region Constructor

            public AuthenticateUser()
            {

            }

            #endregion

            #region Public Methods

            public Guid Execute(string userName, string password)
            {
                // perform authentication logic here
            }

            #endregion
        }
    }

    namespace MyApp.Web.Controllers
    {
        public AuthController : Controller
        {
            public ActionResult Login()
            {
                return View();
            }

            public ActionResult Login(string userName, string password)
            {
                var userId = GetAction<MyApp.Authentication.AuthenticateUser>().Execute(userName, password);

                Session["user"] = userId;

                return Redirect("/");
            }

            T GetAction<T>()
                where T : IAction
            {
                return DependencyResolver.Current.GetService<T>();
            }
        }
    }