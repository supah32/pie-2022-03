---
title: "Mechanical System/Design"
permalink: /mechanical/
---

# Mechanical System/Design

The Zoomba includes custom made parts made in Olin College of Engineering’s own shop. Some of the parts were laser cut out with acrylic and MDF board, and other parts were 3D printed using PLA filament. The rest of the parts were already made, bought, or manipulated to fit our needs.

<img src="/assets/images/full_cad_assembly.png" alt="CAD assembly of the entire chassis and all components" style="display: block;
	margin-left: auto;
	margin-right: auto;
	width: 50%;"
/>

All parts of the robot were assembled in Solidworks. In this assembly, some parts are color coded based on manufacturing plans:

* Orange parts were 3D printed
* Blue parts were laser cut

Note that this CAD assembly does not include any wires or the Raspberry Pi casing.


### Chassis

The chassis includes mounting holes for each of the components necessary on the Zoomba – these include electronics, electronic mountings, the vacuuming component, and the motors. There are also slots made onto the chassis to allow for better wire management between the DC motors and the motor shield on the Arduino. The main hole in the middle of the chassis is for the PVC pipe that allows items to be picked up by the vacuum and flow into the container. Hardware includes a mix between M3 screws and 4-40 bolts and nuts used for mounting components onto the chassis.

<!-- <Insert CAD render of Chassis by itself> -->


### Mecanum Wheels
As opposed to omnidirectional wheels (which need 5 driving wheels), mecanum wheels only need 4 driving wheels in order to manuever in all directions.

<img src="/assets/images/mecanum_wheels.jpg" alt="Diagram of how mecanum wheels work" style="display: block;
	margin-left: auto;
	margin-right: auto;
	width: 40%;"
/>

The main important part of the mecanum wheels is the orientation in which they are aligned. By aligning the wheels in an ‘X’ pattern (the top left and bottom right wheels in the same direction, the top right and bottom left wheels in the other direction), the robot can move in all directions. **The omnidirectional maneuverability of the robot fails if this important detail is forgotten.**


### Vacuum

The vacuum component of the Zoomba involves a <a href="https://www.amazon.com/dp/B07SGWNV5J?ref=ppx_yo2ov_dt_b_product_details&th=1" target="_blank">120mm, 4-pin, 12V, DC fan</a>. The fan has a maximum rotational speed of 5300 RPM and a rated airflow for 230 CFM. For reference, an average vacuum has an airflow of about 150 CFM, which is why we chose this particular fan. By mounting the fan ‘backwards’, it allows the airflow to move towards the back and intake through the pipe that is close to the ground to collect items. These items are then deposited inside a container with flip locks for easy garbage disposal.

<!-- <Insert CAD render of Vacuum component/enclosure> -->

To keep larger items from entering and interfering with the fan blades, the vacuum also has a custom mesh that acts as a debris filter. The mesh is created with laser cut part acrylic. It includes a circular shape of cut out hexagons to allow air to flow through the mesh but thick and small enough to ensure items do not go into the blades.

<!-- <Insert CAD render of mesh> -->

