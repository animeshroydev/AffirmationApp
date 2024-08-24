Affirmation App
-------------
This App show image in a scrollable list.

Concepts Covered
-----------------
- Create model class Affirmation for image and string.
- Create data class DataSource for load all list of affirmation.
- Use of Column, Card.
- Using LazyColumn for showing scrollable list.

App Demo
---------
![ArtSpace](https://i.giphy.com/media/v1.Y2lkPTc5MGI3NjExdW9lZmdkcjE1aW9vN3QxdTYyNTB1cGV5ZzV4NHpqYTZ6aTQ5NGd4aCZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/6qP5Pl3tSSqDAX8N9D/giphy.gif)

Step by Step Guide
-------------------
1. Making sure all the image and string stored in the drawable and values -> string.xml respectively.
2. Create a model package and create a data class name Affirmation
```
package com.appmakerszone.affirmation.model

import androidx.annotation.DrawableRes
import androidx.annotation.StringRes

data class Affirmation(

    @StringRes
    val stringResourceId: Int,

    @DrawableRes
    val imageResourceId: Int
)
```
3. Create a package name data and define a loadAffirmations() function to load and return all the Affirmation item from resource.
```
package com.appmakerszone.affirmation.data

import com.appmakerszone.affirmation.R
import com.appmakerszone.affirmation.model.Affirmation

class DataSource() {
    fun loadAffirmations(): List<Affirmation> {
        return listOf<Affirmation>(
            Affirmation(R.string.affirmation1, R.drawable.image1),
            Affirmation(R.string.affirmation2, R.drawable.image2),
            Affirmation(R.string.affirmation3, R.drawable.image3),
            Affirmation(R.string.affirmation4, R.drawable.image4),
            Affirmation(R.string.affirmation5, R.drawable.image5),
            Affirmation(R.string.affirmation6, R.drawable.image6),
            Affirmation(R.string.affirmation7, R.drawable.image7),
            Affirmation(R.string.affirmation8, R.drawable.image8),
            Affirmation(R.string.affirmation9, R.drawable.image9),
            Affirmation(R.string.affirmation10, R.drawable.image10)
        )
    }

}
```
4. In MainActivity.kt, create a composable AffirmationCard to display single item of Affirmation.
```
@Composable
fun AffirmationCard(affirmation: Affirmation, modifier: Modifier = Modifier) {

    Card(modifier = modifier) {
        Column {
            Image(
                painter = painterResource(id = affirmation.imageResourceId),
                contentDescription = stringResource(id = affirmation.stringResourceId),
                modifier = Modifier
                    .fillMaxWidth()
                    .height(194.dp),
                contentScale = ContentScale.Crop
            )

            Text(
                text = LocalContext.current.getString(affirmation.stringResourceId),
                modifier = Modifier.padding(16.dp),
                style = MaterialTheme.typography.headlineSmall
            )

        }
    }

}
```
5. Preview this code with initial hardcoded text and image res id.
```
@Preview(showBackground = true, showSystemUi = true)
@Composable
private fun AffirmationCardPreview() {
    AffirmationCard(
        affirmation = Affirmation(
            stringResourceId = R.string.affirmation1,
            imageResourceId = R.drawable.image1
        ),
        modifier = Modifier.padding(10.dp)
    )
}
```
6. Create a AffirmationList composable function and use LazyColumn
- In Jetpack Compose, a scrollable list can be made using the LazyColumn composable. The difference between a LazyColumn and a Column is that a Column should be used when you have a small number of items to display, as Compose loads them all at once. A Column can only hold a predefined, or fixed, number of composables. A LazyColumn can add content on demand, which makes it good for long lists and particularly when the length of the list is unknown. A LazyColumn also provides scrolling by default, without additional code. Declare a LazyColumn composable inside of the AffirmationList() function. Pass the modifier object as an argument to the LazyColumn.
- In the lambda body of the LazyColumn, call the items() method, and pass in the affirmationList. The items() method is how you add items to the LazyColumn. 
- A call to the items() method requires a lambda function. In that function, specify a parameter of affirmation that represents one affirmation item from the affirmationList.
```
@Composable
fun AffirmationList(affirmationList: List<Affirmation>, modifier: Modifier = Modifier) {
    LazyColumn(modifier = modifier) {
        items(affirmationList) { affirmation ->
            AffirmationCard(
                affirmation = affirmation,
                modifier = Modifier.padding(8.dp)
            )
        }
    }
}
```
7. If you want, you can preview this too.
```
@Preview(showBackground = true, showSystemUi = true)
@Composable
private fun AffirmationAppPreview() {
    AffirmationsApp()
}
```
8. Finally create AffirmationsApp composable and call AffirmationList, pass DataSource().loadAffirmations() as parameter.
```
@Composable
fun AffirmationsApp() {
    val layoutDirection = LocalLayoutDirection.current
    Surface(
        modifier = Modifier
            .fillMaxSize()
            .statusBarsPadding()
            .padding(
                start = WindowInsets.safeDrawing
                    .asPaddingValues()
                    .calculateStartPadding(layoutDirection),
                end = WindowInsets.safeDrawing
                    .asPaddingValues()
                    .calculateEndPadding(layoutDirection),
            ),
    ) {
        AffirmationList(affirmationList = DataSource().loadAffirmations())
    }
}
```
9. Call in the onCreate, setContent
```
class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContent {
            AffirmationTheme {
                AffirmationsApp()
            }
        }
    }
}
```
Wollah! Run the app now...
