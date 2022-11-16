# Self-Use Log

## Remarks
- the input argument `sample_ratio` is effective to balance quality and speed. The higher, the slower and denser the computation/result is.
A good practice would be `sample_ratio=4 or 8`.
- `skip_path_consistency=True` can speed up but degrade the quality slightly. Perceptually, no big difference.


## Experiments on the Snowboard sequence.
- The input image sequence has 66 frames, and seems to be about 10 fps.
- The following command gives reasonable reconstruction in an efficient manner, which takes `95.633910` seconds.
```
python run_particlesfm.py --image_dir ./example/snowboard/images --output_dir ./outputs/snowboard/ --sample_ratio=8 --skip_path_consistency
```
- The output means a point cloud with 19216 points. The meaning of `num_observations` is unknown to me yet.
```
{'num_reg_images': 66, 'num_sparse_points': 19216, 'num_observations': 164894, 'mean_track_length': 8.581078, 'num_observations_per_image': 2498.393939, 'mean_reproj_error': 0.608517}
```

- When `skip_path_consistency=False`, particlesfm additionally optimizes the point tracking. Then it takes `127.527402` seconds to produce
the following results, with more reconstructed points.
```
{'num_reg_images': 66, 'num_sparse_points': 19561, 'num_observations': 168449, 'mean_track_length': 8.611472, 'num_observations_per_image': 2552.257576, 'mean_reproj_error': 0.615594}
```

- Qualitive comparison: left and right are with and without `skip_path_consistency`, respectively. Perceptually, no big difference up to a global transformation.

<img src="misc/media/snowboard_skip.png" alt="drawing" height="250"/>
<img src="misc/media/snowboard_noskip.png" alt="drawing" height="250"/>



---