+++
title = 'JavaScript イベントリスナー'
weight = 5
+++

## JavaScript ブラウザ側

### イベントリスナー (EventListener)

以下の例は `#target` にイベントリスナーを登録する方法です：

```js
document.querySelector('#target').addEventListener('click', (e) => {
  e.preventDefault(); // イベントのデフォルト動作をキャンセルします。
  e.stopPropagation(); // イベントの伝播をキャンセルします。
  e.stopImmediatePropagation(); // イベントの伝播をキャンセルします (同じ要素に登録されたも含めて)。
  console.log(e.currentTarget === document.querySelector('#target'));
});
```

### イベント (Event Objects)

以下はよく使われる HTML イベントです：

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
