<template>
  <div class="wrapper-popup" v-bind:class="getPopup">
      <div class="rule">
        <h3>Rule</h3>
        <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Modi temporibus maiores 
          obcaecati debitis molestiae quae sapiente dolorem reprehenderit repudiandae unde.</p>
          <button 
              class="confirm"
              v-on:click="confirm"
              >Start Game</button>
      </div>
  </div>
</template>

<script>
export default {
  name: 'comp-popup-rule',
  props: {
      isOpenPopup: {type: Boolean, default: false}
  },
  data() {
    return {
      
    }
  },
  methods: {
    confirm(){
      this.$emit('handleConfirm')
    }
  },
  computed: {
    getPopup(){
      return {
        'open-popup': this.isOpenPopup
      }
    }
  }
}
</script>

<style>
  .wrapper-popup {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background-color: rgba(0, 0, 0, 0.4);
    opacity: 0;
    visibility: hidden;
  }
  .wrapper-popup.open-popup {
    opacity: 1;
    visibility: visible;
  }
  .rule {
    width: 350px;
    padding: 20px;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%) scale(1.2);
    position: absolute;
    background-color: white;
    font-family: Arial, Helvetica, sans-serif;
    transition: all 0.3 ease;
  }
  .open-popup .rule{
    transform: translate(-50%, -50%) scale(1);
  }
  .rule h3 {
    margin-bottom: 30px;
  }
  .rule .confirm {
    cursor: pointer;
    margin-top: 30px;
    border: 2px solid #333;
    padding: 10px 15px;
    background-color: #fff;
    color: #333;
    transition: all 0.3 ease;
  }
  .rule .confirm:hover {
    background-color: #333;
    color: #fff;
  }
  /* buit-in css3 with vuejs */
</style>