# MuseGAN

[MuseGAN](https://salu133445.github.io/musegan/) is a project on music
generation. In essence, we aim to generate polyphonic music of multiple tracks
(instruments) with harmonic and rhythmic structure, multi-track interdependency
and temporal structure. To our knowledge, our work represents the first approach
that deal with these issues altogether.

The models are trained with
[Lakh Pianoroll Dataset](https://salu133445.github.io/lakh-pianoroll-dataset/)
(LPD), a new [multi-track piano-roll](https://salu133445.github.io/musegan/data)
dataset, in an unsupervised approach. The proposed models are able to generate
music either from scratch, or by accompanying a track given by user.
Specifically, we use the model to generate pop song phrases consisting of bass,
drums, guitar, piano and strings tracks.

Sample results are available [here](https://salu133445.github.io/musegan/results).

## BinaryMuseGAN

[BinaryMuseGAN](https://salu133445.github.io/bmusegan/) is a follow-up project
of the [MuseGAN](https://salu133445.github.io/musegan/) project.

In this project, we first investigate how the real-valued piano-rolls generated
by the generator may lead to difficulties in training the discriminator for
CNN-based models. To overcome the binarization issue, we propose to append to
the generator an additional refiner network, which try to refine the real-valued
predictions generated by the pretrained generator to binary-valued ones. The
proposed model is able to directly generate binary-valued piano-rolls at test
time.

We trained the network with
[Lakh Pianoroll Dataset](https://salu133445.github.io/lakh-pianoroll-dataset/)
(LPD). We use the model to generate four-bar musical phrases consisting of eight
tracks: *Drums*, *Piano*, *Guitar*, *Bass*, *Ensemble*, *Reed*, *Synth Lead* and
*Synth Pad*. Audio samples are available
[here](https://salu133445.github.io/bmusegan/samples).

## Run the code

### Prepare Training Data

- Prepare your own data or download our training data

  The array will be reshaped to (-1, `num_bar`, `num_timestep`, `num_pitch`,
  `num_track`). These variables are defined in `config.py`.

  - [`lastfm_alternative_5b_phrase.npy`](https://drive.google.com/uc?export=download&id=1F7J5n9uOPqViBYpoPT5GvE4PjCWhOyWc) (2.1 GB)
    contains 12,444 four-bar phrases from 2,074 songs with *alternative* tags.
    The shape is (2074, 6, 4, 96, 84, 5). The five tracks are *Drums*, *Piano*,
    *Guitar*, *Bass* and *Strings*.
  - [`lastfm_alternative_8b_phrase.npy`](https://drive.google.com/uc?export=download&id=1x3CeSqE6ElWa6V7ueNl8FKPFmMoyu4ED) (3.6 GB)
    contains 13,746 four-bar phrases from 2,291 songs with *alternative* tags.
    The shape is (2291, 6, 4, 96, 84, 8). The eight tracks are *Drums*, *Piano*,
    *Guitar*, *Bass*, *Ensemble*, *Reed*, *Synth Lead* and *Synth Pad*.
  - Download the data with this [script](training_data/download.sh).

- (optional) Save the training data to shared memory with this [script](training_data/store_to_sa.py).

- Specify training data path and location in `config.py`. (see below)

### Configuration

Modify `config.py` for configuration.

- Quick setup

  Change the values in the dictionary `SETUP` for a quick setup. Documentation
  is provided right after each key.

- More configuration options

  Four dictionaries `EXP_CONFIG`, `DATA_CONFIG`, `MODEL_CONFIG` and
  `TRAIN_CONFIG` define experiment-, data-, model- and training-related
  configuration variables, respectively.

  > The automatically-determined experiment name is based only on the values
defined in the dictionary `SETUP`, so remember to provide the experiment name
manually (so that you won't overwrite a trained model).

### Run

```sh
python main.py
```

## Papers

- Hao-Wen Dong and Yi-Hsuan Yang,
  "Convolutional Generative Adversarial Networks with Binary Neurons for
  Polyphonic Music Generation",
  *arXiv preprint, arXiv:1804.09399*, 2018.
  [[arxiv](https://arxiv.org/abs/1804.09399)]

- Hao-Wen Dong\*, Wen-Yi Hsiao\*, Li-Chia Yang and Yi-Hsuan Yang,
  "MuseGAN: Multi-track Sequential Generative Adversarial Networks for
  Symbolic Music Generation and Accompaniment,"
  in *AAAI Conference on Artificial Intelligence* (AAAI), 2018.
  [[arxiv](http://arxiv.org/abs/1709.06298)]
  [[slides](https://salu133445.github.io/musegan/pdf/musegan-aaai2018-slides.pdf)]

- Hao-Wen Dong\*, Wen-Yi Hsiao\*, Li-Chia Yang and Yi-Hsuan Yang,
  "MuseGAN: Demonstration of a Convolutional GAN Based Model for Generating
  Multi-track Piano-rolls,"
  in *ISMIR Late-Breaking and Demo Session*, 2017.
  (non-peer reviewed two-page extended abstract)
  [[paper](https://salu133445.github.io/musegan/pdf/musegan-ismir2017-lbd-paper.pdf)]
  [[poster](https://salu133445.github.io/musegan/pdf/musegan-ismir2017-lbd-poster.pdf)]

\* *These authors contributed equally to this work.*
