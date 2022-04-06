# chatInterface
## Création du nouveau projet compose avec Android Studio  
creer un nouveau projet **Empty Compose Activity**  

![New project](https://github.com/mouniraz/chatInterface/blob/main/Capture.png)  

## Fonction Composable 
**1) ajouter un text dans l'interface principale  
```kotlin
class MainActivity : ComponentActivity() {     
    override fun onCreate(savedInstanceState: Bundle?) {        
        super.onCreate(savedInstanceState)     
        setContent {        
                 Text("Android")        
        }       
    } }
 ``` 
 **2) definir une fonction composable **
 ```kotlin
 @Composable
fun MessageCard(name: String) {
    Text(text = "Hello $name!")
}
```
  
 **3) faire appel à cette fonction dans la fonction onCreate
```kotlin
class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContent {
                 MessageCard("Android")
        }
    }
}
```



