---
layout: page
title: CXSOM RL - Vertical Rocket Control
description: Self-organizing maps for predictive control of a vertical rocket.
img:
importance: 8
category: robotics
redirect: https://github.com/Ekeichi/cxsom-rl-2
---

Project developed at CentraleSupélec using connected CXSOM maps to control a vertical rocket. The architecture used maps representing rocket velocity, distance from the target altitude, and acceleration.

The goal was to remove acceleration from the input and predict it from the learned map dynamics, evaluating whether the SOM-based architecture could control the rocket while the target altitude changed periodically.

**Tools and topics:** CXSOM, self-organizing maps, reinforcement learning, predictive control.

Related documentation: [CXSOM presentation](https://frezza.pages.centralesupelec.fr/cxsom-web/presentation/main/index.html).
