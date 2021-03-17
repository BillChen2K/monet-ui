<template>
<v-container>
  <v-row align-content="right" style="transition: all 1s">
    <v-col xs="12" align="right">
      <v-btn outlined class="mn-button mx-2" onclick="window.open('https://github.com/billchen2k/monet-ui', '_blank')">
        GITHUB
      </v-btn>

      <v-dialog
          v-model="aboutDialog"
          class="mn-dialog"
          width="500"
      >
        <template v-slot:activator="{ on, attrs }">
          <v-btn outlined class="mx-2 mn-button" v-bind="attrs" v-on="on">
            ABOUT
          </v-btn>
        </template>

        <v-card>
          <v-card-title class="headline grey darken-3">
            MoNet
          </v-card-title>
          <v-card-text class="py-4">
            <p>MoNet 利用 CycleGAN 网络，将图片转换成不同的风格。</p>
            <p>East China Normal University, 2021</p>

          </v-card-text>

          <v-divider></v-divider>

          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn
                class="mn-button"
                color="white"
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
