<template>
  <LuckyWheel
  class="m-turntable"
    ref="myLucky"
    width="200px"
    height="200px"
    :blocks="blocks"
    :prizes="prizes"
    :buttons="buttons"
    @start="startCallBack"
    @end="endCallBack"
  />

<div>
    <el-checkbox v-model="checked1" label="Option1" border></el-checkbox>
    <el-checkbox v-model="checked2" label="Option2" border></el-checkbox>
  </div>
</template>

<script>
import { ElCheckbox } from 'element-plus'
import 'element-plus/es/components/checkbox/style/css'
const arr = [1, 2, 3, 4, 5, 6];
const color = ["#e9e8fe", "#b8c5f2"];

export default {
  components: { ElCheckbox },
  data() {
    const result = arr.map((value, index) => {
      return {
        background: color[index % 2],
        fonts: [
          {
            text: value,
          },
        ],
      };
    });
    const checkboxState = {
      
    }
    return {
      blocks: [{ padding: "10px", background: "#869cfa" }],
      prizes: result,
      buttons: [
        { radius: "40%", background: "#617df2" },
        { radius: "35%", background: "#afc8ff" },
        {
          radius: "30%",
          background: "#869cfa",
          pointer: true,
          fonts: [{ text: "开始", top: "-10px" }],
        },
      ],
      checkedState: {

      }
    };
  },
  methods: {
    startCallBack() {
      // 开始游戏
      this.$refs.myLucky.play();
      // 假设接口的请求速度是5s
      setTimeout(() => {
        // 5s后拿到后端返回的中奖索引
        const index = Math.floor(Math.random() * arr.length);
        // 然后停止游戏 (缓慢停止)
        this.$refs.myLucky.stop(index);
      }, 1000);
    },
    endCallBack(prize) {
      // 当完全停止时, 触发回调函数
      alert(prize.fonts[0].text);
    },
  },
};
</script>

<style scoped>
  .m-turntable {
    margin: 0 auto;
  }
</style>