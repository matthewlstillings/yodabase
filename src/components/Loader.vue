<template>
  <div id="loader" class="contain">
    <div class="loader_wrapper">
      <div class="loader_spinner"></div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Loader"
};
</script>

<style lang="scss">
#loader.contain {
  position: relative;
}
.loader_wrapper {
  position: absolute;
  left: 50%;
  top: 3rem;
  transform: translate(-50%);
}
.loader_spinner {
  height: 115px;
  width: 115px;
  border: 5px solid transparent;
  border-top-color: #ffe81f;
  border-bottom-color: #ffe81f;
  border-radius: 50%;
  -webkit-animation: spin 3s linear infinite;
  animation: spin 3s linear infinite;
}

.loader_spinner::before {
  content: "";
  position: absolute;
  top: 20px;
  right: 20px;
  bottom: 20px;
  left: 20px;
  border: 5px solid transparent;
  border-top-color: white;
  border-bottom-color: white;
  border-radius: 50%;
  -webkit-animation: spin 1.5s linear infinite;
  animation: spin 1.5s linear infinite;
}
@keyframes spin {
  from {
    -webkit-transform: rotate(0deg);
    transform: rotate(0deg);
  }
  to {
    -webkit-transform: rotate(360deg);
    transform: rotate(360deg);
  }
}
</style>