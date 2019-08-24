<template>
  <div id="app" class="app">
    <h1 class="app-header">Vue Emoji Panel</h1>
    <div class="emoji-panel-stack">
      <div class="emoji-panel-demo-text">
        <textarea 
          v-model="emojiPanelDemoText"
          class="emoji-panel-demo-text__input">
        </textarea>
      </div>
      <div class="emoji-panel__container">
        <EmojiPanel :filter="'joy'" @emoji:select="handleEmojiPanelSelect"/>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import EmojiPanel from './components/EmojiPanel.vue';

@Component({
  components: {
    EmojiPanel,
  },
})
export default class App extends Vue {
  private emojiPanelDemoText: string = "What's the emotion I'm looking for... 🤔";

  private handleEmojiPanelSelect(emoji: string) {
    this.emojiPanelDemoText += emoji;
  }
}
</script>

<style lang="scss">
@import '~normalize.css/normalize.css';

html, body {
  height: 100%;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #eaf2ef;
  background: #912f56;
  height: 100%;
}

.app {
  
}

.app-header {
  text-align: center;
  margin-top: 0;
  padding-top: 100px;
}

.emoji-panel-stack {
  width: 400px;
  margin: 100px auto 0;
}

.emoji-panel-stack > * {
  margin-top: 40px;

  &:first-child {
    margin-top: 0;
  }
}

.emoji-panel-demo-text {
  
}

.emoji-panel-demo-text__input {
  display: block;
  box-sizing: border-box;
  width: 100%;
  border-radius: 18px;
  background: rgba(0, 0, 0, 0.15);
  color: #eaf2ef;
  border: none;
  padding: 12px;
  font-size: 18px;
  resize: none;
  height: 96px;
}
</style>
