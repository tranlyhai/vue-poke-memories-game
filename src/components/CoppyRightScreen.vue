<template>
  <section class="copyright">
    <p>This game owned by TLH in vue 3 - <a href="#">View Here</a></p>
  </section>
</template>

<script>
export default {
  name: "CoppyRight"
}
</script>

<style lang="css" scoped>
.copyright {
  position: fixed;
  left: 50%;
  transform: translateX(-50%);
  bottom: 1.5rem;
  color: var(--light);
  z-index: 3;
  font-size: 1.5rem;
}

.copyright a {
  color: #f4dc26;
}
</style>
