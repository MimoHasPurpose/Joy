Notes taken while making this project:
- basic setup:
	- In this project, we will make 3 independent scenes: 	Player, Mob, and HUD, which we will combine into the game's Main scene.

	- In a larger project, it might be useful to create folders to hold the various scenes and their scripts, but for this relatively small game, you can save your scenes and scripts in the project's root folder, identified by res://. You can see your project folders in the FileSystem dock in the lower left corner:


	- Creating the player scene

	- With the project settings in place, we can start working on the player-controlled character.

	- The first scene will define the Player object. One of the benefits of creating a separate Player scene is that we can test it separately, even before we've created other parts of the game.

- coding the player:

we'll add player movement, animation, and set it up to detect collisions.

To do so, we need to add some functionality that we can't get from a built-in node, so we'll add a script. Click the Player node and click the "Attach Script" button:

Using the export keyword on the first variable speed allows us to set its value in the Inspector. This can be handy for values that you want to be able to adjust just like a node's built-in properties. Click on the Player node and you'll see the property now appears in the Inspector in a new section with the name of the script. Remember, if you change the value here, it will override the value written in the script.


Now we can use the _process() function to define what the player will do. _process() is called every frame, so we'll use it to update elements of our game, which we expect will change often. For the player, we need to do the following:

    Check for input.

    Move in the given direction.

    Play the appropriate animation.



\$ is shorthand for get_node(). So in the code above, $AnimatedSprite2D.play() is the same as get_node("AnimatedSprite2D").play().

In GDScript, \$ returns the node at the relative path from the current node, or returns null if the node is not found. Since AnimatedSprite2D is a child of the current node, we can use $AnimatedSprite2D.
`
Now that we have a movement direction, we can update the player's position. We can also use clamp() to prevent it from leaving the screen. Clamping a value means restricting it to a given range. Add the following to the bottom of the _process function (make sure it's not indented under the else):



Preparing for collisions:

We want Player to detect when it's hit by an enemy, but we haven't made any enemies yet! That's OK, because we're going to use Godot's signal functionality to make it work.

Add the following at the top of the script. If you're using GDScript, add it after extends Area2D. If you're using C#, add it after public partial class Player : Area2D:



This defines a custom signal called "hit" that we will have our player emit (send out) when it collides with an enemy. We will use Area2D to detect the collision. Select the Player node and click the "Node" tab next to the Inspector tab to see the list of signals the player can emit: