<template>
  <div class="semi-body-register d-flex">
    <div class="main-container-register d-flex m-5">
      <div class="container1-register m-5 d-flex flex-column col-3">
        <a href="https://www.freepnglogos.com/pics/coffee-logo-png" title="Image from freepnglogos.com"
          ><img src="https://www.freepnglogos.com/uploads/coffee-logo-png/coffee-logo-design-creative-idea-logo-elements-2.png" height="500" alt="coffee logo design creative idea logo elements"
        /></a>
        <img src="https://www.freepnglogos.com/pics/coffee-logo-png" alt="" srcset="" />
      </div>
      <div class="container2-register m-5 d-flex flex-column col-7">
        <h1>Register</h1>
        <br />
        <form class="col-8" @submit.prevent="toRegister">
          <!-- First Name input -->
          <div class="form-outline mb-4">
            <input type="text" id="inputFirstNameRegister" class="form-control" placeholder="e.g. John" v-model="firstName" />
            <label class="form-label" for="inputFirstNameRegister">First Name</label>
          </div>

          <!-- Last Name input -->
          <div class="form-outline mb-4">
            <input type="text" id="inputLastNameRegister" class="form-control" placeholder="e.g. Doe" v-model="lastName" />
            <label class="form-label" for="inputLastNameRegister">Last Name</label>
          </div>

          <!-- Email input -->
          <div class="form-outline mb-4">
            <input type="email" id="inputEmailRegister" class="form-control" placeholder="e.g. johndoe@mail.com" v-model="email" />
            <label class="form-label" for="inputEmailRegister">Email address</label>
          </div>

          <!-- Password input -->
          <div class="form-outline mb-4">
            <input type="password" id="inputPasswordRegister" class="form-control" placeholder="**********" v-model="password" />
            <label class="form-label" for="inputPasswordRegister">Password</label>
          </div>

          <!-- Phone Number input -->
          <div class="form-outline mb-4">
            <input type="text" id="inputPhoneNumberRegister" class="form-control" placeholder="e.g. 08123456789" v-model="phoneNumber" />
            <label class="form-label" for="inputPhoneNumberRegister">Phone Number</label>
          </div>

          <!-- Address input -->
          <div class="form-outline mb-4">
            <input type="text" id="inputAddressRegister" class="form-control" placeholder="e.g. Jl. Asia Afrika No.17" v-model="address" />
            <label class="form-label" for="inputAddressRegister">Address</label>
          </div>

          <!-- Submit button -->
          <button type="submit" class="btn-signin btn btn-primary btn-block mb-4">Sign up</button>

          <!-- Register buttons -->
          <div class="text-center">
            <p>Back to <router-link class="to-login" to="/login">Login</router-link></p>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
import Swal from 'sweetalert2';
export default {
  name: 'Register',
  data() {
    return {
      firstName: '',
      lastName: '',
      email: '',
      password: '',
      address: '',
      phoneNumber: '',
    };
  },
  methods: {
    toRegister() {
      const payload = {
        email: this.email,
        password: this.password,
        username: this.username,
        phoneNumber: this.phoneNumber,
        address: this.address,
        firstName: this.firstName,
        lastName: this.lastName,
      };
      this.$store
        .dispatch('toRegister', payload)
        .then(() => {
          Swal.fire({
            position: 'top-end',
            icon: 'success',
            title: 'Success Register',
            footer: `Please login first`,
            showConfirmButton: false,
            timer: 2500,
          });
          this.$router.push('/login');
        })
        .catch((err) => {
          if (err.response.data.message == 'Email must be unique') {
            Swal.fire({
              position: 'center',
              icon: 'error',
              title: 'Email already been used',
              footer: `Error ${err.response.status}: ${err.response.statusText}`,
              showConfirmButton: false,
              timer: 2000,
            });
          } else {
            Swal.fire({
              position: 'center',
              icon: 'error',
              title: err.response.data.message,
              footer: `Error ${err.response.status}: ${err.response.statusText}`,
              showConfirmButton: false,
              timer: 2000,
            });
          }
        });
    },
  },
};
</script>

<style>
.semi-body-register {
  justify-content: center;
  align-items: center;
  /* height: 100vh; */
  background-color: #4b450e;
}
.container1-register {
  justify-content: center;
  align-items: center;
}
.container2-register {
  justify-content: center;
  align-items: center;
  display: flex;
}
.main-container-register {
  background-color: #bfd973;
  width: 75vw;
  /* height: 75vh; */
  border-radius: 40px;
}
.container2-register h1 {
  color: #4b450e;
}
.container2-register .btn-signin {
  background-color: #4b450e;
  border-color: #4b450e;
}
.container2-register .btn-signin:hover {
  background-color: #dbb736;
  border-width: 1px;
  color: #4b450e;
  font-weight: bold;
}
.container2-register .to-login {
  color: #4b450e;
}
.container2-register .to-login:hover {
  font-weight: bold;
}
.main-container-register img {
  margin-bottom: 30px;
}
</style>
