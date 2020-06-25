# Gaze_Controlled_Keyboard

## Table of Content:
* [Overview](https://github.com/ShubhangiDabral13/Gaze_Controlled_Keyboard#Overview)
* [Motivation](https://github.com/ShubhangiDabral13/Gaze_Controlled_Keyboard#Motivation)
* [Core-Logic](https://github.com/ShubhangiDabral13/Gaze_Controlled_Keyboard#Core-Logic)
* [Inspiration From](https://github.com/ShubhangiDabral13/Gaze_Controlled_Keyboard#Inspiration-From)


## Overview 
The “Gaze controlled keyboard” is a project where we will control the keyboard through our eyes using Python with Opencv, completely from scratch.The goal of such app is to write without using the hands. 

## Motivation 
To implement the technology for a better tomorrow is the motivation for this project.
I came across Opencv and read about it through various blogs on it. Thus the zeal to work on opencv sparked within me and the idea to  create the virtual keyboard which could be controlled by our gaze without using the hands.Such applications are really important for people affected by quadriplegia who completely lost the control of their limbs.




## Core-Logic
This project is built in 2 main parts.
  * Eye detection: detection of the eyes, their movement and most important their blinking.
  * Virtual keyboard: a keyboard on the screen where we’re going to select the letters by just using our eyes.

### 1.1Eye detection
We are taking the frames in real time from the webcam, so to detect the eyes we will use face landmarks detection approach. We can find 68 specific landmarks of the face. To each point there is a specific index assigned.
We will use the following landmark points to detect the eye.

* Left eye points: (36, 37, 38, 39, 40, 41)
* Right eye points: (42, 43, 44, 45, 46, 47)

![landmarks_points_eyes](https://user-images.githubusercontent.com/44902363/85774006-10714180-b73c-11ea-93ff-542ff0a70958.png)


### 1.2 Detecting the blinking
when we detected the eye, we also detected two lines: an horizontal line and a vertical line crossing the eye.

This is how the lines look like when the eye is open.

![eye_open](https://user-images.githubusercontent.com/44902363/85774949-f2f0a780-b73c-11ea-8fce-027d367ca5be.jpg)


This when the eye is closed.

![eye_closed](https://user-images.githubusercontent.com/44902363/85774947-f1bf7a80-b73c-11ea-85a6-815ad3ce5cf1.jpg)

We will take horizontal line as the point of reference, and from this we calculate the ratio in comparison with the vertical line.
If this ratio is more than 5.7 than the eyes are blinking otherwise they are open.

### 1.3 Gaze Detection

The idea is to devide the keyboard in two parts. If we look on the left side only the left part of the keyboard will be activated, while if we look on the right side only the letter on the right part of the keyboard will light up.

![left_right_gazecontrolled_keyboard](https://user-images.githubusercontent.com/44902363/85775667-9b067080-b73d-11ea-9920-38ed79ccb7f4.png)


Hence for that we need to detect the gaze of our eyes wether they are looking in left or right differection.

![eye_gaze-1024x421](https://user-images.githubusercontent.com/44902363/85776013-ee78be80-b73d-11ea-8251-27bb4fcd1d97.png)

What at a first glance is really clear, by looking at the image above, it’s that the sclera (white part of the eye) fills the right part of the eye when the eye is looking at the left, the opposite happens when it’s looking to the right and when it’s looking to the center the white is well balanced between left and right.

The idea is to split the eye in two parts and to find out in which of the two parts there is more sclera visible.


![eye_splitted](https://user-images.githubusercontent.com/44902363/85776329-3b5c9500-b73e-11ea-9f67-c91a6c61cbb1.png)

If the sclera is more visible on the right part, so the eye is looking at the left (our left) like in this case.Technically to detect the sclera we convert the eye into grayscale, we find a treshold and we count the white pixels.

We divide the white pixels of the left part and those of the right part and we get the gaze ratio. If the gaze ratio is smaller than 1 when looking to the right side and greater than 1.7 when the eyes are looking to the left side.

### 2.1 Virtual Keyboard

The idea is to display the Keys on the screen and light them up one at time. Once the key we want to press is lighted up, we simply would need to close our eyes and the key will be pressed.

Using numpy and cv2 we will create a simple keyboard 

![keyboard_left-300x180](https://user-images.githubusercontent.com/44902363/85778101-db66ee00-b73f-11ea-9dbf-ebc6a8ef6b75.jpg)

This is a left side keyboard.

### 2.2 Light up letters each 10 frames
Basically we are lighting up a letter for 10 frames, and after that we light up the next one, so that when we reach the letter we want to press, we simply close our eyes and it gets pressed.


**Final result**

![Screenshot (206)](https://user-images.githubusercontent.com/44902363/85778920-b32bbf00-b740-11ea-973d-e5fdc864ba21.png)

Thus able to type hello through my eye motion.


## Inspiration From

* Pyscource [blogs](https://pysource.com/category/tutorials/gaze-controlled-keyboard/) by Sergio Canu



### Author

#### Shubhangi Dabral (ShubhangiDabral13)
<a href="https://twitter.com/Shubhi_Dabral"><img 
src="https://news.wjct.org/sites/wjct/files/styles/medium/public/201407/v65oai7fxn47qv9nectx.png" align="left" height="50" width="50" ></a>
<a href="https://www.linkedin.com/in/shubhangi-dabral-b79705145/"><img src="https://cdn2.iconfinder.com/data/icons/simple-social-media-shadow/512/14-512.png" align="left" height="60" width="60" ></a>


