<template>
<transition name="slide-down">
    <div class="ta-dialog__wrapper" v-if="isShow">
    <div class="ta-dialog">
      <div class="ta-dialog__header">
        <span>{{ title }}</span>
        <i class="ios-close-empty" @click="handleCancel()"></i>
      </div>
      <div class="ta-dialog__body">
        <slot></slot>
      </div>
      <div class="ta-dialog__footer">
        <button @click="handleCancel()">取消</button>
        <button @click="handleOk()">确定</button>
      </div>
    </div>
  </div>
</transition>
    
</template>

<script>
export default {
  name: 'dialog',
  props: {
    title: {
      type: String,
      default: '标题'
    },
  },
  data(){
      return {
          sideDown: "side-down",
          isShow: true
      }
  }, 
  methods: {
    handleCancel() {
        this.isShow = false
      this.$emit('cancel')
    },

    handleOk() {

      this.$emit('ok')
    },
  },
}
</script>
<style lang="scss" scope>
.ta-dialog__wrapper {
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 9999999;
    position: relative;
    background: rgba(0,0,0,0.5);
    .ta-dialog{
       width: 400px;
       height: 200px;
       background: #fff;
       display: flex;
       flex-direction: column;
       justify-content: space-between;
       .ta-dialog__footer{
           display: flex;
           justify-content: flex-end;
           button{
               margin:0 10px 10px 0;
           }
       }
    }
}
.slide-down-enter-active {
  animation: dialog-enter ease .3s;
}

.slide-down-leave-active {
  animation: dialog-leave ease .5s;
}

@keyframes dialog-enter {
  from {
    opacity: 0;
    transform: translateY(-50px);
  }

  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes dialog-leave {
  from {
    opacity: 1;
    transform: translateY(0);
  }

  to {
    opacity: 0;
    transform: translateY(-50px);
  }
}
</style>
