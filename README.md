# unity3d-union-pizzeria - Link: https://drive.google.com/file/d/1fOR8FsTaj5RuBPJYpXC8Clom35k0EFU1/view?usp=sharing
Unity 3d application showing a working simulation of a trainee working in a restaurant
Unity Version Used: 2020.3.29f1 (LTS).
Download>Unzip>Open_in_unity>Start Playing!

1. Abstract
- The project is a simulation of working in a restaurant (based on the Union building food stall, UWM). 
- It is not a real-life simulation. 
- The tasks are slightly gamified. 
- It is developed using the Unity cross platform game engine. 
- It is a unity 3d application. 
- All the 3D meshes in the project are developed using Autodesk Maya and Blender software. 
- The UV maps are textured using Unity and Krita software. 
- The .apk file is developed for windows. 
- The objective of the project is to simulate a food preparation task done by new trainees working at the restaurant. 
- The user will be the Trainee and would be able to move around, interact with the food models and prepare the requested order. 
- This simulation demonstrates the working of different Unity core modules such as Graphics (Textures, Shaders, Materials), Physics, Scripting, Animation, UI, Navigation and   pathfinding. 

2. Program design 

2.1	Models

Food Prefab 1
•	Contains all the Topping Ingredients
•	There are three toppings (Pepperoni, Mushroom, Olive)
•	They share the same mesh with 3 different textures. 
•	They are discrete.

Food Prefab 2
•	Contains all the Crust Ingredients
•	There are two types of crust (Normal, Deep Dish)
•	They are discrete.
•	They also contain three hidden meshes placed inside them for the two continuous items i.e., Cheese and Sauce. They are hidden during start and the respective meshes are displayed when the respective ingredients are used.

Food Prefab 3
•	Contains all the Cheese Ingredients
•	They are of three types (Mozzarella, Cheddar, Parmesan)
•	They share the same mesh but have different textures and color
•	Shader Graph has been used for the cheese textures.
•	This is a continuous item, and it triggers the cheese meshes (respective to the type of cheese) on the pizza dough during use.
 
Food Prefab 4
•	Contains the Sauce
•	The sauce bottle is used to trigger the sauce mesh present on the pizza dough.
•	This is a continuous variable. 
•	Shader graph is used for the texture of the sauce mesh.

Stall
•	Contains all the models used in the food stall excluding the food prefabs.
•	The models 9 models are:
  o	Ingredients Tray
  o	Pizza Prep Board
  o	Pizza Delivery Tray
  o	Sneeze Guard
  o	Stall Body
  o	Stall Counter
  o	Stall Head Board
  o	Stall Interactive Display
  o	Stall Menu Board
•	Contains the game manager component 
•	Contains the Player Component along with the UI
•	Contains a reflection probe

Navigation Pathfinding
•	Contains all the models used in the scene excluding the food prefabs and the stall prefab
•	The contain the Atrium, delivery robot, cleaning robot and delivery cabin models.

2.2	Materials/Textures

•	The project uses various types of materials and display textures through Base Map, Metallic Map, Normal Map, Emission Map for various meshes.
•	The textures are both created in Photoshop/Krita and a few are downloaded from the internet.
•	The Normal, Bump maps are created on the software and exported as a .png file are used in the project as textures.
•	The sauce mesh and the cheese mesh textures are created through shader graphs.


2.3	UI

•	Player Canvas
This UI elements displays the ‘Item Name’ on the bottom right of the screen and ‘Timer’ sprite on the bottom left of the screen when the game is running
•	HeadBoard Back Screen
This displays the Pizza order name, the step-by-step instructions on the back side of the headboard.
•	Interactive Display
This displays the Overall rules during gameplay and the accuracy and feedback once the order is delivered. 

2.4	Scripts

-MoveCamera - Script used to move camera based on mouse movements 
| 
-Movement - Script used to move player character inside the stall
|
 -GameConstants - A Class which has all the constants used in the project 
| 
-Item - Defines an item that can be picked up, interacted and dropped 
| -Base - A place where an item can be placed 
|------Board - A Base which is used for preparing pizza 
|------Pizza - A Base which refers to where the Pizza crust, cheese, sauce, toppings can be added 
|------Oven - A Base in which a pizza can be baked, timer included. 
|------DeliveryTray - A Base which will trigger completion of round when a baked pizza is placed. 
|-Order - A class which contains basic details about the order like type of toppings, crust, cheese needed. 
| -GameManager - The script responsible for managing order (order entered in the inspector before gameplay) and its progress 
| -Pickup - Script that is attached to player which takes care of pickup, drop and interacting with Base and Item
| -MenuBoard – The script controls the menu items inputs to be taken as an order on runtime.
| -NavMovement – This script controls the Delivery Robot 
| -CleaningRobot1 – This script controls the CleaningRobots.

3. Working Logics 

The ‘UnionPizzeria’ Scene contains the final project scene.

3.1	Rules:

•	Movement/Pick Up
1.	The ‘W’, ‘S’, ‘A’, ‘D’ and the ‘Up’, ‘Down’, ‘Left’, ‘Right’ is used for the forward, backward, left and right player movement respectively inside the stall.
2.	The crosshair pointer is used for the ray cast functionality and any interaction is done using that.
3.	When the pointer is used the keys ‘’E and ‘Q’ to interact with the objects. In case of Toppings, sauce bottle, cheese, pizza crusts, prep board, ‘E’ picks up the object and ‘Q’ drops it. In case of oven ‘E’ opens the oven door. In case of Delivery tray, ‘E’ triggers feedback. In case of menu board, ‘E’ takes menu items as input orders.
4.	The mouse scroll button is used for triggering the sauce mesh and the cheese mesh (once the pizza is placed on the prep board). 

•	Assembly/Pickup
1.	Only the pizza crust can be placed on the prep board
2.	The sauce must be added first on the pizza dough
3.	Only if the sauce is present, the cheese can me added.
4.	The toppings are added after the cheese (any toppings can be added to the pizza)
5.	The pizza can be place in the oven only using prep board. (i.e., we have to carry the prep board with the pizza on top and then interact with the oven)
6.	The oven animation is triggered (only after complete assembly of pizza), and the timer event (different for normal crust and deep dish) is triggered.
7.	The pizza is picked up from oven once timer is complete and placed on delivery tray (only after placing in the oven and then placed on the deliver tray, the feedback is triggered).
8.	The Feedback and accuracy is triggered when delivery tray has the pizza.
9.	Pressing ‘Esc’ triggers the nav mesh agent to deliver the pizza

•	Menu
1.	The menu is generated in three ways.
2.	Type 1: The menu can be set on the game manager where we can choose the type of crust, cheese, topping, and extras. This has more priority i.e., if there is a menu on the game manager, that menu will be considered first during gameplay.
3.	Type 2: The order is randomly generated during gameplay after each order completion. (Developer feature: ‘R’ key triggers the menu change event and ‘X’ key triggers the scene reset event – not used during gameplay).
4.	Type 3: Pressing ‘E’ on the front side of the menu board takes that order during gameplay.


•	Accuracy/Feedback
1.	The accuracy is calculated using a dictionary which stores the pizza preparation order (the one we make), the height values of the sauce and cheese meshes, how much topping is used (each time ‘E’ is pressed, a count value is calculated), the time kept inside the oven.
2.	The accuracy score is first 100f and as we keep comparing, we keep reducing the score and adding comments to the feedback string (Refer to DeliveryTray.cs script)		

4. Conclusion

- The Union Pizzeria Project was as culmination of working with various 3d modelling, raster graphics softwares and bringing them all into Unity to create a gamified workflow of a restaurant functioning simulation. 
- Various concepts have been explored, learned and executed as a part of this project (3D modeling, UV Unwrapping, Texturing, Rendering, Animation, Shaders, UI, Triggers/Bounds, Scripting, Navigation/Pathfinding etc ). 
- This project was a demonstration of how different things interact with each other and how all the modules are interlinked with each other and how they all come together as a whole project. 
