# Visual Odometry for Maze Navigation

## Description

This is the project for the graduate class ROB-GY 6203 Robot Perception at NYU Tandon SOE between Panayiotis Christou, Jesse Inouye and Ifedayo Olasunya.  
In this project we are tasked to explore a maze created using textures as walls in PyGame to find the target images. The project is split in 2 phases, the exploration and the navigation phase.
The goal of the project is  to implement computer vision techniques, either classical or deep learning, to detect the target images and to be able to navigate back to them in navigation phase.  
The grading criterion was completing the navigation to the target images in under 2 minutes as well us how fast we submitted a solution with the allocated time being 1 hour. 

## Solution Approach

- We implemented feature detection and matching using FLANN akd KDTree from the OpenCV library to find the descriptor of each frame at each processing step. 
- We used the descriptors found during feature detection between saved sequential frames to find the essential matrix (see visualization below) and used that to implement SLAM. 
- We decompose the essential matrix intro the translation and rotation matrices and use those to calculate the new rotation of the player and the translation at each processing step.
- Using the rotaion and the translation we map the position of the player at each processing step and create a map of the path taken by the player (see visualization below).
- We implemented target image detection and matching using VLAD. For VLAD we saved the descriptors of each image for processing after the exploration phase was done.
- Using VLAD we were able to quickly find the target in navigation phase using the ball tree created in exploration phase to query the target images' descriptors.
- We navigate as quickly as possible to the target location making sure to avoid any collision with the walls or ending the phase before being in the proper radius phasing the target wall texture.

## Optimizations

- Some of the textures on the walls were of plain colors and that made feature detection difficult. In order to circumvent that we processes the image by converting it to gray scale, applying in series an equalized histogram filter, a gaussian blur filter and a sobel filter and then changing the contrast using an alpha value of 2 and a beta value of 0 (see vizualization below).
- Because of the now increasingly higher number of detected feature descriptors we were able to have a more accurate path which allowed us to save a frame for processing every 3 frames rather than every frame.
- To reduce the inaccuracies of the mapped path we reduced the calculation of the rotation and translation matrices to only occur when the pressed keys were left/right and forward/backward respectively which made the calculation faster and reduced excess computation.
- To further make the map better in every calculation of the translation/rotation, we made sure to use only the highest magnitude of the two transformations (even when calculating only one of the transformations due to matrix multiplication we had some error which resulted in a small magnitude in the other transformation as well) when plotting the map which removed all curves from the map and plotted only straight lines (see vizualization below).
- Since the time of solution was only for the navigation phase, we moved all of the processing, including building the ball tree for VLAD, in the exploration phase. This simple trick effectively brought us in the proper submission range in regards to time.  
We implemented several classical computer vision techniques along with some deep learning to complete the project but found that with the hardware we had available, the deep learning implementations for feature detection and matching slowed us down. We kept them implemented and you can find the cloned repo for superglue as well, feel free to switch the function used in the player code to test the deep learning implementation youselves.

## Value of the solution
Learnied how to implement SLAM and VLAD using both classical feature detection and matching as well as using a neural network (in this case pretrained SuperGlue). Learned how to optimize code by making certain choices between accuracy and speed. Implemented OpenCV functions and in the process implement the mathematics that underline computer vision. 

## Results
Our submission was at 6 minutes with a completion time around 1 minute and 50 seconds. We were able to properly map the maze and to perform feature detection and matching as well as VLAD and SLAM and we were able to draw the target image location on the map for navigation. Since the target images were given from 4 orthogonal POVs we were only able to match 1 or 2 depending on the traversed path in the maze which is reasonable since matching all 4 meant we had to have a 360 rotation at the target location which is not possible when time is a grading metric and you don't know the target before the navigation phase begins. 

## Visualizations/Examples
### Feature Matching between adjacent frames
![Feature Matching Example](https://github.com/panaschristou/Visual-Odometry-for-Maze-Navigation/blob/main/figures/feature_matching_adj_frames.jpg)

### Mapped Maze Path
![Maze Example](https://github.com/panaschristou/Visual-Odometry-for-Maze-Navigation/blob/main/figures/maze_map.jpg)

### Target Matches
![Target Matches](https://github.com/panaschristou/Visual-Odometry-for-Maze-Navigation/blob/main/figures/target_matches.jpg)













