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
    },
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.card {
    width: 100%;
    height: 100%;
    cursor: pointer;
    position: relative;
}

.flipCardActive .flip-card-inner {
  transform: rotateY(-180deg);
  background-color: #e8c2ff;

}

.flip-card-front img {
  position: relative;
  width: 100%;
  height: 100%;
}



.flip-card {
    background-color: transparent;
    width: 200px;
    height: 200px;
    perspective: 1000px; 
    background-color: transparent;
      border-radius: 20px;
}
  
.flip-card-inner {
  background-color: rgb(251, 251, 251);
  position: relative;
  width: 100%;
  border-radius: 20px;
  height: 100%;
  text-align: center;
  transition: transform 0.8s;
  transform-style: preserve-3d;
  
}



.flip-card-front,
.flip-card-back {
  position: absolute;
  width: 100%;
  height: 100%;
  border-radius: 20px;
  -webkit-backface-visibility: hidden;
  backface-visibility: hidden;
  
}


.flip-card-front {

  border-radius: 20px;
  background-color: #e8c2ff;
  transition: all 0.8s;

  
}

.flip-card-front:hover {
  background-color: #d28efc;
}

.flip-card-front img {
 
  border-radius: 20px;

  transform-style: preserve-3d; 
}

#img2 {
    transition: transform 0.8s;
}

#img2:hover {
  transform: rotate(360deg);
}


.flip-card-back {

  border-radius: 20px;
  color: white;
  transform: rotateY(180deg);
}

.flip-card-back img {
  border-radius: 20px;
}

</style>