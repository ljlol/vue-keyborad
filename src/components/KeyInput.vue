<template>
  <div>
    <input type="text" ref="keyboard" v-model="inputValue" @focus="onFocus">
    <Keyboard :option="option" @keyVal="getInputValue" @close="option.show = false"></Keyboard>
  </div>
</template>
<script>
import Keyboard from '../components/Keyboard'
export default {
  components: {
    Keyboard
  },
  data() {
    return {
      option: {
        show: false,
        sourceDom: ''
      },
      inputValue: ''
    }
  },
  props: {},
  created() {},
  methods: {
    getInputValue(val) {
      if(val === 'delete'){
        this.inputValue = this.inputValue.slice(0,this.inputValue.length -1)
      }else{
        this.inputValue += val
      }

      this.setCursorPosition()
    },
    onFocus() {
      this.$set(this.option, 'show', true)
      this.$set(this.option, 'sourceDom', this.$refs['keyboard'])
    },
    //获取光标位置
    getCursorPosition() {
      let doc = this.$refs['keyboard']
      if (doc.selectionStart) return doc.selectionStart
      return -1
    },
    //设置光标位置 已实现
    setCursorPosition() {
      let doc = this.$refs['keyboard']
   
      setTimeout(()=>{
            doc.setSelectionRange(doc.value.length,doc.value.length)
            doc.focus()
      },50)
      
    }
  }
}
</script>
<style lang="less" scoped>

</style>
