<template>
    <div class="grid-item">
        <img src="../assets/circleWhite.png" alt="" 
        class="img-fluid zoomIn"
        v-if="iconname === 'kreis'"
        />
        <img src="../assets/crossWhite.png" alt="" 
        class="img-fluid zoomIn"
        v-else-if="iconname === 'kreuz'"
        />
    </div>
</template>



<script>
import { defineComponent, onMounted } from 'vue';
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
      onMounted(() => {
      console.log('mounted!')
    })

    return
  }
    
})
</script>



<style lang="scss" scoped>
img {
  width: 80px;
  height: 80px;
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

.grid-item{
  height: 150px;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>