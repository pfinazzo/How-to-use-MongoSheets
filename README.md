# How to use MongoSheet 
#### for non-programmers who want to use Google Sheets to manipulate data (CRUD operations) on mLab

- Figured this would be a good thing for agile development teams, letting non programmers with access to a google sheet to seed an mlab database

- special note for programmers: my use of "", a.k.a. quotation marks in this tutorial are not meant to mean a JavaScript String, they are used the same as they are in plain english

___
## Requirements 
* a Database hosted on [mLab](mlab.com)
* Google Chrome
* a google account to save [Google Sheets](https://www.google.com/sheets/about/)
*  Knowledge of JavaScript O.O.P and MongoDB is helpful but not absolutely necessary

You will need to know the difference between an array and an object

Technically an Array is a type of object but for our purposes an array is data held between the characters [ ], and an object is data held between the the characters { }

## Install MongoSheet as a Chrome Extension

* Navigate to [this site](https://chrome.google.com/webstore/detail/mongosheet/malanmbliiillkcjmedoacklhhemhfhk) and download the MongoSheet chrome extension by clicking the install button near the top right corner of the screen

## Connect a blank spreadsheet to the database
* Open up a blank google sheet in [Google Sheets](https://www.google.com/sheets/about/)

![Imgur](https://i.imgur.com/3DiqC2S.png)

* In the toolbar at the top click on the option "Add-ons"
* Select MongoSheet and click Open

![img](https://i.imgur.com/HeawW2C.png)

* You will notice a sidebar opens on the left hand side, this will be the interface you use to connect your spreadsheet to your database and then perform operations on your spreadsheet and database

![](https://imgur.com/cpabsZ0.png)

* Open up a new tab (command + T) and navigate to your [mLab](mlab.com) and sign into your account

* Once you have signed in, find the link in the top right corner that has your username and click on it

![img](https://i.imgur.com/9y19F70.png)

* Scroll down until you find your API key 

* Highlight the API key and copy it to your clipboard (Mac OS = command + C, Windows = Control + C)

![img](https://i.imgur.com/USMF30F.png)

* Once you have copied your key to your clipboard, you must enable the mLab Data API by simply clicking "Enable Data API access"

![img](https://i.imgur.com/wMcVxyR.png)

* you will notice when it has been clicked the status will say "Data API access: Enabled" and the button will switch to saying "Disable Data API access"

![img](https://i.imgur.com/OCqliJR.png)

* Once you have enabled the data API access you can now use MongoSheet to connect using the api key you copied beforehand

* Go back to MongoSheet and click the button at the top that says API key

![](https://i.imgur.com/JIbStMR.png)

* A form will pop up asking for the key, paste in the key (Mac OS = command + v, Windows = Control + V), and click "ADD"

![img](https://i.imgur.com/e7nMA1p.png)

Now that MongoSheet has connected to your mLab, the next step is to connect to the database. 

* Click the button that says "Connect to DB"

![img](https://i.imgur.com/3umidPm.png)

* This will navigate you to a page where you can choose a database and subsequently you can choose the collection you want to pull data from in whichever database you have chosen. For this step I find it best to choose a collection that has the most amount of references and/or embedding of arrays and other objects. Its best to make the top level model pull the data first because its easier to see which columns will need to be references to seperate spreadsheets. After you choose a collection hit the "Connect" button.

![img](https://i.imgur.com/1aDme6a.png)

![img](https://i.imgur.com/jGNKCPQ.png)

Congratulations you have now connected your database to MongoSheet
___

## Pulling data from mLab into your first spreadsheet

___

* You will notice that after you hit the Connect button earlier, the mongosheet page is naviagated to a new page with Create, Read, Update and Delete buttons. 

Welcome to the new way to perform CRUD operations, this will be your homebase for all manipulation of data through the spreadsheet

___

* Before you can pull the data from your database the spreadsheet needs to be set up correctly so that it may parse the data correctly.

* First you must name the spreadsheet at the bottom with EXACTLY the same name as the collection you connected to. Casing is important. I am connected to a collection named "products", so I will name my first spreadsheet as "products" as well. To rename a spreadsheet, simply right click on the name towards the bottom of the page and click "Rename".  

![img](https://i.imgur.com/Im1P1zO.png)

* The next thing you will want to do is name each of your keys in your top level collection as the names of each column in the spreadsheet, in my case I have attached to product model the following keys:(Image: String, Labels: Array, History: Array, Reviews: Array, Name: String, Category: String, Brand: reference, Venue: reference, Description: String, Weight: String, Price: Number, Rating: Number, Popularity: Number, Ingredients: String, ID: Number, UPC: String, Current: Boolean) Keep in mind I will be using dummy data just to show how mongosheet works. 

![](https://i.imgur.com/b90YtzS.png)

* WAIT... you may have noticed there is a odd column name at the far left of my spreadsheet named "_id.$oid". 

* _id is an automatically assigned object when an object is created in MongoDB and $oid is a key on this object that contains the string that mongodb automatically assigns for identification purposes.

* Once you have all of your columns named EXACTLY as your keys are in the collection, press the "READ" button in the far right in MongoSheet

* This should pull all the data in to your spreadsheet, it will tell you if there is an error in the bottom right hand corner of the webpage

## Linking Objects to Separate Spreadsheets

* In my case both "brand" and "venue" are embedded objects in the "products" collection

* Use the + button in the bottom left corner of the page to add a new spreadsheet (this will be our "brand" object spreadsheet)

* Rename the spreadsheet to the EXACT name of the column in your spreadsheet (the exact key in your top level collection)

* Again, name each column in this spreadsheet EXACTLY as the corresponding embedded objects keys, and again you will need to add _id.$oid as the first column just like you did with the main.

* Now click the three lines in the top left corner of the mongosheet interface

![](https://i.imgur.com/JOdaw3I.png)

* select "Spreadsheet Operations"

![](https://i.imgur.com/0tpY5D8.png)

* It will take you to this page

![](https://i.imgur.com/uK6YGhk.png)

* Click the "Fill Data" button

![](https://i.imgur.com/eREFVqS.png)

* Now there will be a menu asking for a "source sheet". The source sheet will be the parent sheet that the object is embedded on, a.k.a. the first sheet we made, so for me that sheet is "products"

* now click the "Fill Data" button again. This button will fill your spreadsheet with the appropriate data. If the names of the colums and the spreadsheet dont align perfectly  with their corresponding keys or if "_id.$oid" is not the name of the first column it will not come up

It should now look like this
![](https://i.imgur.com/t9FHh8J.png)

Almost done!

* Now we just have to link the data in the original first spreadsheet

* Navigate to the first spreadsheet, for me this is "products"

* Highlight the cells that contain the embedded objects we are about to link

![](https://i.imgur.com/0USzPlV.png)

image of highlighted cells

* Now click the "Link Data" button and select "Link As Object"

* this will create a reference for each object selected to its corresponding object in the second sheet grabbing by its _id.$oid

it should now look like this

![](https://i.imgur.com/Jw6ma8j.png)

## Linking Arrays to Separate Spreadsheets

* Linking Arrays to separate spreadsheets is a slightly different process. Because Objects have an _id object containing a $oid key with a string that is unique, they can be referenced in the parent spreadsheet (in this case 'products') by referencing this string. Arrays do not have this object embedded, and therefore, they need to be referenced by their row in the parent spreadsheet. To do this we will make a new column in the parent sheet ('products') and we will name it '$rowID'. 

![](https://i.imgur.com/MJIeu9z.png)

* now we need to make each cell fill with text that is the result of an internal google sheets function

* Just like in the JavaScript String prototype methods we can use a function called "concat" to concatenate two different strings together

* In any cell in the $rowId column type the following: =CONCAT("row",row()) 

![](https://i.imgur.com/Ss0kkXn.png)

* add this function to every cell in the $rowID column

* Now do the same process as creating an object reference, create a new spreadsheet by clicking the + at the bottom left, then right click the name at the bottom of the spreadsheet and click "Rename" to rename it to the EXACT name of the key that holds the array, a.k.a. the name of the column storing the arrays in the parent spreadsheet ('products')

* Add a column with $rowID to the new spreadsheet

* This tutorial will use the 'labels' arrays as an example

![](https://i.imgur.com/t9FHh8J.png)

* Just like we did with Objects, press "Fill Data" to bring up the menu where you will select the parent sheet to pull data from (in my case 'products') and then simply click "Fill Data" again and MongoSheet will automatically fill the data

![](https://i.imgur.com/t9FHh8J.png)

* As you can see when it organizes by row it makes each element a new line in the new table even if its on the same row

Almost there!

* Now you can head back to the parent spreadsheet ('products') 

* On the parent spreadsheet, highlight all cells containing data in the column with the name of the data your linking (in my case 'labels')

![](https://i.imgur.com/7meg86L.png)

* Now click the "Link Data" button in MongoSheet to create refernces to the arrays in the other spreadsheet

![](https://i.imgur.com/K6Mwxlt.png)

Congratulations, your arrays are now linked as a separate spreadsheet


## Creating (Seeding) Data in MongoSheet

To create data we will need to click the icon with three horizontal lines in the top left corner of MongoSheet again and navigate back to the Database Operations page

* For testing purposes I will create a duplicate of an existing product

* To create a new object in in your collection first fill in all the fields besides _id.$oid 

![](https://i.imgur.com/8sXR67E.png)

* Once all the fields are set to the values you wish them to be, click the 3 little dots under the "Create" button

![](https://i.imgur.com/twivls8.png)

* This will take you to a page where you specify which rows you are trying to add

* For me this row ranges from 9-9 because I'm only adding one product on row 9 so my page looks like this:

![](https://i.imgur.com/IwkVOlB.png)

* Type in the correct rows and click the "Save" button

* You will see a _id.$oid become automatically generated and if you check your mLab, you will see a new entry into your collection

![](https://i.imgur.com/uTMKwnp.png)

Congratulations you just created data through Google Sheets!

## Updating Data on MongoSheet

* This process is very similar to the process of creating data

* First go ahead an edit the contents of the cell

* I will be editing my image string in my last product from 'image' to 'image2'

![](https://i.imgur.com/lkvc7ti.png)

*  Now click on the 3 dots below the "Update" Button in your mongosheet interface
![](https://i.imgur.com/8qMwyUj.png)
Which will bring you here:

![](https://i.imgur.com/gqnZLm0.png)
* Choose the range of rows you have updated and hit "Save"

* Finally, hit the "Update" button and your database will be updated

![](https://i.imgur.com/Xe5vXqB.png)



## Deleting data

This step is exactly the same as Updating data.

* Click the 3 dots below the "Delete" button

![](https://i.imgur.com/iZf9X6S.png)


* Specify the row range to delete

![](https://i.imgur.com/cLaOtqG.png)

* Hit "Save" and then hit the delete button, which will perform the Delete operation on your database

![](https://i.imgur.com/jN4rwly.png)

Note: This will delete it from your database but not your spreadsheet, you will have to delete the row from the spreadsheet manually

___

Congratulations! You now are able to perform full CRUD operations on your database through MongoSheet!









