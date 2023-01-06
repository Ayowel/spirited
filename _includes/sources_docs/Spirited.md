## Spirited

This class provides rendering for mostly-linear effects
such as "mystic" particles, rain, or snow.

### Arguments

Tuple arguments may be written as a single value and will be implicitly expanded.
Tuple arguments with two values should be interpreted as ranges with a minimum and a maximum value.

* `sprite_list` **<[Displayable]>**
    An array of images to use as sprites

* `renewal_rate` **\<number>**
    On average, how many sprites should be generated per second while the minimum rate is not reached

* `initial_count` **\<number>**
    How many sprites should be generated at the start

* `minimum_pool` **\<number>**
    Minimum number of sprites that must exist at the same time

* `maximum_pool` **\<number>**
    Maximum number of sprites that may exist at the same time

* `speed` **<(number, number)>**
    How slow/fast a sprite may move

* `direction` **<(number, number)>**
    Valid direction angle for a sprite (in radians)

* `roll` **<(number, number)>**
    How far from its base direction line a sprite may "wobble"

* `ttl` **<(number, number)>**
    How long a sprite may live (in seconds)

* `fadein` **<(number, number)>**
    The time it should take for a sprite to reach 100% opacity as it appears (in seconds)
  *  This time IS part of the sprite's lifetime (see `ttl`)

* `fadeout` **<(number, number)>**
    The time it should take for a sprite to reach 0% opacity as it disappears (in seconds)
  *  This time IS NOT part of the sprite's lifetime (see `ttl`)

* `bounding_box` **<(number, number, number, number)>**
    If != None, border limits beyond which a sprite WILL be deleted before its lifespan expires
  * The tuple's values affect the borders in the following order: (left, top, right, bottom)
  * Positive values move the border right or down, negative values move it left or up
  * The calculation is performed relative to the top left corner of the sprites

* `spawn_box` **<(number, number, number, number)>**
    The border limits within which a particle may be created
  * The tuple's values affect the borders in the following order: (left, top, right, bottom)
  * Positive values move the border right or down, negative values move it left or up
  * The calculation is performed relative to the top left corner of the particle sprites

* `repulsor_strength` **\<number>**
    How fast sprites should run away from the mouse' cursor

* `repulsor_radius` **\<number>**
    How far the mouse's position affects sprites

* `repulsor_hardness` **\<number>**
    How strong the repulsor is at the max distance compared to on the cursor (as a multiplicator)

* `repulsor_mode` **\<number>**
  *  0 to have a simple repulsor
  *  1 to have a tornado around the cursor
  *  Other values are unsupported

* `alpha_levels` **\<int>**
    How many transparency levels to use when fading a sprite in/out

* `guideline` **\<function>**
    A custom function that takes five parameters and handles the displacement of a sprite:
  *  param1: A SpiritedSpriteInfo instance. Update param1.sprite.x and param1.sprite.y to set its position.
  *  param2: The time ellapsed since the Spirited displayable was first shown.
  *  param3: The time ellapsed since the last update in milliseconds.
  *  param4: A tuple that contains the displacement calculated based on Spirited's parameters.
            This displacement must be part of the tuple returned by the function to be applied to the sprite.
  *  param5: A tuple that contains the displacement that would be caused by the mouse's cursor's position.
            This displacement must be part of the tuple returned by the function to be applied to the sprite.

* `spawn_guideline` **\<function>**
    A custom function called as soon as a new sprite is created
  * param1: A SpiritedSpriteInfo instance.
  * param2: The time ellapsed since the Spirited displayable was first shown.