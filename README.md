GUNDAM_RX78
========================================================================================================================================================================
Controlar los movimientos del Gundam en un ROS, con la ayuda de otras herramientas como Gazebo.

Pre-requisitos 馃搵
----------------------
El sistema operativo utilizado es Ubuntu 18.04 Es necesario tener ROS instalado, con el entorno de trabajo configurado. Los pasos para la instalacion y configuraci贸 pueden verse en:
```
 http://wiki.ros.org/melodic/Installation/Ubuntu
```

Paquetes de ROS para robots de GUNDAM 

original: https://github.com/gundam-global-challenge/gundam_robot.git


![GUNDAM Gazebo Simulation](imgs/gundam_AKG.jpg)


C贸mo configurar el espacio de trabajo
----------------------
Con el entorno de trabajo de ROS configurado, se siguieron los pasos del archivo de GUNDAM bajo el apoyo con el archivo alojado en el Github.

```
$ mkdir -p catkin_ws/src
$ cd catkin_ws
$ wstool init src
$ wstool merge -t src https://raw.githubusercontent.com/gundam-global-challenge/gundam_robot/.gundam.rosinstall
$ wstool update -t src
$ source /opt/ros/$ROS_DISTRO/setup.bash
$ rosdep install -y -r --from-paths src --ignore-src
$ catkin build
$ source devel/setup.bash
```

Visualizar modelo URDF
===========================

Se procede a colocar la l铆nea de comando para arrancar el GUNDAM
Archivo URDF en rviz, puede usar el archivo `display.launch`.
```
$ roslaunch gundam_rx78_description display.launch
```

![Rviz](imgs/rviz.png)


![Rviz](imgs/rviz.gif)

Mapa de Panam谩
===========================

![Rviz](imgs/mapPanama.png)







Ejecutar la simulaci贸n de gazebo
============================

Para ejecutar una simulaci贸n de gazebo.

```
$ roslaunch gundam_rx78_gazebo gundam_rx78_world.launch
```

Para controlar los 谩ngulos de las articulaciones
------------

Puede ejecutar un patr贸n de caminata similar a un "robot" en la simulaci贸n

```
$ roslaunch gundam_rx78_gazebo gundam_rx78_walk.launch
```

```
# paso
$ rosrun gundam_rx78_control joint_trajectory_client_csv.py `rospack find gundam_rx78_control`/sample/csv/step.csv
# Caminar hacia adelante
$ rosrun gundam_rx78_control joint_trajectory_client_csv.py `rospack find gundam_rx78_control`/sample/csv/walk-forward.csv
# caminar hacia atr谩s
$ rosrun gundam_rx78_control joint_trajectory_client_csv.py `rospack find gundam_rx78_control`/sample/csv/walk-backward.csv
# caminar a la derecha
$ rosrun gundam_rx78_control joint_trajectory_client_csv.py `rospack find gundam_rx78_control`/sample/csv/walk-to-right.csv
# caminar a la izquierda
$ rosrun gundam_rx78_control joint_trajectory_client_csv.py `rospack find gundam_rx78_control`/sample/csv/walk-to-left.csv
# Girar a la derecha
$ rosrun gundam_rx78_control joint_trajectory_client_csv.py `rospack find gundam_rx78_control`/sample/csv/turn-right.csv
# Girar a la izquierda
$ rosrun gundam_rx78_control joint_trajectory_client_csv.py `rospack find gundam_rx78_control`/sample/csv/turn-left.csv
```

```
# Levantar los brazos y caminar
$ rosrun gundam_rx78_control joint_trajectory_client_csv.py `rospack find gundam_rx78_control`/sample/csv/up.csv
```

![Simulation](imgs/gundamAKG.gif)

Tengamos en cuenta que actualmente tenemos varias limitaciones en esta simulaci贸n, solo tenemos un controlador de posici贸n etc.

Tambi茅n se pueden encontrar archivos de control de movimiento de muestra en el directorio `gundam_rx78_control/sample`.

joint_trajectory_client_csv.py
----------------------

Usando el control de gundam con joint_tajectory_client_csv.py e ingresando un archivo .csv

Este utilizar谩 los patrones indicados en el archivo para simular el movimiento del gundam seg煤n los valores de los 谩ngulos de cada componente.

Autores 鉁掞笍
----------------------
* Gloris Cede帽o		 
* Deyka Jordan 	
* Azael Batista 		
* Isaac Perdomo
* Iv谩n Saavedra		 
* Mario Villarreal
* Samuel Olmedo 	 
* Franger Lezcano
* Elena Linares 		
* Alexis Garc铆a
* Jorge Mu帽oz 

Otros comentarios 馃巵
----------------------
El gran reto que se tuvo fue evitar que el robot cayese al vac铆o, apenas se abre el entorno.

video de Youtube: 
----------------------

https://youtu.be/hVrQR7l3-CA
