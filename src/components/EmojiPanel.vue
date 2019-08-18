<template>
  <div class="emoji-panel">
    <div class="emoji-filter">
      <input 
        type="text" 
        v-model="filter" 
        class="emoji-filter__input" 
        placeholder="Search..."
      />
    </div>

    <div class="emoji-list">
      <div 
        v-for="emoji in filteredEmojis" 
        :key="emoji.annotation"
        class="emoji-list__item"
        @click="$emit('emoji:select')">
        {{ emoji.unicode }}
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';
import { CompactEmoji, Shortcode } from 'emojibase'
import emojiData from 'emojibase-data/en/compact.json';

@Component
export default class EmojiPanel extends Vue {
  filter : string = ''

  get filteredEmojis() : Array<CompactEmoji> {
    if (this.filter === undefined || this.filter === '') {
      return emojiData;
    }

    return emojiData.filter((dataPoint : CompactEmoji) => {
      return dataPoint.shortcodes.some((shortcode : Shortcode) => {
        return shortcode.startsWith(this.filter);
      })
    });
  }
}
</script>

<style lang="scss">
.emoji-panel {
  box-shadow: rgba(0, 0, 0, 0.1) 0px 0px 0px 1px, rgba(0, 0, 0, 0.35) 0px 1px 10px;
  border-radius: 6px;
  padding: 10px;
  width: 400px;
}

.emoji-filter__input {
  display: block;
  box-sizing: border-box;
  width: 100%;
  border-radius: 18px;
  background: rgba(0, 0, 0, 0.05);
  border: none;
  padding: 12px;
}

.emoji-list {
  align-items: flex-start;
  align-content: flex-start;
  display: flex;
  flex-flow: row wrap;
  margin-top: 10px;
  height: 300px;
  overflow-x: hidden;
  overflow-y: scroll;
}

.emoji-list__item {
  font-size: 30px;
  line-height: 36px;
  width: 30px;
  height: 30px;
  padding: 5px;
  cursor: pointer;

  &:hover {
    background: rgba(0, 0, 0, 0.05);
    border-radius: 5px;
  }
}
</style>