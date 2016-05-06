# How To use the Micro Numa Automation System (MNAS) 


## Nerve Center

* In a terminal, run the spinalhub:
```
~/MNAS/nerve-center$ ./organ.run
```


## Models Manager

* The model manager is a Node webkit organ that contains the models of the system and also the library is-sim. The different html files of is-sim (admin, desk, lab, organisation, login) will be displayed in the webkit.

* The models of the MNAS are coded in CoffeeScript. To use it, you need to convert them in JavaScript using the organ.build script:
```
~/MNAS/models-manager$ ./organ.build
```

* The library is-sim should not be modified in any case, but if you do it, you need to compile it using the command:
```
~/MNAS/models-manager/is-sim$ make
```

* To run node webkit, use the organ.run script:
```
~/MNAS/models-manager$ ./organ.run
```
This should open a window with the page "http://localhost:8888/html/is-sim/desk.html".
Note: You can also run the is-sim pages in your web browser.


## is-sim very-quickstart

* In the desk page (localhost:8888/html/is-sim/desk.html), create a new organisation, then double-click it to open the organisation page.

* In the organisation page (localhost:8888/html/is-sim/organisation.html), add the new applications: **Ground**, **Numa** and **Team**.

* In the desk page, create a new project, then double-click it to open the lab page. At this moment, you should only work in this window.

* You can observe the hub FileSystem in the page "http://localhost:8888/html/is-sim/admin.html".


## MNAS Model

* In the desk page, include the three applications of your organisation ("Apps" button). This will add three items in the tree view ("Scene" window).
Note: the include order is not important.

* At the beginning, there is only the ground. The Numa building is not built and there is nobody in the Numa team.

* Build the Numa building: click the **Numa** tree item then click the "Add a floor" button (Up arrow icon). This adds a new floor to the building. You can add 7 floors to build the entire Numa. You can also delete the last floor by clicking the "Delete a floor" button (Down arrow icon).

* Floors are the children tree items of the Numa item. You should see them in the Scene window. They also have their own children, which are the different spaces of the floor. Each floor contains 4 spaces/rooms (**Space 1**, **Space 2**, **Space 3** and **Space 4**) and two stairs (**Stairs 1** and **Stairs 2**).

* You can visualize or not each individual space by clicking the corresponding blue eye icon in the Scene window. If you select a item in the Scene window, the 3D corresponding model is hightlighted in blue.

* You can change the attributes of each space: select a space then change the values in the Inspector window. In particular, the fire detection attribute is mainly used in the system: when set to 1, it means that a fire occured in the space (you should observe the associated 3D model color turning to red).

* Fill the Numa team: select the **Team** item then click the "Add an employee to the team" button (user profil pic icon). This adds a new employee item to the Team. An employee item contains a random name, an associated id and a random location (a floor + a space) in the building. You can see this location in the 3D window: each employee is represented by a colored point.

* As for the building spaces, you can choose to visualize or not each employee. You can also change the location of the point, its color or its radius in the Inspector window. By selecting an employee in the Scene window, the edge of the associated 3D point is highlighted. 


## Model saving (IMPORTANT)

* Save the **Numa** and **Team** models: select an item then click the "Save building/team" button (floppy disk icon). A pop-up will appears asking you to name your models. This name corresponds to the name of the file stored in the hub FileSystem. 

* Note: All the default organs are used to get the files named "Numa" and "Team". To use the organs without modifying them, you should save your models with these names.


## Fire detection organ (Qt)

* This Qt organ is used to randomly generate fire in spaces of the Numa building. Once a fire is created, the associated space 3D model will turn into red, and an alert will pop in the terminal where the organ is running.

* As this is a Qt organ, you have to compile it first and each time the code is modified. In a new terminal, run the command:
```
~/MNAS/fire-detection-organ$ ./organ.build
```

* To run the organ, use this command:
```
~/MNAS/fire-detection-organ$ ./organ.run
```


## Nearest humans detection organ (NodeJS)

* This Node organ runs when a fire is generated in a space (with the fire detection organ or by manually setting the fire detection attribute to 1). It calculates the distances between each employee localized in the floor and the center position of the 3D model. Then it picks the three nearest employees to the fire location and send an alert in the terminal with all the information.

* To run the organ, use this command:
```
~/MNAS/nearest-humans-detection-organ$ nodejs index.js
```


## Stairs organ (NodeJS)

* This Node organ indicates the state of the two stairs of the building. Each stairs has two states: OK and not OK. When OK (default state), the color of the 3D models is green. When not OK, the color is grey.
The state is determined with the detection of fires in the stairs. When a fire occurs in a floor, all the stairs above will be unusable and in that case the state is set to not OK.
(IN PROGRESS) 

* To run the organ, use this command:
```
~/MNAS/stairs-organ$ nodejs index.js
```




