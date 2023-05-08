<template>
    <header class="header">
        <a class="toggle" @click="toggleMenu" v-if="!hideToggle">
          <i class="fa angle fa-bars"></i>
        </a>
        <h1 class="title">
            <router-link to="/">{{ title }}</router-link>
        </h1>
        <UserDropdown v-if="!hideUserDropdown" />
    </header>
</template>

<script>
import UserDropdown from "./UserDropdown";

export default {
  name: "Header",
  components: { UserDropdown },
  props: {
    title: String,
    hideToggle: Boolean,
    hideUserDropdown: Boolean,
  },
  computed: {
    icon() {
      return this.$store.state.isMenuVisible
        ? "fa-angle-left"
        : "fa-angle-down";
    },
  },
  methods: {
    toggleMenu() {
      this.$store.commit("toggleMenu");
    },
  },
};
</script>

<style>
.header {
  grid-area: header;
  /* background: linear-gradient(to right, #1e469a, #49a7c1); */
  background: #1f2837;

  display: flex;
  justify-content: center;
  align-items: center;
  border-bottom: 1px solid #ccc;
}

.title {
  font-size: 2rem;
  color: #fff;
  font-weight: bolder;
  flex-grow: 1;
  text-align: center;
  margin: 0 auto;
  margin-left: 40px;
}

.title a {
  color: #fff;
  text-decoration: none;
}

.title a:hover {
  color: #ccc;
  text-decoration: none;
}

header.header > a.toggle {
  width: 60px;
  height: 100%;
  color: #000;
  justify-self: flex-start;
  text-decoration: none;

  display: flex;
  justify-content: center;
  align-items: center;
}

header.header > a.toggle:hover {
  cursor: pointer;
}

.angle {
  font-size: 2.5rem;
  color: #ccc;
}

.angle:hover {
  font-size: 2.6rem;
  color: #ccc;
}
</style>
