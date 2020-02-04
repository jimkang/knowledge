# Web Audio

- Oscillator nodes cannot be reused
- You can't play more than one AudioContext at a time; everything is expected to be done in a single context. When you get a new context and start playing through it, the old ones stop.
