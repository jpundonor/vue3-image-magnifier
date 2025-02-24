<template>
  <div
    class="magnifier-container"
    role="button"
    aria-label="Image magnifier"
    tabindex="0"
    @click="onClick"
    @keydown="onkeydown"
    @mousemove="onMouseMove"
    @mouseleave="onMouseLeave"
    @touchstart="onTouchStart"
    @touchmove="handleMove"
    @touchend="onTouchEnd"
  >
    <img
      :src="src"
      class="magnifier-image"
      ref="imageRef"
      :alt="alt"
    />
    <div
      v-if="showZoom"
      class="zoom-result"
      :style="zoomStyle"
      aria-hidden="true"
    ></div>
    <span class="sr-only">
      Use the mouse or the keyboard (Enter or Space) to activate the magnifier.
    </span>
  </div>
</template>

<script>
/**
 * Vue Image Magnifier Component
 *
 * This component provides a zoom effect on an image when the user hovers
 * or touches the image. The zoom area displays a magnified section of the image.
 *
 * Props:
 * - src (String, required): The URL of the image to magnify.
 * - zoomLevel (Number, default: 2): The intensity of the zoom.
 * - zoomWidth (Number, default: 200): The width of the magnified area.
 * - zoomHeight (Number, default: 200): The height of the magnified area.
 * - zoomBorder (String, default: "2px solid #333"): The border style for the zoom area.
 * - zoomRadius (String, default: "5px"): The border radius for the zoom area.
 * - autoZoom (Boolean, default: true): If true, the zoom activates on mouse move.
 */
export default {
  props: {
    src: {
      type: String,
      required: true,
    },
    alt: {
      type: String,
      default: "Image to magnify",
    },
    zoomLevel: {
      type: Number,
      default: 2,
    },
    zoomWidth: {
      type: Number,
      default: 200,
    },
    zoomHeight: {
      type: Number,
      default: 200,
    },
    zoomBorder: {
      type: String,
      default: "2px solid #333",
    },
    zoomRadius: {
      type: String,
      default: "5px",
    },
    autoZoom: {
      type: Boolean,
      default: true,
    },
  },
  data() {
    return {
      showZoom: false, // Controls the visibility of the zoom area
      zoomStyle: {}, // Holds the dinamic styles settings for the zoom effect
    };
  },
  methods: {
    /**
     * Toggles the zoom display on click when autoZoom is disabled.
     */
    onClick() {
      if (!this.autoZoom) {
        this.showZoom = !this.showZoom;
      }
    },

    /**
     * Handles the keydown event to activate the zoom area when the Enter or Space key is pressed.
     *
     * @param {KeyboardEvent} event - The keydown event.
     */	
    onkeydown(event) {
      if (!this.autoZoom && event.key === "Enter" || event.key === " ") {
        event.preventDefault();
        this.onClick();
      }
    },

    /**
     * Updates the zoom style based on the provided x and y coordinates.
     * Calculates the position of the zoom area and the corresponding background position.
     *
     * @param {Object} param0 - Object containing the x and y coordinates.
     */
    updateZoomStyle({ x, y }) {
      const image = this.$refs.imageRef;
      const rect = image.getBoundingClientRect();

      // Calculate cursor position relative to the image
      const relX = x - rect.left;
      const relY = y - rect.top;

      // Determine the ratio of the cursor position (0 to 1)
      const ratioX = relX / rect.width;
      const ratioY = relY / rect.height;

      // Total dimensions for the background image at the zoom level
      const bgWidth = image.width * this.zoomLevel;
      const bgHeight = image.height * this.zoomLevel;

      // Determine the maximum background shift to keep the zoom area in range
      const maxX = bgWidth - this.zoomWidth;
      const maxY = bgHeight - this.zoomHeight;

      // Calculate the background position based on the ratio
      const backgroundPosX = ratioX * maxX;
      const backgroundPosY = ratioY * maxY;

      // Update the style for the zoom area
      this.zoomStyle = {
        left: `${relX - this.zoomWidth / 2}px`,
        top: `${relY - this.zoomHeight / 2}px`,
        width: `${this.zoomWidth}px`,
        height: `${this.zoomHeight}px`,
        border: this.zoomBorder,
        borderRadius: this.zoomRadius,

        backgroundImage: `url(${this.src})`,
        backgroundSize: `${bgWidth}px ${bgHeight}px`,
        backgroundPosition: `-${backgroundPosX}px -${backgroundPosY}px`,
      };
    },

    /**
     * Handles both mouse and touch move events.
     * Detects the type of event and extracts the appropriate x and y coordinates.
     *
     * @param {Event} event - The mouse or touch event.
     */
    handleMove(event) {
      let x, y;
      if (event.type.startsWith("touch")) {
        const touch = event.touches[0];
        x = touch.clientX;
        y = touch.clientY;
        // Prevent default to avoid scrolling while touching
        event.preventDefault();
      } else {
        x = event.clientX;
        y = event.clientY;
      }
      this.updateZoomStyle({ x, y });
    },

    /**
     * Handles mouse move events.
     * When autoZoom is enabled, the zoom area is activated and updated continuously.
     *
     * @param {MouseEvent} event - The mouse move event.
     */
    onMouseMove(event) {
      if (this.autoZoom) {
        this.showZoom = true;
        this.handleMove(event);
      } else {
        if (this.showZoom) {
          this.handleMove(event);
        }
      }
    },

    /**
     * Hides the zoom area when the mouse leaves the image.
     */
    onMouseLeave() {
      this.showZoom = false;
    },

    /**
     * Activates the zoom area when a touch event starts.
     *
     * @param {TouchEvent} event - The touch start event.
     */
    onTouchStart(event) {
      this.showZoom = true;
      this.handleMove(event);
    },

    /**
     * Hides the zoom area when the touch event ends.
     */
    onTouchEnd() {
      this.showZoom = false;
    },
  },
};
</script>

<style scoped>
.magnifier-container {
  position: relative;
  display: inline-block;
}

.magnifier-image {
  width: 100%;
  height: 100%;
  cursor: zoom-in;
}

.zoom-result {
  position: absolute;
  background-repeat: no-repeat;
  box-shadow: 2px 2px 10px rgba(0, 0, 0, 0.5);
  pointer-events: none;
}

.sr-only {
  position: absolute;
  width: 1px;
  height: 1px;
  padding: 0;
  margin: -1px;
  overflow: hidden;
  clip: rect(0, 0, 0, 0);
  border: 0;
}
</style>
