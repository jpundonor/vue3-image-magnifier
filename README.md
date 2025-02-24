# Vue Image Magnifier

## Overview

The **Vue Image Magnifier** component allows you to add a zoom effect on images in your Vue application. Users can hover over or touch the image to see a magnified section of it. The component is highly customizable, offering options for zoom level, dimensions, border style, and more.


[![npm](https://img.shields.io/npm/v/vue3-image-magnifier?color=%2300f)](https://www.npmjs.com/package/vue3-image-magnifier)
[![npm bundle size](https://img.shields.io/bundlephobia/minzip/vue3-image-magnifier)](https://bundlephobia.com/package/vue3-image-magnifier)
![NPM Downloads](https://img.shields.io/npm/dw/vue3-image-magnifier)
![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)

![Screenshot Image Magnifier](screenshots/image.png) 

## Features

- **Hover or touch** to activate the zoom effect.
- **AutoZoom** option to automatically enable zoom on mouse move.
- **Keyboard support** to toggle zoom with Enter or Space (when `autoZoom` is disabled).
- **ARIA attributes** (`role="button"`, `tabindex="0"`, `aria-label`) for screen reader compatibility.
- **Customization** for zoom level, zoom area size, border style, radius, etc.

## Installation

```bash
npm install vue3-image-magnifier
```


## Requirements

- [Vue 3](https://vuejs.org/) or higher

## Usage
```vue
<template>
  <ImageMagnifier src="https://example.com/image.jpg" :zoomLevel="3" />
</template>

<script>
import ImageMagnifier from 'vue3-image-magnifier';

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
| `alt` | String | `Image to magnify` | The alt text for the image (for accessibility). |
| `zoomLevel` | Number | `2` | The intensity level for the zoom effect. |
| `zoomWidth` | Number | `200` | The width (in pixels) of the magnified area. |
| `zoomHeight` | Number | `200` |	The height (in pixels) of the magnified area. |
| `zoomBorder` | String | `2px solid #333` | CSS border style for the zoom area. |
| `zoomRadius` | String | `5px` | CSS border-radius for the zoom area. |
| `autoZoom` | Boolean | `true` | If true, the zoom effect is activated on mouse move or touch automatically. |


## Accessibility
- The main container uses `role="button"`, `tabindex="0"`, and `aria-label` to be navigable via keyboard.
- When `autoZoom` is disabled, you can toggle the zoom with Enter or Space.
- The zoom area (floating div) uses `aria-hidden="true"` so it’s ignored by screen readers.
- A `.sr-only` label is included to provide extra instructions for screen readers without affecting the visual interface.

## Changelog
See the [CHANGELOG.md](./CHANGELOG.md) for a complete list of changes.

## Contributing

Contributions are welcome! Feel free to open an issue or a pull request if you have any ideas, questions, or suggestions.


## License
This project is licensed under the MIT License.