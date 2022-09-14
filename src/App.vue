<template>
  <div id="app">
    <el-form :model="form" :rules="rules">
      <el-form-item label="手机号" prop="phone">
        <privacy-input v-model="form.phone" :slice="[3, 7]"></privacy-input>
      </el-form-item>
      <el-form-item label="身份证" prop="id">
        <privacy-input v-model="form.id" :slice="[5]"></privacy-input>
      </el-form-item>
    </el-form>
  </div>
</template>

<script>
import PrivacyInput from "./components/PrivacyInput";
export default {
  name: "App",
  data() {
    return {
      form: {
        phone: "",
        id: "",
      },
      rules: {
        phone: [
          {
            required: true,
            message: "必填",
          },
        ],
      },
    };
  },
  components: {
    PrivacyInput,
  },
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
