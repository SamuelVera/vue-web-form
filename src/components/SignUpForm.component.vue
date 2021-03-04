<template>
  <form>
    <label>Email:</label>
    <!--v-model directive is used for 2-way databinding-->
    <!--v-model binds the given property of the data object to this input-->
    <input type="email" required v-model="email" />

    <label>Password:</label>
    <input type="password" required v-model="password" />

    <label>Role:</label>
    <!--v-model for a select-->
    <select v-model="role">
      <option value="developer">Web Developer</option>
      <option value="designer">Web Designer</option>
    </select>

    <div class="terms">
      <!--v-model for checkbox-->
      <input v-model="terms" type="checkbox" required />
      <label>Accept terms and conditions</label>
    </div>

    <!--
      Select from many and save the value into an array
      <div>
        <input type="checkbox" value="react" v-model="frameworks" />
        <label>React</label>
      </div>
      <div>
        <input type="checkbox" value="angularjs" v-model="frameworks" />
        <label>Angular JS</label>
      </div>
      <div>
        <input type="checkbox" value="vuejs3" v-model="frameworks" />
        <label>Vue JS 3</label>
      </div>
      <div>
        <input type="checkbox" value=".net" v-model="frameworks" />
        <label>.NET</label>
      </div>
    -->
  </form>
</template>

<script>
export default {
  data() {
    return {
      /**User email */
      email: "",
      /**User password */
      password: "",
      /**User role */
      role: "",
      /**Terms accepted or not */
      terms: false,
      /**User frameworks */
      //frameworks: [],
    };
  },
};
</script>

<style>
form {
  max-width: 420px;
  margin: 30px auto;
  background: white;
  text-align: left;
  padding: 40px;
  border-radius: 10px;
}
label {
  color: #aaa;
  display: inline-block;
  margin: 25px 0 15px;
  font-size: 0.6em;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-weight: bold;
}
input,
select {
  display: block;
  padding: 10px 6px;
  width: 100%;
  box-sizing: border-box;
  border: none;
  border-bottom: 1px solid #ddd;
  color: #555;
}
input[type="checkbox"] {
  display: inline-block;
  width: 16px;
  margin: 0 10px 0 0;
  position: relative;
  top: 2px;
}
</style>
