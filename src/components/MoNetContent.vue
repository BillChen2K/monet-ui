<template>
<v-container>
  <v-fade-transition mode="out-in">
    <div class="hint-text mt-12" align="center" v-if="showHint">
      <h2>使用指引</h2>
      <p>选择一张希望进行风格迁移的原图片</p>
      <v-icon>mdi-chevron-down</v-icon>
      <p>从塞尚、莫奈、夏天、冬天、浮世绘、梵高中选择一种转换风格</p>
      <v-icon>mdi-chevron-down</v-icon>
      <p>生成图片</p>
      <v-btn icon large outlined class="mn-button-round"
             @click="showHint = false"
      ><v-icon>mdi-arrow-right</v-icon></v-btn>
    </div>
    <div v-else class="mt-12">
      <v-row>
        <v-col xs="12" sm="12" md="5" align="center">
          <v-img class="mn-img" :lazy-src="realImg"></v-img>
          <v-btn large class="mn-button" outlined style="position: relative; top: -50%">BROWSE</v-btn>
        </v-col>

        <v-col class="container-feature" md="2" align="center">
          <div style="height: 18rem;">
            <div style="height: 33%;">

              <v-btn height="5rem" width="5rem" class="mn-button mn-button-feature" outlined>
                <div>
                  <v-icon>mdi-download</v-icon>
                </div>
                <div>
                  下载
                </div>
              </v-btn>

            </div>
            <div style="height: 33%;">
              <v-icon large style="margin-top: 1.8rem">mdi-brush</v-icon>
            </div>
            <div style="height: 33%;">

              <v-btn style="margin-top:1rem" height="5rem" width="5rem" class="mn-button mn-button-feature" outlined>
                <div>
                  <v-icon>mdi-refresh</v-icon>
                </div>
                <div>
                  重选
                </div>
              </v-btn>

            </div>
          </div>

        </v-col>


        <v-col xs="12" sm="12" md="5" align="center">
          <v-img class="mn-img img-processing" :lazy-src="fakeImg"></v-img>

          <div style="position: relative; top: -50%; user-select: none; font-weight: bold; font-size: 1.2rem">
            PROCESSING...
          </div>

        </v-col>
      </v-row>

      <!-- Selector -->
      <v-row>

      </v-row>
    </div>
  </v-fade-transition>

</v-container>
</template>

<script>
export default {
  name: "MoNetContent",

  data: () => ({
    showHint: false,
    realImg: "",
    fakeImg: "",
    stage: 0, // 0: Choose file; 1: Processing; 2: Finished
    submitForm: {
      img: "",
      style: "",
      size: 512
    }
  })
}
</script>

<style scoped>

.hint-text p{
  margin: 2rem;
  font-size: 1.2rem;
}

.mn-img {
  border: white 2px solid;
  width: 95%;
  height: 18rem;
}

.mn-button-feature {

}

.container-feature {
  position: relative;
}

.img-processing {
  background: radial-gradient(ellipse at top, #3d3d3d, #781858);;
}

</style>
