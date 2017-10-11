<template>
    <section class="is-bold app-navbar animated" :class="{ slideInDown: show, slideOutDown: !show }">
        <div class="hero-head">
            <nav class="navbar">
                <div class="navbar-brand">
                    <transition name="scaleFade" mode="out-in">
                        <a class="navbar-item hero-brand" v-if="authStatus" href="/">
                            <img src="~assets/puff.svg" /> &nbsp;
                            <strong>vuexfire</strong> admin
                        </a>
                    </transition>
                    <transition name="scaleFade">
                        <a class="navbar-item hero-brand" v-if="!authStatus" href="/">
                            <img src="~assets/logo.svg" :alt="pkginfo.description">
                            <tooltip :label="'v' + pkginfo.version" placement="right" type="success" size="small" :no-animate="true" :always="true" :rounded="true">
                                <div class="is-hidden-mobile">
                                    <span class="vue">Vue</span>
                                    <strong class="admin">Admin</strong>
                                </div>
                            </tooltip>
                        </a>
                    </transition>

                    <div class="navbar-burger burger" data-target="navMenuTransparentExample">
                        <span></span>
                        <span></span>
                        <span></span>
                    </div>
                </div>

                <div id="navMenuTransparentExample" class="navbar-menu">
                    <div class="navbar-start">

                    </div>

                    <div class="navbar-end">
                        <router-link v-if="!this.$store.state.auth.loggedIn" to="/login-firebase" class="navbar-item">Login Firebase</router-link>
                        <a v-if="this.$store.state.auth.loggedIn" @click="signOut" class="navbar-item">Logout</a>

                        <a class="navbar-item is-hidden-tablet" @click="toggleSidebar({opened: !sidebar.opened})">
                            <i class="fa fa-bars" aria-hidden="true" v-show="!sidebar.hidden"></i>
                        </a>

                        <!-- <a class="navbar-item is-hidden-desktop-only" href="https://github.com/jgthms/bulma" target="_blank">
                                        <span class="icon" style="color: #333;">
                                          <i class="fa fa-lg fa-github"></i>
                                        </span>
                                      </a>
                                      <a class="navbar-item is-hidden-desktop-only" href="https://twitter.com/jgthms" target="_blank">
                                        <span class="icon" style="color: #55acee;">
                                          <i class="fa fa-lg fa-twitter"></i>
                                        </span>
                                      </a>
                                      <div class="navbar-item">
                                        <div class="field is-grouped">
                                          <p class="control">
                                            <a class="bd-tw-button button" data-social-network="Twitter" data-social-action="tweet" data-social-target="http://bulma.io" target="_blank" href="https://twitter.com/intent/tweet?text=Bulma: a modern CSS framework based on Flexbox&hashtags=bulmaio&url=http://bulma.io&via=jgthms">
                                              <span class="icon">
                                                <i class="fa fa-twitter"></i>
                                              </span>
                                              <span>
                                                Tweet
                                              </span>
                                            </a>

                                          </p>
                                          <p class="control">
                                            <a class="button is-primary" href="https://github.com/jgthms/bulma/releases/download/0.6.0/bulma-0.6.0.zip">
                                              <span class="icon">
                                                <i class="fa fa-download"></i>
                                              </span>
                                              <span>Download</span>
                                            </a>
                                          </p>
                                        </div>
                                      </div> -->
                    </div>
                </div>
            </nav>

        </div>
    </section>
</template>

<script>
import Tooltip from 'vue-bulma-tooltip'
import { mapGetters, mapActions } from 'vuex'

export default {

    components: {
        Tooltip
    },

    props: {
        show: Boolean
    },

    computed: mapGetters({
        pkginfo: 'pkg',
        sidebar: 'sidebar',
        authStatus: 'authStatus'
    }),

    methods: {
        ...mapActions([
            'toggleSidebar',
            'signOut'
        ]),
        logout() {
            this.$auth.logout({
                redirect: 'Home',
                makeRequest: false
                // params: {},
                // success: function () {},
                // error: function () {},
                // etc...
            })
        }
    }
}
</script>

<style lang="scss">
@import '~bulma/sass/utilities/initial-variables';

.app-navbar {
    position: fixed;
    min-width: 100%;
    z-index: 1024;
    box-shadow: 0 2px 3px rgba(17, 17, 17, 0.1), 0 0 0 1px rgba(17, 17, 17, 0.1);

    .container {
        margin: auto 10px;
    }

    .nav-right {
        align-items: stretch;
        align-items: stretch;
        flex: 1;
        justify-content: flex-end;
        overflow: hidden;
        overflow-x: auto;
        white-space: nowrap;
    } // .nav-center {
    //   position: relative;
    //   .navbar-item.hero-brand {
    //     position:absolute;
    //     top:5px;
    //   }
    // }
}

.hero .nav {
    background: #ffffff;
}

.hero-brand {
    .vue {
        margin-left: 10px;
        color: #36AC70;
    }
    .admin {
        color: #28374B;
    }
}

.scaleFade-enter-active,
.scaleFade-leave-active {
    opacity: 1;
    transform: scale(1);
    transition: all .25s ease-in-out;
}

.scaleFade-enter,
.scaleFade-leave-active {
    opacity: 0;
    transform: scale(1.1);
}

.slideUp-enter-active,
.slideUp-leave-active {
    opacity: 1;
    transform: translate(0, 0) scale(1);
    transition: all .25s ease-in-out;
}

.slideUp-enter,
.slideUp-leave-active {
    opacity: 0;
    transform: translate(0px, -100px) scale(0.6);
}
</style>
