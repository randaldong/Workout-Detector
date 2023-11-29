# :weight_lifting_man:Workout-Detector:robot:
The exercise pose detection part of the music recommendation project.

## Installation

To install this project, do the following:

- Download this repository

  ```bash
  git clone https://github.com/randaldong/Workout-Detector.git
  ```

- Download [Miniconda](https://docs.conda.io/projects/miniconda/en/latest/miniconda-install.html)/[Anaconda](https://www.anaconda.com/download#downloads)
  To [install `conda` on Raspberry Pi](https://stackoverflow.com/questions/75720056/installing-miniconda-on-raspberry-pi4), run the following command:
  ```bash
  sudo wget http://repo.continuum.io/miniconda/Miniconda3-py39_4.9.2-Linux-aarch64.sh
  sudo /bin/bash Miniconda3-py39_4.9.2-Linux-aarch64.sh
  
  # If conda is installed under root,
  # to run conda command, enter into the root mode
  sudo su
  ```
  Check out [this post](https://stackoverflow.com/questions/50266716/result-consumed-self-buffer-decodedata-self-errors-final-mistake) if the following error shows up:
  ```bash
  Traceback (most recent call last):
      File "/root/miniconda3/lib/python3.9/site-packages/conda/exceptions.py", line 1079, in __call__
        return func(*args, **kwargs)
      File "/root/miniconda3/lib/python3.9/site-packages/conda_env/cli/main.py", line 80, in do_call
        exit_code = getattr(module, func_name)(args, parser)
      File "/root/miniconda3/lib/python3.9/site-packages/conda_env/cli/main_create.py", line 87, in execute
        spec = specs.detect(name=name, filename=filename, directory=os.getcwd())
      File "/root/miniconda3/lib/python3.9/site-packages/conda_env/specs/__init__.py", line 43, in detect
        if spec.can_handle():
      File "/root/miniconda3/lib/python3.9/site-packages/conda_env/specs/yaml_file.py", line 18, in can_handle
        self._environment = env.from_file(self.filename)
      File "/root/miniconda3/lib/python3.9/site-packages/conda_env/env.py", line 159, in from_file
        yamlstr = fp.read()
      File "/root/miniconda3/lib/python3.9/codecs.py", line 322, in decode
        (result, consumed) = self._buffer_decode(data, self.errors, final)
    UnicodeDecodeError: 'utf-8' codec can't decode byte 0xff in position 0: invalid start byte
  ```

- Open the Anaconda Prompt and cd to the target folder, run the following commands:

  ```bash
  conda env create --name music --file environment.yml
  conda activate music
  pip install -r requirements.txt
  ```

- To run this app, use command line:

  ```powershell
  streamlit run app.py
  ```

## Pose Detection

- Bicep Curl 
- Shoulder Press
- Squat
- Idle or wrong


Fig. Pose Landmarks from Google [MediaPipe](https://github.com/google/mediapipe/tree/master)
![](https://camo.githubusercontent.com/7fbec98ddbc1dc4186852d1c29487efd7b1eb820c8b6ef34e113fcde40746be2/68747470733a2f2f6d65646961706970652e6465762f696d616765732f6d6f62696c652f706f73655f747261636b696e675f66756c6c5f626f64795f6c616e646d61726b732e706e67)


## Features

1. recommend different types of songs when doing different workouts
2. change song when switch exercise poses
3. sound effect & counting for each movement

## Model Training

You can go through `ExerciseDecoder.ipynb` to checkout how the data is collected and how the model is trained. You can also collect customized data and train your own model using this Jupyter Notebook.



retrained the model and increased the accuracy for four types.

previously was using default model for just three types (curl, press, squat), regarding detection with low-confidence as idle. Recorded and labeled new videos last night and trained the model.

## References

- [MediaPipe](https://developers.google.com/mediapipe): An open source, cross-platform, customizable ML solution for live and streaming media.
- [chrisprasanna](https://github.com/chrisprasanna)'s GitHub repository [Exercise_Recognition_AI](https://github.com/chrisprasanna/Exercise_Recognition_AI)

