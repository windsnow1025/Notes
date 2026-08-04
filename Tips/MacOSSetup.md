# MacOS Setup

- View hidden items in finder
```bash
defaults write com.apple.Finder AppleShowAllFiles YES
```

- Disable Mouse Acceleration
  - `Mouse` >> `Advanced...` >> `Turn off Pointer acceleration`

- Trackpad Settings
  - `Trackpad Gestures` >> `More Gestures`
    - `Swipe between pages`: `Scroll Left or Right with Two Fingers`
    - `App Exposé`: `Swipe Down with Four Fingers`
  - Pointer Control
    - `Trackpad Options`
      - `Use trackpad for dragging`
      - `Dragging style`: `Three Finger Drag`

- Disable clicking wallpaper to show desktop
  - `Desktop & Dock` >> `Desktop & Stage Manager`
    - `Click wallpaper to show desktop`: `Only in Stage Manager`

- Terminal Enable Comments
  ```bash
  setopt interactive_comments
  ```

- Prevent Sleeping when Display Off
  - `Battery` >> `Options...`
    - `Prevent automatic sleeping on power adapter when the display is off`

- Set default app for a file type
  - Select a file >> Command + I
    - `Open with`, `Change All...`
