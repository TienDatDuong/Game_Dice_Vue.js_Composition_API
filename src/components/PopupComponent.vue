<template>
  <div class="wrapper-popup" :class="getOpenPopUp">
    <div class="rule">
        <h3>Luật chơi</h3>
      <p>Mất tích bí ẩn không dấu vết suốt 31 năm trời, người phụ nữ bất ngờ được phát hiện tại nơi cách nhà hơn 3.200 km</p>
      <button @click="confirm">Đã hiểu</button>
    </div>
  </div>
</template>
<script setup>
import  {defineProps,defineEmits,computed} from 'vue'

const emit = defineEmits(['confirm'])

const props = defineProps({
  isOpenPopup:{
    type: Boolean,
    default: false
  }
})

  const confirm = () => {
    emit('confirm')
  }
 const  getOpenPopUp = computed(() => { return{'open-popup': props.isOpenPopup}} )

</script>
<style scoped>
.wrapper-popup{
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: rgba(0,0,0,0.4) ;
  opacity: 0;
  visibility: hidden;
}
.wrapper-popup.open-popup{
  opacity: 1;
  visibility: visible;
  transition: all 0.3s ease ;
}
.rule{
  position: absolute;
  background-color: #ffffff;
  width: 350px;
  padding: 30px;
  top: 50%;
  left: 50%;
  transform: translate(-50% , -50%) scale(1.2);
  font-family: Arial;
  transition: all 0.3s ease ;
}
.open-popup .rule{
  transform: translate(-50%,-50%) scale(1);
}
.rule h3{
  margin-bottom: 20px;
}
.rule button{
  margin-top: 20px;
  padding: 10px 15px;
  cursor: pointer;
  transition: all 0.3s ease;
  background-color: #fff;
}
.rule button:hover{
  background-color: #222222;
  color: white;
}
</style>