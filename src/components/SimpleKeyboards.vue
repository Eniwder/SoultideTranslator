<template>
  <div :class="keyboardClass"></div>
</template>

<script>
import Keyboard from "simple-keyboard";
import "simple-keyboard/build/css/index.css";

export default {
  name: "SimpleKeyboard",
  props: {
    keyboardClass: {
      default: "simple-keyboard",
      type: String
    },
    input: {
      type: String
    }
  },
  data: () => ({
    keyboard: null
  }),
  mounted() {
    this.keyboard = new Keyboard(this.keyboardClass, {
      onChange: this.onChange,
      onKeyPress: this.onKeyPress,
      newLineOnEnter: true,
      layout: {
        default: [
          "q w e r t y u i o p {bksp}",
          "a s d f g h j k l {enter}",
          "z x c v b n m",
          "{space}"
        ]
      },
      display: {
        '{bksp}': 'BS',
        '{enter}': 'Enter',
        "{space}": 'Space'
      }
    });
  },
  methods: {
    onChange(input) {
      this.$emit("onChange", input);
    },
    onKeyPress(button) {
      this.$emit("onKeyPress", button);

      /**
       * If you want to handle the shift and caps lock buttons
       */
      if (button === "{shift}" || button === "{lock}") this.handleShift();
    },
  },
  watch: {
    input(input) {
      this.keyboard.setInput(input);
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
div {
  font-family: Soultide;
}
</style>
<style>
.hg-button-bksp,
.hg-button-enter,
.hg-button-space {
  font-family: Arial, Helvetica, sans-serif
}

.hg-button {
  color: white;
}

.hg-theme-default {
  background-color: #6d6d6d;
}

.hg-theme-default .hg-button {
  background-color: #19191c;
}
</style>