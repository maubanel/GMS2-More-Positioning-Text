<img src="https://via.placeholder.com/1000x4/45D7CA/45D7CA" alt="drawing" height="4px"/>

### Screen Positioning I

<sub>[home](../README.md#user-content-gms2-screen-positioning) • [next](../)</sub>

<img src="https://via.placeholder.com/1000x4/45D7CA/45D7CA" alt="drawing" height="4px"/>

Lets take a closer look at how we position text, objects and other items on screen.

<br>

---


##### `Step 1.`\|`MTP`|:small_blue_diamond:

So why does `draw_text(room_width * .5, line_height, "Message");` draw to the screen in the location that it does?  What is `x` and what is `y`?  What does `room_width` represent?

Lets look at this is some detail.  We are positioning objects on the screen using the [cartesian coordinate system](https://en.wikipedia.org/wiki/Cartesian_coordinate_system).

You have most likely seen this in school, it is a two axis representation of an two dimensional area with an x-axis that runs East/West and a y-axis that runs North/South. 
	
The intersection of the two axis is point (0,0).  The X axis is positive towards the right and the Y axis is positive upwards.

![Illustratoin of cartesian coordinate system](images/CartesianCoordinateSytem.gif)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 2.`\|`FHIU`|:small_blue_diamond: :small_blue_diamond: 

To position points we move along the **X** & **Y** axis.  So for position *(2, -2)* we go two positions to the right on the x axis (away from (0,0)) and two positions down on the y axis.  For point *(-2, 4)* we go two to the left on the x axis and four upwards in y.  So they end up here.

![Putting two points in cartesian coordinate system](images/TwoPointsOnCartesianPlane.gif)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 3.`\|`MTP`|:small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

**GameMaker** is slightly different.  First point *(0,0)* is at the top left corner of the room.  **Y** is positive going down and *negative* moving **upwards**. So the quadrant that the room is in is all x-axis positive and y-axis positive.  Moving downscreen is also y positive.  The top right corner of the room is the *(0, room_width)*. The bottom left corner is *(0, room_height)* and the bottom right is *(room_width, room_height)*.  The top center is *(room_width/2, 0)*.  The middle center is *(room_width/2, room_height/2)*.  

![GameMaker coordinate system](images/GameMakerCartesianPlanA.gif)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 4.`\|`MTP`|:small_blue_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

Create a new room called `rm_position_objects` and place it at the top of the **Room Order** list.

![add room called rm_position_objects and place at top of room order](images/positionObjectsRoom.gif)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 5.`\|`MTP`| :small_orange_diamond:

Open the room **rm_position_objects**. We do not use hard coded numbers for the room height and width.  That way we can change the size of the room and our game will still work.  If you go to the room you will see the **Width** and **Height** and these are the same values stored in `room_width` and `room_height`.

![alt_text](images/ScreenPos.png)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 6.`\|`MTP`| :small_orange_diamond: :small_blue_diamond:

Right click on **Objects** and select **Create | Object** called `obj_position_objects`. Add a **Draw | Draw** event to draw to screen.

![add object obj_position_objects and add a draw event](images/positionObjectsObject.gif)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 7.`\|`MTP`| :small_orange_diamond: :small_blue_diamond: :small_blue_diamond:

Press the <kbd>Variable Definitions</kbd> button and then press the <kbd>Add</kbd> button.  **Name** the variable `line_height` and set the **Default** to `22`.  Change the **Type** to `integer`.

![add a variable called line_height of type integer set to 22](images/AddLineHeight.gif)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 8.`\|`MTP`| :small_orange_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

Now add to the **Draw** script:

* Center align text
* Draw a title in the middle of the screen
* Reset text alignment

![draw title](images/Script.gif)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 9.`\|`MTP`| :small_orange_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

Add a **obj_position_objects** to **rm_position_objects**.  Now *press* the <kbd>Play</kbd> button in the top menu bar to launch the game. See the title in the center of the screen.

![add obj_object_positions to room and run game](images/AddToRoomRun.gif)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 10.`\|`MTP`| :large_blue_diamond:

So if we want to draw a line underneath, then we can figure out 2 steps of 22 pixels down on the y-axis.  This gets us to `44` pixels down on the y axis. The x-axis would go from `0` to `room_width -1` to draw a line right across the screen.

Why `room_width - 1`? This is because the first pixel on the left is accessed with unit `0` so a the last pixel is the width of the room minus one pixel (as 0 is one). 

![alt_text](images/lineTitlePlacement.png)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 11.`\|`MTP`| :large_blue_diamond: :small_blue_diamond: 

Let's use **[draw_line(x1, y1, x2, y2)](https://manual.yoyogames.com/#t=GameMaker_Language%2FGML_Reference%2FDrawing%2FBasic_Forms%2Fdraw_line.htm)**. `(x1, y1)` is the start of the line, and `(x2, y2)` is the end of the line. We are also going to use **[draw_set_color(color)](https://manual.yoyogames.com/GameMaker_Language/GML_Reference/Drawing/Colour_And_Alpha/draw_set_colour.htm)**.  We will pass as an argument to this function the *enumerator* `c_yellow`.  We will reset the color back to white after drawing the line.  Type the following to the bottom of the **obj_data_types_controller Draw Event**.

![Adds line under title](images/drawLine.png)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>


##### `Step 12.`\|`MTP`| :large_blue_diamond: :small_blue_diamond: :small_blue_diamond: 

Now *press* the <kbd>Play</kbd> button in the top menu bar to launch the game. We should see a yellow line under the text.

![line uynder title in game](images/lineUnderTitle.png)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 13.`\|`MTP`| :large_blue_diamond: :small_blue_diamond: :small_blue_diamond:  :small_blue_diamond: 

Lets look at placing 2-D sprites, something more game-y, into this two dimensional room.  We will put a red triangle, blue square and green circle on line 25 from the far left, center and right respectively.  We want it to look like: 

![Concept art for 3 new objects we will add](images/ConceptArtForPlacement.png)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 14.`\|`MTP`| :large_blue_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:  :small_blue_diamond: 

![alt_text](images/.png)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 15.`\|`MTP`| :large_blue_diamond: :small_orange_diamond: 

![alt_text](images/.png)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 16.`\|`MTP`| :large_blue_diamond: :small_orange_diamond:   :small_blue_diamond: 

![alt_text](images/.png)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 17.`\|`MTP`| :large_blue_diamond: :small_orange_diamond: :small_blue_diamond: :small_blue_diamond:

![alt_text](images/.png)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 18.`\|`MTP`| :large_blue_diamond: :small_orange_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

![alt_text](images/.png)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 19.`\|`MTP`| :large_blue_diamond: :small_orange_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

![alt_text](images/.png)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 20.`\|`MTP`| :large_blue_diamond: :large_blue_diamond:

![alt_text](images/.png)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 21.`\|`MTP`| :large_blue_diamond: :large_blue_diamond: :small_blue_diamond:

![alt_text](images/.png)

___


<img src="https://via.placeholder.com/1000x4/dba81a/dba81a" alt="drawing" height="4px" alt = ""/>

<img src="https://via.placeholder.com/1000x100/45D7CA/000000/?text=Next Up - ADD NEXT TMTPE">

<img src="https://via.placeholder.com/1000x4/dba81a/dba81a" alt="drawing" height="4px" alt = ""/>

| [home](../README.md#user-content-gms2-screen-positioning) | [next](../)|
|---|---|

