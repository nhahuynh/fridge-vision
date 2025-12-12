# AI Usage Log

## 1. Project Initialization & Architecture

- **Date**: December 10, 2025
- **Tool Used**: Gemini
- **Question Asked**: "Help me write a python computer vision program that can classify grocery items from a picture of a fridge."
- **What I Learned**:
  I learned that YOLOv8 is the optimal model for this real-time detection task and that my dataset (GroceryStoreDataset) was natively formatted for classification, not detection. I understood that I needed to convert these classification labels into "pseudo-bounding boxes" for YOLO to accept them.
- **How I Applied It**:
  I set up the initial project structure, installed the `ultralytics` library, and defined the project scope to focus on fine-tuning a pre-trained YOLO model for fridge items.

## 2. Dataset Conversion & Formatting

- **Date**: December 10, 2025
- **Tool Used**: Gemini
- **Question Asked**: "I'm getting a KeyError: 'Class ID'."
- **What I Learned**:
  I learned how to use `%%writefile` to manage YAML configurations directly in Jupyter and realized that real-world CSV data often requires cleaning (e.g., stripping hidden whitespaces in headers) before processing with Pandas.
- **How I Applied It**:
  I included a conversion script that automatically downloads the dataset from GitHub, cleans the CSV headers, and reformats the directory structure into the standard `images/labels` format required by YOLO.

## 3. Visualization & Inference

- **Date**: December 10, 2025
- **Tool Used**: Gemini
- **Question Asked**: "Can you add code to visualize the images next to the prediction output?"
- **What I Learned**:
  I learned that YOLO processes images in BGR color space while screens display RGB, requiring conversion for correct display. I also understood how to use `matplotlib` to render inline visualizations in a notebook environment.
- **How I Applied It**:
  I added a visualization cell to my notebook that immediately plots the bounding boxes over my test images, allowing me to visually confirm if the model was detecting the items correctly.

## 4. Addressing Domain Shift

- **Date**: December 10, 2025
- **Tool Used**: Gemini
- **Question Asked**: "How can I improve the accuracy?"
- **What I Learned**:
  I learned about the concept of "Domain Shift"—where a model trained on perfect studio images fails on messy, real-world images. I discovered that mixing "natural/messy" validation data into the training set can help the model generalize better.
- **How I Applied It**:
  I implemented a Python script to shuffle 50% of the "natural" validation images into the training folder to force the model to learn from more difficult examples. It also suggested to me that I can manually add new training data consisting of photos that are more like "real-life" in terms of lighting and composition to help the model learn better.

## 5. Integrating Custom Data

- **Date**: December 10, 2025
- **Tool Used**: Gemini
- **Question Asked**: "Where should I put the new training images?"
- **What I Learned**:
  I learned that manually adding real-world photos is the most effective way to boost accuracy, but they must be strictly organized by folder names that match the class IDs for automated labeling to work.
- **How I Applied It**:
  I created a directory structure (`New_Training_Data/Apple`, `New_Training_Data/Milk`) and generated an "Ingest Script" to automatically generate labels and merge my new photos into the main training set.

## 6. Training Optimization (GPU)

- **Date**: December 10, 2025
- **Tool Used**: Gemini
- **Question Asked**: "It's taking a really long time to run through 50 epochs."
- **What I Learned**:
  I learned that increasing model complexity (from `yolov8n` to `yolov8s`) significantly increases computation time and that my model runtime was on CPU as default. It helped remind me to switch to the T4 GPU runtime in Google Colab to accelerate training.
- **How I Applied It**:
  I reconfigured my Google Colab environment to use the T4 GPU. I also set the number of epochs to 10 to balance out performance and time.

## 7. Automated Data Pipeline

- **Date**: December 10, 2025
- **Tool Used**: Gemini
- **Question Asked**: "Can you modify this code to fetch the TEST_IMAGES_DIR from a github link instead?"
- **What I Learned**:
  I learned that Google Colab environments only cache the image files temporarily. To test on new data added to the project github, I need to programmatically delete and re-clone the repository.
- **How I Applied It**:
  I updated my inference script to include a `shutil.rmtree` and `git clone` sequence, ensuring my model always tests against the absolute latest images I upload to my `fridge-vision` repository.

## 8. Interactive Evaluation

- **Date**: December 11, 2025
- **Tool Used**: Gemini
- **Question Asked**: "Can you update this metrics script so it will match with my latest prediction?"
- **What I Learned**:
  I learned that calculating accuracy requires another step of generating "answer keys" for the test data which we had not include in our scripts.
- **How I Applied It**:
  I implemented the extra step of data prepping which is generating "answer keys" so the test data predictions can be benchmarked.

## 9. Automated Ground Truth Generation

- **Date**: December 11, 2025
- **Tool Used**: Gemini
- **Question Asked**: "How do we add hidden .txt answer keys?"
- **What I Learned**:
  I learned that "Ground Truth" labels are simply text files matching the image filename. I understood that I could automate the creation of these files by mapping folder names or filenames to class IDs.
- **How I Applied It**:
  I generated a "Smart Key Generator" script that scans my test images and automatically creates the required `.txt` files, allowing YOLO to calculate Mean Average Precision (mAP) automatically without manual entry.

## 10. Robust Filename Matching

- **Date**: December 11, 2025
- **Tool Used**: Gemini
- **Question Asked**: "Can we modify this so that the file names don't have to match exactly?"
- **What I Learned**:
  I learned how to implement "fuzzy" logic to match files like `Apple_01.jpg` to the class `Apple` by checking if the filename starts with any known class string, prioritizing longer names (e.g., checking "Pineapple" before "Apple") to avoid false positives.
- **How I Applied It**:
  I refined the label generation script to support loose naming conventions, enabling me to drop files named `Apple_1.jpg` or `Milk_Front.jpg` into the test folder and still generate accurate ground truth labels automatically.
