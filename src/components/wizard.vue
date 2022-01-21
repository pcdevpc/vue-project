<template>
  <div class="wizard">
    <div class="form">
      <video
        controls="controls"
        preload="auto"
        poster="https://ce.prismview.com/api/files/templates/4doy2zpkcxt1ic3/poster/poster.jpg"
        src="https://ce.prismview.com/api/files/templates/4doy2zpkcxt1ic3/main/360/4doy2zpkcxt1ic3_360.mp4"
        type="video/mp4"
      ></video>
      <div>
        <b-form @submit="onSubmit" @reset="onReset" v-if="show">
          <div class="row">
            <label class="col">Project Name:</label>

            <b-form-input
              class="col"
              id="input-1"
              v-model="form.name"
              type="name"
              required
            ></b-form-input>
          </div>

          <div class="row">
            <label class="col">File Format:</label>
            <b-form-select
              class="col"
              id="input-2"
              v-model="form.outputOptions"
              :options="outputOptions"
              required
            ></b-form-select>
          </div>

          <b-form-group id="input-group-3" v-slot="{ ariaDescribedby }">
            <div class="row">
              <label class="col">Display Size:</label>
              <b-form-checkbox-group
                class="col"
                v-model="form.displaySize"
                id="checkboxes-3"
                :aria-describedby="ariaDescribedby"
              >
                <b-form-checkbox value="oneTwenty8">128X128</b-form-checkbox>
              </b-form-checkbox-group>
            </div>
          </b-form-group>

          <b-form-group id="input-group-4" v-slot="{ ariaDescribedby }">
            <div class="row">
              <label class="col">Social Media Size(s):</label>
              <b-form-checkbox-group
                class="col"
                v-model="form.socialMediaSize"
                id="checkboxes-4"
                :aria-describedby="ariaDescribedby"
              >
                <b-form-checkbox value="standard"> Standard </b-form-checkbox>
                <b-form-checkbox value="hd">HD</b-form-checkbox>
              </b-form-checkbox-group>
            </div>
          </b-form-group>

          <b-button type="submit" variant="primary">Submit</b-button>
          <b-button type="reset" variant="danger">Reset</b-button>
        </b-form>
        <b-card class="mt-3" header="Form Data Result">
          <pre class="m-0">{{ form }}</pre>
        </b-card>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "wizard",

  data() {
    return {
      form: {
        name: "",
        outputOptions: null,
        displaySize: [],
        socialMediaSize: [],
      },
      outputOptions: [{ text: "", value: null }, "WMV", "MP4", "JPG"],
      show: true,
    };
  },
  mounted() {
    axios
      .get(
        "https://hoazygo0r9.execute-api.us-west-2.amazonaws.com/default/wizard-test"
      )
      .then((response) => {
        this.form = response.data;
      });
  },
  methods: {
    onSubmit(event) {
      event.preventDefault();
      alert(JSON.stringify(this.form));
    },
    onReset(event) {
      event.preventDefault();
      this.form.name = "";
      this.form.outputOptions = null;
      this.form.displaySize = [];
      this.form.socialMediaSize = [];
      this.show = false;
      this.$nextTick(() => {
        this.show = true;
      });
    },
  },
};
</script>

<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
video {
  width: 100%;
  background-color: #d3d3d3;
  -webkit-box-sizing: border-box;
  object-fit: contain;
  box-sizing: border-box;
}
.form {
  margin: 0 auto 0 auto;
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-orient: vertical;
  -webkit-box-direction: normal;
  -ms-flex-direction: column;
  flex-direction: column;
  -webkit-box-align: center;
  -ms-flex-align: center;
  align-items: center;
  -webkit-box-pack: center;
  -ms-flex-pack: center;
  justify-content: center;
  width: 100%;
}

.wizard {
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-orient: vertical;
  -webkit-box-direction: normal;
  -ms-flex-direction: column;
  flex-direction: column;
  height: auto;
  width: 100%;
  margin: 20px auto 0 auto;
}

@media only screen and (min-width: 1200px) {
  .wizard {
    max-width: 750px;
  }
} ;
</style>
