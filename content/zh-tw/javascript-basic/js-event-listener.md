+++
title = 'JavaScript 事件監聽器'
weight = 5
+++

## JavaScript 瀏覽器端

### 事件監聽器 (EventListener)

以下範例是為 `#target` 註冊一個事件監聽器：

```js
document.querySelector('#target').addEventListener('click', (e) => {
  e.preventDefault(); // 取消事件原本的動作。
  e.stopPropagation(); // 取消事件傳遞。
  e.stopImmediatePropagation(); // 取消事件傳遞，包含同一元素註冊的監聽器。
  console.log(e.currentTarget === document.querySelector('#target'));
});
```

### 事件 (Event Objects)

以下是 HTML 常用的事件：

| **Class**           | **Event**            | **Inheritance**                          |
| ------------------- | -------------------- | ---------------------------------------- |
| Event               | `DOMContentLoaded`   | `.`                                      |
| UIEvent             | `abort`              | `.` → `Event`                            |
|                     | `beforeunload`       |                                          |
|                     | `error`              |                                          |
|                     | `load`               |                                          |
|                     | `resize`             |                                          |
|                     | `scroll`             |                                          |
|                     | `select`             |                                          |
|                     | `unload`             |                                          |
| InputEvent          | `input`              | `.` → `UIEvent` → `Event`                |
| FocusEvent          | `focus`              | `.` → `UIEvent` → `Event`                |
|                     | `focusin`            |                                          |
|                     | `blur`               |                                          |
|                     | `focusout`           |                                          |
| KeyboardEvent       | `keydown`            | `.` → `UIEvent` → `Event`                |
|                     | `keypress`           |                                          |
|                     | `keyup`              |                                          |
| TouchEvent          | `touchstart`         | `.` → `UIEvent` → `Event`                |
|                     | `touchmove`          |                                          |
|                     | `touchend`           |                                          |
|                     | `touchcancel`        |                                          |
| MouseEvent          | `click`              | `.` → `UIEvent` → `Event`                |
|                     | `contextmenu`        |                                          |
|                     | `dblclick`           |                                          |
|                     | `mousemove`          |                                          |
|                     | `mousedown`          |                                          |
|                     | `mouseup`            |                                          |
|                     | `mouseenter`         |                                          |
|                     | `mouseleave`         |                                          |
| WheelEvent          | `wheel`              | `.` → `MouseEvent` → `UIEvent` → `Event` |
| DragEvent           | `drag`               | `.` → `MouseEvent` → `UIEvent` → `Event` |
|                     | `dragstart`          |                                          |
|                     | `dragend`            |                                          |
|                     | `dragenter`          |                                          |
|                     | `dragleave`          |                                          |
|                     | `dragover`           |                                          |
|                     | `drop`               |                                          |
| AnimationEvent      | `animationstart`     | `.` → `Event`                            |
|                     | `animationiteration` |                                          |
|                     | `animationend`       |                                          |
| ClipboardEvent      | `cut`                | `.` → `Event`                            |
|                     | `copy`               |                                          |
|                     | `paste`              |                                          |
| HashChangeEvent     | `hashchange`         | `.` → `Event`                            |
| PageTransitionEvent | `pageshow`           | `.` → `Event`                            |
|                     | `pagehide`           |                                          |
| PopStateEvent       | `popstate`           | `.` → `Event`                            |
| ProgressEvent       | `loadstart`          | `.` → `Event`                            |
|                     | `error`              |                                          |
| StorageEvent        | `storage`            | `.` → `Event`                            |
| TransitionEvent     | `transitionend`      | `.` → `Event`                            |
