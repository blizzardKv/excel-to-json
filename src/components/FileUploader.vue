<template>
  <div>
    <div style="margin-bottom: 40px">
      <input accept=".xlsx" type="file" id="file" @change="handleFileUpload">
      <label for="file">Insert file here</label>
    </div>
    <div ref="output" style="border: 1px solid red;">{{ exportedStrings }}</div>
  </div>
</template>

<script>
import { read } from "xlsx";

export default {
  name: 'FileUploader',
  data() {
    return {
      exportedStrings: 'none',
    };
  },
  methods: {
    handleFileUpload(evt) {
      const file = evt.target.files[0];
      const reader = new FileReader();

      reader.onload = (e) => {
        let comboString = '';
        const data = e.target.result;
        const cfb = read(data, {type: 'binary'});

        cfb.Strings.forEach((string) => {
          comboString += `${string.t} `;
        });
        this.exportedStrings = comboString;
      };

      reader.readAsBinaryString(file);
    }
  }
}
</script>

<style scoped>

</style>
