<template>
  <form @submit.prevent="handleSubmit">
    <label>Email</label>
    <input type="email" v-model="email" required />

    <label>Password</label>
    <input type="password" v-model="password" required />
    <p v-if="passwordErr" class="error">{{ passwordErr }}</p>

    <label>Role</label>
    <select v-model="role">
      <option value="developer">Developer</option>
      <option value="designer">Designer</option>
    </select>

    <label>Skills (alt + ,)</label>
    <input type="text" v-model="tempSkills" @keyup.alt="addSkill" />
    <div
      v-for="skill in skills"
      :key="skill"
      class="pill"
      @click="deleteSkill(skill)"
    >
      {{ skill }}
    </div>

    <div class="term">
      <input id="term" type="checkbox" required v-model="terms" />
      <label for="term">Accept term & condition</label>
    </div>

    <div class="submit">
      <button type="submit">Create an Account</button>
    </div>
  </form>

  <p>
    email: {{ email }} - password: {{ password }} - Role: {{ role }} - Terms:
    {{ terms }}
  </p>
</template>

<script>
export default {
  data() {
    return {
      email: "",
      password: "",
      role: "",
      terms: false,
      skills: [],
      tempSkills: "",
      passwordErr: "",
    };
  },

  methods: {
    addSkill(e) {
      if (e.key === "," && this.tempSkills) {
        if (!this.skills.includes(this.tempSkills)) {
          this.skills.push(this.tempSkills);
        }
        this.tempSkills = "";
      }
    },

    deleteSkill(skill) {
      this.skills = this.skills.filter((sk) => sk !== skill);
    },
    handleSubmit() {
      //validate password
      this.passwordErr =
        this.password.length > 5 ? "" : "Password at Least 5 Character";
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
  letter-spacing: 1px;
  border-radius: 20px;
  font-weight: bold;
  color: #777;
  font-size: 12px;
  cursor: pointer;
}

button {
  background: #066dffff;
  border: 0;
  padding: 10px 20px;
  margin-top: 20px;
  color: white;
  border-radius: 20px;
}

.submit {
  text-align: center;
}

.error {
  color: #ff0062;
  margin-top: 10px;
  font-size: 0.8em;
  font-weight: bold;
}
</style>
