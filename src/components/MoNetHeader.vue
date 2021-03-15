<template>
  <v-container>

    <div class="mn-bg-header">MoNet</div>

    <v-row align-content="center" class="pt-6">
      <v-col align="center" xs="6" sm="6" class="mn-text-header mx-auto ">
          MoNet
      </v-col>
      <v-col align="center" xs="6" sm="12" class="mn-text-subheader mx-auto">
          Intelligent Image Style Transformation
      </v-col>
    </v-row>

  </v-container>
</template>

<script>
  export default {
    name: 'MoNetHeader',

    data: () => ({

    }),
  }
</script>

<style>

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
  font-size: 7rem;
  background-image: radial-gradient(ellipse at top, #CD54A6, #134DFF);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  line-height: 5rem;
  z-index: 1;
  user-select: none;
}
.mn-text-subheader {
  color: #EEEEEE;
  z-index: 1;
}
</style>
