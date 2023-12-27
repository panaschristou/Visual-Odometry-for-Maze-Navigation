# Visual Odometry for Maze Navigation

## Description
This is the project for the graduate class ROB-GY 6203 Robot Perception at NYU Tandon SOE between Panayiotis Christou, Jesse Inouye and Ifedayo Olasunya.  
In this project we are tasked to explore a maze created using textures as walls in PyGame to find the target images. The project is split in 2 phases, the exploration and navigation phase.
The goal of the project is for the team members to implement computer vision techniques, either classical or deep learning, to detect the images and to be able to navigate back to them in navigation phase.  
The grading criterion was completing the navigation to the target images in under 2 minutes as well us how fast we submitted a solution with the allocated time being 1 hour. Our submission was at 6 minutes with a completion time around 1 minute and 50 seconds.

## Solution Approach

- We implemented feature detection and matching using FLANN akd KDTree from the OpenCV library. 
- We used the descriptors found during feature detection between saved sequential frames to find the essential matrix. 
- We decompose the essential matrix intro the translation and rotation matrices and use those to calculate the new rotation of the player and the translation at each processing step.
- Using the rotaion and the translation we map the position of the player at each processing step and create a map of the path taken by the player. 
We implemented several classical computer vision techniques along with some deep learning to complete the project but found that with the hardware we had available, the deep learning implementations for feature detection and matching slowed us down.  














