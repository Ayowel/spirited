## SpiritedSpriteInfo

This class is a container for Ren'Py-native sprite objects.

This should only be necessary when creating a custom guideline.

### Attributes

Attributes with "(from `attribute`)" are calculated based on attributes
provided to `Spirited` at its instanciation. Need to add attributes for
your guideline ? Prefix `gl_` or `guideline_` to their name. We will
never use such attribute names when updating SpiritedSpriteInfo.

* `sprite`
    The Ren'Py particle object. Its x and y attributes must be updated
    to make particles move
* `cycle`
    In which life phase the particle is
  * `0` Particle is appearing
  * `1` Particle is at 100% opacity
  * `2` Particle is disappearing
* `speed` (from `speed`)
    How fast the sprite moves (in pixel/second)
* `direction` (from `direction`)
    The sprite's direction angle (in radians)
* `roll` (from `roll`)
    How far from the direction's line the sprite may roll (in pixels)
* `opacity`
    The current particle opacity level if it's appearing or disappearing
* `duration` (from `ttl`)
    How long this particle will stay before disappearing
* `birth_time`
    The time this particle was birthed (relative to Spirited's time)
* `fadein`
    (from `fadein`) The time the particle takes to become visible
* `fadeout`
    (from `fadeout`) The time the particle takes to become invisible and die
* `roll_offset`
    Internal variable used by Spirited to ensure that particles rolling are not synced
* `rid`
    Internal variable used by Spirited to track which image should be used