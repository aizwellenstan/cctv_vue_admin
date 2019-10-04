<template>
  <div class="example">
    <div class="tabs">
      <TabItem
        v-for="item in list"
        :key="item.id"
        v-model="currentId"
        v-bind="item"
      />
    </div>
    <div id="contents" class="contents">
      <div v-if="currentId === 1">
        <tab1 v-if="renderComponent1" />
      </div>
      <div v-else-if="currentId === 2">
        <tab2 v-if="renderComponent2" />
      </div>
    </div>
  </div>
</template>

<script>
import TabItem from './TabItem.vue'
import Tab1 from './Tab1.vue'
import Tab2 from './Tab2.vue'

export default {
  components: {
    TabItem,
    Tab1,
    Tab2
  },
  data() {
    return {
      renderComponent1: true,
      renderComponent2: true,
      currentId: 1,
      list: [
        {
          id: 1,
          label: 'Tab1'
        },
        {
          id: 2,
          label: 'Tab2'
        }
      ]
    }
  },
  computed: {
    current() {
      return this.list.find(el => el.id === this.currentId) || {}
    }
  },
  methods: {
    forceRerender() {
      // Remove my-component from the DOM
      this.renderComponent = false

      this.$nextTick(() => {
        // Add the component back in
        this.renderComponent = true
      })
    }
  }
}
</script>

<style scoped>
.example {
	position: absolute; top: 0; left: 0; height: 100%; width: 100%;
}
.contents {
	height: 100%;
  position: relative;
  overflow: hidden;
  border: 2px solid #000;
}
.item {
  box-sizing: border-box;
  padding: 10px;
  width: 100%;
  transition: all 0.8s ease;
}
/* トランジション用スタイル */
.v-leave-active {
  position: absolute;
}
.v-enter {
  transform: translateX(-100%);
}
.v-leave-to {
  transform: translateX(100%);
}
.camdiv {
	float:left;
	width: 12.5%;
	height: 110px
}
</style>
