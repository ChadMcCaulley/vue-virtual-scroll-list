<template>
  <div class="example">
    <github-corner />
    <introduction description="The <code>scrollElement</code> prop allows for scrollbars that are not attached or at the page level." />

    <div class="example-content">
      <div ref="scrollElement" class="scroll-element">
        <div class="box">
          Some Header
        </div>
        <virtual-list class="list-page scroll-touch" ref="vsl"
          :data-key="'id'"
          :data-sources="items"
          :data-component="itemComponent"
          :estimate-size="135"
          :item-class="'list-item-page'"
          :scroll-element="scrollElement"
          v-on:totop="totop"
          v-on:tobottom="tobottom"
        />
        <div class="bottom">
          <h2>This is page footer</h2>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Item from './Item'

import { Random } from '../../common/mock'
import getSentences from '../../common/sentences'
import genUniqueId from '../../common/gen-unique-id'

const TOTAL_COUNT = 1000

const DataItems = []
let count = TOTAL_COUNT
while (count--) {
  const index = TOTAL_COUNT - count
  DataItems.push({
    index,
    name: Random.name(),
    id: genUniqueId(index),
    desc: getSentences()
  })
}

export default {
  name: 'page-mode',

  components: {
  },

  data () {
    return {
      items: DataItems,
      itemComponent: Item,
      scrollElement: null
    }
  },
  mounted() {
    this.scrollElement = this.$refs.scrollElement
  },
  methods: {
    totop () {
      console.log('reach totop')
    },
    tobottom () {
      console.log('reach tobottom')
    }
  }
}
</script>

<style lang="less">
.list-page {
  width: 100%;
  border: 2px solid;
  border-radius: 3px;
  overflow-y: auto;
  border-color: dimgray;

  .list-item-page {
    display: flex;
    align-items: center;
    padding: 1em;
    border-bottom: 1px solid;
    border-color: lightgray;
  }
}
.bottom {
  padding: 2em 0;
}
.box {
  height: 300px;
  margin-bottom: 100px;
  background: rgba(0,0,0,0.3);
}
.scroll-element {
  overflow: scroll;
  height: 800px;
  padding-right: 20px;
  overflow-x: hidden;
}
</style>
