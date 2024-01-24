<template>
  <nav class="navbar navbar-expand-lg bg-black">
    <div class="container-fluid">
      <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation" >
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav me-auto mb-2 mb-lg-0">
          <li class="nav-item fs-4" v-for="item in menu" :key="index">
            <router-link :to="{ name: item.name }" class="nav-link text-white" active-class="active">{{ item.label }}</router-link>
          </li>
        </ul>
      </div>
    </div>
  </nav>
</template>

<script>
export default {
  name: "AppHeader",
  data() {
    return {
      menu: [
        {
          label: "Home",
          name: "home",
        },
        {
          label: "Projects",
          name: "projects",
        },
        {
          label: "Contact Us",
          name: "contacts",
        },
      ],
    };
  },
};
</script>

<style lang="scss" scoped>

nav {
  position: fixed;
  top: 0;
  width: 100%;
  z-index: 99;
  height: 60px;
}

.active {
  color: chartreuse!important;
}
</style>
