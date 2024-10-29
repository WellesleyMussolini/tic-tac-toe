<template>
  <section>
    <div
      v-for="index in 9"
      :key="index"
      :class="`cell cell--${index}`"
      @click="$emit('startGame', index - 1)"
    >
      <div class="mark mark--x" v-show="marks[index - 1] === 'X'"></div>
      <div class="mark mark--o" v-show="marks[index - 1] === 'O'"></div>
      <label
        class="label label--x"
        v-show="!marks[index - 1] && shadowVisibility.X"
      ></label>
      <label
        class="label label--o"
        v-show="!marks[index - 1] && shadowVisibility.O"
      ></label>
    </div>
  </section>
</template>

<script>
export default {
  props: {
    shadowVisibility: {
      type: Object,
      required: true,
    },
    marks: {
      type: Array,
      required: true,
    },
  },
};
</script>

<style scoped>
.cell .mark {
  display: none;
}

.cell .mark--x,
.cell .mark--o {
  display: block;
}

.cell .label--x,
.cell .label--o {
  visibility: visible;
}

section {
  flex: 1 1 auto;
  display: grid;
  grid-template: repeat(3, min-content) / repeat(3, min-content);
  justify-content: center;
  align-content: center;
}

.cell {
  position: relative;
  width: 88px;
  height: 88px;
  border: solid 4px #ddd;
}

.cell--1,
.cell--2,
.cell--3 {
  border-top-color: transparent;
}

.cell--1,
.cell--4,
.cell--7 {
  border-left-color: transparent;
}

.cell--3,
.cell--6,
.cell--9 {
  border-right-color: transparent;
}

.cell--7,
.cell--8,
.cell--9 {
  border-bottom-color: transparent;
}

.label {
  position: absolute;
  width: 100%;
  height: 100%;
  cursor: pointer;
  visibility: hidden;
}

.label--x::before {
  content: "";
  position: absolute;
  left: 50%;
  top: 50%;
  width: 80%;
  height: 12px;
  border-radius: 6px;
  background: #f4f4f4;
  transform-origin: center;
  transform: translate(-50%, -50%) rotate(45deg);
  opacity: 0;
  transition: opacity 0.2s;
}

.label--x::after {
  content: "";
  position: absolute;
  left: 50%;
  top: 50%;
  width: 80%;
  height: 12px;
  border-radius: 6px;
  background: #f4f4f4;
  transform-origin: center;
  transform: translate(-50%, -50%) rotate(-45deg);
  opacity: 0;
  transition: opacity 0.2s;
}

.label--o::before {
  content: "";
  position: absolute;
  left: 50%;
  top: 50%;
  width: 80%;
  transform-origin: center;
  opacity: 0;
  transition: opacity 0.2s;
  height: 80%;
  border-radius: 50%;
  transform: translate(-50%, -50%);
  height: 80%;
  border-radius: 50%;
  box-shadow: inset 0 0 0 12px #f0f0f0;
  transform: translate(-50%, -50%);
}

.label:hover::before {
  opacity: 1;
}

.label:hover::after {
  opacity: 1;
}

.mark {
  position: absolute;
  width: 100%;
  height: 100%;
  z-index: 1;
  display: none;
  animation: mark-entrance 0.2s cubic-bezier(0, 0.8, 0.2, 1.2) both;
}

@keyframes mark-entrance {
  from {
    opacity: 0;
    transform: scale(0) rotate(-15deg);
  }
}

.mark--o::before {
  content: "";
  position: absolute;
  left: 50%;
  top: 50%;
  width: 80%;
  height: 80%;
  border-radius: 50%;
  box-shadow: inset 0 0 0 12px #ef908c;
  transform: translate(-50%, -50%);
}

.mark--x::before {
  content: "";
  position: absolute;
  left: 50%;
  top: 50%;
  width: 80%;
  height: 12px;
  border-radius: 6px;
  background: #8c90ef;
  transform-origin: center;
  transform: translate(-50%, -50%) rotate(45deg);
}

.mark--x::after {
  content: "";
  position: absolute;
  left: 50%;
  top: 50%;
  width: 80%;
  height: 12px;
  border-radius: 6px;
  background: #8c90ef;
  transform-origin: center;
  transform: translate(-50%, -50%) rotate(-45deg);
}
</style>
