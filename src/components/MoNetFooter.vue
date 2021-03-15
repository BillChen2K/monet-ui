<template>
<v-container>
  <v-row align-content="right">
    <v-spacer></v-spacer>
    <v-col sm="4">
      <v-btn outlined class="mn-button" onclick="window.open('https://github.com/billchen2k/monet-ui', '_blank')">
        GITHUB
      </v-btn>

      <v-dialog
          v-model="aboutDialog"
          width="500"
      >
        <template v-slot:activator="{ on, attrs }">
          <v-btn outlined class="ml-4 mn-button" v-bind="attrs" v-on="on">
            ABOUT
          </v-btn>
        </template>

        <v-card>
          <v-card-title class="headline grey darken-3 mb-2">
            MoNet
          </v-card-title>
          <v-card-text class="pb-2">
            关于文字
          </v-card-text>

          <v-divider></v-divider>

          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn
                color="blue"
                text
                @click="aboutDialog = false"
            >
              OK
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>
    </v-col>
  </v-row>
</v-container>
</template>

<script>
export default {
name: "MoNetFooter",

  data: () => ({
    aboutDialog: false
  })
}
</script>

<style scoped>

</style>
