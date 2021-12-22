<template>
  <div class="gugu" flex="dir:top main:justify">
    <div>
      <div class="header" flex="main:justify cross:center">
        <div class="label">欢迎使用耳仔翻译器
          <br>明鸽不说暗话：о̆喜о̌喜о̄喜о̂喜 о̇喜嘻о̋喜о̉喜 ӧ喜о̍喜о̅喜о̎喜        
        </div>
      </div>
      <div class="input">
        <img class="clear" @click="clearHandle" v-if="msg" src="../assets/del_1.svg" alt="">
        <van-field
          v-model="msg"
          label="内容"
          ref="inputRef"
          type="textarea"
          :autosize="{ maxHeight: 300, minHeight: 70 }"
          placeholder="请输入要翻译的内容/嘻嘻语"
          autofocus
        />
      </div>
      <van-button :data-clipboard-text="result" class="copy copyJs" type="primary">复制结果</van-button>
      <p class="result">{{ result }}</p>
    </div>
    <div class="foot">
      <van-collapse v-model="activeNames">
        <van-collapse-item title="About" name="1">
          <a href="https://github.com/yuan1/gugu"> Github地址</a>
        </van-collapse-item>
      </van-collapse>
    </div>
  </div>
</template>

<script setup lang="ts">
  import Clipboard from 'clipboard'
  import { computed, onMounted, ref } from 'vue'
  import { translateEachOther } from '@/util'
  import { Toast } from 'vant'

  const msg = ref<string>('')
  const inputRef: any = ref(null)
  const result = computed(() => {
    return translateEachOther(msg.value)
  })
  const clearHandle = () => {
    msg.value = ''
    inputRef.value.focus()
  }
  onMounted(() => {
    const cli = new Clipboard('.copyJs')
    cli.on('success', function (e) {
      Toast('复制成功')
      e.clearSelection()
    })
  })
  const activeNames = ref([])

</script>

<style scoped>
a {
  color: #1989fa;
}

.gugu {
  padding: 16px 24px;
  position: relative;
  min-height: 100vh;
  .foot{
    margin-top: 8px;
    a{
      line-height: 20px;
    }
  }
}

.input {
  position: relative;

  .clear {
    top: 4px;
    right: 4px;
    position: absolute;
    width: 14px;
    z-index: 3;
  }
}

.header {
  padding: 8px 16px;

  .label {
  }
}

.copy {
  float: right;
  margin: 8px 0;
}

.result {
  clear: both;
  position: relative;
}
</style>
