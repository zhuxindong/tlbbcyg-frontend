<template>
  <div class="dashboard-container">
    <div class="dashboard-text">

      <!-- name: {{ name }} -->
      简单说明：
      可以点击左侧的按条件查询

    </div>
  </div>
</template>

<script>
import { mapGetters } from 'vuex'

export default {
  name: '天龙八部畅易阁助手',
  computed: {
    ...mapGetters([
      'name'
    ])
  }
}
</script>

<style lang="scss" scoped>
.dashboard {
  &-container {
    margin: 30px;
  }
  &-text {
    font-size: 30px;
    line-height: 46px;
  }
}
</style>
