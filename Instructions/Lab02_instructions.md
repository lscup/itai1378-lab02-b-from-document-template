# Lab 1: Interactive Image Processing Application

In this lab, you will build an interactive image processing application using Jupyter Notebook. You will utilize libraries like OpenCV, Matplotlib, and ipywidgets to create a graphical interface that allows users to manipulate and visualize images.

### Objectives
- Understand and use OpenCV for image processing
- Learn to create interactive widgets with ipywidgets
- Implement image transformation and visualization techniques

### Prerequisites
- Basic understanding of Python programming
- Familiarity with Jupyter Notebooks
- Basic knowledge of image processing concepts

---

## 2. Algorithm/Concept Background

Image processing involves various techniques to enhance, transform, and analyze images. In this lab, you will use the following concepts:

- **Grayscale Conversion**: Transforming a color image to shades of gray.
- **Brightness Adjustment**: Increasing or decreasing the brightness of an image.
- **Resizing**: Changing the dimensions of an image.
- **Rotation**: Rotating an image by certain angles.

Here's how a grayscale conversion works:

```python
# Example: Converting an image to grayscale
import cv2
image = cv2.imread('color_image.jpg')
gray_image = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
```

### Important Properties
| Property | Description |
|----------|-------------|
| Time Complexity | Varies with operation (O(n) for pixel-wise operations) |
| Key Terms | Grayscale, Brightness, Resize, Rotate |

---

## 3. Your Coding Environment

### Workspace Layout
| Area | What It Does |
|------|--------------|
| Code Editor (left) | Edit your files using the tabbed editor |
| Terminal (right) | See output when you click the **Run** button |
| AI Tutor (chat panel) | Ask your AI Tutor for help — it knows this lab and can guide you step by step |

### Workflow
1. Edit your code in the editor tabs
2. Click **Run** to execute and see output in the terminal
3. When ready, click **Commit** to save your work to GitHub and trigger the autograder
4. A ✅ (green check) or ❌ (red X) will appear showing whether tests passed

**Tip**: Commit early and often to track your progress!

---

## 4. Project Structure

```plaintext
.
├── notebook.ipynb  # YOUR WORK
├── outputs/        # Output images
```

---

## 5. Step-by-Step Implementation

### Step 1: Import Libraries and Initialize
Start by importing the necessary libraries and initializing global variables.

```python
# Import libraries
import cv2
import numpy as np
from matplotlib import pyplot as plt
import ipywidgets as widgets
from IPython.display import display
import os

# Initialize global variables
original_bgr, original_rgb, processed_rgb = None, None, None
```

This code sets up your environment for image processing and visualization.

### Step 2: Create Output Areas
Create widget output areas for displaying images and messages.

```python
msg_out = widgets.Output()
img_out = widgets.Output()
hist_out = widgets.Output()
```

These will be used to display the interface components.

### Step 3: Define Helper Functions
Implement `show_images` and `show_histogram` functions to manage displays.

```python
def show_images(original_rgb, processed_rgb):
    with img_out:
        img_out.clear_output(wait=True)
        fig, axes = plt.subplots(1, 2, figsize=(10, 5))
        axes[0].imshow(original_rgb)
        axes[0].set_title('Original Image')
        axes[1].imshow(processed_rgb)
        axes[1].set_title('Processed Image')
        for ax in axes:
            ax.axis('off')
        plt.show()
```

These functions will help in visualizing the images.

### Step 4: Implement Callback Functions
Setup the callback functions for interactive controls.

For example, the `on_browse_image_clicked` function:

```python
def on_browse_image_clicked(b):
    from google.colab import files
    uploaded = files.upload()
    for filename in uploaded.keys():
        original_bgr = cv2.imread(filename)
        if original_bgr is not None:
            global original_rgb, processed_rgb
            original_rgb = cv2.cvtColor(original_bgr, cv2.COLOR_BGR2RGB)
            processed_rgb = original_rgb.copy()
            show_images(original_rgb, processed_rgb)
            with msg_out:
                msg_out.clear_output()
                print(f'Loaded image: {filename}')
```

This allows users to load and display an image.

### Step 5: Setup Interface
Define the layout and controls for the application.

```python
browse_button = widgets.Button(description='Browse Image')
...
controls = widgets.VBox([browse_button, ...])
right_side = widgets.VBox([img_out, hist_out])
ui = widgets.HBox([controls, right_side])

display(msg_out, ui)
with msg_out:
    print('Please click Browse Image to start.')
```

This code sets up the interactive layout of your application.

---

## 6. Testing Your Code

### Run Your Code
Click **Run** to execute and check the output.

### Submit for Grading
Click **Commit**, enter a message, and look for a ✅ or ❌.

**Expected Output:**
```plaintext
Please click Browse Image to start.
```

---

## 7. Autograding

| Test | Points | What It Checks |
|------|--------|----------------|
| Test Import Libraries | 10 | Verifies all libraries are imported correctly |
| Test Show Images Function | 20 | Checks the implementation of the show_images function |
| Test Show Histogram Function | 20 | Checks the implementation of the show_histogram function |
| Test Browse Image Callback | 20 | Ensures the image upload and display works |
| Test Grayscale Conversion Callback | 15 | Validates grayscale conversion |
| Test Brightness Change Callback | 15 | Evaluates brightness adjustment |

**Total Points: 100**

---

## 8. Lab Report

Click the README.md tab and fill in your lab report.

```markdown
# Lab Report

## Student Information
- **Name:**
- **Date:**

## Key Concepts
- What is image processing?
- Explain the use of OpenCV in image processing.

## Tracing Exercise
- Trace the grayscale conversion process with an example.

## Complexity Analysis
| Operation | Time Complexity |
|-----------|-----------------|
| Grayscale Conversion | O(n) |

## Reflection Questions
1. What challenges did you face during this lab?
2. How did you approach debugging?
3. What did you learn about image processing?
```

---

## 9. Submission Checklist

- [ ] All functions implemented
- [ ] Click Run — output matches expected
- [ ] Click Commit — autograder shows green check
- [ ] Lab report completed in README.md
- [ ] Final commit with completed lab report