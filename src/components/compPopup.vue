<template>
  <div class="comp-popup">
    <div class="wrapper-popup " v-bind:class="OpenPopup">
      <div class="rule">
        <h2>Rule Dice Game</h2>
        <br>
        <p>
          Lorem, ipsum dolor sit amet consectetur adipisicing elit. Quisquam
          quos delectus, modi minus assumenda laboriosam ratione! Dolorem fugit
          minima atque dignissimos animi reprehenderit odit inventore.
          Dignissimos perspiciatis labore dolorum laboriosam.
        </p>
        <br>
        <button @click="submitOK">OKEY</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "comp-popup",
  props:{
    isOpenPopup:{type: Boolean, default: false}
  },
  data() {
    return {};
  },
  methods:{
    submitOK(){
      this.$emit('handleClosePopup')
    }
  },
  computed:{
    OpenPopup: function(){
      return{
      'popup-scale': this.isOpenPopup
      }
    }
  }
};
</script>

<style>
.wrapper-popup {
  position: fixed;
  top: 0;
  right: 0;
  left: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.4);
  opacity: 0;
  visibility: hidden;
  transition:  all .3 ease;
}
.wrapper-popup.popup-scale{
  opacity: 1;
  visibility: visible;
}
.rule {
    background-color: aliceblue;
    padding: 10px;
    width: 300px;
    top: 50%;
    left: 50%;
    transform: translate(-50%,-50%) scale(1.3);
    position: absolute;
    transition: all .3s ease;
    border-radius: 16px;
    display: flex;
    flex-direction: column;
    align-items: center;
}
.popup-scale .rule{
  transform: translate(-50%,-50%) scale(1);
}
.rule button{
    background: black;
    color: white;
    width: 100px;
    height: 50px;
    border-radius: 16px;
}
</style>