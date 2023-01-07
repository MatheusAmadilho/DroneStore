<template>
  <div id="footer">
    <p>DronesStore &copy; 2023</p>
  </div>
</template>

<script>
export default {
  name: "Footer"
}
</script>

<style scoped>
  #footer {
    height: 120px;
    background-color: #222;
    border-top: 4px solid #111;
    color: #fff;
    display: flex;
    align-items: center;
    justify-content: center;
    bottom: 0;
    width: 100%;
    position: fixed;
  }
</style>