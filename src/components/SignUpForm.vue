<template>
  <form @submit.prevent="handleSubmit" @keydown="handleEnter">
    <label>Email:</label>
    <input type="email" required v-model="email" />
    <label>Password:</label>
    <input type="password" required v-model="password" />
    <div v-if="passError" class="err">{{ passError }}</div>
    <label>Role:</label>
    <select v-model="role">
      <option value="web developer">web developer</option>
      <option value="web designer">web designer</option>
    </select>
    <input
      type="text"
      v-model="tempSkill"
      placeholder="your skills..."
      @keyup="addSkill"
      class="skills"
      
    />
    <div class="pills" v-for="skill in skills" :key="skill" >
      <span @click="deleteSkill(skill)">{{ skill }}</span>
    </div>
    <div class="term">
      <input type="checkbox" v-model="terms" />
      <label>Accept roles</label>
    </div>
    <div class="submit">
      <button>Create Account</button>
    </div>
  </form>
</template>

<script>
export default {
  data() {
    return {
      email: "",
      password: "",
      role: "",
      terms: false,
      tempSkill: "",
      skills: [],
      passError: "",
    };
  },
  methods: {
    addSkill(e) {
      if (e.key === "Enter" && this.tempSkill) {
     
        if (this.skills.includes(this.tempSkill)) {
          alert("This skill has already added");
        } else {
        
          this.skills.push(this.tempSkill);
          this.tempSkill = "";
        }
      }
    },
    deleteSkill(skill) {
      this.skills = this.skills.filter((item) => item !== skill);
      console.log(this.skills);
    },
    handleSubmit(e) {
      if(e.key == 'Enter'){
        return;
      }
      this.passError =
        this.password.length < 6 ? "the min of pass lenght is 6 char" : "";
      console.log("email:", this.email);
      console.log("password:", this.password);
      console.log("role:", this.role);
      console.log("skills:", this.skills);
      console.log("terms accepted:", this.terms);
    },
  handleEnter(e){
    if(e.keyCode == 13)
    e.preventDefault()
    return false;
  }
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
  margin: 25px 0px 15px;
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
  margin: 0px 10px 0 0;
  position: relative;
  top: 2px;
}
.pills {
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
}
button {
  background: rgb(13, 0, 255);
  border: none;
  border-radius: 10px;
  color: white;
  padding: 10px;
  cursor: pointer;
}
.submit {
  text-align: center;
}
.err {
  color: crimson;
  margin: 7px 0px;
  font-size: 0.8rem;
  font-weight: bold;
}
.skills{
  margin-top: 30px;
}
</style>
