# Game - Cartoon Cat

## General Information

| Title | Description |
| ----------- | ------------------------------------ |
| Engine | Unity (3D) |
| Language(s) | C# |
| Project Time Duration | 2 Weeks (Early July of 2021 - Late July of 2021) |
| Status: | Published as Demo |
| Help? | None, developed entirely solo |

<center>
![Image title](../Assets/ss1.JPG)
</center>
<center>
![Image title](../Assets/ss2.JPG)
</center>
<center>
![Image title](../Assets/ss3.JPG)
</center>
<center>
![Image title](../Assets/ss4.JPG)
</center>


## Outcome & Analytics of Release

I ended up actually releasing this game on October 8th, 2022, about a year later than when I finished it. I decided to take this leap since I had nothing to lose and it would be better than simply keeping it to rot on my desktop. I ended up releasing it to itch.io (Popular distributer) and it ended up being a huge sucsess and taking off. Here is it's official store page:

<center>
<iframe frameborder="0" src="https://itch.io/embed/1135056?bg_color=000000&amp;fg_color=ffffff&amp;link_color=fa7f06&amp;border_color=ffffff" width="552" height="167"><a href="https://nick-niles.itch.io/cartoon-cat-demo">Cartoon Cat (DEMO) by Nick Niles</a></iframe>
</center>

Within the first day, 3 seperate YouTuber's ended up making a let's play/gameplay walkthrough of the entire game, and I was thrilled by this. Launch day with 0 marketing received around 79 views and 21 downloads, with day two continuing and even beating day 1. Here are some of the videos people made:

<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/4nXsLmyQIOg" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/ITi_NVnVlnM" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/Wy7Z8ZTDJ5c" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</center>

On top of the videos, on day one, I recieved a 5 star review and many wonderful comments. This all gave me both experience in releasing a game and taught me a few things that I could change for future releases. Since the game was considered to be a "demo" and the end of the game upon beating it told the player that a full release was in development, this demo release set me up for a later release of a full game.

## Other People's Thoughts, & Reviews on the Game

As mentioned, the game got a lot of attention. Here is a gallery of reviews, comments, feedback, and more of the game by people:

<center>
![Image title](../Assets/cc_r6.PNG){ align=center }
</center>
<center>
![Image title](../Assets/cc_r1.PNG){ align=center }
</center>
<center>
![Image title](../Assets/cc_r2.PNG){ align=center }
</center>
<center>
![Image title](../Assets/cc_r3.PNG){ align=center }
</center>
<center>
![Image title](../Assets/cc_r4.PNG){ align=center }
</center>
<center>
![Image title](../Assets/cc_r5.PNG){ align=center }
</center>

## Initial Development

As for the game's development, a lot of prototyping and testing went into it. As you see in the final game, the camera and textures are in a pixelated old play-station style of graphics, as well as the environment and props being low poly. Initially, all of this was the same except the camera was going to be clear:

<center>
![Image title](../Assets/cc_cameraNoFilter.PNG){ align=center }
</center>

The player also was originally going to be equiped with a gun, but this was later scrapped for a hammer, camera, and flashlight. I also ended up as I said moving towards a PS style camera filter.

## Making a Pixelated Play-Station Style Camera

Here is what the final effect looks like:

<center>
![Image title](../Assets/cc_filteredCamera.PNG){ align=center }
</center>

This is achieved in a rather complex way. I begin by giving the player a camera whose view of the world is constantly stored as a render texture. This texture is then compressed to 256x256 pixels:

<center>
![Image title](../Assets/cc_renderText.PNG){ align=center }
</center>

From here, this render texture is displayed on a 2D one-sided face in the game world:

<center>
![Image title](../Assets/cc_inWorldText.PNG){ align=center }
</center>

And a regular camera is placed in front of this to see this view. Also note that the user interface is overalayed on the final camera and not the one that goes to the render texture.

## Creating an Immersive AI

When you get to the end of the game, you are trapped in a maze with the Cartoon Cat himself, and he is given AI in order to correctly navigate said maze. This was done using some clever code in tandem with Unity's built-in NavMesh component/system. First, I set all of the floor and wall objects of the maze to be static objects via the ticker in the inspector. I then went to Window>AI>Navigation and baked the NavMesh for the entire level. Here is a visualization of said NavMesh for the maze level:

<center>
![Image title](../Assets/cc_navMesh.PNG){ align=center }
</center>

The blue represents valid positions for the AI to move upon. From here, I ended up adding a set of points to each intersection of hallways in the maze and a set of points for where the AI could choose to go next from the intersection they were currently at, it had a random chance to pick either of the connected directions to go in. 

<center>
![Image title](../Assets/cc_aiNodes.PNG){ align=center }
</center>

The cat would also, when it sees the player via a RayCast projected from it's head, would drop it's current target node and begin simply chasing the player while they were within 5 seconds of the most recent sighting. Here is some early development footage of this in action:

<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/TtikbjamvFU?start=19" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</center>

Of course, since there are no walls, you are practically always in range of him, but this demo video atleast showcases the cat's ability to follow the player and navigate around the map. The cat essentially uses a state machine of enums to determine his current behavior:

```
public enum AItypeData
{
    Patrol,
    Chase
};
```

These are changed based off the vision of the cat by simply assigning a new enum, and doing so will immedietly switch it's behavior via the Update() method:

```
if (currentaiType == AItypeData.Chase)
{
    nav.speed = 4.25f;
    if (nav != null)
    {
        nav.SetDestination(GameObject.FindWithTag("Player").transform.position);
    }
}
else
{
    nav.speed = 3.5f;
    if (movingToPoint == null)
    {
        movingToPoint = FindNearestPoint();
    }

    nav.SetDestination(movingToPoint.transform.position);
}
```

While the code for the cat, more expansive than this, isn't necisarilly complicated, it creates for a realistic feeling AI.

## Guiding the Player

When it comes to telling the player what do to or how to interact, it can be pretty complex. I went with the approach of a task list, which would display when you were assigned a task, when you had one active, and even when you completed a task. It was also accompanied by sound effects:

<center>
<figure markdown>
  ![Image title](../Assets/cc_taskList.PNG){ align=center }
  <figcaption>Task List in the Top Right Corner</figcaption>
</figure>
</center>

<center>
<figure markdown>
  ![Image title](../Assets/cc_newTask.PNG){ align=center }
  <figcaption>Displayed UI Element when a new Task is Assigned</figcaption>
</figure>
</center>

This helps the player not only avoid confusion but also keep track of what to do if there are multiple tasks, like later in the game:

<center>
<figure markdown>
  ![Image title](../Assets/cc_multiTask.PNG){ align=center }
  <figcaption>Example of Multiple Tasks in the Top Right</figcaption>
</figure>
</center>

Additional ways of assisting the player are floating in-world indicators. I used these throughout the game to distinguish to the player what are props and what are actual interactable objects. There are two types, camera and eye icons. The camera icon indicates that the player needs to take a photograph using the Camera item of the given area:

<center>
![Image title](../Assets/cc_cameraIcon.PNG){ align=center }
</center>

And secondly the eye icon indicates that the object needs to be interacted with because it is readable/grabbable:

<center>
<figure markdown>
  ![Image title](../Assets/cc_eyeIcon.PNG){ align=center }
  <figcaption>Example of a Grabbable Eye Icon Object</figcaption>
</figure>
</center>

<center>
<figure markdown>
  ![Image title](../Assets/cc_readable.PNG){ align=center }
  <figcaption>Example of a Readable Eye Icon Object</figcaption>
</figure>
</center>

## Telling a Story through a Game

When it comes to horror games, it helps build suspense and create a sense of realism when the world is set in a realistic/good story environment. I went about telling a story in my game in a couple of ways.

### Visual Story Telling

Throughout the game, the environment tells the most of the story, and it also connects with readable story elements throughout the game too. For example, in the first newspaper, found on the hood of a police car, talks about the police officer and his purpose of being here, which is reinforced by his abandoned police car found outside when you first start the game:

<center>
![Image title](../Assets/cc_ve1.PNG){ align=center }
</center>

And there are many more elements that tell the story and tie in with other storytelling elements:

<center>
![Image title](../Assets/cc_ve2.PNG){ align=center }
</center>
<center>
![Image title](../Assets/cc_ve3.PNG){ align=center }
</center>
<center>
![Image title](../Assets/cc_maze_ve1.PNG){ align=center }
</center>
<center>
![Image title](../Assets/cc_maze_ve2.PNG){ align=center }
</center>
<center>
![Image title](../Assets/cc_maze_ve3.PNG){ align=center }
</center>

### Text-Based/Straight Forward Story Telling

Throughout the game, the player finds News Papers that are the heavy lifters of the story telling. They include a date, allowing the player to piece together a timeline of events, and they also tell the story of what happened.

<center>
![Image title](../Assets/cc_np1.PNG){ align=center }
</center>
<center>
![Image title](../Assets/cc_maze_np1.PNG){ align=center }
</center>
<center>
![Image title](../Assets/cc_maze_np2.PNG){ align=center }
</center>
<center>
![Image title](../Assets/cc_maze_np3.PNG){ align=center }
</center>

### Dialouge Story Telling/Assistance

Additionally, a dialouge system, where text is displayed at the bottom of the player's screen, is also used. This helps guide the player if they don't understand something and also helps build the story.

<center>
![Image title](../Assets/cc_d1.PNG){ align=center }
</center>

## Future Plans

As of writing this, I just released the game 2 days ago. Depending on how it's release continues and how many people are interested, I'll likely make a full release version of the game in the near future, and if I do so, I'll update this page to reflect that.