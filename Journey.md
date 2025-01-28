# Database Project

### Example given:

    - Create an user, a recipe, ingredientRecipe, ingredient and comment
    - Define each of these tables and make so that we can connect to a C# code
    - Test and debug all the way until it's good enough and no errors

---

## IMPORTANT DETAILS:

### user:

    - email
    - name
    - vegetarian
    - age
    - country
    - USERID - PK

### recipe

    - name
    - description
    - category
    - difficulty
    - USERID - FK
    - RECIPEID - PK

### ingredientInRecipe

    - quantity
    - unit
    - RECIPEID - FK #1
    - INGREDIENTID - FK #2
    - ingredientInRecipe - PK

### ingredient

    - name
    - group
    - INGREDIENTID - PK

### comment

    - content
    - date
    - USERID - FK #1
    - RECIPEID - FK #2
    - COMMENTID - PK

So now all that the things have been defined, we need to create the database, and after the respective tables;

w

---

# Creation

### database

```SQL
CREATE DATABASE RUMOS

use RUMOS
GO
--- just making said database
```

### tables

> since SQL has user as a reserved keyword i'll be using Users like António from my class

```SQL 
CREATE TABLE Users (
    UserID UNIQUEIDENTIFIER PRIMARY KEY DEFAULT NEWID(),
    Email VARCHAR(255) NOT NULL,
    Name VARCHAR(255) NOT NULL,
    Veggie BIT NOT NULL,
    Age INT NOT NULL,
    Country VARCHAR(255) NOT NULL,
    Password VARCHAR(255) NOT NULL
);

CREATE TABLE Recipe (
    RecipeID UNIQUEIDENTIFIER PRIMARY KEY DEFAULT NEWID(),
    UserID UNIQUEIDENTIFIER NOT NULL,
    Name VARCHAR(255) NOT NULL,
    Description VARCHAR(255) NOT NULL,
    Category VARCHAR(255) NOT NULL,
    Difficulty INT NOT NULL,
    Duration INT NOT NULL, -- in minutes
    Country VARCHAR(255) NOT NULL,
    CONSTRAINT FK_RECIPE_USER FOREIGN KEY (UserID) REFERENCES Users(UserID)
);

CREATE TABLE Ingredient (
    IngredientID UNIQUEIDENTIFIER PRIMARY KEY DEFAULT NEWID(),
    Name VARCHAR(255) NOT NULL,
    GroupFood VARCHAR(255) NOT NULL -- Removed trailing comma
);

CREATE TABLE IngredientRecipe (
    RecipeID UNIQUEIDENTIFIER NOT NULL,
    IngredientID UNIQUEIDENTIFIER NOT NULL,
    Quantity INT NOT NULL,
    Unit VARCHAR(100) NOT NULL,
    CONSTRAINT PK_IngredientRecipe PRIMARY KEY (RecipeID, IngredientID),
    CONSTRAINT FK_IngredientRecipe_Recipe FOREIGN KEY (RecipeID) REFERENCES Recipe(RecipeID),
    CONSTRAINT FK_IngredientRecipe_Ingredient FOREIGN KEY (IngredientID) REFERENCES Ingredient(IngredientID)
);

CREATE TABLE Comment (
    CommentID UNIQUEIDENTIFIER PRIMARY KEY DEFAULT NEWID(),
    UserID UNIQUEIDENTIFIER NOT NULL,
    RecipeID UNIQUEIDENTIFIER NOT NULL,
    Content VARCHAR(255) NOT NULL,
    DateComment DATETIME NOT NULL DEFAULT GETDATE(),
    CONSTRAINT FK_Comment_User FOREIGN KEY (UserID) REFERENCES Users(UserID),
    CONSTRAINT FK_Comment_Recipe FOREIGN KEY (RecipeID) REFERENCES Recipe(RecipeID)
);

```
---

# C# integration

Going to make this all work on Visual Studio.

Just clone the repository from Carlos Github, and place the following repo in the sync cloud so that i can access it on my desktop

