# Fused-Planes: Why Train a Thousand Tri-Planes When You Can Share?

### ICLR 2026

**Official paper implementation**
> Karim Kassab*, Antoine Schnepf*, Jean-Yves Franceschi, Laurent Caraffa, Flavian Vasile, Jeremie Mary, Andrew Comport $^\dagger$, Valérie Gouet-Brunet $^\dagger$ (* $^\dagger$ indicate equal contribution)<br>
| [Project Page](https://fused-planes.github.io) | [Full paper](https://openreview.net/forum?id=bAG7lS1AUL) | [Preprint](https://arxiv.org/abs/2410.23742) |<br>

<b>Abstract:</b> *Tri-Planar NeRFs enable the application of powerful 2D vision models for 3D tasks, by representing 3D objects using 2D planar structures. This has made them the prevailing choice to model large collections of 3D objects. However, training Tri-Planes to model such large collections is computationally intensive and remains largely inefficient. This is because the current approaches independently train one Tri-Plane per object, hence overlooking structural similarities in large classes of objects. In response to this issue, we introduce Fused-Planes, a novel object representation that improves the resource efficiency of Tri-Planes when reconstructing object classes, all while retaining the same planar structure. Our approach explicitly captures structural similarities across objects through a latent space and a set of globally shared base planes. Each individual Fused-Planes is then represented as a decomposition over these base planes, augmented with object-specific features. Fused-Planes showcase state-of-the-art efficiency among planar representations, demonstrating $7.2 \times$ faster training and $3.2 \times$ lower memory footprint than Tri-Planes while maintaining rendering quality. An ultra-lightweight variant further cuts per-object memory usage by $1875 \times$ with minimal quality loss.*

![LatentScenes](assets/ls_videos.gif)

## Setup
In this section we detail how prepare the environment for training numerous scenes.

### Environment 
Our code has been tested on:
- Linux (Debian)
- Python 3.11.9
- Pytorch 2.0.1
- CUDA 11.8
- `L4` and `A100` NVIDIA GPUs


You can use Anaconda to create the environment:
```
conda create --name igae -y python=3.11.9
conda activate igae
```
Then, you can install pytorch with Cuda 11.8 using the following command:
```
pip install torch==2.0.1 torchvision==0.15.2 torchaudio==2.0.2 --index-url https://download.pytorch.org/whl/cu118 --upgrade
```
_You may have to adapt the cuda version according to your hardware, we recommend using CUDA >= 11.8_

To install the remaining requirements, execute:
```
pip install -r requirements.txt
```

## Usage

### Data
ShapeNet data can be requested from the [offical website](https://shapenet.org).
Basel Faces data can be found at the [following link](https://huggingface.co/datasets/k-kassab/fused-planes-data).

### Define data directory
You must specify the path to the fused-planes-data by defining the environment variable DATA_DIR
```
export DATA_DIR=".../fused-planes-data"
```
or by changing the variable ``DATA_DIR`` in igae/datasets/dataset.py .

### Training numerous scenes
This section illustrates how to learn numerous cars from shapenet.
#### Stage 1
To launch stage 1, run:
```
bash run_stage1.sh stage1/cars.yaml
```
#### Stage 2
To launch stage 2, run:
```
bash run_stage2.sh stage2/cars.yaml
```

## Visualization / evaluation
We visualize and evaluate our method using [wandb](https://wandb.ai/site). 
You can get quickstarted [here](https://docs.wandb.ai/quickstart).

## Notice 
This work is closely related to our paper [Bringing NeRFs to the Latent Space:
Inverse Graphics Autoencoder](https://ig-ae.github.io), whose [implementation](https://github.com/k-kassab/igae) encompasses functionalities for both projects.
Feel free to explore our other work if it piques your interest.

## A Note on License
This code is open-source. We share most of it under the [Apache 2.0 License](https://www.apache.org/licenses/LICENSE-2.0).
However, parts of the code in [igae](igae) are distributed under a more restrictive license.
Refer to the igae [README](igae/README.md) for more details.

## Citation

If you find this research project useful, please consider citing our work:
```
@inproceedings{fused-planes,
        title={{Fused-Planes: Why Train a Thousand Tri-Planes When You Can Share?}},
        author={Karim Kassab and Antoine Schnepf and Jean-Yves Franceschi and Laurent Caraffa and Flavian Vasile and Jeremie Mary and Andrew I. Comport and Valerie Gouet-Brunet},
        booktitle={The Fourteenth International Conference on Learning Representations},
        year={2026},
        url={https://openreview.net/forum?id=bAG7lS1AUL}
}
```