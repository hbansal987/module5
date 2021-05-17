---
title: Third-person camera controller - part 2
slug: third-person-camera-controller-part-2
description: Let's write a script for your camera which will follow our main character as it walks. The camera will also be able to zoom in and zoom out.
isPublicLesson: true
---

## Third-person camera controller - part 2

1. Let's now make a C# script for our camera to follow the character as it moves. Go to the `Script` folder in the _project window_,  right-click and select `Create > C# Script` and name it  `CameraController`.
2. Copy and paste this code into the `CameraController.cs` file.

```csharp
//using namespaces
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class CameraController : MonoBehaviour
{
    public GameObject target;// reference to the target Object (so we can look at it when we are in normal play mode (not customizing))
    public float zoomSpeed = 700;// // speed of zooming the camera in or out
//using the LateUpdate() event method which is called after the Update() event method
    void LateUpdate()
    {
//transform.LookAt() method is used to rotate a game object so that its forward vector points at another point
        transform.LookAt(target.transform); // look at the target
    var mouseScroll = Input.GetAxis("Mouse ScrollWheel");//// check how much mouse was scrolled (use for camera zooming)
  

    if (mouseScroll != 0)// if mouseScroll value is not equal to 0
    {
        transform.Translate(transform.forward * mouseScroll * zoomSpeed * Time.deltaTime, Space.Self);//// zoom the camera in or out
    }
}
}
```
3. **Code Explain!** </br>
**Objective!** </br>
The script is for your camera which will follow our main character as it walks. The camera will also be able to zoom in and zoom out. </br>
**Start!** </br>
We use a Gameobject variable named "target" to tell our camera the object it has to follow. In our case, the camera is following the main character (as it is 3rd person view game).!! </br>
Also the zoom speed is set. This can also be changed from the inspector window as it is set to public. Setting a variable as public helps us to access it from outside this particular script. We can access it from other scripts and it can also be accessed directly from our Unity Inspector window. We do not particullarly need CameraController.cs script to access a public variable. !!</br>
**Update!**</br>
The late update function is called after the simple update function is called. This means it is called after the player has moved. Just like the simple Update function it is called every frame. It helps to order the execution of the script. The primary functions like movement of player should be in the update function and called first. We need to move the camera after the movement of the player so we use the LateUpdate function. !!</br>
Firstly using the LookAt function we change the camera position to face towards the position of the target. The forward vector is rotated to in such a way that it is placed towards our taget. The upwards vector points in the World Up direction. Only the direction of the forward vector is changed. !!</br> 
Then at every instance we get the value of the scroll button of the mouse. If the value is non zero (we have move the scroll of the mouse) then we change the camera translation. This gives the effect of zooming in and zooming out. Transform.forward gets the z component (blue axis). We multiply it with the scroll value, predefined zoom speed and the time frame interval. Hence we zoom in and zoom out in the forward direction (blue axis). As our camera moves in the forward direction and we have and orthographic view for our scene. We tend to see things enlargerd (as our camera is closed to them) or smaller (as our camera is far from them). This causes the zooming effect in our game. !! </br>
**Conclusion!** </br>
So basically our camera follows the target (our main character). To continue the flow of the proecess the movemnet of the camera is after the movement of the target. We can change the foward and backward position of the camera to make it zoom in and zoom out respectively. 

[comment]: <GM: console - "The referenced script (Unknown) on this Behaviour is missing!" Also - drop the script into the inspector window rather than the hierarchy window? Do they both work the same?>

4. Attach the `CameraController` script to the main camera by dragging and dropping the script to the `Main Camera` object in the _hierarchy window_. And then in the _inspector window_ set the `Target` of the script to our character, `ModularCharacterBase`, under the Assets list **In the hierarchy window!**. 

[comment]: <GM: what do you mean by zooming the camera in and out?>

5. Go ahead and click on Play and try zooming the camera in and out. Also notice that the Camera object now follows our character as it moves. **The zoom in and zoom out is done by the mouse scroll wheel.!**
