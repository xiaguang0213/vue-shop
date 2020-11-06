<template>
    <div>
        <el-container>
            <el-header>
                <el-button type="info" @click="logout">退出</el-button>
            </el-header>
                <el-container>
                    <el-aside width="200px" height="">Aside</el-aside>
                    <el-main>Main</el-main>
                </el-container>
        </el-container>
    </div>
</template>
<script>
export default {
  data () {
    return {
      value: ''
    }
  },
  methods: {
    logout () {
      window.sessionStorage.clear()
      this.$router.push('/login')
    }
  }
}
</script>
