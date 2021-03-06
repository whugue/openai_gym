# OpenAI Gym [![CircleCI](https://circleci.com/gh/kengz/openai_gym.svg?style=shield)](https://circleci.com/gh/kengz/openai_gym) [![Code Climate](https://codeclimate.com/github/kengz/openai_gym/badges/gpa.svg)](https://codeclimate.com/github/kengz/openai_gym)

[OpenAI Gym Doc](https://gym.openai.com/docs) | [OpenAI Gym Github](https://github.com/openai/gym) | [RL intro](https://gym.openai.com/docs/rl)

Working out at the (OpenAI) gym. **Note this is still under development, but will be ready before Nov 5**


## Installation

```shell
git clone https://github.com/kengz/openai_gym.git
cd openai_gym
python setup.py install
```

*Note that by default it installs Tensorflow for Python3 on MacOS. [Choose the correct binary to install from TF.](https://www.tensorflow.org/versions/r0.11/get_started/os_setup.html#pip-installation)*

```shell
# for example, TF for Python2, MacOS
export TF_BINARY_URL=https://storage.googleapis.com/tensorflow/mac/cpu/tensorflow-0.11.0rc1-py2-none-any.whl
# or Linux CPU-only, Python3.5
export TF_BINARY_URL=https://storage.googleapis.com/tensorflow/linux/cpu/tensorflow-0.11.0rc1-cp35-cp35m-linux_x86_64.whl
sudo pip install --upgrade $TF_BINARY_URL
```


## Usage

Run the scripts inside the `rl/` folder. It will contain:
- `run_gym_tour.py`: a tour of the OpenAI gym
- `run_tabular_q.py`: a tabular q-learner
- `run_dqn.py`: a NN-based q-learner

To save a log, run like so:

```shell
python rl/run_dqn.py 2>&1 | tee run.log
```


## Roadmap

- [x]get the gym tour done
- [x]add `util.py`, refactor system
- [x]add and build test code
- [x]clear the DQN class off the TF code, to make it backend-agnostic
- [x]faster CI builds, with real runs of rl in test
- [meh]tag memory to indicate if it's from random action
- [x]memory-decay - solve the problem caused by having majority of random experience
- [x]YAYY. get NN q-learner working and solve the cartpole problem
- [x]add visualization: average/total reward, loss(we'll see)
- [x]get the tabular q-learner working
- better parameter selection, to tune for a problem (can use the parallelization in util.py)
- parametrize epsilon anneal steps by MAX_EPISODES etc, so parameter selection can be more automatic across different problems. Use sine x exp decay graph?
- solve the stability problem - some runs start out bad and end up bad too
- do policy iteration (ch 4 from text)
- other more advanced algos
- add some graphs for repo page


## Authors

- Wah Loon Keng
- Laura Graesser
