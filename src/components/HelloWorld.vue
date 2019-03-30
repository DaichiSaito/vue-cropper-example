<template>
  <div>
    <input type="file" v-on:change="onFileChange()">
    <div class="content">
      <div class="show-info">
        <h2>Cropper Example</h2>
        <div class="vue-cropper-wrap">
          <vueCropper
            ref="cropper"
            :img="option.img"
            :outputSize="option.size"
            :outputType="option.outputType"
            :autoCrop="option.autoCrop"
            :autoCropWidth="option.autoCropWidth"
            :autoCropHeight="option.autoCropHeight"
            :centerBox="option.centerBox"
            :fixedBox="option.fixedBox"
          ></vueCropper>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { VueCropper } from "vue-cropper";
export default {
  components: {
    VueCropper
  },
  data() {
    return {
      option: {
        img: "",
        size: 1,
        outputType: "jpeg",
        autoCrop: true,
        autoCropWidth: 400,
        autoCropHeight: 400,
        centerBox: true,
        fixedBox: true
      }
    };
  },
  methods: {
    onFileChange() {
      var file = event.target.files[0];
      if (!/\.(gif|jpg|jpeg|png|bmp|GIF|JPG|PNG)$/.test(event.target.value)) {
        alert(".gif,jpeg,jpg,png,bmpファイルしかアップロードできません。");
        return false;
      }
      var reader = new FileReader();
      reader.onload = e => {
        let data;
        if (typeof e.target.result === "object") {
          data = window.URL.createObjectURL(new Blob([e.target.result]));
        } else {
          data = e.target.result;
        }
        this.option.img = data;
      };
      reader.readAsArrayBuffer(file);
    }
  }
};
</script>

<<style>
  * {
    margin: 0;
    padding: 0;
  }

  .content {
    margin: auto;
    max-width: 1200px;
    margin-bottom: 100px;
  }

  .show-info {
    margin-bottom: 50px;
  }

  .show-info h2 {
    line-height: 50px;
  }

  .vue-cropper-wrap {
    height: 500px;
  }
</style>

