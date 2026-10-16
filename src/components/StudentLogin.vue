
<template>
  <div class="login-container">
    <div class="edit-form">
      <h2>Student Login</h2>

      <form @submit.prevent="login">
        <label for="studentId">Student ID</label>
        <input
          id="studentId"
          v-model="studentLoginRequest.studentId"
          required
        />

        <label for="password">Password</label>
        <input
          id="password"
          type="password"
          v-model="studentLoginRequest.password"
          required
        />

        <button type="submit">Login</button>
        <button type="button" @click="showModal = true">
          Create Account
        </button>
      </form>

      <p v-if="message">{{ message }}</p>
    </div>

    <div v-if="showModal" class="modal-overlay">
      <div class="modal-card">
        <h2>Create Student Account</h2>

        <form @submit.prevent="submitRegistration">
          <label for="newStudentId">Student ID</label>
          <input id="newStudentId" v-model="newStudent.studentId" required />

          <label for="newPassword">Password</label>
          <input
            id="newPassword"
            type="password"
            v-model="newStudent.password"
            required
          />

          <label for="studentName">Full Name</label>
          <input id="studentName" v-model="newStudent.name" required />

          <label for="studentEmail">Email</label>
          <input
            id="studentEmail"
            type="email"
            v-model="newStudent.email"
            required
          />

          <button type="submit">Submit</button>
          <button type="button" @click="closeModal">Cancel</button>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "StudentLogin",

  data() {
    return {
      studentLoginRequest: {
        studentId: "",
        password: ""
      },
      message: "",
      showModal: false,
      newStudent: {
        studentId: "",
        password: "",
        name: "",
        email: ""
      }
    };
  },

  methods: {
    login() {
      this.message =
        "Login form is ready. A backend login service is not connected yet.";
    },

    submitRegistration() {
      console.log("Registration details entered:", this.newStudent);
      this.message = "Demo registration form submitted.";
      this.closeModal();
    },

    closeModal() {
      this.showModal = false;
      this.newStudent = {
        studentId: "",
        password: "",
        name: "",
        email: ""
      };
    }
  }
};
</script>

<style scoped>
.login-container {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  background: #eaf2f8;
  padding: 20px;
}

.edit-form,
.modal-card {
  width: 100%;
  max-width: 360px;
  padding: 25px;
  background: white;
  border-radius: 8px;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.15);
}

label {
  display: block;
  margin-top: 12px;
  margin-bottom: 5px;
}

input {
  box-sizing: border-box;
  width: 100%;
  padding: 9px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

button {
  margin-top: 15px;
  margin-right: 8px;
  padding: 9px 12px;
  cursor: pointer;
}

.modal-overlay {
  position: fixed;
  inset: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 20px;
  background: rgba(0, 0, 0, 0.5);
}
</style>
