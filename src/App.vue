<template>
  <v-app>
    <v-main>
      <MoNetHeader />
      <MoNetContent />
      <MoNetFooter />
    </v-main>
  </v-app>
</template>

<script>
import MoNetHeader from "@/components/MoNetHeader";
import MoNetContent from "@/components/MoNetContent";
import MoNetFooter from "@/components/MoNetFooter";

export default {
  name: 'App',

  components: {
    MoNetFooter,
    MoNetContent,
    MoNetHeader,
  },

  data: () => ({
    //
  }),
};
</script>

<style>

</style>
