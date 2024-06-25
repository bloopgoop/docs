---
layout: default
title: What I learned
parent: Simplify
nav_order: 4
---

# What I learned

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

## Electron Framework

[Electronjs] is an open-source framework for building out desktop applications.
It embeds Chromium and [Node.js] so developers can use regular HTML, CSS, and JavaScript.
Here are some things I've learned while developing using electron:

### The Electron Process Model

> Electron inherits its multi-process architecture from Chromium, which makes the framework architecturally very similar to a modern web browser.

There are two types of processes: **main** and **renderer**

#### Main Process

There is a single **main** process for each electron app which runs in a [Node.js] environment. It can require modules and use built in [Node.js] APIs such as the
_File System_ api. The **main** process is also responsible for managing windows and the application lifecycle.

#### Renderer Process

There could be multiple **renderer** processes in an Electron application. The **renderer** process is responsible for displaying web content. All renderer processes should follow web standards, meaning it should be written in HTML, CSS, and JavaScript

### Communication Between Processes

In some cases, a renderer will need to access a [Node.js] API. Before Electron v5, by default, node integration was included in the renderer processes. This method introduced a [vulnerability](https://blog.devsecurity.eu/en/blog/joplin-electron-rce) and is still an option but is no longer recommended. The Electron team now recommends turning `nodeIntegration:false` and using the **Inter-Process Communication(IPC)** as a workaround for this vulnerability.

![Electron Architecture](https://miro.medium.com/v2/resize:fit:1400/1*5G9BFD2ItXo6lv2pinEJrA.png)

The IPC encourages an event-driven architecture by allowing the **main** and **renderer** process to send messages to each other, and performing an action on recieving it.

## React useReducer

While working on the project, I used a [context](https://react.dev/reference/react/useContext) to manage the app's logic. It included a ton of states such as _sliderVolume, masterVolume, loop, shuffle, playlist_ which all needed to be updated when users clicked certain buttons. I initially designed the context to use a [useState](https://react.dev/reference/react/useState) for each of these variables but it resulted in unnecessary rerenders and bugs. To simplify the logic, I used the [useReducer](https://react.dev/reference/react/useReducer) hook to manage the app's complex logic.

Let's look at some old code relating to the _sliderVolume_ state:

```js
const [muted, setMuted] = useState(false);
const [sliderVolume, setSliderVolume] = useState(
  // 0-100
  localStorage.getItem("sliderVolume")
    ? Number(localStorage.getItem("sliderVolume"))
    : 50
);

useEffect(() => {
  if (player) {
    console.log(calcTotalVolume(sliderVolume, masterVolume));
    player.volume = calcTotalVolume(sliderVolume, masterVolume);
  }
  if (sliderVolume === 0) {
    setMuted(true);
  } else {
    setMuted(false);
  }
}, [sliderVolume, masterVolume]);
```

In this code snippet, my component has a _sliderVolume_ state which when changed, sets the _muted_ state depending on the _sliderVolume_ state. This logic unecessarily rerenders the component twice, once when _setSliderVolume_ is called which causes the useEffect to trigger, and a second time when _setMuted_ is called in the useEffect. Here's how this logic is achieved in less lines of code and less rerenders using a reducer:

```js
function playerReducer(state: Player, action) {
  switch (action.type) {
    ...
    case actionTypes.SET_SLIDER_VOLUME:
      state.player.volume = calcTotalVolume(action.payload, state.masterVolume);
      if (action.payload === 0) {
        return { ...state, sliderVolume: action.payload, muted: true };
      } else {
        return { ...state, sliderVolume: action.payload, muted: false };
      }
    ...
```
Overall, the reducer function is less complex and rerenders the component less times.

## TanStack Table
[TanStack Table] is a versatile library for building and manageing data tables in web applications. I used this when creating the playlists table which holds the title, artist, album, duration, etc... for a song. 

![Playlist](/assets/images/playlist.png)

Here is one core component of a TanStack Table:

### [Column Defs](https://tanstack.com/table/latest/docs/guide/column-defs)
Column Defs determine the columns of the table. Each cell is an object with customizable properties and customizable HTML
```js
export const columns: ColumnDef<Song>[] = [
  {
    accessorKey: "title",
    header: "Title",
    cell: ({ row }) => {
      const song = row.original;
      return (
        <div className="flex items-center gap-2 w-full h-full truncate">
          <div className="w-12">
            <Image
              mime={song.image_mime}
              buffer={song.image_buffer}
              alt="cover"
            />
          </div>
          <div className="flex flex-col">
            <div className="font-bold">
              {song.title ? song.title : song.path}
            </div>
            <div className="text-sm text-muted-foreground">
              {song.artist && song.artist}
            </div>
          </div>
        </div>
      );
    },
  },
  ...
  ```

[Node.js]: https://nodejs.org/en
[Electronjs]: https://www.electronjs.org/
[TanStack Table]: https://tanstack.com/table/latest