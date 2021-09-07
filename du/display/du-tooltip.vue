<template>
  <div class="tooltip">
    <div>
      <slot></slot>
    </div>
    <div v-if="label" class="tooltiptext" :class="[classObject[placement]]">
      {{ label }}
    </div>
  </div>
</template>

<script>
export default {
  props: {
    label: { type: String, default: "" },
    placement: { type: String, default: "top" },
  },

  data() {
    return {
      classObject: [
        "top",
        "topLeft",
        "topRight",
        "left",
        "leftTop",
        "leftBottom",
        "bottom",
        "bottomLeft",
        "bottomRight",
        "right",
        "rightTop",
        "rightBottom",
      ].reduce((a, b) => {
        a[b] = `${b}Class`
        return a
      }, {}),
    }
  },
  methods: {},
}
</script>
<style scoped>
.tooltip {
  position: relative;
  cursor: pointer;
  z-index: 10001;
  text-align: center;

  --margin-distance: 12px;
  --tooltiptext-height: 30px;
  --half-tooltiptext-height: 15px;
  --triangle-border-width: 6px;
  --triangle-border-width: 6px;
  --triangle-offset-vertical: 5px;
  --triangle-offset-horizon: 10px;
}

.tooltip .tooltiptext {
  height: 30px;
  line-height: 30px;
  min-width: 20px;
  width: max-content;
  background-color: black;
  color: #fff;
  text-align: center;
  padding: 0px 5px;
  font-size: smaller;
  /* only opacity 0 then the element still is there */
  visibility: hidden;
  opacity: 0;
  transition: all 0.3s;
  
  position: absolute;
}

.tooltip:hover .tooltiptext {
  visibility: visible;
  opacity: 1;
}

.tooltip .tooltiptext::after {
  content: "";
  width: 0;
  height: 0;
  line-height: 0;
  font-size: 0;
  border-width: var(--triangle-border-width);
  border-style: solid;
  position: absolute;
}

/* different placement class */
/* how to make small triangle adaptive? */
/* top effect on father element */
/* translate effect on self element */

/* topClass */
.tooltip .topClass {
  top: calc(-100% - var(--margin-distance));
  left: 50%;
  transform: translate(-50%, 0);
}
.tooltip .topClass::after {
  border-color: black transparent transparent transparent;
  top: 100%;
  left: calc(50% - var(--triangle-border-width));
}

/* bottomClass */
.tooltip .bottomClass {
  bottom: calc(-100% - var(--margin-distance));
  left: 50%;
  transform: translate(-50%, 0);
}
.tooltip .bottomClass::after {
  border-color: transparent transparent black transparent;
  bottom: 100%;
  left: calc(50% - var(--triangle-border-width));
}

/* leftClass */
.tooltip .leftClass {
  top: 0;
  bottom: 0;
  margin-top: auto;
  margin-bottom: auto;
  right: calc(100% + var(--margin-distance));
}
.tooltip .leftClass::after {
  border-color: transparent transparent transparent black;
  top: calc(50% - var(--triangle-border-width));
  left: 100%;
}

/* leftTopClass */
.tooltip .leftTopClass {
  top: 0;
  right: calc(100% + var(--margin-distance));
}
.tooltip .leftTopClass::after {
  border-color: transparent transparent transparent black;
  top: var(--triangle-offset-vertical);
  left: 100%;
}

/* leftBottomClass */
.tooltip .leftBottomClass {
  bottom: 0;
  right: calc(100% + var(--margin-distance));
}
.tooltip .leftBottomClass::after {
  border-color: transparent transparent transparent black;
  bottom: var(--triangle-offset-vertical);
  left: 100%;
}

/* rightClass */
.tooltip .rightClass {
  top: 0;
  bottom: 0;
  margin-top: auto;
  margin-bottom: auto;
  left: calc(100% + var(--margin-distance));
}
.tooltip .rightClass::after {
  border-color: transparent black transparent transparent;
  top: calc(50% - var(--triangle-border-width));
  right: 100%;
}

/* rightTopClass */
.tooltip .rightTopClass {
  top: 0;
  left: calc(100% + var(--margin-distance));
}
.tooltip .rightTopClass::after {
  border-color: transparent black transparent transparent;
  top: var(--triangle-offset-vertical);
  right: 100%;
}

/* rightBottomClass */
.tooltip .rightBottomClass {
  bottom: 0;
  left: calc(100% + var(--margin-distance));
}
.tooltip .rightBottomClass::after {
  border-color: transparent black transparent transparent;
  bottom: var(--triangle-offset-vertical);
  right: 100%;
}

/* topLeftClass */
.tooltip .topLeftClass {
  top: calc(-100% - var(--margin-distance));
}
.tooltip .topLeftClass::after {
  border-color: black transparent transparent transparent;
  top: 100%;
  left: var(--triangle-offset-horizon);
}

/* bottomLeftClass */
.tooltip .bottomLeftClass {
  bottom: calc(-100% - var(--margin-distance));
}
.tooltip .bottomLeftClass::after {
  border-color: transparent transparent black transparent;
  bottom: 100%;
  left: var(--triangle-offset-horizon);
}

/* topRightClass */
.tooltip .topRightClass {
  top: calc(-100% - var(--margin-distance));
  right: 0;
}
.tooltip .topRightClass::after {
  border-color: black transparent transparent transparent;
  top: 100%;
  right: var(--triangle-offset-horizon);
}

/* bottomRightClass */
.tooltip .bottomRightClass {
  bottom: calc(-100% - var(--margin-distance));
  right: 0;
}
.tooltip .bottomRightClass::after {
  border-color: transparent transparent black transparent;
  bottom: 100%;
  right: var(--triangle-offset-horizon);
}
</style>
