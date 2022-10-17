<template>
  <div class="container">
    <div class="inputArea">
      在這裡輸入（中英文皆可）：
      <el-input v-model="input" placeholder="Please input" clearable/>
    </div>
    甫語言翻譯結果：
    <div class="outputArea">
<!--      <button @click="copy('#resultBox')"> 複製！</button>-->
<!--      <el-input class="resultBox" type="textarea" rows="5" v-model="ericResult" disabled placeholder="" />-->
      {{ericResult}}
    </div>
  </div>
</template>

<script>
import {ref} from 'vue'

const input = ref('')
export default {
  name: "encode",
  data() {
    return {
      input: input,
      ericResult: "",
    }
  },
  methods: {
    handleInput(str) {
      // translate input to binary
      var result = [];
      var list = str.split("");
      console.log("list " + list);
      for (var i = 0; i < list.length; i++) {
        var item = list[i];
        var binaryStr = item.charCodeAt().toString(2);
        result.push(binaryStr);
      }
      var binaryResult = result.join("");

      // translate binary to eric
      var ericResult = [];
      for (var i = 0; i< result.length; i++) {
        for (var j = 0; j < result[i].length; j++) {
          var item = result[i][j];
          if (item == "0")
            ericResult.push("吧");
          else
            ericResult.push("啦");
        }
        ericResult.push(" ");
      }
      this.ericResult = ericResult.join("")
    },
    copy(cls){
      var dom = document.querySelector(cls) // 要复制文字的节点
      if (navigator.userAgent.match(/(iPhone|iPod|iPad);?/i)) { // 区分ios设备
        window.getSelection().removeAllRanges() // 这段代码必须放在前面否则无效
        var range = document.createRange()
        // 选中需要复制的节点
        range.selectNode(dom)
        // 执行选中元素
        window.getSelection().addRange(range)
        // 执行 copy 操作
        var successful = document.execCommand('copy')
        // 移除选中的元素
        window.getSelection().removeAllRanges()
        console.log('复制成功')
      } else {
        //非ios设备
        dom.select() // 选择对象
        if(document.execCommand('Copy',false,null)){
          console.log("复制成功")
        } // 执行浏览器复制命令
      }
    }
  },
  watch: {
    input: function (newVal, oldVal) {
      this.handleInput(newVal)
      console.log(newVal)
    }
  }
}
</script>

<style lang="scss" scoped>
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  background-color: #c6ddf6;
  padding: 2rem;
  border-radius: 2rem;

  .outputArea{
    max-width: 90%;
    padding: 1rem;
  }
}
</style>