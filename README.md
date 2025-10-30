# Fridge Vision

## Team Members

- Nha Huynh
- Elijah Raines
- Triet Le
- Richard Rodriguez

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

## Resources Needed

Google Colab Pro for GPU access

## Risks & Mitigation

| Risk         | Probability | Mitigation                                                         |
| :----------- | :---------- | :----------------------------------------------------------------- |
| Low accuracy | Medium      | Use data augmentation and experiment with different architectures. |
| Missing data | High        | Switch to Roboflow dataset or another public alternative.          |
