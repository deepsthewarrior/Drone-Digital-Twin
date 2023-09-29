This project was done from the SupRTwin: Sensing, Understanding, and Provisioning of Robotic Digital Twins at Universität des Saarlandes.

#### Objective:
 To construct a Digital Twin of the environment as captured by the Drone during its flight. 
##### Overview:
Drone takes an inspection flight in a confined environment. Deep learning model YOLOv5 is deployed to detect the objects in the input stream from the drone. From the detected object, location of the objects are found based on the location of the drone and the bounding box pixels. 
<p>
    <img src="/images/Screenshot from 2023-09-29 11-36-45.png" width="1437" height="319" />
</p>



Overall,  implementation-wise we can split  the process into 3 phases.

<p>
    <img src="/images/Screenshot from 2023-09-29 11-29-48.png" width="1063" height="525" />
</p>


##### Drone API:
Drone API which are implemented in MQTT APIs are subscribed and published with appropriate params to successfully send/receive data from and to the drone.  
<p>
    <img src="/images/Screenshot from 2023-09-29 11-46-23.png" width="1866" height="880" />
</p>


##### Object Detection:
We created a custom dataset of objects with training set of 4.1K images, validation set of 628 images, testing set of 212 images. 
<p>
    <img src="/images/Screenshot from 2023-09-29 11-40-31.png" width="1904" height="833" />
</p>


We then used YOLOv5 model to train the dataset. And obtained the following performance. 
We see that box_loss is steadily lowered both train and validation set loss. 
<p>
    <img src="/images/Screenshot from 2023-09-29 11-53-56.png" width="1235" height="646" />
</p>


##### Object Location Estimation:
We used Homography matrix and change the center pixels of the image to Mapping matrix using Homography matrix obtained using the intrinsic and extrinsic camera parameters. 
<p>
    <img src="/images/Screenshot from 2023-09-29 12-12-56.png" width="1474" height="791" />
</p>


We get the object's bounding box and center. 
<p>
    <img src="/images/Screenshot from 2023-09-29 12-02-45.png" width="1474" height="791" />
</p>

Then we use rotation matrix in z-axis to reverse rotate the object's co-ordinate along the z-axis with respect  to the drone's rotation.
<p>
    <img src="/images/Screenshot from 2023-09-29 12-44-01.png" width="1474" height="489" />
</p>



##### Digital Twin in Unity3D:
 With the adjusted object's location and class of object in hand, we reconstruct the whole scene in Unity 3D. We are already provided with the scene's environment in Unity 3D in which we place the detected objects dynamically on the fly.
 <p>
    <img src="/images/Screenshot from 2023-09-29 11-43-55.png" width="1879" height="880" />
</p>


##### Final Flow:
Finally the end-end flow looks like this. 
 <p>
    <img src="/images/Screenshot from 2023-09-29 12-49-54.png" width="1539" height="836" />
</p>


###### Repo:
This project was done in collaboration with the German Research Center for Artificial Intelligence and ZeMA - Zentrum für Mechatronik und Automatisierungstechnik gemeinnützige GmbH.
Implementation's Repo: [https://mrk40.dfki.de/drone-inspection-seminar/droneinspection](https://mrk40.dfki.de/drone-inspection-seminar/droneinspection)
 <p>
    <img src="/images/Screenshot from 2023-09-29 12-56-08.png" width="1539" height="836" />
</p>
