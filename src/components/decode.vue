<template>
  <div class="container">
    <div class="inputArea">
      在這裡輸入甫語言：
      <el-input v-model="input" placeholder="Please input" clearable/>
    </div>
    人類語言翻譯結果：
    <div class="outputArea">
      {{humanResult}}
    </div>
  </div>
</template>

<script>
import {ref} from 'vue'

const input = ref('')
export default {
  name: "decode",
  data() {
    return {
      input: input,
      humanResult: "",
    }
  },
  methods: {
    handleInput(str) {
      // translate eric to binary
      var result = []
      var list = str.split("")
      for (var i = 0; i < list.length; i++) {
        var item = list[i];
        if (item == "吧")
          result.push("0")
        else if (item == "啦")
          result.push("1")
        else
          result.push(" ")
      }
      result = result.join("").split(" ")
      console.log(result)
      // translate binary to human
      var humanResult = []
      for(var i=0;i < result.length;i++){
        var item = result[i];
        var asciiCode = parseInt(item,2);
        var charValue = String.fromCharCode(asciiCode);
        humanResult.push(charValue);
      }
      this.humanResult = humanResult.join("")
    }
  },
  watch: {
    input: function (newVal, oldVal) {
      this.handleInput(newVal)
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