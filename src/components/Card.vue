<template>
 <div class="card" v-on:click="selectedCard"> 
     <div class="flip-card" :class="{flipCardActive: isActive}">
      <div class="flip-card-inner">
        <div class="flip-card-front" :style="bgColor">
          <img id="img2" src="../assets/logo2.svg">
        </div>
        <div class="flip-card-back">
          <img :src="img">
        </div>
      </div>
    </div>
 </div>
</template>

<script>
let selectedImage1; 
export default {
  name: 'Card',
  props: {
    img: String,
    value: Number,
    isActive: Boolean,
    bgColor: String
  },
  data() {
    return {
      isActive: false
    }
  },
  methods: {
    selectedCard: function (){
        this.isActive = !this.isActive;
        this.$emit('isActive', this.isActive);
    },
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">


</style>