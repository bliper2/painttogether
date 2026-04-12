# 🎨 PaintTogether — Setup Guide

A real-time multiplayer painting canvas.  
Everyone who visits the page **shares the same canvas and sees each other paint live.**

## Controls

| Action         | Shortcut        |
|----------------|-----------------|
| Pen tool       | `P`             |
| Eraser tool    | `E`             |
| Brush smaller  | `[`             |
| Brush bigger   | `]`             |
| Save as PNG    | Right panel button |
| Clear canvas   | Right panel button (clears for everyone) |

---

## How it works

- Strokes are pushed to **Firebase Realtime Database** as you draw
- All connected clients receive new strokes instantly via WebSocket
- Remote cursors show where other painters are moving
- Online users list updates automatically when people join/leave
- Canvas persists between sessions (clears only when someone presses Clear)
