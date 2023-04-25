---
title: Choosing A Game Engine
date: '2023-04-18'
cover: img/choosing-game-engines.webp
description: >-
  Choosing a game engine for your first game or new prototype can be difficult
  and if wrong can waste time. In this post we compare two of the major engines
  from a existing C# developer's perspective.
---


Choosing a game engine for your first game or new prototype can be difficult and if wrong can waste time. As someone who has experience in C# we will be focusing on two major game engines that have good support for C# and these are Unity and Godot. In this post we will be analysing both the benefits and disadvantages of each engine in the context of developing a prototype or first game.

## Unity

Unity is a game engine that was first released in 2005, it supports multiple platforms and is one of the most popular game engines used today. The editor works on Windows, MacOS, and Linux with support for Apple Silicon.

Unity has the advantage of being a very mature platform with a proven track record, this also extends to resources with there being an endless number of resources for Unity. The editor is also fairly easy to use and the asset store allows for a vast number of assets to be obtained that would help with creating a prototype fast.

Unity also has great support for C#, with it being the primary language used for scripting and IDEs like JetBrains Rider having extension support to make development even easier.

These benefits do come at a cost though with free plan having a splash screen and the Plus version being $399 per seat, which can be a lot of money for an indie game developer or someone who is releasing their first game.

## Godot

Godot is an Open-Source game engine that was first released in 2014, the editor runs on Windows, MacOS, Linux and BSD. Godot 4 has recently released and has many changes that make C# development a better experience such as using .NET 6.

Godot’s primary scripting language is GDScript which is pretty similar to Python and the internal IDE allows users to debug their GDScript code. C# is also supported for scripting but feels less polished than using GDScript, you can use the internal IDE or something like Rider which I would recommend.

One of the disadvantages of using Godot 4 is the lack of resources compared to Godot 3, these older resources can still be used but you will need to cross reference forums on the changes between 3 and 4.

## Which One?

Both Godot and Unity have their advantages and disadvantages which for Unity include the great number of resources and first-class C# support, and for Godot are it being open source and more lightweight.

Unity provides a much better developer experience for anyone using C# as Godot is not there yet with IDE extensions and you always have the feeling that GDScript would be a better choice in Godot.

On terms of price though Godot is free and open source which allows a first-time developer to publish a game without paying any fees or displaying a splash screen.

Unity has a greater number of resources and Godot currently has the issue of the resources being out of date due to the recent launch of Godot 4.

While Godot has a large number of resources, they are mostly for Godot 3 right now and need to be updated to be used without constantly referencing forums. This could change in the future when the resources are updated but right now Unity’s resources are much better for a first timer.

## Conclusion

For our next prototype game, we will be using Unity after experimenting with both Godot 4 and Unity, this is due to the quicker time for development with Unity and the better developer experience for C# developers. Feel free to let us know what your opinions on Unity and Godot are in the comments below.
