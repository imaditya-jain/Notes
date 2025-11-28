# React Fiber

React Fiber is the new reconciliation engine introduced in React 16. It makes React faster, interruptible, and smarter.

## Why Fiber Was Needed

- Old React used a synchronous, recursive render mechanism that:
- blocked the UI when components were large
- couldn’t split rendering into smaller pieces
- couldn’t pause work
- couldn’t resume work
- couldn’t abort work
- couldn’t prioritize urgent tasks

This caused laggy typing, janky animations, and slow updates on heavy UI trees.

## What Fiber Introduced

Fiber gives React the ability to:
- split rendering work into small chunks
- pause rendering anytime
- resume work later
- abort unnecessary work
- prioritize important tasks (like typing and clicks)
- maintain a smooth and responsive UI

## The Fiber Node

At the core of Fiber is the "Fiber Node," a JavaScript object that represents a unit of work in the React tree. Each Fiber Node contains information about the component, its state, props, and effects.

Each Fiber Node stores:

- component type
- props & state
- pending updates
- side effects
- priority
- pointers: ```child, sibling, return```

These pointers form a tree-like linked list that React can walk without recursion, allowing pausing/resuming work.

## Two-Phase Rendering

Fiber processes updates in two phases:'

### What is reconciliation?
The algorithm React uses to diff one tree with another to determine which parts need to be changed.

**Render Phase (Reconciliation)**

- Builds a work-in-progress tree
- Can be paused, resumed, or aborted
- Calculates changes (diffing)

**Commit Phase**
- Applies changes to the DOM
- Synchronous and fast
- Cannot be paused

## Double Buffering

React keeps two trees:

- Current Fiber Tree → what’s on screen
- Work-in-Progress Tree → next UI state

When ready, React swaps them efficiently.

## Prioritized Scheduling

Fiber introduces a priority system (lanes), ensuring:

- high-priority updates (typing, clicks) run first
- low-priority work (background rendering) waits

This is the foundation for Concurrent Mode and Time-Slicing.

## Conclusion

React Fiber revolutionized how React handles rendering, making it more efficient and responsive. It laid the groundwork for advanced features like Concurrent Mode, enabling developers to build smoother user experiences.