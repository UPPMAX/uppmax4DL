# Running TensorBoard on Snowy

!!! info

    - TensorBoard can be used to visualise, debug, and profile your model.
    - TensorBoard is accessed from a web browser. You may start it in an interactive session and access it via an ssh-tunnel or ThinLinc.

## 1. Connect to Rackham using ThinLinc.

You may download the ThinLinc client from here:
https://www.cendio.com/thinlinc/download

You may also use the web browser to connect:
https://rackham-gui.uppmax.uu.se
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
OR

```bash
module use /sw/EasyBuild/snowy-gpu/modules/all
module load TensorFlow/2.5.0-fosscuda-2020b
```

TensorBoard can be started from the command line as `tensorboard`. You need to specify a directory for the logs using the `--logdir` option.

Example:
```bash
tensorboard --logdir=./tensorboard-log-dir
```
Change the path & name `./tensorboard-log-dir` as you wish.

By default, TensorBoard will attach the port `6006` to localhost. If it's taken, it will chose another one. You may see the chosen port in the output when you start TensorBoard from the command line.

## 4. Accesss TensoBoard

### Solution 1: Using ssh-tunnelling

```bash
ssh -L 8080:localhost:6006 user@rackham.uppmax.uu.se
```
Update the port if needed.

Next, on your computer open a web browser and visit http://localhost:8080. You should now see the Tensorboard UI.


### Solution 2: Using ThinLic

- Launch a web browser on ThinLinc.
- Visit `http://localhost:6006`. Update the port if needed.


