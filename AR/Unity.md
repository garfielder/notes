
## Unity 3D

Introduction <br>
https://docs.unity3d.com/Manual/PrimitiveObjects.html

Tutorial <br>

https://unity3d.com/cn/learn/tutorials

API<br>

https://docs.unity3d.com/ScriptReference/Application.LoadLevel.html


## Tips
### Material 

Create Material : assets --> create --> material

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
