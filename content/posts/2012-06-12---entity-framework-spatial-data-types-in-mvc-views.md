---
title: Spatial data types in Entity Framework and MVC
date: "2012-06-12"
template: "post"
draft: false
slug: "/posts/2012/entity-framework-spatial-data-types-in-mvc-views/"

tags:
- ".net"
- "mvc"
- "entity framework"
- "spatial"
description: "I was slapped with another funny one with Entity Framework and MVC today.  I wanted to access a System.Data.Spatial.DbGeography part of the Entity Framework in one of my views.  But I kept getting the error saying that DbGeography was in an assembly that wasn't referenced."
---
I was slapped with another funny one with Entity Framework and MVC today.  I wanted to access a `System.Data.Spatial.DbGeography` part of the Entity Framework in one of my views.  But I kept getting the error saying that `DbGeography` was in an assembly that wasn't referenced.

This was the error, to be precise.

    Compiler Error Message: CS0012: The type 'System.Data.Spatial.DbGeography' is defined in an assembly that is not referenced. You must add a reference to assembly 'System.Data.Entity, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089'.

It took me a little while to figure it out since I knew I had that assembly referenced in my project.

The solution was to add this to the `~/Views/Web.config` (and any `Web.config` under any areas that may also utilise this)


    <compilation debug="true" targetFramework="4.0">
      <assemblies>
        <add assembly="System.Data.Entity, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"/>
      </assemblies>
    </compilation>

Easy as pie.