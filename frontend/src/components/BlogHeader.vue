<template>
  <nav class="navbar navbar-expand-lg bg-light navbar-light">
    <div class="container">
      <router-link class="navbar-brand" :to="{name: 'Home'}">
        Kai's Blog
      </router-link>
      <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent"
              aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>

      <!-- start Navbar Content-->
      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav ms-auto mb-2 mb-lg-0">
          <!-- start Home-->
          <li class="nav-item">
            <router-link class="nav-link" :to="{name: 'Home'}">
              Home
            </router-link>
          </li>
          <!-- end Home-->

          <!-- start Skills-->
          <li class="nav-item">
            <router-link class="nav-link" :to="{name: 'MySkills'}">
              My Skills
            </router-link>
          </li>
          <!-- end About-->

          <!-- start Blog-->
          <li class="nav-item">
            <router-link class="nav-link" :to="{name: 'Blog'}">
              Blog
            </router-link>
          </li>
          <!-- end Blog-->

          <!-- start About-->
          <li class="nav-item">
            <router-link class="nav-link" :to="{name: 'About'}">
              About
            </router-link>
          </li>
          <!-- end About-->

          <!-- start User Center-->
          <!-- if user is login-->
          <li class="nav-item dropdown" v-if="hasLogin">
            <a class="nav-link dropdown-toggle" href="#" id="navbarDropdownMenuLink" role="button"
               data-bs-toggle="dropdown" aria-expanded="false">
              <i class="bi bi-person-circle"></i>
            </a>
            <ul class="dropdown-menu" aria-labelledby="navbarDropdownMenuLink">
              <li>
                <a class="dropdown-item" href="#">
                  Signed in as: <br>
                  <b>{{username}}</b>
                </a>
              </li>
              <li><hr class="dropdown-divider"></li>
              <li>
                <router-link class="dropdown-item" :to="{ name: 'UserCenter', params: { username: username }}">User
                  Center
                </router-link>
              </li>
              <li>
                <router-link class="dropdown-item" :to="{ name: 'ArticleCreate' }" v-if="isSuperuser">Published
                  Articles
                </router-link>
              </li>
              <li><hr class="dropdown-divider"></li>
              <li>
                <router-link class="dropdown-item" to="/" v-on:click.prevent="logout()">Log Out</router-link>
              </li>
            </ul>
          </li>

          <!-- if user is not login-->
          <li class="nav-item" v-else>
            <router-link to="/login" class="nav-link">Login</router-link>
          </li>
          <!-- end User Center-->
        </ul>

      </div>
      <!-- end Navbar Content-->
    </div>
  </nav>
</template>

<script>
import authorization from '@/utils/authorization';

export default {
  name: 'BlogHeader',
  data: function () {
    return {
      username: '',
      hasLogin: false,
      isSuperuser: JSON.parse(localStorage.getItem('isSuperuser.myblog')),
    }
  },
  mounted() {
    authorization().then((data) => [this.hasLogin, this.username] = data);
  },
  methods: {
    logout() {
      localStorage.clear();
      window.location.reload(false);
    },
    refresh() {
      this.username = localStorage.getItem('username.myblog');
    }
  }
}
</script>

<style scoped>
/* hover effect for link */
.navbar .navbar-nav .nav-link:hover {
  color: #0ac4c4;
}

/*@media only screen and (min-width: 960px) {*/
/*  .navbar .navbar-nav .nav-link {*/
/*    padding: 1em 0.7em;*/
/*  }*/

/*  .navbar {*/
/*    padding: 0;*/
/*  }*/

/*  .navbar .navbar-brand {*/
/*    padding: 0 0.7em;*/
/*  }*/
/*}*/

/*.navbar .navbar-nav .nav-link {*/
/*  position: relative;*/
/*}*/

/*.navbar .navbar-nav .nav-link::after {*/
/*  position: absolute;*/
/*  bottom: 0;*/
/*  left: 0;*/
/*  right: 0;*/
/*  margin: auto;*/
/*  background-color: #0ac4c4;*/
/*  color: transparent;*/
/*  width: 0%;*/
/*  content: '';*/
/*  height: 3px;*/
/*  transition: all 0.5s;*/
/*}*/

/*.navbar .navbar-nav .nav-link:hover::after {*/
/*  width: 100%;*/
/*}*/
</style>