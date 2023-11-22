# :weight_lifting_man:Workout-Detector:robot:
The exercise pose detection part of the music recommendation project.

## Installation

- Download this repository

  ```bash
  git clone https://github.com/randaldong/Workout-Detector.git
  ```

- Download [Miniconda](https://docs.conda.io/projects/miniconda/en/latest/miniconda-install.html)/[Anaconda](https://www.anaconda.com/download#downloads)

- Open the Anaconda Prompt and cd to the target folder, run the following commands:

  ```bash
  conda env create --name music --file environment.yml
  conda activate music
  ```

- To run this app, use command line:

  ```powershell
  streamlit run app.py
  ```

## Pose Detection

- Idle
- Bicep Curl 
- Shoulder Press
- Squat



![](https://camo.githubusercontent.com/7fbec98ddbc1dc4186852d1c29487efd7b1eb820c8b6ef34e113fcde40746be2/68747470733a2f2f6d65646961706970652e6465762f696d616765732f6d6f62696c652f706f73655f747261636b696e675f66756c6c5f626f64795f6c616e646d61726b732e706e67)Fig. Pose Landmarks from Google [MediaPipe](https://github.com/google/mediapipe/tree/master)

## Features

1. recommend different types of songs when doing different workouts
2. change song when switch exercise poses
3. sound effect & counting for each movement

## References

- [MediaPipe](https://developers.google.com/mediapipe): An open source, cross-platform, customizable ML solution for live and streaming media.
- [chrisprasanna](https://github.com/chrisprasanna)'s GitHub repository [Exercise_Recognition_AI](https://github.com/chrisprasanna/Exercise_Recognition_AI)

