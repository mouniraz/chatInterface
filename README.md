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

3) definir la classe data Message
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

## Mise en forme du layouts avec le Modifier 
1) ajout d un padding autour de chaque ligne message
```kotlin
fun MessageCard(message: Message) {
    
    Row(modifier=Modifier.padding(all=8.dp)) 
    ........
    
 2) Mise en fore de l´image (taille, clip)
 
 Image(painter = painterResource(id = R.drawable.profile),
            contentDescription ="Profile image",
        modifier=Modifier.size(40.dp)
            .clip(shape= CircleShape),

            )
  ```
  3) ajouter un espace vertical entre les texts
  ```kotlin
   Column(){
            Text(text = message.author)
            Spacer(modifier = Modifier.height(4.dp))
            Text(text = message.body)

        }
   ```
   4) ajouter un espace horizontal 
```kotlin
Image(painter = painterResource(id = R.drawable.profile),
            contentDescription ="Profile image",
        modifier=Modifier.size(40.dp)
            .clip(shape= CircleShape),

            )
        Spacer(modifier = Modifier.width(8.dp))
  ```
## Material Design
utiliser le theme par defaut créé au nom de l´application   
![default Theme](https://github.com/mouniraz/chatInterface/blob/main/themepng.png)   
1) changer les couleurs
```kotlin
Image(painter = painterResource(id = R.drawable.profile),
            contentDescription ="Profile image",
        modifier=Modifier.size(40.dp)
            .clip(shape= CircleShape)
            .border(1.5.dp, MaterialTheme.colors.secondary, CircleShape)

        )
        Spacer(modifier = Modifier.width(8.dp))

        Column(){
            Text(text = message.author,
                color = MaterialTheme.colors.secondaryVariant
            )
```
         
2) changer les typographies 

```kotlin
 Column(){
            Text(text = message.author,
                color = MaterialTheme.colors.secondaryVariant,
                style = MaterialTheme.typography.subtitle2

            )
            Spacer(modifier = Modifier.height(4.dp))
            Text(text = message.body,
                style = MaterialTheme.typography.body2

            )
  ```
  3)formes
  ```kotlin
  Surface(shape = MaterialTheme.shapes.medium, elevation = 1.dp) {
                Text(
                    text = message.body,
                    modifier = Modifier.padding(all = 4.dp),
                    style = MaterialTheme.typography.body2
                )
            }
  ```
  
## Listes de messages
1)definir une fonction qui affiche une listes de messages 
```kotlin 
@Composable
fun Conversation(messages: List<Message>) {
    LazyColumn {
        items(messages) { message ->
            MessageCard(message)
        }
    }
}
```
2) importer une listes de messages
iporter cette liste dans un fichier kt dans le projet [sampleData](https://gist.github.com/yrezgui/26a1060d67bf0ec2a73fa12695166436)

