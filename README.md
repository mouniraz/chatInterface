# chatInterface
## Création du nouveau projet compose avec Android Studio  
creer un nouveau projet **Empty Compose Activity**  

![New project](https://github.com/mouniraz/chatInterface/blob/main/Capture.png)  

## Fonction Composable 
1) ajouter un text dans l'interface principale  
```kotlin
class MainActivity : ComponentActivity() {     
    override fun onCreate(savedInstanceState: Bundle?) {        
        super.onCreate(savedInstanceState)     
        setContent {        
                 Text("Android")        
        }       
    } }
 ``` 
 2) definir une fonction composable **
 ```kotlin
 @Composable
fun MessageCard(name: String) {
    Text(text = "Hello $name!")
}
```
  
 3) faire appel à cette fonction dans la fonction onCreate
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
## Preview Android Studio  
Pour voir le preview de votre code avant execution ajouter l'annotaion @Preview á la fonction DefaultPreview
```kotlin
@Preview
@Composable
fun DefaultPreview() {
    ChatInterfaceTheme {
        MessageCard("Android")
    }
}
```
## Les Layouts
Pour utiliser plusieurs compose dans l´interface graphique, il faut définir un layout pour organiser le compose (utiliser Row ou Column)  
1) ajouter un layout Column pour placer les 2 text
```kotlin 
@Composable
fun MessageCard(name: String) {

    Column(){
        Text(text = "Hello $name!")
        Text(text = "Hello $name!")

    }
}
```
2) ajouter une image dans un layout row 

```kotlin

@Composable
fun MessageCard(name: String) {
    Row() {
        Image(painter = painterResource(id = R.drawable.profile), 
            contentDescription ="Profile image" )
        Column(){
            Text(text = "Hello $name!")
            Text(text = "Hello $name!")

        }
    }

}
```

3) definir la classe data Message
```kotlin
data class Message(val author: String, val body: String)
```
4) redefinir MessageCard  
```kotlin 

@Composable
fun MessageCard(message: Message) {
    Row() {
        Image(painter = painterResource(id = R.drawable.profile),
            contentDescription ="Profile image" )
        Column(){
            Text(text = message.author)
            Text(text = message.body)

        }
    }

}
```



