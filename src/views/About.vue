<template>
  <div class="about">
    <div class="route" v-finger:tap="handlerBackHome">Home</div>
    <van-button type="warning" v-finger:tap="keyboardShow">警告按钮</van-button>

    <van-cell-group>
      <van-field v-model="value" placeholder="请输入" />
    </van-cell-group>

    <div v-finger:tap="handlerReload">点击刷新当前页面</div>

    <van-number-keyboard safe-area-inset-bottom :show="keyboardController" />
  </div>
</template>

<script>
import { apiAddress } from '@/request/api';

export default {
  name: 'About',

  inject: ['reload'],

  data() {
    return {
      keyboardController: false,
      value: ''
    };
  },

  created() {
    apiAddress({
      type: 0,
      sort: 1
    }).then((res) => {
      console.log(res);
    });
  },

  methods: {
    keyboardShow(e) {
      this.keyboardController = !this.keyboardController;
    },

    handlerBackHome() {
      this.$router.go(-1);
    },

    handlerReload() {
      this.$destroy();
      this.reload();
    }
  }
};
</script>
