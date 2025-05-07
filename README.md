# TO CONVIENIENTLY RUN THE DEMONSTRATION:

To conveniently check the output of my work without having to pull the repository and follow the setup instructions, please access the google colab version of the front-end file serving component of my project.

Notebook Name: `demonstration_without_full_videos_colab_version.ipynb`
Colab Link: https://colab.research.google.com/drive/1T7lFV7xyOlWHkG1KkKEBnuvrpVgjGF3a?usp=sharing

This notebook is the same as the colab version. It requires a single change with respect to `moviepy` package usage as the only real difference between how the colab notebook functions versus how my actual repo functions.

<br>

# FOR LOCAL INSTALLATION AND USAGE:

## Setup Information

My python version: Python 3.12.3

I used a virtual environment for this project; the requirements.txt contains the packages that I had to install in order for this project to work on my local machine. The current code also requires cuda

<br>

## Instructions:

Pull the repository and install `requirements.txt`

### For `demonstration_with_full_videos.ipynb`:

You need to run `setup_stuff.ipynb` first in order to pull the original dataset from huggingface and parse them to their encoded video format, which will be stored in the `/full_video` folder. The setup will also download the dataset to local storage folder `/raw_original_video_dataset`.

<br>

### For `demonstration_without_full_videos.ipynb`:

You just need to run this file, there is no need to run `setup_stuff.ipynb`. Please note that this is effectively the same notebook as the one from the colab link.


### For `demonstration_without_full_videos_colab_version.ipynb`

This notebook is included for reference purposes; it will not work in the environment as the `movie.py` import to make it work is different.
