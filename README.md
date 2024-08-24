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