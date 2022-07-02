---
title: 'Creating Terra Ball for Metroidvania Month 16'
description: In which me and a friend create a stupidly difficult platformer
date: 2022-07-02T00:00:00Z
---

![Cover Image for Terra Ball](/assets/images/posts/terra-ball-cover.png#article-centered "Title")

Metroidvania Month 16 is a popular game jam on Itch.io that pushes participants to create a metroidvania-style game
within the somewhat limited timespan of _one month_. However, for me and my friend, that timespan was closer to three days.
A deadly combination of college finals and plain 'ol procrastination left us with only a bare-bones project with the
clock rapidly ticking down. Over the next few days, we were really forced to crunch to get our project over the line.

Our game was written in Love2D, a Lua framework that gives all the basic tools needed to throw together a game, along
with an engine that can take advantage of cool optimizations like LuaJIT and work across all platforms. The downside of
using this framework, however, was that we needed to build the more advanced elements (like tile-mapping, animations, and input control)
by ourselves. There were third-party scripts that could accomplish these tasks, but incorporating them into our project seamlessly
ended up being somewhat of an issue. For example, the library we used for loading in our tile-map did not mesh well with
the library we used to facilitate our ECS (entity-component-system) architecture.

To work around this, we actually didn't put the individual tiles into the ECS world, but instead put the entire map
in as one entity, then used a separate system to draw the entire thing to the screen in one big batch. However, since
the default draw function would render the map on a separate canvas without respecting the camera transformations, we chose
to use the layer render function instead, which respected any graphical transformations to the default canvas. Luckily for us,
the tile-mapping framework we used also had integrations for the physics plugin, so registering the map with the physics
world was surprisingly easy.

The code to draw the tileset ended up being surprising simple for how much time we spent figuring it out:
```lua
function mapDrawSystem:drawWithCamera(e)
	e.tileset:drawTileLayer(e.tileset.layers["Cave"])
end
```

This was just one of many problems we had to solve in order to get the game out the door. Honestly, I'm surprised we
were able to finish it in time! Even though it was far from perfect, it was a great learning experience, and that
experience with Love2D would come in handy when completing my second game jam project, [Silent Star](https://triangle-land.itch.io/silent-star). But that deserves
a whole separate blog post!

_You can play Terra Ball [here](https://penquin22.itch.io/terra-ball)._