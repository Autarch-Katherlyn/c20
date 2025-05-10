---
title: render_model
stub: false
about: 'tag:h3/render_model'
---
The render_model tag contains the markers and visual geometry for [objects](~object) such as [vehicles](~vehicle), [scenery](~), [bipeds](~biped), and [weapons](~weapon) among others. It is not collideable nor animated on its own, and objects may reference additional [collision_model](~), [physics_model](~), and [model_animation_graph](~) tags. This tag supports regions, permutations, damage states, and shaders. Render models have a maximum vertex limit of 32,767 per region.

# Shaders
Each part of a model can reference a different [shader](~), like the Warthog's windscreen uses a glass.shader while its body uses an exterior.shader. Shaders can various properties and settings as well as different material types which affects how projectiles and other things interact with them. Some parts of a model use a [shader_decal](~) which is used for stickers, decals, and similar types of textures with transparent backgrounds.

# Nodes
Nodes can be thought of as the model's "skeleton" and can be animated to move parts of the model. Each vertex can be influenced by up to 2 nodes. Nodes are also known as bones.

# Markers
Markers are simple named points with orientation attached to a model. Think of them as hardpoints. Since they are parented by nodes, they can be animated. Markers can be used for a variety of purposes, such as attaching objects together, both through model attachments such as a Scorpion turret or with scripts (e.g. Pelicans carrying Warthogs), attaching widgets like [antenna](~), or firing [projectiles](~projectile) from in the case of weapons. You can view object markers with `render_model_markers 1`.

This tag only contains the marker data but other tags usually determine how they are used. However, certain marker names have special behaviour in-engine:

* `head`:
  * Determines where AI look at when scripted to talk to another character.
  * Base location for the friendly indicator in multiplayer.
  * Used as a ray origin when testing if AI can see their enemy.
* `primary_trigger`: Where a weapon's primary trigger projectiles and effects come from. See also the [_projectiles use weapon origin_ field](~weapon#tag-field-triggers-flags-projectiles-use-weapon-origin).
* `secondary_trigger`: As above, for secondary triggers (second trigger slot).
* `body`
* `front`: Possibly used to used to see if you're facing a [device_control](~), if present.
* `ground_point`: Determines the resting point for [items](~item).
* `left_hand`: Used during the grenade throwing animation.
* `melee`: Where melee damage comes from here. If not present, the engine picks an unknown default location.
* `hover_thrusters`:
  * When used on a vehicle with "alien scout" or "alien fighter" [vehicle physics type](~vehicle#tag-field-vehicle-type), spawns [an effect](~vehicle#tag-field-effect) when the vehicle is hovering close to the ground. This can be seen at a piloted Banshee's wingtips when sitting on the ground.
  * When the vehicle physics type is "human plane", creates a similar dust effect if the marker is pointed at nearby ground. Used for the Pelican's thrusters.
* `jet_thrusters`: Can also be used for vehicles with "human plane" physics to create the Pelican's thruster dust effect.

Commonly used marker names without hard-coded behaviour include:

* `primary_ejection`: Used to indicate where casings fly out when firing the primary trigger.

# Regions
Regions are named sections of the model which can have multiple [permutations](#permutations). There is a maximum of 16 regions. Region names are used by the engine to relate parts of the render model with the [collision model](~collision_model). For example, a Flood combat form losing an arm or damaging the Wraith's wings.

Regions render in the order they are stored in the tag. When naming regions, consider that they will be sorted by name when compiled into the `.render_model`. This can be important for [skyboxes](~skyboxes#regions) and objects with multiple layers of alpha-blended transparent shaders need a correct sorting order to be explicitly defined otherwise they won't look right.

# Permutations
A permutation is a variation of a [region](#regions) that can be randomly selected. There is a maximum of 128 permutations per region. They are often used to give [bipeds](~biped) visual variety.

# Damage State
A damage state is what is visually shown when an object is damaged. Halo 3 supports 4 damage states; minor, medium, major, and destroyed. You can specify what permutation you want to be used as the appearance in the [model](~). Most models name the permutation to match the corresponding damage state.

# Level of detail
  Unlike Halo CE and Halo 2, Halo 3 does not use levels of detail (LoDs) models.
