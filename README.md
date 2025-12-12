# Fridge Vision

## Team Members

- **Nha Huynh**
  - Oversaw project and coordinated tasks/deliverables.
  - Set up github repository following project guidelines
  - Generated code and troubleshot technical issues.
  - Recorded video demo.
  - Created AI log and results/metrics materials.
  - Wrote README sections (Technical Details, How to Run, Dataset, Metrics, AI usage, Improvements).
  - Created AI log
  - Created results/metrics materials
- **Elijah Raines**
  - Collected and organized the custom fruit training dataset (Golden-Delicious, Kiwi, Mango, Oranges, Tomatoes, Peach).
  - Created the Test_images folder for evaluating the model on real-world items.
  - Ran model predictions on test images and noted detection accuracy and misclassifications.
  - Assisted with running the model in Colab and checking for false positives.
  - Wrote README sections covering the fruit dataset, test images, and detection results.
- **Triet Le**
  - Proposal based on original SOW
  - Presentation creation with notes from team
  - Reflections creation with notes from team
- **Richard Rodriguez**
  - Created original scope of work and timeline
  - Ensured README formating consistancy
  - Code testing in Colab and image dataset gathering
  - GitHub documentation updates
  - Audio Voice over using the ClipChamp text to speech AI tool

## Tier Selection

**Tier:** Tier 1

**Justification:** We wanted to tackle a small and common problem and do it well rather than failing to execute a complicated higher tier problem.

## Problem Statement

People often forget what's in their fridge, leading to costly food waste and duplicate purchases that particularly affect busy families and sustainability advocates. This is a significant issue, as U.S. households waste up to $2,913 annually on spoiled food, but solving it would save money, reduce environmental impact, and streamline grocery planning.

## Solution Overview

Our solution is a computer vision system that detects and counts current food items in the fridge, so user would know what they already have at home when they are shopping at the grocery store.

## Technical Approach

Our core technical approach is object detection using the YOLOv8 model. We will start with a pre-trained version and fine-tune it on our custom dataset using the Ultralytics YOLOv8 repository, which is built on PyTorch. We chose YOLOv8 because it is state-of-the-art, offering an excellent balance of speed and accuracy that is ideal for real-time applications.

## Dataset Plan

- **Source:** GroceryStoreDataSet on Github
- **Size:** 117 MB
- **Labels:** Bounding boxes
- **Link:** https://github.com/marcusklasson/GroceryStoreDataset

## Metrics

- **Primary Metric:** Detection Accuracy (Target: 90%+)
- **Secondary Metrics:**
  - **Inventory Completeness Score:** (Detected unique items / Actual unique items) $\ge$ 90%. _This measures how well our system captures the full set of items, not just accuracy per item._
  - **Processing Time:** $< 1$ second/image
  - **Usability Score:** Based on user feedback.

## Week-by-Week Plan

| Week        | Task                            | Milestone           |
| :---------- | :------------------------------ | :------------------ |
| 10 (Oct 30) | Get dataset, set up environment | Dataset ready       |
| 11 (Nov 6)  | Train or fine-tune model        | Model working       |
| 12 (Nov 13) | Test and improve                | Good accuracy       |
| 13 (Nov 20) | Create demo / video             | Demo ready          |
| 14 (Nov 27) | Final testing / documentation   | Everything done     |
| 15 (Dec 4)  | Present project                 | 🎉 Presentation day |

## Custom Fruit Training Dataset

A manually collected and organised dataset stored in: [data/New_Training_Data](data/New_Training_Data/)

| Folder Name           | Description          |
| --------------------- | -------------------- |
| **Golden-Delicious/** | Yellow apple variety |
| **Kiwi/**             | Kiwi fruit images    |
| **Mango/**            | Mango fruit images   |
| **Oranges/**          | Orange fruit images  |
| **Tomatoes/**         | Tomato images        |
| **peach/**            | Peach images         |

### Purpose

- Provide additional **clean, well-labeled images** for common fridge fruits
- Improve detection and classification performance
- Address class imbalance and missing fruit categories in the original dataset

### Notes

- Each folder represents a class label
- Images were cleaned, resized, and organised consistently
- The dataset supports both classification and YOLO preprocessing

---

Test Images Dataset

Located in: [data/Test_images](data/Test_images/)

Includes a mix of real-world items such as:

- Apples (multiple lighting conditions)
- Oranges
- Peaches
- Mango
- Kiwi
- Grapefruit
- Milk carton
- Orange juice bottle
- Packaged items for false-positive testing

---

### Purpose

- Evaluate whether the model generalises to **real fridge photos**
- Identify problems such as:
  - Similar fruit confusion (e.g., tomatoes vs apples)
  - Low-light or angled images lower confidence
  - Packaged items triggering incorrect predictions

### Example Findings

- Fruit classes with many training samples were detected accurately
- Items with similar shapes/colours produced confusion
- Non-fruit items (milk, juice) helped identify false positives
- Testing images revealed where the dataset needed improvement

---

# 🧠 Technical Approach

### Model

- **YOLOv8**
- Pretrained weights fine-tuned on grocery and custom fruit images
- Trained using **Ultralytics** framework
- Evaluated using custom test images and built-in model metrics

## Resources Needed

Google Colab Pro for GPU access (T4 GPU)

## Risks & Mitigation

| Risk         | Probability | Mitigation                                                         |
| :----------- | :---------- | :----------------------------------------------------------------- |
| Low accuracy | Medium      | Use data augmentation and experiment with different architectures. |
| Missing data | High        | Switch to Roboflow dataset or another public alternative.          |

## Technical Details

### Approach

- **Task**: Object Detection & Classification
- **Model**: YOLOv8
- **Framework**: PyTorch
- **Key Libraries**: ultralytics, opencv, pandas, matplotlib, Pillow

### System Architecture

[Input] → [Preprocessing] → [Model] → [Post-processing] → [Output

### Dataset

- Source: https://github.com/marcusklasson/GroceryStoreDataset (2485)
- Size: 2497 images (including manual additions)
- Classes: 81
- Split: Train: 2497 images, Test: 14 images

### How to Run

- Upload jupyter notebook file FridgeVision.ipynb to Google Colab workspace
- Select T4 GPU runtime
- Run each cell sequentially

## Performance Metrics

### 🏆 AUTOMATED RESULTS

| Metric        | Score  |
| :------------ | :----- |
| **mAP@50**    | 83.23% |
| **Precision** | 78.35% |
| **Recall**    | 78.89% |

#### Success Cases

![Apple prediction](https://github.com/nhahuynh/fridge-vision/blob/main/results/images/apple_prediction2.png)
![Orange prediction](https://github.com/nhahuynh/fridge-vision/blob/main/results/images/orange_prediction.png)

#### Failed Cases

![Failed donut prediction](https://github.com/nhahuynh/fridge-vision/blob/main/results/images/donut_prediction_failed.png)
![Failed apple prediction](https://github.com/nhahuynh/fridge-vision/blob/main/results/images/mango_prediction_failed.png)

## Demo Video
https://drive.google.com/file/d/1pUnDDA4kwknCO_mYSJpW__mWYeC_Gzz7/view?usp=sharing


## Reflections

Fridge Vision Project Reflection

This Fridge Vision project was an exciting hands-on opportunity to explore real-world computer vision challenges using YOLOv8. Throughout development, we encountered both technical obstacles and time-management struggles that ultimately shaped the outcome of the model.

**TECHNICAL CHALLENGES**:
One major challenge was learning and fine‑tuning YOLOv8 for object detection. Although powerful, the model required multiple training sessions to reduce overfitting, improve predictions, and understand how hyperparameters impacted performance. Working with the GroceryStoreDataset also posed limitations because it did not fully match real fridge environments. Issues such as class imbalance, poor lighting, clutter, and occlusion required additional data cleaning and augmentation.
A key performance limitation was the model’s inability to reliably distinguish tomatoes from apples. Both share similar shape, color, and texture, so without enough diverse training images, YOLOv8 tended to classify both as apples. The dataset lacked enough tomato examples from different angles and lighting conditions, which prevented the model from learning subtle visual differences. This resulted in frequent misclassification and highlighted how important balanced, high‑quality training data is.

**TIME MANAGEMENT CHALLENGES**:
The project timeline was organized week by week, but actual development rarely aligned perfectly with the plan. Model training and debugging consistently required more time than expected, forcing adjustments to milestones. Another challenge was balancing deeper experimentations, such as testing alternative models or advanced augmentation, against tight deadlines. Learning to prioritize core functionality over perfection was a key part of staying on track.
Team coordination also required more effort than anticipated. Syncing datasets, sharing updates, and consolidating progress took additional time, but improved communication helped the group work more efficiently.

**OVERALL MODEL PERFORMANCE**:
The model performed fairly well on large, visually distinct objects, such as milk cartons and eggs. However, performance dropped with small or visually similar classes. The tomato‑vs‑apple confusion demonstrated the limits of the dataset and the need for more domain‑specific data. Despite these issues, the project showed that YOLOv8 is effective for real‑time fridge item detection when supported by strong training data.

We found that performance improved significantly when the number of epochs was increased from 5 to 10. This shows that the more training runs the model experiences, the better it performs.

**KEY TAKEAWAYS**:

- High‑quality, well‑balanced datasets are just as important as model choice.
- Real-world environments introduce unique challenges like occlusion and poor lighting.
- Flexible planning is essential because training and debugging often take longer than expected.
- Clear team communication helps avoid delays and repeated mistakes.

This project enhanced our understanding of object detection, dataset preparation, and model evaluation. The challenges and failures contributed significantly to the learning experience. This project significantly enhanced our understanding of object detection, dataset preparation, and model evaluation. Throughout the process, we delved deep into the complexities of each stage, allowing us to gain valuable insights. The challenges we encountered, along with the failures we faced, transformed the learning experience into something profoundly enriching. Each obstacle prompted us to rethink our strategies, experiment with different approaches, and ultimately develop more robust solutions. By reflecting on these setbacks, we were able to identify gaps in our knowledge and improve our techniques, making the entire experience not only educational but also rewarding. Overall, this project has laid a solid foundation for our future work in this field.

## AI Usage Documentation

- See detailed log: [https://github.com/nhahuynh/fridge-vision/blob/main/docs/AI_usage_log.md]
- Used AI for: Understanding architectures, debugging, code generation
- Key learnings: We learned how to organize folder structure to preprocess the data for training and prediction, as well as setting up the model and do E2E results validation.
- Code attribution: Gemini AI

## Future Improvements

- Do validation step
- Split images for testing and validation more appropriately

## References

1. [https://github.com/marcusklasson/GroceryStoreDataset]

## License

[MIT / Apache / Academic Use Only]

## Acknowledgments

- Thanks to Professor McManus for a great semester!
- Pre-trained models from [Ultralytics]
- Dataset from [https://github.com/marcusklasson/GroceryStoreDataset]
- AI assistance from Gemini AI
