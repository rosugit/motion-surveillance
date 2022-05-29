# motion-surveillance

The aim of this project is to build a home surveillance system besed on movement and face recognition. Using a simple web camera we capture a video stream which is used to detect any movement, and if there is any, run a facial recognition module which captures facial landmarks of a person and classifies it using hand-tailored distance-based features.

Frameworks:
* Python
  * OpenCV (camera API, image processing), mediapipe (facial landmarks)

<!---
how to make hyperlinks:
[Contribution guidelines for this project](docs/1.png)
-->

## The terminal

The terminal is a control panel which encompasses 6 components: the original video stream, movement detection matrix, movement detection time series, first order differenced movement detection time series, facial landmark detection, and face classification output.

The terminal utilizes 3 classes:

* `Camera`: responsible for the web camera I/O
* `Graph`: responsible for constructing the terminal
* `Face`: responsible for face landmark detection

Terminal's interface is shown below.

> insert finished terminal screenshot

### Component 1: original video stream

This shows the live video feed directly from the web camera. The `Camera` class accepts parameters for the camera port (`camera_port`) and the frame rate (`video_delay`), assuming the hardware is able to handle higher FPS.

### Component 2: movement detection matrix

Movement detection (MD) matrix is calculated using the following logic: $MD_{x,y} = |F^0_{x,y} - F^1_{x,y}|$, where $x,y$ - corresponding pixel coordinates and $F^1, F^0$ are current and previous frames transformed into grayscale. 

Essentially MD is a frame with the same resolution as camera feed that shows absolute difference between two frames. If there is no movement/change in both frames, then they are pixel-to-pixel identical and $MD=0$; if something has changed between frames, then $MD>0$ and increasing depending on the magnitude of the change.

### Component 3: movement detection time series

This component is simple aggregation of MD matrix. To transform a 2-dimentional movement matrix into a single numerical we take a standard devion of each instance: $\sigma(MD)$.

To visualize this component a custom function was built to have a chart that live updates. It shows a limit-bound recent history of the time series (horizontal scaling) and dynamic height (vertical scaling). As alternative, `matplotlib.animation.FuncAnimation` was tried, but due to unintuitive syntax and various issues with implementation aw hand-made solution was chosen instead.


### Experiment 1: distance adjustment

![alt text](docs/fig_1_1.png)
![alt text](docs/fig_1_2.png)


### Experiment 2: rotation

rotate face left right up down and zoom in 2-3 time

### Experiment 3: face expressions

try differenet face expression (smile, angry, laugh, passive, etc)

### Experiment 3: abrupt movement

see if there are any break points in landmark detection


<details><summary>CLICK ME</summary>
<p>
### We can hide anything, even code!
</p>
</details>


Here is a simple footnote[^1].
[^1]: My reference.
