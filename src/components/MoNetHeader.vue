<template>
  <v-container>

    <div class="mn-bg-header">MoNet</div>
    <transition name="slide-fade">
      <v-row align-content="center" class="pt-6"  v-if="showTitle">
        <v-col align="center" xs="6" sm="6" class="mn-text-header mx-auto">
          MoNet
        </v-col>
        <v-col align="center" xs="6" sm="12" class="mn-text-subheader mx-auto">
          Intelligent Image Style Transformation
        </v-col>
      </v-row>
    </transition>


  </v-container>
</template>

<script>
  export default {
    name: 'MoNetHeader',

    data: () => ({
      showTitle: false
    }),

    mounted() {
      this.showTitle = true;
    }
  }
</script>

<style>

.slide-fade-enter-active {
  transition: all 0.8s ease;
}
.slide-fade-leave-active {
  transition: all .8s cubic-bezier(1.0, 0, 0.8, 1.0);
}
.slide-fade-enter, .slide-fade-leave-to
  /* .slide-fade-leave-active below version 2.1.8 */ {
  transform: translateY(-20px);
  opacity: 0;
}

.mn-bg-header {
  position: fixed;
  font-size: 18rem;
  opacity: 0.1;
  left: 50%;
  top: -15%;
  transform: translate(-50%, 0);
  z-index: 0;
  user-select: none;
}

.mn-text-header {
  font-size: 8rem;
  background-image: radial-gradient(ellipse at top, #CD54A6, #134DFF);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  line-height: 5rem;
  z-index: 1;
  font-weight: bold;
  user-select: none;
}
.mn-text-subheader {
  color: #EEEEEE;
  z-index: 1;
  font-size: 1.2rem;
  user-select: none;
}
</style>
