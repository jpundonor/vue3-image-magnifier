# Vue Image Magnifier

## Overview

The **Vue Image Magnifier** component allows you to add a zoom effect on images in your Vue application. Users can hover over or touch the image to see a magnified section of it. The component is highly customizable, offering options for zoom level, dimensions, border style, and more.


[![npm](https://img.shields.io/npm/v/vue3-image-magnifier?color=%2300f)](https://www.npmjs.com/package/vue3-image-magnifier)
[![npm bundle size](https://img.shields.io/bundlephobia/minzip/vue3-image-magnifier)](https://bundlephobia.com/package/vue3-image-magnifier)
![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)

![Screenshot Image Magnifier](screenshots/image.png) 

## Installation

```bash
npm install vue3-image-magnifier
```


## Requirements

- [Vue 3](https://vuejs.org/) or higher

## Usage
```bash
<template>
  <ImageMagnifier src="https://example.com/image.jpg" :zoomLevel="3" />
</template>

<script>
import ImageMagnifier from 'vue-image-magnifier';

export default {
  components: {
    ImageMagnifier,
  },
};
</script>
```

## Props

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `src` | String | Required | URL of the image to magnify. |
| `zoomLevel` | Number | `2` | The intensity level for the zoom effect. |
| `zoomWidth` | Number | `200` | The width (in pixels) of the magnified area. |
| `zoomHeight` | Number | `200` |	The height (in pixels) of the magnified area. |
| `zoomBorder` | String | `2px solid #333` | CSS border style for the zoom area. |
| `zoomRadius` | String | `5px` | CSS border-radius for the zoom area. |
| `autoZoom` | Boolean | `true` | If true, the zoom effect is activated on mouse move or touch automatically. |


## Events

The component supports both mouse and touch events:

#### **Mouse Events**
- `@mousemove`: Activates and updates the zoom when moving the mouse.
- `@mouseleave`: Hides the zoom area when the mouse leaves the image.
- `@click`: Toggles the zoom display when `autoZoom` is disabled.

#### **Touch Events**
- `@touchstart`: Activates the zoom on touch.
- `@touchmove`: Updates the zoom position during touch.
- `@touchend`: Hides the zoom when the touch ends.


## Contributing

Contributions are welcome! Feel free to open an issue or a pull request if you have any ideas, questions, or suggestions.


# License
This project is licensed under the MIT License.