# Rotation in Minescript

## Pitch

Given as a number (degrees) |  -90 to 90.

- -90: Directly up
- 0: Directly forward
- 90: Directly Downward

## Yaw

Given as a number (degrees) | -∞ to ∞

Yaw follows the standard trigonometry rules:
- 0 & 360: Represent the same number
- Rotations above 360 and below 0 CAN wrap around
- 90 degrees represent cardinal directions

Additionally, minecraft DOES NOT clamp these values. You can get yaw values like -2573.234 or 7203.10, which is used by both the client and the server.

## Performing Math

When doing trig functions, always convert the units from Degrees to Radians.
