# License
The codes originated from [nerfstudio-gaussian-splatting](https://github.com/MstXy/nerfstudio-gaussian-splatting) and [NeRFStudio]() are licensed under the Apache-2.0 license. 

The [submodules/diff-gaussian-rasterization](https://github.com/graphdeco-inria/diff-gaussian-rasterization) ([License](https://github.com/graphdeco-inria/diff-gaussian-rasterization/blob/main/LICENSE.md)), [submodules/simple-knn](https://gitlab.inria.fr/bkerbl/simple-knn.git), some codes and files copied from [graphdeco-inria/gaussian-splatting](https://github.com/graphdeco-inria/gaussian-splatting) ([License](https://github.com/graphdeco-inria/gaussian-splatting/blob/main/LICENSE.md)) that used to implement gaussian splatting here are separately licensed.

# Gaussian Splatting Viewer & Render

## NOTE
 * Not well tested, rendering only (no training), not as fast as SIBR viewers
 * The render quality of the nerfstudio web viewer could be the same as the SIBR viewers. You need to
 	* increase the render resolution (the `Max Res` option under the `CONTROLS` tab)
  	* increase jpeg quality (`--config.viewer.jpeg-quality 100`) or switch to png format (`--config.viewer.image-format png`)
 * The default orientation may not correct, you can
	* add `--no-auto-reorient` option to `run_viewer.py` or `render.py` if you want the viewer use the same coordination system as the input dataset
	* click `RESET UP DIRECTION` under the "SCENE" tab to use your current viewpoint as the orientation
 	* use `--ref-orientation IMAGE_NAME` option to specific an image as the reference orientation
 * Hold down the right button of your mouse to move the camera a little bit before pressing `W`, or your camera may be frozen after moving a short distance.
   * A fixup has been submitted: https://github.com/nerfstudio-project/nerfstudio/pull/2404
   * Or use this viewer: https://nsv.cslab.pro/23-09-15-1/?websocket_url=ws://localhost:7007
 * Press `F5` to refresh the page if the web viewer stops updating the content (not sure why currently, hard to reproduce). If you are creating camera path, click 'EXPORT PATH' to download your camera path before refreshing, and you can click 'LOAD PATH' to restore from the downloaded file later.

## Installation

### Step-1
Install nerfstudio dependencies.
You must run `pip install -e .` for this repository if you reusing a virtual environment of other nerfstudio

### Step-2 
```bash
pip install plyfile==0.8.1
pip install ./submodules/diff-gaussian-rasterization
pip install ./submodules/simple-knn
```

## Usage
### Viewer: 

```bash
python nerfstudio/scripts/gaussian_splatting/run_viewer.py --model-path GAUSSIAN_TRAINING_OUTPUT_MODEL_DIR --config.pipeline.model.nn-com-path UNET_NAME
```

<img src="docs/_static/imgs/SUNDAE-viewer-png.png" width=640>


### Render:
```bash
python nerfstudio/scripts/gaussian_splatting/render.py camera-path \
    --model-path GAUSSIAN_TRAINING_OUTPUT_MODEL_DIR \
    --camera-path-filename YOUR_CAMERA_PATH_FILE.json \
    --output-path YOUR_OUTPUT_MP4_FILE.mp4
```


