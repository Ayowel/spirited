## Screen-based usage

It's possible to add Spirited effects to a screen like any other screen
object with the keyword `spirited`. Note that if more than one image is
added to the effect, each particle will use a random one.

Create a simple 'mystical' effect.


{% include gif.html name="example_simple_81f0dd3e" %}

```py
image mystic_particle:
    "#fff"
    xysize (8, 8) alpha 0.3

screen example_spirited_sample():
    spirited:
        image "mystic_particle"
        # Go up, direction in degrees
        direction (80, 100)
```

Make particles avoid the cursor.


{% include gif.html name="example_cursor_interaction_c66c75f7" %}

```py
image red_particle:
    "#d44"
    xysize (45, 45) alpha 0.7

screen example_spirited_cursor():
    # Cursor-fearing spirits
    spirited:
        image "red_particle"
        # Move slowly
        speed (5, 30)
        # Configure how hard particles should be pushed back
        repulsor_strength 400
        # Configure how far particles should be to be affected
        repulsor_radius 300
```

Many parameters may be used to customize the particle's behavior for a
specific scene.


{% include gif.html name="example_rain_70d51079" %}

```py
image rain_particle:
    "#5656b8"
    xysize (7, 10) alpha 0.6

screen example_spirited_rain():
    # Make it rain at the center of the screen
    spirited:
        image "rain_particle"
        # Have rain only in the middle of the screen
        xpos 0.3 xsize 0.3
        # Go up, direction in degrees
        direction (-100, -80)
        # Make particles spawn above the screen and immediately appear at 100% opacity
        spawn_box (0, -100, 0, -config.screen_height)
        fadein 0
        # Ensure rain particles are deleted once they are below the screen
        bounding_box (None, None, None, 0)
        # Spawn 500 particles per seconds, limit their total count to avoid lags on smaller configurations
        renewal_rate 500
        maximum_pool 1300
        # Make particles fall fast to emulate rain
        # and die quickly so that some despawn while still on screen.
        speed (500, 800)
        ttl (0.3, 5)
```

## Image-based usage

Spirited may also be used to initialize an image by creating a new object
instance.

Basic 'wind' effect.


{% include gif.html name="example_image_simple_0a705ec9" %}

```py
image particle_wind:
    "#8f8"
    alpha 0.3 xysize (10, 7)

image spirited simple = Spirited(
    sprite_list = ["particle_wind"],
    direction = (-10, 10), # Go to the right, direction is in degrees
    spawn_box = (-config.screen_width, 0, 0, 0) # Start spawning at the left of the screen
    )

label spirited_example_image_simple:
    show spirited simple
    "Carefull, wind is blowing eastward"
    hide spirited simple with dissolve
    return
```

Multiple instances may be used to produce more complex effects.


{% include gif.html name="example_image_multi_cba1ef52" %}

```py
image particle_up:
    "#f88"
    alpha 0.7 xysize (10, 10)

image particle_down:
    "#88f"
    alpha 0.7 xysize (10, 10)

image spirited_up = Spirited(
    sprite_list = ["particle_up"],
    direction = 90, # Reds go up, direction is in degrees
    )
image spirited_down = Spirited(
    sprite_list = ["particle_down"],
    direction = -90, # Blues go down, direction is in degrees
    )

label spirited_example_image_multi:
    show spirited_up
    show spirited_down
    "Hot air goes up, Cold air goes down"
    hide spirited_up
    hide spirited_down
    with dissolve
    return
```

Create advanced effects by using the guideline or the spawn_guideline.
This example uses the spawn_guideline to make particles appear around the cursor


{% include gif.html name="example_spawn_guideline_7269da3d" %}

```py
init python:
    def cursor_spawn(sprite, st):
        # Relocate particles in a circle around the cursor
        import math
        import random
        effect_radius = 50
        radius = random.uniform(0, effect_radius)
        angle = random.uniform(0, 2 * math.pi)

        pos = renpy.get_mouse_pos()
        sprite.sprite.x = math.cos(angle) * radius + pos[0]
        sprite.sprite.y = math.sin(angle) * radius + pos[1]

image particle_light:
    "#fff"
    alpha 0.5 xysize (10, 10)

image spirited cursor = Spirited(
    sprite_list = ["particle_light"],
    # Go down slowly
    direction = (-100, -80),
    speed = (20, 60),
    # Use a custom spwn rule
    spawn_guideline = cursor_spawn,
    # Configure how and how long the particles are visible
    ttl = (0.5, 1),
    fadein = 0, fadeout = 0.3,
    # Configure how particles are generated
    initial_count = 0, renewal_rate = 50,
    )

label spirited_example_cursor_effect:
    show spirited cursor
    "Magic at the tip of your cursor."
    hide spirited cursor with dissolve
    return
```
