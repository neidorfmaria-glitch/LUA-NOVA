"""Two-dimensional orbit simulation using Euler and RK4 integration."""

from __future__ import annotations

import math
from dataclasses import dataclass
from typing import Callable


# SI units: metres, seconds, kilograms
G = 6.67430e-11
CENTRAL_MASS = 5.972e24
MU = G * CENTRAL_MASS


@dataclass
class State:
    """Position and velocity of the orbiting body."""

    x: float
    y: float
    vx: float
    vy: float


def acceleration(x: float, y: float) -> tuple[float, float]:
    """Return gravitational acceleration at position (x, y)."""

    radius = math.hypot(x, y)

    if radius == 0.0:
        raise ValueError("Gravitational acceleration is undefined at the origin.")

    factor = -MU / radius**3
    return factor * x, factor * y


def derivatives(state: State) -> State:
    """Return dx/dt, dy/dt, dvx/dt, and dvy/dt."""

    ax, ay = acceleration(state.x, state.y)
    return State(state.vx, state.vy, ax, ay)


def add_scaled(state: State, derivative: State, scale: float) -> State:
    """Return state + scale * derivative."""

    return State(
        state.x + scale * derivative.x,
        state.y + scale * derivative.y,
        state.vx + scale * derivative.vx,
        state.vy + scale * derivative.vy,
    )


def euler_step(state: State, dt: float) -> State:
    """Advance one step using semi-implicit Euler integration."""

    derivative = derivatives(state)

    # Update velocity first, then position.
    vx = state.vx + derivative.vx * dt
    vy = state.vy + derivative.vy * dt

    return State(
        state.x + vx * dt,
        state.y + vy * dt,
        vx,
        vy,
    )


def rk4_step(state: State, dt: float) -> State:
    """Advance one step using fourth-order Runge-Kutta integration."""

    k1 = derivatives(state)
    k2 = derivatives(add_scaled(state, k1, dt / 2.0))
    k3 = derivatives(add_scaled(state, k2, dt / 2.0))
    k4 = derivatives(add_scaled(state, k3, dt))

    return State(
        state.x + dt * (k1.x + 2*k2.x + 2*k3.x + k4.x) / 6.0,
        state.y + dt * (k1.y + 2*k2.y + 2*k3.y + k4.y) / 6.0,
        state.vx + dt * (k1.vx + 2*k2.vx + 2*k3.vx + k4.vx) / 6.0,
        state.vy + dt * (k1.vy + 2*k2.vy + 2*k3.vy + k4.vy) / 6.0,
    )


def simulate(
    initial_state: State,
    dt: float,
    steps: int,
    step_function: Callable[[State, float], State],
) -> list[State]:
    """Return the state at every simulation step, including the initial state."""

    if dt <= 0.0:
        raise ValueError("dt must be greater than zero.")

    if steps < 0:
        raise ValueError("steps must not be negative.")

    states = [initial_state]
    state = initial_state

    for _ in range(steps):
        state = step_function(state, dt)
        states.append(state)

    return states


def specific_energy(state: State) -> float:
    """Return specific orbital energy in joules per kilogram."""

    speed_squared = state.vx**2 + state.vy**2
    radius = math.hypot(state.x, state.y)
    return 0.5 * speed_squared - MU / radius


def angular_momentum(state: State) -> float:
    """Return specific angular momentum in m²/s."""

    return state.x * state.vy - state.y * state.vx


def print_summary(method: str, initial: State, final: State) -> None:
    """Print the final state and numerical conservation errors."""

    initial_energy = specific_energy(initial)
    final_energy = specific_energy(final)

    initial_momentum = angular_momentum(initial)
    final_momentum = angular_momentum(final)

    energy_error = abs((final_energy - initial_energy) / initial_energy)
    momentum_error = abs((final_momentum - initial_momentum) / initial_momentum)

    print(f"\n{method}")
    print(f"Final position: x={final.x:.3f} m, y={final.y:.3f} m")
    print(f"Final velocity: vx={final.vx:.3f} m/s, vy={final.vy:.3f} m/s")
    print(f"Relative energy error: {energy_error:.3e}")
    print(f"Relative angular-momentum error: {momentum_error:.3e}")


def main() -> None:
    initial_state = State(
        x=7.0e6,
        y=0.0,
        vx=0.0,
        vy=7.5e3,
    )

    # About 100 seconds with the original settings.
    dt = 0.001
    steps = 100_000

    euler_states = simulate(initial_state, dt, steps, euler_step)
    rk4_states = simulate(initial_state, dt, steps, rk4_step)

    print_summary("Semi-implicit Euler", initial_state, euler_states[-1])
    print_summary("RK4", initial_state, rk4_states[-1])


if __name__ == "__main__":
    main()
