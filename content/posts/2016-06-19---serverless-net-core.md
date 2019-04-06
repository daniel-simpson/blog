---
title: Serverless .NET Core
date: "2016-06-19"
template: "post"
draft: false
slug: "/posts/2016/serverless-net-core/"
category: "Technology"
tags:
- "serverless"
- "coreclr"
- ".net"
- "csharp"
description: "I have been playing around a lot with AWS Lambda lately, writing most of my functions in Javascript.  It made me wonder what other languages/platforms would be well suited to such an environment.  Javascript works well because it's lightweight and flexible.  Lambda has the option for Java but has some performance issues due to the spinup time of the JVM."
---
I have been playing around a lot with AWS Lambda lately, writing most of my functions in Javascript.  It made me wonder what other languages/platforms would be well suited to such an environment.  Javascript works well because it's lightweight and flexible.  Lambda has the option for Java but has some performance issues due to the spinup time of the JVM.

When Microsoft announced .NET Core they said that it was meant to be a lightweight runtime where most features were "opt-in", making the connection between this and the serverless infrastructure seemed like a natural progression.

I spent the morning prototyping this.  It turns out that in conjunction with Docker it actually seems quite feasible.

These where the questions I faced.  Some of them remain unsolved.

1. How do you execute arbitrary code?
2. Do I use the Rosyln library to compile code on the fly?
3. What about external library references? – This is extra important given the fact that .NET Core depends heavily on NuGet packages.
4. How do you package up the code for deployment to where it will be executed?
5. Where will the code actually be executed?
6. How do I control execution capping it at a set runtime duration?
7. How does data get passed into the function being executed?
8. How does the function return data to the caller?
9. How do the functions _actually_ get called?
10. If using Docker, where are the images stored?
11. How are Docker images distributed between servers that execute them?
12. How do you handle multiple functions?
13. How do you keep spin-up times to a minimum?

I opted for using pre-compiled assemblies instead of dynamic compilation of C# code via Roslyn.  This gets bootstrapped by a simple module I built that handles passing information into the function, logging, etc...

To deploy a function one simply creates a git repository which triggers a Docker image build on each push.

Execution is proxied through nginx which spins up the associated Docker image.

It's all in prototype phase at the moment but it's definitely something I plan on pursuing further.

A basic function looks like this.

    using Microsoft.Extensions.Logging;

    namespace TestFn
    {
        public class EntryPoint
        {
            readonly ILogger _log;

            public EntryPoint(ILoggerFactory loggerFactory)
            {
                _log = loggerFactory.CreateLogger<EntryPoint>();
            }

            public void Run(string param)
            {
                _log.LogInformation("Hello from TestFn!");
                _log.LogInformation($"Input: {param}");
            }
        }
    }