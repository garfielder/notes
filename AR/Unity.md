
## Unity 3D

Introduction <br>
https://docs.unity3d.com/Manual/PrimitiveObjects.html

Tutorial <br>

https://unity3d.com/cn/learn/tutorials

API<br>

https://docs.unity3d.com/ScriptReference/Application.LoadLevel.html


## Tips
### Material 

Create Material : assets --> create --> material <br>
To assign material to a gameobject, just drag the material in the assets in Project view into the object

### texture 
Method one: <Br>
   1. Create a subdirectory with name "textures". optional. 
   2. right click 'texture`, select 'import New asset', unfortunatly, only one texture can be loaded onetime. 

### Script

Load a scence 
```c#
using UnityEngine;
using UnityEngine.SceneManagement;

public class ExampleClass : MonoBehaviour {
    void Start () {
        // Only specifying the sceneName or sceneBuildIndex will load the scene with the Single mode
        SceneManager.LoadScene ("OtherSceneName", LoadSceneMode.Additive);
    }
}
```
https://docs.unity3d.com/ScriptReference/SceneManagement.SceneManager.LoadScene.html


Mouse and Keyboard

```c#
void Update() {
        if (Input.GetMouseButtonDown(0))
            Debug.Log("Pressed left click.");
        
        if (Input.GetMouseButtonDown(1))
            Debug.Log("Pressed right click.");
        

        
    }
```
