<template>
<div>
  <br/>
  <center><h2>Machine Learning Web Portal</h2></center>
  <uploader :options="log_options" class="uploader-example">
    <b>Upload Log Files:</b>
    <uploader-unsupport></uploader-unsupport>
    <uploader-drop>
      <p>Drop files here to upload or</p>
      <uploader-btn>select files</uploader-btn>
      <uploader-btn :attrs="attrs">select images</uploader-btn>
      <uploader-btn :directory="true">select folder</uploader-btn>
    </uploader-drop>
    <uploader-list></uploader-list>
  </uploader>

  <uploader :options="pm_options" class="uploader-example">
    <uploader-unsupport></uploader-unsupport>
    <uploader-drop>
      <p>Drop files here to upload or</p>
      <uploader-btn>select files</uploader-btn>
      <uploader-btn :attrs="attrs">select images</uploader-btn>
      <uploader-btn :directory="true">select folder</uploader-btn>
    </uploader-drop>
    <uploader-list></uploader-list>
  </uploader>

  <uploader :options="alarm_options" class="uploader-example">
    <uploader-unsupport></uploader-unsupport>
    <uploader-drop>
      <p>Drop files here to upload or</p>
      <uploader-btn>select files</uploader-btn>
      <uploader-btn :attrs="attrs">select images</uploader-btn>
      <uploader-btn :directory="true">select folder</uploader-btn>
    </uploader-drop>
    <uploader-list></uploader-list>
  </uploader>

  <div class="myform">
  <b-form @submit="onSubmit" @reset="onReset" v-if="show">
    <b-form-group
      id="input-group-1"
      label="Email address:"
      label-for="input-1"
      description="We'll never share your email with anyone else."
    >
      <b-form-input
        id="input-1"
        v-model="form.email"
        type="email"
        placeholder="Enter email"
        required
      ></b-form-input>
    </b-form-group>

    <b-form-group id="input-group-2" label="Your Name:" label-for="input-2">
      <b-form-input
        id="input-2"
        v-model="form.name"
        placeholder="Enter name"
        required
      ></b-form-input>
    </b-form-group>

    <b-form-group id="input-group-3" label="Food:" label-for="input-3">
      <b-form-select
        id="input-3"
        v-model="form.food"
        :options="foods"
        required
      ></b-form-select>
    </b-form-group>

    <b-form-group id="input-group-4" v-slot="{ ariaDescribedby }">
      <b-form-checkbox-group
        v-model="form.checked"
        id="checkboxes-4"
        :aria-describedby="ariaDescribedby"
      >
        <b-form-checkbox value="me">Check me out</b-form-checkbox>
        <b-form-checkbox value="that">Check that out</b-form-checkbox>
      </b-form-checkbox-group>
    </b-form-group>

    <b-button type="submit" variant="primary">Submit</b-button>
    <b-button type="reset" variant="danger">Reset</b-button>
  </b-form>
  <b-card class="mt-3" header="Form Data Result">
    <pre class="m-0">{{ form }}</pre>
  </b-card>
</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      log_options: {
        target: "http://fedora.durd.site:5000/upload_logs",
        testChunks: false,
        chunkSize: 1024 * 1024 * 2, // 1MB
        simultaneousUploads: 3, // 并发上传数
        headers: {
          "access-token": "abcd1234",
        },
      },
      alarm_options: {
        target: "http://fedora.durd.site:5000/upload_alarm",
        testChunks: false,
        chunkSize: 1024 * 1024 * 2, // 1MB
        simultaneousUploads: 3, // 并发上传数
        headers: {
          "access-token": "abcd1234",
        },
      },
      pm_options: {
        target: "http://fedora.durd.site:5000/upload_pms",
        testChunks: false,
        chunkSize: 1024 * 1024 * 2, // 1MB
        simultaneousUploads: 3, // 并发上传数
        headers: {
          "access-token": "abcd1234",
        },
      },
      attrs: {
        accept: "image/*",
      },
      form: {
        email: "",
        name: "",
        food: null,
        checked: [],
      },
      foods: [
        { text: "Select One", value: null },
        "Carrots",
        "Beans",
        "Tomatoes",
        "Corn",
      ],
      show: true,
    };
  },
  options: {
    inquiry: [
      { value: "feature", text: "Feature Request" },
      { value: "bug", text: "Bug Report" },
      { value: "support", text: "Support" },
    ],
  },
  methods: {
    onSubmit(event) {
      event.preventDefault();
      alert(JSON.stringify(this.form));
    },
    onReset(event) {
      event.preventDefault();
      // Reset our form values
      this.form.email = "";
      this.form.name = "";
      this.form.food = null;
      this.form.checked = [];
      // Trick to reset/clear native browser form validation state
      this.show = false;
      this.$nextTick(() => {
        this.show = true;
      });
    },
  },
};
</script>

<style>
@import "https://cdnjs.cloudflare.com/ajax/libs/bulma/0.4.4/css/bulma.min.css";
.myform {
  width: 880px;
  padding: 15px;
  margin: 20px auto 0;
  font-size: 12px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.4);
}
.uploader-example {
  width: 880px;
  padding: 15px;
  margin: 20px auto 0;
  font-size: 12px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.4);
}
.uploader-example .uploader-btn {
  margin-right: 4px;
}
.uploader-example .uploader-list {
  max-height: 120px;
  overflow: auto;
  overflow-x: hidden;
  overflow-y: auto;
}
</style>
