<template>
  <div>
    <el-dropdown @command="onCommand">
      <span class="el-dropdown-link">
        <svg-icon style="color: #fff; font-size: 20px" icon-class="language" />
      </span>
      <el-dropdown-menu slot="dropdown">
        <el-dropdown-item
          :disabled="key === $i18n.locale"
          :key="key"
          :command="key"
          v-for="(value, key) in messages"
          >{{ value.name }}</el-dropdown-item
        >
      </el-dropdown-menu>
    </el-dropdown>
  </div>
</template>

<script>
import { messages } from '@/i18n'
import Cookies from 'js-cookie'
export default {
  name: 'ToggleLang',
  data() {
    return {
      messages
    }
  },

  created() {},

  methods: {
    onCommand(val) {
      console.log(val)
      this.$root.$i18n.locale = val
      this.$router.go(0)
      Cookies.set('lang', val)
    }
  }
}
</script>

<style scoped></style>
