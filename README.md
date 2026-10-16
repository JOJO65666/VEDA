# VEDA

[VEDA.ipynb](VEDA.ipynb) implements a voxel-based workflow for detecting geometric edge candidates in LAS point clouds.

## Algorithm steps

1. **Load and align the point cloud.** Read the LAS coordinates and rotate the cloud so that a supplied reference normal aligns with the vertical axis.
2. **Construct the voxel grid.** Estimate the mean nearest-neighbor spacing and use a scaled spacing value to define the cubic voxel size.
3. **Build height profiles.** Scan the voxel grid along rows and columns. Represent each vertical voxel stack by its mean height or its highest voxel, depending on the stack occupancy, to form 2.5D profiles.
4. **Detect edge candidates.** Fit LOESS curves to the height profiles using multiple smoothing and residual-threshold settings. Identify regions where absolute residuals exceed the threshold and retain the largest residuals within each region.
5. **Merge detections.** Take the union of the row-wise and column-wise detections across parameter settings, then map the selected voxels back to the corresponding point-cloud indices.
6. **Visualize and export.** Display candidate edge points in red and the remaining points in blue, and export the colored point cloud as a LAS file.
