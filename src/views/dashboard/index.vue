<template>
  <div class="app-container">
    <a-card>
      <a-collapse v-model="activeKey" :bordered="false">
        <a-collapse-panel key="0" header="项目介绍">
          <a href="https://github.com/Tumo-Team/Tumo-Boot" target="_blank">Tumo-Boot</a>
          是基于SpringBoot、Spring Security、Ant Design Vue开发的一套简洁、规范、开箱即用的权限系统，前后端分离结构。
        </a-collapse-panel>
        <a-collapse-panel key="1" header="项目源码">
          <p>
            Tumo Boot：
            <a href="https://github.com/Tumo-Team/Tumo-Boot" target="_blank">https://github.com/Tumo-Team/Tumo-Boot</a>
          </p>
          <p>
            开发文档：
            <a href="http://docs.boot.tycoding.cn/" target="_blank">http://docs.boot.tycoding.cn/</a>
          </p>
        </a-collapse-panel>
        <a-collapse-panel key="2" header="联系作者">
          <p>
            Blog:
            <a href="https://tycoding.cn" target="_blank">https://tycoding.cn</a>
          </p>
          <p>
            Github:
            <a href="https://github.com/TyCoding" target="_blank">https://github.com/TyCoding</a>
          </p>
          <p>
            QQ Group:
            <a href="#">866685601</a>
          </p>
        </a-collapse-panel>
      </a-collapse>
    </a-card>
  </div>
</template>

<script>

export default {
  name: 'Dashboard',
  components: {},
  data() {
    return {
      activeKey: ['0', '1', '2']
    }
  }
}
</script>

<style lang="less" scoped>
a {
  color: #1890ff;
}
</style>
