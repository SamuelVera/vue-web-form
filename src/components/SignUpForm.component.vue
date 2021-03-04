<template>
  <!--Listen to the submit event of the form and use modifier prevent to prevent default behavior-->
  <form @submit.prevent="onSubmit">
    <label>Email:</label>
    <!--v-model directive is used for 2-way databinding-->
    <!--v-model binds the given property of the data object to this input-->
    <input type="email" required v-model="email" />

    <label>Password:</label>
    <input type="password" required v-model="password" />
    <p v-if="passwordError" class="error">{{ passwordError }}</p>

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

    <!--Keyboard events-->
    <label>Skills:</label>
    <!--Listen for @keyup event with alt key pressed -->
    <input @keyup.alt="addSkill" type="text" v-model="tempSkill" />
    <div
      class="pill"
      v-for="(skill, idx) in skills"
      @click="deleteSkill(idx)"
      :key="skill"
    >
      {{ skill }}
    </div>

    <!--Submit button-->
    <div class="submit">
      <button type="submit">Create an account</button>
    </div>
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
      /**User skills */
      skills: [],
      /**Temporal skill to add to the array */
      tempSkill: "",
      //Errors
      /**Password error */
      passwordError: "",
    };
  },
  methods: {
    /**Adds a skill to the array */
    addSkill(e) {
      if (this.tempSkill && e.key === ",") {
        //Add skill only when user presses the comma and there's data
        if (!this.skills.includes(this.tempSkill)) {
          //Avoid duplicates
          //Push to array
          this.skills.push(this.tempSkill);
        }
        //Clear temporal
        this.tempSkill = "";
      }
    },
    /**Deletes a given skill based on the index */
    deleteSkill(idx) {
      //Filter the given index
      this.skills = this.skills.filter((_, i) => i !== idx);
    },
    /**Handle submit form */
    onSubmit() {
      //Validate password
      this.passwordError =
        this.password.length > 5
          ? ""
          : "Password must be at least 6 characters long";
      if (!this.passwordError) {
        //No error, do submit logic
        console.log("Email:", this.email);
        console.log("Password:", this.password);
        console.log("Role:", this.role);
        console.log("Skills:", this.skills);
        console.log("Accepted terms:", this.terms);
      }
    },
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
.pill {
  display: inline-block;
  margin: 20px 10px 0 0;
  padding: 6px 12px;
  background: #eee;
  border-radius: 20px;
  font-size: 12px;
  letter-spacing: 1px;
  font-weight: bold;
  color: #777;
  cursor: pointer;
  opacity: 1;
  transition: 0.3s;
}
.pill:hover {
  opacity: 0.7;
}
button {
  background: #0b6dff;
  border: 0;
  padding: 10px 20px;
  margin-top: 20px;
  color: white;
  border-radius: 20px;
  cursor: pointer;
  opacity: 1;
  transition: 0.3s;
}
button:hover {
  opacity: 0.7;
}
.submit {
  text-align: center;
}
p.error {
  color: #ff0062;
  margin-top: 10px;
  font-size: 0.8em;
  font-weight: bold;
}
</style>
