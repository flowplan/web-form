<template>
  <form @submit.prevent="handleSubmit">
    <label>Email</label>
    <input v-model="email" type="email" required />

    <label>Password</label>
    <input v-model="password" type="password" required />
    <div v-if="passwordError" class="error">{{ passwordError }}</div>

    <label>Role:</label>
    <select v-model="role">
      <option value="Designer">Web Designer</option>
      <option value="Developer">Web Developer</option>
    </select>

    <label>Skills:</label>
    <input type="text" v-model="tempSkill" @keyup.alt="addSkill" />
    <div v-for="skill in skills" :key="skill" class="pill">
      <span @click="deleteSkill(skill)">{{ skill }}</span>
    </div>

    <div class="terms">
      <input v-model="terms" type="checkbox" required />
      <label>Accept Terms and Conditions</label>
    </div>

    <div class="submit">
      <button>Create Account</button>
    </div>

    <!-- <div>
      <input type="checkbox" value="ace" v-model="names" />
      <label>Ace</label>
    </div>
    <div>
      <input type="checkbox" value="darwin" v-model="names" />
      <label>Darwin</label>
    </div>
    <div>
      <input type="checkbox" value="flow" v-model="names" />
      <label>Flow</label>
    </div> -->
  </form>

  <p>Email: {{ email }}</p>
  <p>Password: {{ password }}</p>
  <p>Role: {{ role }}</p>
  <p>Terms Accepted: {{ terms }}</p>
  <!-- <p>Names: {{ names }}</p> -->
</template>

<script>
export default {
  data() {
    return {
      email: "",
      password: "",
      role: "Designer",
      terms: false,
      tempSkill: "",
      skills: [],
      passwordError: "",
      //   names: [],
    };
  },
  methods: {
    addSkill(e) {
      if (e.key === "," && this.tempSkill) {
        if (!this.skills.includes(this.tempSkill)) {
          this.skills.push(this.tempSkill);
        }
        this.tempSkill = "";
      }
    },
    deleteSkill(skill) {
      //deleting a array
      this.skills = this.skills.filter((item) => {
        //matching the (item) and skills

        //condition if the filter is same it is remove from array
        return skill !== item;
      });
    },
    handleSubmit() {
      //validatepassword
      // character length validation
      this.passwordError =
        this.password.length > 5 ? "" : "Password must 6 characters long";

      if (!this.passwordError) {
        console.log("email: ", this.email);
        console.log("password: ", this.password);
        console.log("roles: ", this.role);
        console.log("skills: ", this.skills);
        console.log("term accepeted: ", this.terms);
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
  border-bottom: 1px white solid;
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
  margin: 0 10px 0 0;
  padding: 6px 12px;
  background: #eee;
  border-radius: 20px;
  letter-spacing: 1px;
  font-weight: bold;
  color: #777;
  cursor: pointer;
}

button {
  background: rgb(95, 95, 255);
  border: 0;
  padding: 10px 20px;
  margin-top: 20px;
  color: white;
  border-radius: 20px;
  cursor: pointer;
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