<template>
  <div class="auth-page">
    <!-- Registration Screen -->
    <div v-if="isRegister" class="registration">
      <h2>Register</h2>
      <form @submit.prevent="register">
        <label>Full Name</label>
        <input type="text" v-model="registerData.fullName" required />

        <label>Email</label>
        <input type="email" v-model="registerData.email" required />

        <label>Password</label>
        <input type="password" v-model="registerData.password" required />

        <label>Confirm Password</label>
        <input type="password" v-model="registerData.confirmPassword" required />

        <div class="terms">
          <input type="checkbox" v-model="registerData.agreeToTerms" required />
          <span>I agree to the terms & conditions</span>
        </div>

        <button type="submit">Register</button>
        <button type="button" @click="socialLogin">Register with Google</button>
        <p>Already have an account? <a href="#" @click="toggleScreen">Login here</a></p>
      </form>
    </div>

    <!-- Login Screen -->
    <div v-else class="login">
      <h2>Login</h2>
      <form @submit.prevent="login">
2ff54040c3fd86023cdaafc9bef468
  <input type="email" v-model="loginData.email" required />

        <label>Password</label>
        <input type="password" v-model="loginData.password" required />

        <button type="submit">Login</button>
        <button type="button" @click="socialLogin">Login with Google</button>
        <p><a href="#" @click="forgotPassword">Forgot Password?</a></p>
        <p>Don't have an account? <a href="#" @click="toggleScreen">Register here</a></p>
      </form>

    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isRegister: true,
      registerData: {
        fullName: '',
        email: '',
        password: '',
        confirmPassword: '',
        agreeToTerms: false
      },
      loginData: {
        email: '',
        password: ''
      },
       greeting: 'Hello from Parent'
    };
  },

  methods: {
    toggleScreen() {
      this.isRegister = !this.isRegister;
    },
    register() {
      if (this.registerData.password !== this.registerData.confirmPassword) {
        alert('Passwords do not match');
        return;
      }
      alert('Registration Successful');
    },
    login() {
      alert(`Logging in with ${this.loginData.email}`);
    },
    socialLogin() {
      alert('Logging in with Google');
    },
    forgotPassword() {
      alert('Password reset link sent');
    }
  }
};
</script>

<style scoped>
.auth-page {
  font-family: Arial, sans-serif;
  padding: 20px;
  max-width: 400px;
  margin: auto;
  background: #f9f9f9;
  border-radius: 8px;
}
form {
  display: flex;
  flex-direction: column;
}
label {
  margin-top: 10px;
  display: block;    /* Ensures the label is on its own line */
  text-align: left;  /* Aligns text to the left */
}
input {
  padding: 8px;
  margin: 5px 0;
  border: 1px solid #ccc;
  border-radius: 4px;
}
button {
  padding: 10px;
  margin-top: 10px;
  background: #2686edbf;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}
button:hover {
  background: #0056b3;
}
a {
  color: #007bff;
  cursor: pointer;
}
.terms {
  display: flex;
  align-items: center;
  margin-top: 10px;
}
</style>
