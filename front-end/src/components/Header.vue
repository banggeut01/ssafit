<template>
  <v-app-bar class="px-7" app flat color="#556AE9" height="100">
    <v-toolbar-title>
      <router-link to="/">
        <v-img contain width="200px" height="55px" src="@/assets/logo_test.png"></v-img>
      </router-link>
    </v-toolbar-title>
    <v-spacer></v-spacer>
    <div v-if="isIntro" class="headerDiv px-10 d-none d-lg-flex align-center">
      <router-link to="/" @click.native="$vuetify.goTo('#Effect')" class="headerLink" style="color: white;">BENEFITS</router-link>
      <router-link to="/" @click.native="$vuetify.goTo('#Explanation')" class="headerLink" style="color: white;">HOW TO USE</router-link>
      <router-link to="/" @click.native="$vuetify.goTo('#Statistic')" class="headerLink" style="color: white;">STATISTICS</router-link>
      <router-link to="/" @click.native="$vuetify.goTo('#Recommendation')" class="headerLink" style="color: white;">RECOMMEND</router-link>
    </div>
    <v-spacer></v-spacer>
    <v-toolbar-items class="hidden-sm-and-down">
      <div class="my-auto mx-2" @click="moveMain">
        <v-btn large text color="white" v-on:mouseover="mouseover" v-on:mouseleave="mouseleave">
          <div v-if="is_hover">
            <img height="44px" src="@/assets/fire_btn.gif" alt="animated_fire">
          </div>
          <div v-else>
            GO
          </div>
        </v-btn>
      </div>
      <div v-if="islogin" class="my-auto mx-2">
        <v-btn v-if="user.name !='test'" key="MY PAGE" to="/userinfo" large text color="white">
          MY PAGE
        </v-btn>
      </div>
      <div v-if="!islogin" class="my-auto mx-2">
        <v-btn large color="#FF7033" key="LOG IN" to="/login" style="color: white;">
          LOG IN
        </v-btn>
      </div>
      <div v-if="islogin" class="my-auto mx-2">
        <v-btn large color="#FF7033" key="LOG OUT" @click="logout" style="color: white;">
          LOG OUT
        </v-btn>
      </div>
    </v-toolbar-items>
    <HelpIcon v-if="!isIntro"></HelpIcon>
  </v-app-bar>
</template>

<script>
  import HelpIcon from '@/components/items/HelpIcon.vue';

  export default {
    name: 'Header',
    components: {
      HelpIcon,
    },
    props: {
      isIntro: {
        type: Boolean,
        default: false
      }
    },
    data() {
      return {
        is_hover: false
      }
    },
    computed: {
      islogin() {
        return this.$store.state.auth.token
      },
      user() {
        return this.$store.state.auth.user
      }
    },
    methods: {
      mouseover: function () {
        this.is_hover = true
      },
      mouseleave: function () {
        this.is_hover = false
      },
      moveMain() {
        this.$router.push({name: 'Main'})
      },
      logout() {
        this.$store.dispatch('logout')
        .then(() => {
          this.$router.push('/')
        })
      }
    }
  }
</script>

<style>
.headerDiv {
  height: 55px;
  padding-top: 11px;
  padding-bottom: 11px;
  border: 3px solid rgb(87, 107, 234);
  border-radius: 2em;
  box-shadow:1px 1px #768BFE, -1px -1px rgb(81, 102, 224), 1px 1px inset #768BFE, -1px -1px inset rgb(81, 102, 224);
}

.headerLink {
  text-decoration: none;
  margin: 0 10px 0px 10px;
  font-family: 'Varela Round', sans-serif;
}

</style>