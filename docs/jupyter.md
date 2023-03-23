# Running Jupyter on Snowy

!!! info

    - You can run Python in `jupyter-notebook` or `jupyter-lab`, which provide a web interface with possibility of inline figures and debugging.
    - `jupyter-lab` is installed in the `python` modules `>=3.10.8`.
    - You may also install your own version of `jupyter-notebook` or `jupyter-lab` if you have certain version requirements.

## 1. Connect to Rackham using ThinLinc.

You may download the ThinLinc client from here:
<https://www.cendio.com/thinlinc/download>

You may also use the web browser to connect:
<https://rackham-gui.uppmax.uu.se>
You need to set up 2FA for the ThinLinc web.

## 2. Open a terminal in ThinLinc and ask for an interactive session to Snowy.

```bash
salloc -A naiss2023-22-247 -p node -N 1 -M snowy --gpus=1 --gpus-per-node=1 -t 04:00:00
```

Note: We have a magnetic 4-node reservation for today: `naiss2023-22-247_1`.

Is the GPU visible?
```bash
echo $CUDA_VISIBLE_DEVICES
```

## 3. Load the needed modules

```bash
module load python_ML_packages/3.9.5-gpu
pip list
```

And start the Jupyter notebook:
```bash
jupyter-notebook --ip 0.0.0.0 --no-browser
```

## 4. Open the notebook.

### Solution 1:
Click on any of the links.
This will open a Jupyter notebook in a Firefox browser on Rackham.

### Solution 2:
Instead of opening Jupyter in a browser in ThinLinc, you may use the browser on your computer.
You need to use ssh-tunnelling for this:

```bash
ssh -L 8000:s175:8888 iusan@rackham.uppmax.uu.se
```

If you cannot open the notebook using the links above, try changing it to:
`localhost:<port>/?token<tokenID>`
Example: `localhost:8000/?token=ab8a98df7b6606316849015daebaca5d2fa6331d32a47446`
      
