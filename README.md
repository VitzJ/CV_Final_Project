# TO CONVIENIENTLY RUN THE DEMONSTRATION:

To conveniently check the output of my work without having to pull the repository and follow the setup instructions, please access the google colab version of the front-end file serving component of my project.

Notebook Name: `demonstration_without_full_videos_colab_version.ipynb`
Colab Link: https://colab.research.google.com/drive/1T7lFV7xyOlWHkG1KkKEBnuvrpVgjGF3a?usp=sharing

This notebook is the same as the colab version. It requires a single change with respect to `moviepy` package usage as the only real difference between how the colab notebook functions versus how my actual repo functions.

## IMPORTANT: YOU MUST RUN THE PIP INSTALL BUBBLE ONCE, AND THEN RESTART THE NOTEBOOK SESSION (Navigate to Runtime -> Restart Session). IF YOU DO NOT DO THIS, FFMPEG WILL NOT BE PROPERLY UTILIZED BY THE VIDEO SPLITTER DURING RETRIEVAL

<br>

## My Dataset:

I created a dataset to preserve my custom segmentations which can be found via the link below:

HuggingFace Dataset: [JohnVitz/CV_Final_Project_Video_With_Chunked_Captions_Bert_Topic_1](https://huggingface.co/datasets/JohnVitz/CV_Final_Project_Video_With_Chunked_Captions_Bert_Topic_1)

This dataset is formulated in `Bert_Topic_Chunking_Full_Pipeline.ipynb` which is detailed after the 

<br>

# FOR LOCAL INSTALLATION AND USAGE:

## Setup Information

My python version: Python 3.12.3

I used a virtual environment for this project; the requirements.txt contains the packages that I had to install in order for this project to work on my local machine. The current code also requires cuda

<br>

## Demonstration Instructions (varies based on file chosen):

Note: PLEASE USE THE COLAB NOTEBOOK LINK TO RUN THE DEMONSTRATION, BELOW IS AN EXPLANATION OF THE RELEVANT PROJECT FILES.

<br>

### For `demonstration_without_full_videos_colab_version.ipynb`

This notebook is included for reference purposes; it will not work in the environment as the `movie.py` import to make it work is different.

<br>

### For `demonstration_with_full_videos.ipynb`:

Pull the repository and install `requirements.txt`

You need to run `setup_stuff.ipynb` first in order to pull the original dataset from huggingface and parse them to their encoded video format, which will be stored in the `/full_video` folder. The setup will also download the dataset to local storage folder `/raw_original_video_dataset`.

<br>

### For `demonstration_without_full_videos.ipynb`:

You just need to run this file, there is no need to run `setup_stuff.ipynb`. Please note that this is effectively the same notebook as the one from the colab link.


<br>

### For `Bert_Topic_Chunking_Full_Pipeline.ipynb`

This file requires a small edit to work standalone versus its current state;

Replace:

```python
from datasets import load_from_disk

video_dataset = load_from_disk("raw_original_video_dataset")
```

With:

```python
from datasets import load_dataset

dataset = load_dataset("aegean-ai/ai-lectures-spring-24")
```

#### Processing includes:

- Deduplication of initial captions (captions that are purely comprised of prior or next captions
- Getting a Single Caption String for Each Video
- Restoring Punctuations in each of the the Single Caption Strings
- Mapping the punctuations from the single strings to each caption selectively
- Applying a Sliding Window to Capture some `window_size` amount of captions in order to compile them together into a single chunk for Bert-Topic
- Formatting for input into BertTopic; getting embeddings utilizing `all-mpnet-base-v2` model and`SentenceTransformer` package
- Applying a Wrapper to Load the BertTopic model that includes defining a custom UMAP and a custom HDBSCAN
- Applying a function to get deduplicated segmentations while allowing for some overlap between these segmentations based on a minimum clip duration floor
  
- A dynamic visualization of the potential topics / their respective windows.
  
![image.png](attachment:image.png)

- Setting up a final pipeline to apply the same processing across all video file / caption pairs
- Utilizing the pipeline to gather the final embeddings for the custom caption segmentations and pushing the dataset to huggingface

This dataset is then used as the basis for the demonstration files; it is also linked above in the section `Preface`.
