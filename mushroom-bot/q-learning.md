---
title: Q-learning
layout: default
parent: Mushroom Bot
nav_order: 3
---
# Q-learning
{: .fs-9 }

> Q-Learning is one model of reinforcement learning, where a function Q(s, a) outputs an estimate of the value of taking action a in state s. 

In this bot's case, the state is the position of character along with the timeframe.

**s = (position, time)**

Actions is defined as the set of all actions the bot can take. Usually
moving up, down, left or right.

**a = {up, down, left, right}**

The reward/Q-value is the mobs defeated by an action in a given timeframe. Since the mobs defeated count can not be negative, I added a default bias of -4 so that the bot may be punished when performing non-optimal movements.

Using these measures, the bot is capable of improving upon its past knowledge using this equation:

***Q(s, a) ⟵ Q(s, a) + α(new value estimate - Q(s, a))***