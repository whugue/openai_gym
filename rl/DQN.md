# Deep Q Learning notes


```
discounted future reward, with discount factor γ
R[t] = r[t] + γ r[t+1] + γ^2 r[t+2] + ...
R[t] = r[t] + γ R[t+1]
define function to calc best score as end game after performing action a in state s,
i.e. max discount future reward
Q(s_t, a_t) = max_π R[t+1]

where π is the policy, to yield the highest Q val of all actions
s.t. π(s) = argmax_a Q(s, a)

obtain by Bellman equation
Q(s, a) = r + γ max_a' Q(s', a')

can approx iteratively using table
by carry out a, obs reward r and new state s', with max a'
Q(s, a) = Q(s, a) - α Q(s, a) + α(r + γ max_a' Q(s', a'))

The above can be done by a simple table,
but we can use a neural net to represent Q function,
taking s, a, outputting single Q(s,a), or even better, 
taking s (observation space dim), outputting Q(s, a) for a in A (number of output units same a num_actions)
then output (real values) can be regressed, optimized with simple square loss:
L = 0.5*(r + γ max_a' Q(s', a') - Q(s,a))^2
inside the () is target minus prediction

Algo:
given a transition <s, a, r, s'>, do update Q by:
1. Do a feedforward pass with s to get predicted Q vals for all actions in A
2. Do a feedforward pass for next state s' and calc max over all output units max_a' Q(s', a')
3. Set Q-value TARGET (like target Y) for action a to r + γ max_a' Q(s', a'). For other actions, set TARGET as the same returned from (1.), i.e. with 0 errors.
4. update weights using backprop


Experience replay:
all experience <s, a, r, s'> need to be stored in replay memory
Then training, pick random samples instead of the latest
to break the similarity of subsequent training that would drive into local minimum

Exploration-exploitation:
do ε-greedy exploration - with prob ε to choose random action, else go with greedy action with highest Q-value
decrease ε over time from 1 to 0.1

Deep Q-learning algo:
init replay memory D
init action-value fn Q with random weights
observe initial state s
repeat
  select an action a
    with prob ε select a random action
    otherwise select a = argmax_a' Q(s, a') (step 1. above)
  carry out a
  observe reward r and new state s'
  store exp <s, a, r, s'> in replay memory D

  sample random transitions <ss, aa, rr, ss'> from D
  calculate target for each minibatch transition
    if ss' is terminal state then tt = rr
    otherwise set tt = rr + γ max_a' Q(s', a') (from step 2, 3 above)
  train the Q network using (tt - Q(ss, aa))^2 as loss (backprop step 4 above)

  s = s'

until terminated

p/s there are more tricks, target network, error clipping, reward clipping etc.
```