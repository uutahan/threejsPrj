I will try to explain the code here.
-So first of all we need to get mouse position in 3d when mouse wheel event occurs.
-First we ge mouse position on screen with: event.clientX, but this is not according to our canvas. 
-We modify it slightly. (When mouse hovering above left-top corner of canvas our point should be (0,0) ).
-Then we make this point between -1,1. So now its in our near frustrum.
-Then we use unproject to get a vector looking to the world from our camera. But it is according to world coordinates. Lets call it x.
-Then we substract our camera's position from our vector x. Then we normalize it. 
-Now we have a vector that looks to our world from our camera according to the mouse position. Call it y.
-Next we need to find how much we need to add vector y to our camera's position to find our 3d position in world.
-We calculate distance and we add that much.

-We have a virtual sphere for trackball controls, every manipulation(dolly,zoom,pan) done through manipulating this sphere, for zooming we need to manipulate its radius.
-Then we need to get our virtual shpere's prev radius and current radius(radius gets updated when wheel event occurs),
-We set our target(where we look at) to mouse3D position when wheeling.
-How much we will set our target is according to prevRadius/current radius ratio. if its 1(same), we dont change it. (Basically we interpolate between mouse3D pos and our current target.)

-We do similar things for orthogonal camera too. But we change zoom of camera this time instead of radius of our virtual sphere.

-To solve scrolling issue inside our canvas, we listen for mouse enter event, when it enters the canvas,
-we add css class to our body element using dom manipulation, this class prevent scrolling.
-when mouse goes outside of the canvas (mouse out event), we remove our css class from body and make it scrollable again.
