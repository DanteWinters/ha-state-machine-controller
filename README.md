# Introduction

The goal of this project is to have a state machine controller that can easily be used to implement state machine systems.

Currently, this repository is conceptual only. Once concept is proven, the README will be updated with instructions on how to use it.

## State machine definition

A state machine is a system that is designed and implemented around set states. They are often used in embedded systems.
It can only exist within those states and will execute code for the state that it is in, or entering. One variable controls the state that the system is in. From there, it only takes actions that are defined within that state. States can have an 'on-entry' and 'on-exit' functionality.

Here is an example. We define the state machine for lights in a room. These lights have 2 states `ON` and `OFF`.

- `OFF`
  - `on-entry` - Switch off the light
  - Listens to a motion sensor. If motion is detected, it changes to the `ON` state.
  - `on-exit` - None
- `ON`
  - `on-entry` - Switch on the light. Start a timer for 5 minutes.
  - Listens to a motion sensor and the timer. If motion is detected, restart the timer. If the timer runs out, change to `OFF` state.
  - `on-exit` - None
- Default state: `OFF`

The default state is for when the system starts up initially, or if something happens that the systems jumps to an undefined state.


There is a discussion on the HA forum that can be found [here](https://community.home-assistant.io/t/complex-automations-state-machine/335368) about implementing it.

## Roadmap

- `YAML` definition. The commands will be stored as `YAML` files. It will be best to save each state as an individual file. This means backups are easier and each file can be reloaded on change without affecting others.
- `Listeners`. Have the system jump through states.
- `UI`. Have an easy UI for implementing systems.
- `Timers`. Instead of using timers that need to be created for each machine, the goal will be to use timestamps as a comparative state.
