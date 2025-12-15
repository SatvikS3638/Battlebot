# Initial Considerations

The aim of this project is to design and fabricate a combat robot for a university level competition to participate in the 15 kg weight class in a 16 feet side square arena. 

## Weapon Mechanism Selection
The weapon mechanism selected can be the central idea around which a combat robot is designed. Although an [elementary study](https://scholars.fhsu.edu/cgi/viewcontent.cgi?article=1346&context=sacad) says that weapon class does not affect a battlebot’s performance, it affects the geometry, weight distribution, power requirements, and almost about every other aspect of it. Wedges, Drill, Crushers, Lifters and various kinds of spinners are some of the most common mechanisms in competitions. An extensive list can be found [here](https://battlebots.fandom.com/wiki/Category:Weapons). 

Thus, after careful consideration it was decided that the Drum Spinner be the weapon of choice for the robot. It is essentially a large cylinder spinning at high RPM with extrusions to transfer high amount of kinetic energy to the opponent during collisions and do damage. The largest disadvantage which must be kept in mind that a spinning drum at one end makes it difficult to control the robot.

![Minotaur by Team RioBotz, A combat robot featured in the Battlebots TV Show, with a Drum Spinner as its primary weapon.](/assets/Minotaur-Bot-S2019-1140x760.jpg) 
"Minotaur, the heaviest drum spinner bot from Team RioBotz in the American TV Show Battlebots."

## Control Device Selection
The easiest and most inexpensive method to control an electronic device is using a commercial microcontroller. The [Arduino Uno R3](https://docs.arduino.cc/hardware/uno-rev3/) was selected as the main processing unit for the circuit since not only it was cheap and easily available, the makers had previous expertise in operating the same. 

