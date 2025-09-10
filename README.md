# Video Object Tracking with Lucas–Kanade and Inverse Compositional Methods

This project explores **video object tracking** through multiple implementations of the **Lucas–Kanade algorithm** and the **Matthews–Baker inverse compositional method**. It demonstrates the effectiveness of translation-only, affine, robust, and pyramidal variants of Lucas–Kanade, and compares them with the inverse compositional approach for efficiency and accuracy.

---

## Project Overview

The key objectives are:
- Implement **Lucas–Kanade tracker** for translation-only motion.
- Extend to **affine tracking** for handling rotation, scale, and shear.
- Implement **inverse compositional affine tracking (Matthews–Baker)** for computational efficiency.
- Add **robustness** via Huber and Tukey M-estimators to handle illumination changes and outliers.
- Integrate a **pyramidal approach** to handle large frame-to-frame displacements.
- Evaluate these trackers on sequences (`car1`, `car2`, `landing`) and visualize bounding box tracking results.

---

## Repository Structure
```text
.
├── InverseCompositionAffine.py   # Inverse compositional affine tracking
├── LucasKanade.py                # Translation-only Lucas–Kanade tracker
├── LucasKanadeAffine.py          # Affine Lucas–Kanade tracker
├── LucasKanadePyramid.py         # Pyramidal Lucas–Kanade tracker
├── LucasKanadeRobust.py          # Robust affine Lucas–Kanade (Huber/Tukey)
├── file_utils.py                  # Utility functions for safe paths and saving results
├── test_ic_affine.py             # Test script for inverse compositional affine tracker
├── test_lk.py                    # Test script for translation-only tracker
├── test_lk_affine.py             # Test script for affine tracker
├── test_lk_affine_robust.py      # Test script for robust affine tracker
├── test_lk_pyramid.py            # Test script for pyramidal tracker
├── results/                      # Saved results (tracked frames with bounding boxes)

```

---

## Implementation Highlights

- **Lucas–Kanade (Translation Only):** Estimates displacement (dx, dy) between frames.
- **Affine Lucas–Kanade:** Extends tracking with a 2×3 affine matrix for more complex transformations.
- **Inverse Compositional Affine:** Precomputes Jacobian and Hessian once, reducing runtime cost significantly.
- **Robust Affine Tracking:** Handles illumination changes and outliers with Huber/Tukey estimators.
- **Pyramidal Lucas–Kanade:** Coarse-to-fine tracking to manage large inter-frame motion.

## Running the Code

### Python version
Python 3.8+

### Install dependencies
pip install numpy scipy opencv-python matplotlib

**## Scripts**

### Translation-only Lucas–Kanade
python test_lk.py car1 0

### Affine Lucas–Kanade
python test_lk_affine.py car2 0

### Robust Affine Lucas–Kanade (Huber/Tukey)
python test_lk_affine_robust.py landing 0

### Pyramidal Lucas–Kanade
python test_lk_pyramid.py car1 0

### Inverse Compositional Affine
python test_ic_affine.py landing 0

- **First argument:** dataset name (car1, car2, or landing)
- **Second argument:** 0 (disable display) or 1 (show results while running)
Outputs are saved under **results/** in subfolders like **results/lk/, results/lk_affine/, results/ic_affine/**, etc.

## Results
- Lucas–Kanade (Translation): Fast, works for small rigid motions, fails under scale/rotation.
- Affine Lucas–Kanade: Handles scale and rotation but slower and sensitive to occlusion.
- Inverse Compositional: Matches affine flexibility, but 3–5× faster due to precomputation.
- Robust Affine: Less sensitive to noise and illumination changes.
- Pyramidal LK: Handles large inter-frame displacements effectively.

**## Acknowledgements**
- Author        : Nagarjunan Saravanan
- Libraries     : NumPy, SciPy, OpenCV, Matplotlib

