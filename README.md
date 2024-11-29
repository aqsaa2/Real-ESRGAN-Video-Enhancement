# Real-ESRGAN Video Enhancement

This repository provides an easy-to-use tool for enhancing video quality by upscaling and improving the resolution using the Real-ESRGAN model. The tool supports video input, enhancement using deep learning-based super-resolution, and downloading the enhanced video output.

## Features

- **Video Upscaling**: Enhance video resolution using the `realesr-animevideov3` model.
- **Real-ESRGAN Integration**: Uses state-of-the-art super-resolution technology to improve video quality.
- **Easy to Use**: Simple commands to upload, process, and download enhanced videos.
- **Supports Videos**: Works with both videos and images for quality enhancement.
- **Customizable Parameters**: Adjust the model and scale settings to fit your needs.

## Requirements

- Python 3.6+
- Google Colab (or local setup with dependencies)
- FFmpeg
- Real-ESRGAN
- Additional Python libraries: `basicsr`, `facexlib`, `gfpgan`, `ffmpeg-python`

## Installation

To use this repository, you will need to clone it and install the required dependencies.

1. **Clone the Repository**:

    ```bash
    git clone https://github.com/yourusername/Real-ESRGAN-Video-Enhancement.git
    cd Real-ESRGAN-Video-Enhancement
    ```

2. **Set Up the Environment**:

    Install the required dependencies using pip:

    ```bash
    pip install basicsr
    pip install facexlib
    pip install gfpgan
    pip install ffmpeg-python
    pip install -r requirements.txt
    ```

    After installing the dependencies, set up the Real-ESRGAN environment:

    ```bash
    python setup.py develop
    ```

## Usage

### Step 1: Upload Video

Upload your input video to be enhanced. You can use the following command to upload the video file:

```python
from google.colab import files
import shutil
import os

upload_folder = 'upload'
result_folder = 'results'

if os.path.isdir(upload_folder):
    shutil.rmtree(upload_folder)
if os.path.isdir(result_folder):
    shutil.rmtree(result_folder)
os.mkdir(upload_folder)
os.mkdir(result_folder)

uploaded = files.upload()
for filename in uploaded.keys():
    dst_path = os.path.join(upload_folder, filename)
    shutil.move(filename, dst_path)


### Step 2: Video Inference (Enhancement)

Run the video inference script to enhance the uploaded video. You can adjust the model name and scale factor based on your requirements.

```python
python inference_realesrgan_video.py -i upload/your_video.mp4 -n realesr-animevideov3 -s 2 --suffix outx2

#### Arguments:

-i, --input: Input video file path.
-n, --model_name: The model name used for enhancement (e.g., realesr-animevideov3).
-s, --outscale: The upscale factor (e.g., 2 for 2x enhancement).
--suffix: The suffix added to the output video file name.


### Step 3: Visualize the Input and Enhanced Videos
After processing, you can visualize the original and enhanced videos directly in the notebook:

```python
from IPython.display import HTML
from base64 import b64encode

def show_video(video_path, video_width = 600):
    video_file = open(video_path, "r+b").read()
    video_url = f"data:video/mp4;base64,{b64encode(video_file).decode()}"
    return HTML(f"""<video width={video_width} controls><source src="{video_url}"></video>""")

# Input video
show_video('upload/your_video.mp4', video_width=1200)

# Enhanced video
show_video('results/your_video_outx2.mp4', video_width=1200)
Step 4: Download the Enhanced Video
Once the video is enhanced, you can download the output:

```python
files.download('results/your_video_outx2.mp4')
Configuration
You can customize the following parameters:

Model Name: Choose between different Real-ESRGAN models for different enhancement levels.
Scale Factor: Adjust the scale factor for video enhancement (e.g., -s 2 for 2x upscaling).
