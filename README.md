# CubeShooter
This project is developed using Unreal Engine 5.6 and C++, showcasing FPS mechanics, dynamic materials, and JSON-driven cube spawning.


## Pre-Requisites:-
Unreal Engine 5.6 installed on your system.

## How to run the project:- 
1. Clone the repository on your machine.
2. Open the .uproject file which will launch Unreal Engine 5.6.
3. Hit the play button in Unreal Editor or press Alt + P.



### Logic Implemented

1. JSON Data Extraction & Parsing
Used Unreal Engine's HTTP and JSON modules to fetch and parse cube data such as color, health, score, and spawn transform.
The data is deserialized into structured C++ objects and stored in separate structs for efficient management.
These structs are then used to spawn cubes dynamically with their respective properties.

2. Dynamic Material System
Implemented a custom material with a Color Control parameter to modify cube appearance.
Using MaterialInstanceDynamic, RGB values are updated at runtime through C++, allowing dynamic color changes.

3. Gun Architecture
Designed a scalable gun system using an abstract base class defining common properties like Ammo, Fire Rate, Damage, and Range.
Currently implemented a HitScan gun using line tracing for instant hit detection.
The system is extendable to support projectile-based weapons with physics-based bullet behavior.

5. Pickups:- 
A Pickup Component which when attached to an object, makes that object pick-able by the player. Right now the player can only pickup guns. If the player already has a gun, then the ammo of the pick-able gun will be added to the player's gun. Functionality to pick up ammo boxes and other items can be implemented without the need to extend the class thanks to Enums.

6. UI implementation using Unreal Motion Graphics (UMG):- 
Two classes were inherited from UMGs User Widget class in C++. The first class called Player HUD Widget class manages the Player's Heads Up Display and is responsible for showing crosshair, player's current score, ammo count and a victory screen congratulating the player for destroying all the cubes. The second class called Cube Health Widget class is reponsible for displaying the current health of each cube.


### Challenges Faced
1. JSON Parsing

Implemented JSON parsing using Unreal Engine’s built-in HTTP and JSON modules, without relying on external plugins.
By working with Http.h and Json.h, I developed a custom solution to send HTTP requests and deserialize the received JSON data into usable C++ objects.
This involved exploring Unreal’s internal modules and applying trial-and-error to successfully extract structured data.

2. Data Extraction & Cube Spawning

Designed a structured approach to store parsed data and spawn cubes dynamically based on it.

Created two custom structs:

FCubeDescription → Stores shared cube properties such as name, color, health, and score

FCubeSpawnInfo → Stores spawn-specific data like cube type, location, rotation, and scale

Used:

TMap<FString, FCubeDescription> → Maps cube types to their properties

TArray<FCubeSpawnInfo> → Stores all spawn instructions

Using this architecture, cubes are spawned dynamically in the world with their respective properties and transformations applied correctly.
