<template>
<v-container>
  <v-stepper>

  </v-stepper>
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
        <v-col xs="12" lg="5" align="center" style="position: relative">
          <v-img class="mn-img" :src="rawImg"></v-img>
          <input style="display: none" ref="fileInput" type="file" @change="fileSelected" formenctype="multipart/form-data">

          <v-btn @click="$refs.fileInput.click()" large class="mn-button" outlined
                 style="position: relative; top: -10rem"
                 v-if="!rawImg">BROWSE</v-btn>
        </v-col>

        <v-col class="container-feature" md="4" lg="2" align="center">
          <div style="height: 18rem; min-width: 8rem;">
            <div style="height: 33%;">
              <v-btn v-if="fakeImg.length" height="5rem" width="5rem" class="mn-button mn-button-feature" outlined
              @click="downloadFile(fakeImg)">
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

              <v-btn v-if="rawImg" style="margin-top:1rem" height="5rem" width="5rem" class="mn-button mn-button-feature" outlined @click="reselect">
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


        <v-col xs="12"  lg="5" align="center">
          <v-img :class="stage == 1 ? 'img-processing': ''" class="mn-img" :src="fakeImg">
            <template v-slot:placeholder v-if="stage==2">
              <div style="user-select: none; font-weight: bold; font-size: 1.2rem">
                DOWNLOADING...
              </div>
              <v-row
                  class="fill-height ma-0"
                  align="center"
                  justify="center"
              >
                <v-progress-circular
                    indeterminate
                    color="grey lighten-5"
                ></v-progress-circular>
              </v-row>
            </template>
          </v-img>

          <div style="height: 1.5rem">
            <v-fade-transition>
              <div v-if="stage == 1 && showProcessing" style="position: relative; top: -10rem; user-select: none; font-weight: bold; font-size: 1.2rem">
                PROCESSING...
              </div>
            </v-fade-transition>
          </div>



        </v-col>
      </v-row>

      <!-- Selector -->
      <v-radio-group v-model="submitForm.style" v-if="rawImg">
        <v-row class="mt-4 mx-auto" style="display: flex; justify-content: space-between; width: 80%; transition: 1s"  >
            <div v-for="one in styles" :key="one.key"  align="center">
              <v-fade-transition>
                <div :class="one.key == submitForm.style ? 'text-gradient-base' : ''"
                     :style="one.key == submitForm.style ?
              'font-size: 1.3rem; font-weight: bold;' : 'font-size: 1.3rem'">{{one.name_en}}</div>
              </v-fade-transition>
              <div>{{one.name_zh}}</div>
              <v-radio :disabled="stage==1" color="white" :value="one.key" class="mx-5 mt-1" @click="transform"></v-radio>
            </div>
        </v-row>
      </v-radio-group>
    </div>

  <v-snackbar
      v-model="snackbar"
  >
    {{ snackbar_text }}
    <template v-slot:action="{ attrs }">
      <v-btn
          color="pink"
          text
          v-bind="attrs"
          @click="snackbar = false"
      >
        Close
      </v-btn>
    </template>
  </v-snackbar>

</v-container>
</template>

<script>

import axios from 'axios'
import config from "@/plugins/config";

export default {

  name: "MoNetContent",

  data: () => ({
    showHint: false,
    rawImg: "",
    realImg: "",
    snackbar: false,
    snackbar_text: "",
    fakeImg: "",
    stage: 0, // 0: Choose file; 1: Processing; 2: Finished
    showProcessing: true,
    submitForm: {
      img: "",
      style: "",
      size: 256
    },
    selectedFile: null,

    styles: [
      {
        name_en: "Cézanne",
        name_zh: "塞尚",
        key: "cezanne"
      },
      {
        name_en: "Monet",
        name_zh: "莫奈",
        key: "monet"
      },
      {
        name_en: "Ukiyoe",
        name_zh: "浮世绘",
        key: "ukiyoe"
      },
      {
        name_en: "Vangogh",
        name_zh: "梵高",
        key: "vangogh"
      },
      {
        name_en: "Summer",
        name_zh: "夏天",
        key: "summer"
      },
      {
        name_en: "Winter",
        name_zh: "冬天",
        key: "winter"
      },
    ]
  }),

  methods: {
    transform() {
      this.fakeImg = ""
      this.stage = 1;
      let formData = new FormData();
      formData.append("img", this.selectedFile);
      formData.append("style", this.submitForm.style);
      formData.append("size", this.submitForm.size);
      axios.post(config.API + "/transform", formData, {
        headers: {
          "Content-Type": 'multipart/form-data'
        }
      })
      .then(res => {
        console.log(res.data);
        if (!res.data.success) {
          throw new Error(res.data.msg)
        }
        this.fakeImg = res.data.data.fakepic
        this.stage = 2
      })
      .catch(err => {
        console.error(err);
        this.submitForm.style = "";
        this.snackbar = true;
        this.snackbar_text = "错误：" + err.message;
        this.stage = 0;
      })


    },

    reselect() {
      this.rawImg = ""
      this.fakeImg = ""
      this.stage = 0
    },

    fileSelected(e) {
      e.preventDefault();
      console.log(e);
      this.selectedFile = e.target.files[0];
      this.rawImg = URL.createObjectURL(this.selectedFile);
      console.log(this.rawImg);
    },

    blink() {
      this.showProcessing = !this.showProcessing;
    },

    downloadFile(url) {
      if (url.match("monet-api")) {
        url = url.replace("http:", "https:");
      }
      let extension = (url.match(/\.([^.]*?)(?=\?|#|$)/) || [])[1];
      axios({
        url: url, //your url
        method: 'GET',
        responseType: 'blob', // important
      }).then((response) => {
        const url = window.URL.createObjectURL(new Blob([response.data]));
        const link = document.createElement('a');
        link.href = url;
        link.setAttribute('download', 'output' + extension); //or any other extension
        document.body.appendChild(link);
        link.click();
      });
    },

  },

  mounted() {
    console.log("Loaded.")
    setInterval(() => {
      this.showProcessing = !this.showProcessing;
    }, 500);
  }
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
  min-width: 24rem;
  background: #2d2d2d;
  height: 18rem;
}

.text-gradient-base {
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-image: radial-gradient(ellipse at top, #fad9ff, #6083fa);
}

.container-feature {
  position: relative;
}

.img-processing {
  background: radial-gradient(ellipse at top, #3d3d3d, #781858);
}

</style>
