<template>
  <v-app>
    <v-app-bar color="grey-darken-4" title="Soultide Tarnslator" :elevation="0" density="compact">
      <template v-slot:append>
        <v-btn icon=" mdi-github" href="https://github.com/Eniwder/SoultideTranslator" target="_blank"></v-btn>
      </template>
    </v-app-bar>
    <v-main>
      <div>
        <p>SoulTide</p>
        <v-textarea v-model="text" class="lang-st" rows="3"></v-textarea>
        <SimpleKeyboard @onChange="onVChange" :input="text" />
      </div>
      <div>
        <img src="@/assets/arrow.png" class="arrow">
        <p>English</p>
        <v-textarea v-model="text" class="lang-en" rows="3"></v-textarea>
      </div>
    </v-main>
  </v-app>
</template>

<script setup>
import { ref, watch, onMounted } from 'vue';
import SimpleKeyboard from "./components/SimpleKeyboards.vue";
const text = ref("")

function onVChange(input) {
  text.value = input;
}

onMounted(() => {
  // const _text = window.location.pathname.replace(/.+\/(.+)/, '$1').substring(1);
  const _text = window.location.search.match(/\?text=(.+)/)
  if (_text) {
    text.value = _text[1].replaceAll('%0A', '\n').replaceAll('%20', ' ').replace(/%[a-zA-Z0-9][a-zA-Z0-9]/g, '');
  }
})

watch(text, () => {
  window.history.replaceState(null, '', `?text=${text.value.replaceAll('\n', '%0A')}`);
})

</script>

<style>
main {
  background: linear-gradient(215deg, #616161 29.9%, #386c8f 80%), linear-gradient(304deg, rgba(63, 91, 78, 0.4) 24.9%, #4d363d 91%), linear-gradient(10deg, #1d2f3b 19.9%, #3d4449 50%), linear-gradient(145deg, #5a9c8e 15.9%, #9c8994 40%);
  flex-grow: 1;
  padding: 2em;
  text-align: center;
  background-blend-mode: hard-light;
  display: flex;
  align-items: center;
  justify-content: center;
  --v-layout-top: 64px !important;
  --v-layout-left: 24px !important;
  --v-layout-right: 24px !important;
}

img {
  display: flex;
  width: 12px;
}

@font-face {
  font-family: 'Soultide';
  src: url('@/assets/mySoultideFont.ttf') format('truetype');
}

p {
  font-family: Arial, Helvetica, sans-serif;
  font-size: 16px;
  position: relative;
  color: lightgray;
  top: 32px;
  left: -46%;
  z-index: 2;
  user-select: none;
}

.lang-st {
  font-family: Soultide;
}

.lang-en {
  font-family: 'IBM Plex Sans', Arial, Helvetica, sans-serif;
}

.lang-st textarea {
  font-size: 28px;
}

.lang-en textarea {
  font-size: 32px;
}

.lang-st textarea,
.lang-en textarea {
  background-color: #19191c;
  color: white;
  padding-top: 48px;
  padding-left: 24px;
}

.arrow {
  margin-top: 12px;
  left: 50%;
  position: relative;
}

.v-textarea .v-field__input {
  -webkit-mask-image: none !important;
}
</style>