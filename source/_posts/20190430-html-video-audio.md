
---
title: HTML5 - Video/Audio Element
date: Thu Jan  3 19:28:07 2019
categories: Web Developer Bootcamp
tag:
- front end
- html
---

### HTML5 Video Element

#### Video format for different browsers

- FireFox 3.5+, chrome 5.0+, Opera 10.5+: `.ogg`
- Safari 3.0+, chrome 5.0+, IE 9.0+: `.mp4/H.264`
- FireFox 4.0+, chrome 6.0+, Opera 10.6+: `.webm`

#### Example

1. Multiple video sources

```html
<video width="320" height="240" controls="controls">
    <source src="XXXX.ogg" type="video/ogg">
    <source src="XXXX.mp4" type="video/mp4">
    Your browser doesn't support video element
</video>>
```

2. Single source

```html
<video src="XXXX.ogg" width="320" height="240" controls="controls">
    Your browser doesn't support video element
</video>
```

#### Different attributes

1. two different ways:
    - `controls`
    - `controls="controls"`

2. list of attributes:
- controls: show control menus for the video
- autoplay: `autoplay="autoplay"` will play the video once ready, for my chrome(Version 73.0.3683.103) can only work with `muted` together.
- height/width: pixels 
- muted/loop: as the meaning of word
- poster: url for the display image before playing the video
- preload: 
    + auto: load the entire video when the page loads
    + metadata: only load metadata when the page loads
    + none: not load the video when the page loads (no preview even)

### Video Track

**Problem**

When I tried some online track file starting from `http` with my Chrome browser, it didn't work and complains `Unsafe attempt to load URL`.

#### Example

```html
<video src="video.ogg" width="320" height="240" controls="controls">
    你的浏览器不支持video元素
    <track src="track_chinese.vtt" srclang="zh" kind="subtitles" label="中文" default>
    <track src="track_english.vtt" srclang="en" kind="subtitles" label="English">
</video>
```

When we want to add customized performance for the subtitles, we can use `::cue` in css.



### HTML5 Audio Element

#### Audio format for different browsers

- FireFox 3.5+, chrome 3.0+, Opera 10.5+: `.ogg`
- Safari 3.0+, chrome 3.0+, IE 9.0+: `.mp3`
- FireFox 3.5+, Safari 3.0+, Opera 10.5+: `.wav`

#### Example

Similar to Video element.

1. Multiple audio sources

```html
<audio controls="controls">
    <source src="XXXX.ogg" type="audio/ogg">
    <source src="XXXX.mp3" type="audio/mpeg">
    Your browser doesn't support audio element
</audio>>
```

2. Single audio source

```html
<audio src="XXXX.mp3" controls="controls">
    Your browser doesn't support audio element
</audio>
```
