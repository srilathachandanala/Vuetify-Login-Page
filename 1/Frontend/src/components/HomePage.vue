<template>
  <div class="containers">
    <h1>Welcome to Home</h1>

    <div class="buttonsHome">
      <button class="btn1">
        <router-link to="/SignUp">Sign Up</router-link>
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "HomePage",
};
</script>

<style>
.containers {
  display: flex;

  justify-content: center;
  align-items: center;
  position: absolute;
  left: 38%;
  top: 0;
  height: 90vh;
}

.buttonsHome {
  display: flex;
  flex-direction: column;
  position: absolute;
  top: 500px;
  padding: 5px;
}

.btn1 {
  width: 100px;
  height: 50px;
  text-decoration: none;
  background: orangered;
}
</style>
