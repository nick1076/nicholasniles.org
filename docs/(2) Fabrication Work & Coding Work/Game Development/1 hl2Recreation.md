# Half-Life 2: Recreation In the Unity Engine

| Title | Description |
| ----------- | ------------------------------------ |
| Engine | Unity (2D & 3D) |
| Language(s) | C# |
| Project Time Duration | 6 Months (Late July of 2021 - Late December of 2021) |
| Status: | Unfinished, no plans to do so |
| Help? | None, developed entirely solo |

# *A mixture of 2D and 3D in one with a full inventory, entity, and damage system all inspired and or based on half-life 2*

<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/n9U_csy2UpQ" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</center>

This game was heavily inspired by Half-Life 2, which is one of my favorite games of all time. I am obsessed with the Half-Life universe that Valve developed, and have played all of the games in the series, including Half-Life Alyx. I was so inspired I decided to attempt to recreate HL2.

# Early Origins of this Project

The game originally began as my own custom physics simulator early on. I started by attempting to make doors that were fully simulated and physics based in Unity along with a basic character controller. Note also that the original game was ripped assets from my Cartoon Cat game, which is were the character controller as well as the textures came from this early on:

<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/785TAzjWHBE?start=33" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</center>

I made it so that the door was locked until the player pushed on it by hitting left click, and then the door became simulated. It also was able to rip off it's hinges if you pushed it too far in one direction. Past this, I further devloped the physics and also introducted the first NPC into the game, that being Half-Life 2's Civil Protection. I also implimented custom gravity and some fun objects to mess around and throw around with this new system:

<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/oPbrWdEJGKg" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</center>

After this, I moved away from the physics simulation idea and more towards the Half-Life recreation idea, adding AI nodes, AI behavior states, as well as the inventory and some items to the game. I also began developing the first official map (shown later in the video), being the initial Point Insertion train station map from Half-Life 2:

<center>
![Image title](../(0)%20ASSETS/9mm.png){ align=center } ![Image title](../(0)%20ASSETS/stun.png){ align=center }
</center>

<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/TGERqA29ndE" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</center>

# Complex Artifical Intelegence

While it may not seem like it, this project had incredibly complex Artifical Intelegence which I had developed. It involved multiple states (such as wonder, chase, stationary, etc.) which were enums in the code that when changed immedietly and dynamically changed the behavior of the NPC. Additionally, the Metrocop NPC, when you walk into them, depending on how many times you have done so recently (within a small time frame) will equip their stun sticks, warn you verbally, and even hit you if you provoke them too many times. This is showcased a later video. Also in this new video, I implimented the voicelines from Half-Life 2, added them to the AI, and also further developed the map and sound design:

<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/m5QMomiTY4I" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</center>

# Texture Process

In the game, you can see that all the textures are low-res looking, and this is done intentially. I purposefully would take a normal scale texture and compress it to something like 128 x 128 to fit the style:

<center>
<figure markdown>
  ![Image title](../(0)%20ASSETS/dirt1.jpg){ align=center }
  <figcaption>Pre-Compressed Dirt Texture</figcaption>
</figure>

<figure markdown>
  ![Image title](../(0)%20ASSETS/metal2.jpg){ align=center }
  <figcaption>Pre-Compressed Wall (Concrete) Texture</figcaption>
</figure>

<figure markdown>
  ![Image title](../(0)%20ASSETS/wood1.jpg){ align=center }
  <figcaption>Pre-Compressed Door (Wooden) Texture</figcaption>
</figure>
</center>

All of the above look incredibly detailed, which they are in the game files, then, as I said, they get heavily compressed to give it a more pixelated style.

# Why 2D and 3D, and not just one?

One major challenge I always face when developing 3D games (Hence why Proelium, my biggest project, is in 2D) is developing 3D models. I have never developed much of a skill for devloping video game assets in a 3D environment, but I am very skilled and have many hours developing pixel art, using the program Aseprite, as you can see below:

<center>
![](../(0)%20ASSETS/aseprite.jpg)
</center>

But, all Half-Life games are 3D! Knowing I coudln't 3D model, could make spritework, but needed to make a 3D game, I decided to do a mix of the two. I ended up drawing the sprites for the characters in 2D and having them face the player to give them a 3D look. I achieved this affect in a very strange way. I made it so that each character in the game had 4 sprites, one for each direction, and based on which side of the character the player would be viewing the character, I would change the sprite renderer of that character to the correct directional sprite as well as make it face the player. This feature was incredibly difficult to program as it required many weird Quaternion calculations, but eventually I got it working. Here is some of the artwork and how I drew these directional sprites:

<center>
![](../(0)%20ASSETS/cp.png)
</center>

I also had planned on implimenting the Half-Life 2 citizen as an NPC in the game, had drawn his sprite, but never got around to actually implimenting it. Here is the concept artwork for the civilian:

<center>
![](../(0)%20ASSETS/civ.png)
</center>

Essentially, the spritesheet would be ripped apart in Unity into the 4 seperate sprites and as I mentioned before would be displayed accordingly. One other major issue arose from this design choice, however, that being how items would be represented in the hands of the NPCs based on direction, because otherwise the item in the NPC's hand would always be in the same position facing the player regardless of direction.

# Giving NPCs Items

To fix this, I painstakingly added in a Vector 3 position as well as a Quaternion rotation for each direction for each character and for each item that could be held by that character. This took forever but was most certainly needed for the game to flow well.

# Moving Towards a Complete Version

I then upgraded the in-game lighting, added many more item, fleshed out the level, added more cutscenes, and even more. This was a huge content update, and I themed the video I made to showcase said update as an almost trailer-like video:

<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/n9U_csy2UpQ" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</center>

As mentioned earlier, the "provoking" of the metrocop NPC is shown in the video above.

# Further Development

Past this, I didn't devlop the project much further. I did however do a bit more development, including the implimentation of the AR-2 from Half-Life (which unfortunately looks like a nerf gun), as well as some visual improvements:

<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/FG6jFZu25_4" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</center>

In this video you can also see another major improvement to the AI, that being that a player carying contriband items (Contriband as shown by the red marks in the item's slot in the inventory) will cause the metro cop NPCs to react differently depending on the level of contriband. Low level contriband, such as the Metro Polce ID item will cause them to walk towards you and attempt to arrest if you are seen carrying it out, but heavy contriband (such as the 9mm or AR2) will cause the NPCs to draw their weapons and immedietly fire at you. 

<center>
<figure markdown>
  ![Image title](../(0)%20ASSETS/ar2.png){ align=center }
  <figcaption>Extreme Contriband</figcaption>
</figure>

<figure markdown>
  ![Image title](../(0)%20ASSETS/keycard.png){ align=center }
  <figcaption>Normal Tier Contriband</figcaption>
</figure>
</center>

After this update/video, development unfortunately ends.