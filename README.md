# :weight_lifting_man:Workout-Detector:robot:
The exercise pose detection part of the music recommendation project.

## Installation

### Install the project

**To install this project, do the following:**

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



### Docker image

This `Streamlit` app is also deployed using `Docker`. Check [this tutorial](https://docs.streamlit.io/knowledge-base/tutorials/deploy/docker) for how. 

Basically, just follow these steps:

- Create Docker assets (`Dockerfile`

- Build a Docker image

  ```bash
  # docker build -t IMAGE_NAME .
  docker build -t workout-detector .
  ```

- Run the Docker container

  ```bash
  # docker run -p 8501:8501 IMAGE_NAME
  docker run -p 8501:8501 workout-detector
  ```

- Publish the image

  ```bash
  # Rename the image
  docker tag workout-detector ranmeraklis/workout-detector
  
  # then, "Push to Hub" in GUI
  ```

- To stop the container

  ```bash
  # docker stop IMAGE_NAME
  docker stop workout-detector
  ```

  

### **SSH into Raspberry Pi**

1. Enable SSH on the Raspberry Pi:

- Boot up your Raspberry Pi and make sure it's connected to your network.

- Open a terminal on the Raspberry Pi or access the terminal through the desktop environment.

- Run the following command to open the Raspberry Pi Configuration Tool:

  ```
  bashCopy code
  sudo raspi-config
  ```

- Navigate to "Interfacing Options" and select "SSH." Enable the SSH service and exit the configuration tool.

2. Find the IP address of your Raspberry Pi:

- On the Raspberry Pi terminal, you can use the following command to find the IP address:

  ```
  bashCopy code
  hostname -I
  ```

- Alternatively, you can check your router's connected devices list to find the IP address assigned to your Raspberry Pi.

3. SSH into the Raspberry Pi from a remote machine:

- Open a terminal on your local machine (not the Raspberry Pi).

- Use the following command to SSH into the Raspberry Pi. Replace `your_pi_ip` with the actual IP address of your Raspberry Pi:

  ```
  bashCopy code
  ssh username@your_pi_ip
  ```

  If this is your first time connecting, you may be asked to confirm the connection by typing "yes."

- Enter the default password for the Raspberry Pi, which is usually `raspberry`. You will be prompted to change the password on the first login.

## Pose Detection

- Bicep Curl 
- Shoulder Press
- Squat
- Idle or wrong

Fig. Pose Landmarks from Google [MediaPipe](https://github.com/google/mediapipe/tree/master)
![](https://camo.githubusercontent.com/7fbec98ddbc1dc4186852d1c29487efd7b1eb820c8b6ef34e113fcde40746be2/68747470733a2f2f6d65646961706970652e6465762f696d616765732f6d6f62696c652f706f73655f747261636b696e675f66756c6c5f626f64795f6c616e646d61726b732e706e67)

Problem: Each time when a valid new pose is detected, it will send the current valid new pose to the server. However, the detection happens each frame, so `self.current_action` can change very frequently, leading to fast switches between "idle or wrong" and other correct poses.

Solution: introduce "freeze time" -- each time when a correct movement is detected, there will be a freeze time for this specific pose (curl, press, or squat). Freeze Time allows users to stay in the state for the current valid pose, even if they are doing it wrong or not doing anything within this short period of time, adding the robustness of the system.

The whole logic will be like:

```python
# Send the current action
#   1. if it's the first frame and nothing has been sent: send
#   2. if it's different from the previous action
#      2.1 if precious action is "idle or wrong": send
#      2.2 if precious action is a valid pose: delayed send
```




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

