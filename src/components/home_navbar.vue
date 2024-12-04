<script setup>
import { ref } from "vue";

const isMenuOpen = ref(false);
const searchQuery = ref("");


const toggleMenu = () => {
  isMenuOpen.value = !isMenuOpen.value;
};

const handleSearch = () => {
  console.log("Searching for:", searchQuery.value);
};
</script>
<template>
  <nav class="navbar">
    <div class="navbar-container">

      <div class="left-section">
        <div class="logo">
          <router-link to="/">
            <img src="../assets/storemesh.png" alt="Logo" class="logo-img" />
          </router-link>
        </div>

        <div class="menu-links" :class="{ open: isMenuOpen }">
          <router-link to="/" class="nav-item">MENU1</router-link>
          <router-link to="/" class="nav-item">MENU2</router-link>
          <router-link to="/" class="nav-item">MENU3</router-link>
          <router-link to="/" class="nav-item">MENU4</router-link>
        </div>
      </div>

      <button class="hamburger" @click="toggleMenu">
        <img src="../assets/menu.png" alt="menu" class="menu-img" />
      </button>


      <div class="menu-icons">

        <form class="search-box" @submit.prevent="handleSearch">
          <input type="text" placeholder="Search..." v-model="searchQuery" class="search-input" />
        </form>
        <div class="profile-icon">
          <img src="../assets/dots-menu.png" alt="menu" class="menu-img" />
        </div>


        <div class="profile-icon">
          <img src="../assets/user.png" alt="Profile" class="profile-img" />
        </div>
      </div>
    </div>

    <div class="search-mobile">
      <img src="../assets/search-interface-symbol.png" alt="Profile" class="search-img" />
    </div>


  </nav>
</template>



<script>
export default {
  name: 'home_navbar',
};
</script>

<style scoped>
.navbar {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  background-color: white;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
  z-index: 1000;
}

.navbar-container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px 20px;
  margin: 0 auto;
}


.left-section {
  display: flex;
  align-items: center;
  gap: 20px;
}


.logo-img {
  max-height: 50px;
  object-fit: contain;
}


.menu-links {
  display: flex;
  gap: 20px;
}

.nav-item {
  text-decoration: none;
  color: black;
  font-size: 16px;
  transition: color 0.3s ease;
}

.nav-item:hover {
  color: #007bff;
}


.hamburger {
  display: none;
  flex-direction: column;
  gap: 5px;
  cursor: pointer;
  border: none;
  background: none;
}

.hamburger span {
  width: 25px;
  height: 3px;
  background-color: black;
  border-radius: 2px;
  transition: all 0.3s ease;
}


.menu-icons {
  display: flex;
  align-items: center;
  gap: 15px;
}

.search-box {
  display: flex;
  align-items: center;
  gap: 5px;
}

.search-input {
  padding: 5px 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

.menu-img {
  width: 30px;
  height: 30px;
  object-fit: cover;
}

.profile-img {
  width: 30px;
  height: 30px;
  border-radius: 50%;
  object-fit: cover;
}

.search-mobile {
  display: none;
}



@media (max-width: 768px) {


  .menu-links {
    display: none;
  }

  .menu-links.open {
    display: flex;
    flex-direction: column;

    position: absolute;
    top: 60px;
    left: 0;
    right: 0;
    background-color: white;
    padding: 10px;
    box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
  }

  .menu-links.open .nav-item {
    margin: 10px 0;
  }


  .hamburger {
    display: flex;
  }

  .menu-icons {
    display: none;

  }

  .menu-img {
    width: 20px;
    height: 20px;
  }

  .logo-img {
    max-height: 40px;
  }

  .search-img {
    width: 20px;
    height: 20px;
  }

  .search-mobile {
    display: flex;
    justify-content: end;
    padding: 0px 25px 10px;
  }
}
</style>
