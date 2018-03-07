<template>
  <div id="app container-fluid">
    <div class="card m-5">
      <div class="card-body">
        <h5 class="card-title">Загрузка изображения</h5>
        <div class="row m-0">
          <div class="col-6 custom-file">
            <input type="file" class="custom-file-input" @change="onFileChange" id="customFile">
            <label class="custom-file-label" for="customFile">Choose file</label>
          </div>
          <div class="col-6"> <img v-show="image" class="img-fluid" :src="image"> </div>
        </div>
      </div>
    </div>
    <div class="card m-5">
      <div class="card-body">
        <h5 class="card-title">Загрузка JSON</h5>
        <div class="row m-0">
          <div class="col-6 custom-file">
            <input type="file" class="custom-file-input" @change="onFileChange" id="customFile">
            <label class="custom-file-label" for="customFile">Choose file</label>
          </div>
          <div class="col-6" v-show="json"> {{ json }} </div>
        </div>
      </div>
    </div>
    <div class="card m-5">
      <div class="card-body">
        <h5 class="card-title">Загрузка текстового файла</h5>
        <div class="row m-0">
          <div class="col-6 custom-file">
            <input type="file" class="custom-file-input" @change="onFileChange" id="customFile">
            <label class="custom-file-label" for="customFile">Choose file</label>
          </div>
          <div class="col-6" v-show="text"> {{ text }} </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "app",
  data() {
    return {
      image: "",
      json: "",
      text: "",
    };
  },
  methods: {
    onFileChange(e) {
      var files = e.target.files || e.dataTransfer.files;
      if (!files.length) return;
      console.log(files[0].type)
      switch (files[0].type) {
        case "text/plain": this.createText(files[0]); break;
        case "": this.createJson(files[0]); break;
        default: this.createImage(files[0]); break;
      }
      if (files[0].type == "") this.createJson(files[0])
      else this.createImage(files[0]);
    },
    createImage(file) {
      var image = new Image();
      var reader = new FileReader();
      var vm = this;

      reader.onload = e => {
        vm.image = e.target.result;
      };
      reader.readAsDataURL(file);
    },
    createJson(file) {
      var reader = new FileReader(); var vm = this;
      reader.onload = e => { vm.json = e.target.result; };
      reader.readAsText(file);
    },
    createText(file) {
      var reader = new FileReader(); var vm = this;
      reader.onload = e => { vm.text = e.target.result; };
      reader.readAsText(file);
    }
  }
};
</script>

<style>

</style>
