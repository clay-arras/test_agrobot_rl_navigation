# Robot Navigation Environment

A custom OpenAI Gymnasium environment for robot navigation through procedurally generated mazes, featuring both continuous (physics-based) and discrete movement implementations.

Credits: the continuous environment includes heavily modified files originally from OpenAI Gymnasium CarRacing Environment

## Features

- **Maze Generation**: Procedurally generated mazes with configurable parameters
- **Robot Dynamics**: Physics simulation with realistic movement, including acceleration, braking, and steering
- **Pathfinding**: A\* and Dijkstra's algorithms for optimal path planning
- **Multiple Environments**:
  - Continuous: Box2D physics with realistic robot dynamics
  - Discrete: Grid-based movement for simpler navigation

## Core Components

- **Continuous Environment**: Physics-based robot navigation

  - Box2D physics engine
  - Customizable robot parameters
  - Real-time visualization with Pygame

- **Discrete Environment**: Grid-based movement system

  - Simple state representation
  - Fast execution for RL training

- **Maze Generation & Pathfinding**
  - Configurable maze parameters (size, complexity)
  - A\* pathfinding with diagonal movement
  - Path optimization

## Usage

```python
# Continuous Environment
from continuous_env.robot_obstacles import RobotObstacles

env = RobotObstacles(render_mode="human")
obs, info = env.reset()

# Action space: [steering, gas, brake, reverse]
action = np.array([0.0, 1.0, 0.0, 0.0])  # Move forward
obs, reward, terminated, truncated, info = env.step(action)

# Discrete Environment
from discrete_env.robot_obstacles_env import RobotObstacleEnv

env = RobotObstacleEnv(render_mode="human")
obs, info = env.reset()

# Action space: Discrete(4) - UP, DOWN, LEFT, RIGHT
action = 0  # Move UP
obs, reward, terminated, truncated, info = env.step(action)
```

## Environment Details

### Observation Space

- Continuous: RGB image (96x96x3)
- Discrete: Dict with grid state and agent position

### Action Space

- Continuous: Box(-1, 1, shape=(4,))
- Discrete: Discrete(4)

### Reward Structure

- Sparse reward on reaching target
- Time penalty to encourage efficiency
- Collision penalties in continuous mode

## Dependencies

- gymnasium
- numpy
- pygame
- Box2D (continuous environment only)
