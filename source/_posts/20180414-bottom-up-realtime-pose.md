---
title: Realtime Multi-Person 2D Pose Estimation using Part Affinity Fields - notes
date: 2018-04-14 15:31:38
categories: Research
tags:
    - pose estimation
---

I read this paper not very carefully when CVPR 2017 accepted list was released, and felt the performance was really impressive. For some reason, once again I re-read this paper and got a more detailed understanding about it.

The most eye-catching key words of this paper are **Realtime** and **Multi-person**. The biggest difference for the common pose estimation methods is that this algorithm DOES NOT require person detector ahead. Though this is the most popular/straightforward solution to the pose estimation problem.

Similar to skeleton detection/body keypoint detection, pose estimation methods aim at detecting and localizing body joints, connecting them to find body parts. This paper proposes an efficient way to address the problem in 2D environment.

### Top-down pose estimation algorithm

#### Overview of top-down algorithms from [paper][4]

According to the [keypoint detection leaderboard][1] from MSCOCO, most of leading algorithms([Megvii (Face++)][2], [RMPE][3]) are two-stage ones as well as top-down ones. They obtain keypoint results by applying single-person skeleton models on the human bounding boxes generated from some advanced object detector/pedestrian detector.

#### Limitation of top-down algorithms

It is clear that top-down algorithms will highly depend on the accuracy and speed of the first-stage person detector. In this case, it will be a hard decision to make for the tradeoff between accuracy and speed. What’s more, the comlexity of top-down algorithms can increase proportionally as the number of people increases. This feature also makes top-down algorithms difficult to scale to indense environments.

### Bottom-up pose estimation algorithm

Naturally bottom-up pose estimation algorithms are on the opposite location with top-down ones. For bottom-up algorithms, the person detector is not required, all they need is the raw image. The principle of bottom-up algorithms is that they will find all potential body parts, then they will match/parse them. This looks perfect for an end-to-end pose estimation system. 

#### Limitation of bottom-up algorithms

<figure>
    <img src="https://cl.ly/3A152A17071t/Image%202018-04-14%20at%203.58.46%20PM.png">
    <figcaption style="text-align: center;">Different association strategies from this paper</figcaption>
</figure>

However the top-down algorithms occupy most leading positions because the final parse requires “costly global inference” as a NP-hard integer linear programming problem according to this paper. Usually it’s going to take time on the order of hours to solve the parsing, which makes top-down algorithms look more efficient.

Some works investigate how to speed up the parsing time but can’t meet the requirement for a real-time compact pose estimation system.

### Innovation

Instead of only detecting body joints, this method also estimates the association between two joints, which is called *Part Affinity Fields* (PAF) in this paper.

<center>
    <img src="https://cl.ly/2h161X1z072R/Image%202018-04-14%20at%204.27.01%20PM.png">
</center>

With a start point and the direction vector, it is much easier to associate body parts.

### Network

<center>
    <img src="https://cl.ly/1p2E3a1V3B2e/Image%202018-04-14%20at%204.31.18%20PM.png">
</center>

This paper ultilizes an iterative process and the algorithm can be divided into three parts:

- Input raw figures to the first CNN to generate confidence map $S^1$ and PAF $L^1$
- Combined $S^{t-1} + L^{t-1} + F$ as the new input
- Apply NMS according to $S^t$ and $L^t$ to select final part candidates, linear integration to calculate association weights, then generate the final parsing result

#### Loss function

$L_2$ loss is selected between the estimated predictions and groundtruths for both sub-networks.

$$
f_S^t = \sum_{j=1}^J \sum_p||S_j^t(p)-S_j^*(p)||_2^2
$$

In the loss of both brachs, $W$ is provided to distinguish between locations missing the annotation or not. The final loss is simply adding two together. 

$$
f = \sum^T_{t=1}(f_S^t + f_L^t)
$$


#### Generation of confidence map

The groundtruth confidence map is generated using the raw figure and 2D annotations for each part. For every location on the map, the confidence value should be 

$$
S_{j,k}^*(P) = exp(-\frac{||p-x_{j,k}||_2^2}{\sigma^2})
$$

Where: 

- $x_{j,k}$: 2D position of body part $j$ for person $k$ 
- $\sigma$: peak width controller

Final/Integrated confidence map is from all individual confidence maps via a max operator as

$$
S_j^(P) = S_{j,k}^(P)
$$



[1]: http://cocodataset.org/#keypoints-leaderboard
[2]: https://arxiv.org/abs/1711.07319
[3]: https://github.com/MVIG-SJTU/RMPE
[4]: https://arxiv.org/pdf/1701.01779.pdf







