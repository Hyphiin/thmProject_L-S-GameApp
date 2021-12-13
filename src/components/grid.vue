<template>
    <div>
        <img src="../assets/circleWhite.png" alt="" 
        class="img-fluid zoomIn"
        v-if="iconname === 'circle'"
        />
        <img src="../assets/crossWhite.png" alt="" 
        class="img-fluid zoomIn"
        v-else-if="iconname === 'cross'"
        />
        <img src="../assets/logo.png" alt="" 
        class="img-fluid zoomIn"
        v-else-if="iconname === 'empty'"
         />
    </div>
</template>



<script>
import { defineComponent } from 'vue';
export default defineComponent({
  name: 'GridTicTacToe',
  components: { },
  props: {
        iconname: {
            type: String,
            required: true
        }
    },
  setup () {

    return
  }
    
})
</script>



<style lang="scss" scoped>
img {
  width: 80px;
}

@keyframes zoomIn {
  from {
    opacity: 0;
    transform: scale3d(0.3, 0.3, 0.3);
  }

  50% {
    opacity: 1;
  }
}

.zoomIn {
  animation-name: zoomIn;
  animation-duration: 1s;
}
</style>