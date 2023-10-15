<template>
     <div class="nav">
    <div class="nav-inner">
      <RouterLink class="logo" to="/">Travel Planner</RouterLink>
      <div class="mobile-nav">
        <button @click="logout" class="mb-nav-btn" v-if="isauth" >Logout</button>
        <RouterLink class="mb-nav-btn" v-else to="/login">Login</RouterLink>
        <RouterLink class="mb-nav-btn" to="/">Home</RouterLink>
        <RouterLink class="mb-nav-btn" to="/about">About</RouterLink>
        <RouterLink class="mb-nav-btn" to="/review">Reviews</RouterLink>
        <RouterLink class="mb-nav-btn" to="/contact">Contact</RouterLink>
        <RouterLink class="mb-nav-btn" to="/planner">Start</RouterLink>
      </div>
      <button class="hamburger">
        <div class="bar"></div>
      </button>
      <div class="links">
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/about">About</RouterLink>
        <RouterLink to="/review">Reviews</RouterLink>
        <RouterLink to="/contact">Contact</RouterLink>
      </div>
      <div class="s-l-btn">
        <RouterLink class="nav-btn" to="/planner">Start</RouterLink>
        <button @click="logout" class="nav-btn" v-if="isauth" >Logout</button>
        <RouterLink class="nav-btn" v-else to="/login">Login</RouterLink>
      </div>
    </div>
    
  </div>
</template>

<script>
import { RouterLink, RouterView } from 'vue-router'
import './Login.vue'
import { getAuth, onAuthStateChanged,  signOut } from "firebase/auth";
import '../assets/main.css'


export default {
  data() {
    return {
      showMenu: false,
      isauth:true
    };
  },
  methods: {
    toggleMobileMenu() {
      this.showMenu = !this.showMenu;
    },
    async logout(event) {
      event.preventDefault();
      const auth = getAuth();
      await signOut(auth); // ล็อคเอ้าท์ผู้ใช้
      this.isLoggedIn = false; // อัปเดต isLoggedIn เป็น false
      this.$router.push("/").catch(() => {}); // ไปยังหน้าหลักหลังจากล็อคเอ้าท์
    }
  },
  created() {
    const auth = getAuth();
    onAuthStateChanged(auth, (user) =>{
      if (user) {
        this.isauth = true
      }else{
        this.isauth = false
      }
    });
  },
  
};

</script>

<style scoped>
.nav {
  position: sticky;
  z-index: 90;
  left: 0;
  top: 0;
  width: 100%;
}
.nav-inner {
  height: 100px;
  width: 100%;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 16px;

  background-color: white;
  color: rgb(255, 0, 0);
  box-shadow: 0px 0.4px 7.5px rgb(121, 121, 121);
}


.links {
  padding: 5px;
  margin-right: 40px;
  display: flex;
  gap: 170px;
}

.logo {
  position: relative;
  font-weight: 700;
  font-size: 2em;
  background: linear-gradient(to top, #eb396e, #ff5454);
    color: transparent;
    -webkit-background-clip: text;
    background-clip: text;
}

.nav-btn {
  appearance: none;
  outline: none;
  border: none;
  background: none;
  cursor: pointer;
  width: 100px;

  display: inline-block;
  padding: 5px 0px;
  background-image: linear-gradient(to right, #cc2e5d, #ff5858);
  border-radius: 8px;

  color: #fff;
  font-size: 18px;
  font-weight: 700;
  text-align: center;

  box-shadow: 3px 3px rgba(0, 0, 0, 0.4);
  transition: 0.4s ease-out;

  &:hover {
    box-shadow: 6px 6px rgba(0, 0, 0, 0.6);
  }
}

.s-l-btn {
  display: flex;
  gap: 20px;

}

/* hamburger */
.hamburger {
  position: relative;
  display: block;
  width: 50px;
  cursor: pointer;
  appearance: none;
  background: none;
  outline: none;
  border: none;
  padding-right: 6px;
}

.hamburger .bar,
.hamburger::after,
.hamburger::before {
  content: "";
  display: block;
  width: 100%;
  height: 5px;
  background: linear-gradient(to right, #cc2e5d, #ff5858);
  margin: 6px 0px;
  transition: 0.4s;
  border-radius: 10px;
  opacity: 100%;
  z-index: 90;
}

.hamburger.is-active .bar {
  opacity: 0;
}

.hamburger.is-active::before {
  transform: rotate(-45deg) translate(-8px, 6px);
}

.hamburger.is-active::after {
  transform: rotate(45deg) translate(-9px, -8px);
}

.mobile-nav {
  position: fixed;
  top: 0;
  right: 0;
  left: 100%;
  width: 100%;
  height: 100vh;
  display: block;
  background-color: rgba(235, 235, 235, 0.8);
  padding-top: 40px;
  transition: 0.4s;
}

.mobile-nav.is-active {
  left: 0;
}

.mb-nav-btn {
  width: 100%;
  max-width: 200px;
  margin: 0 auto 20px;
  display: block;
  text-align: center;
  padding: 5px 16px;
  margin-top: 15px;
  background-color: rgb(255, 255, 255);
  text-decoration: none;
  border-radius: 10px;
  padding: 15px;
}

@media (min-width: 1400px) {
  .mobile-nav {
    display: none;
  }
  .hamburger {
    display: none;
  }
}
@media (max-width: 1400px) {
  .links {
    display: none;
  }
  .nav-btn {
    display: none;
  }
  .b-start {
    display: none;
  }
  .s-l-btn {
    display: none;
  }
}
</style>