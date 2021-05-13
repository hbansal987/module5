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
3. **Code Explain** </br>
Hello Hello

[comment]: <GM: console - "The referenced script (Unknown) on this Behaviour is missing!" Also - drop the script into the inspector window rather than the hierarchy window? Do they both work the same?>

4. Attach the `CameraController` script to the main camera by dragging and dropping the script to the `Main Camera` object in the _hierarchy window_. And then in the _inspector window_ set the `Target` of the script to our character, `ModularCharacterBase`, under the Assets list **In the hierarchy window!**. 

[comment]: <GM: what do you mean by zooming the camera in and out?>

5. Go ahead and click on Play and try zooming the camera in and out. Also notice that the Camera object now follows our character as it moves. **The zoom in and zoom out is done by the mouse scroll wheel.!**
