<template>
  <div class="main-layout">
    <quasar-template-builder @onResize="resize">
      <template #header>
        <template-header :type="getTemplateHeaderType" />
        <q-linear-progress v-if="$store.getters['loading/loading']"
                           color="primary"
                           reverse
                           class="q-mt-sm"
                           indeterminate />
      </template>
      <template #left-drawer>
        <template-side-bar :type="getLeftDrawerType" />
      </template>
      <template #content>
        <div ref="contentInside"
             v-scroll="onContentInsideScroll"
             class="content-inside">
          <q-dialog v-model="confirmDialogData.show"
                    persistent>
            <q-card class="q-pa-md q-pb-none">
              <q-card-section>
                <q-icon name="warning"
                        color="warning"
                        size="2rem" />
                {{confirmDialogData.message}}
              </q-card-section>
              <q-separator />
              <q-card-actions align="right"
                              class="q-pb-none">
                <q-btn v-close-popup
                       color="green"
                       flat
                       @click="confirmDialogAction(true)">بله</q-btn>
                <q-btn v-close-popup
                       color="red"
                       flat
                       @click="confirmDialogAction(false)">خیر</q-btn>
              </q-card-actions>
            </q-card>
          </q-dialog>
          <q-dialog v-model="loginDialog">
            <auth-login />
          </q-dialog>
          <router :include="keepAliveComponents" />
        </div>
        <floating-action-button v-if="isAdmin && canShowFloatingActionBtn" />
      </template>
      <template #footer>
        <app-footer />
      </template>
    </quasar-template-builder>
  </div>
</template>

<script>
import { User } from 'src/models/User.js'
import Router from 'src/router/Router.vue'
import AuthLogin from 'components/Auth/Auth.vue'
import AppFooter from 'src/components/Template/AppFooter.vue'
import KeepAliveComponents from 'src/assets/js/KeepAliveComponents.js'
import templateHeader from 'src/components/Template/Header/TemplateHeader.vue'
import TemplateSideBar from 'src/components/Template/SideBard/TemplateSideBar.vue'
import QuasarTemplateBuilder from 'quasar-template-builder/src/quasar-template-builder.vue'
import FloatingActionButton from 'components/Template/FloatingActionButton/FloatingActionButton.vue'

export default {
  components: {
    AuthLogin,
    Router,
    AppFooter,
    templateHeader,
    TemplateSideBar,
    FloatingActionButton,
    QuasarTemplateBuilder
  },
  data () {
    return {
      user: new User(),
      isAdmin: true,
      isUserLogin: false,
      contentVerticalScrollPosition: 0,
      keepAliveComponents: KeepAliveComponents
    }
  },
  computed: {
    canShowFloatingActionBtn () {
      // return true
      return this.hasDynamicSetting || this.hasDynamicSettingWithParams
    },
    hasDynamicSetting () {
      return !!this.$route.meta?.hasDynamicSetting
    },
    hasDynamicSettingWithParams () {
      return !!this.$route.meta?.hasDynamicSettingWithParams
    },
    loginDialog: {
      get () {
        return this.$store.getters['AppLayout/loginDialog']
      },
      set (newValue) {
        if (!newValue) {
          this.$store.commit('AppLayout/updateLoginDialog', false)
          return
        }
        this.$store.dispatch('AppLayout/showLoginDialog')
      }
    },
    confirmDialogData () {
      return this.$store.getters['AppLayout/confirmDialog']
    },
    getTemplateHeaderType() {
      return this.$store.getters['AppLayout/layoutHeaderType']
    },
    getLeftDrawerType() {
      return this.$store.getters['AppLayout/layoutLeftSideBarType']
    },
    calculateHeightStyle() {
      return this.$store.getters['AppLayout/calculateContainerFullHeight']
    }
  },
  mounted () {
    this.loadAuthData()
  },
  methods: {
    loadAuthData () { // prevent Hydration node mismatch
      this.user = this.$store.getters['Auth/user']
      this.isAdmin = this.$store.getters['Auth/isAdmin']
      this.isUserLogin = this.$store.getters['Auth/isUserLogin']
    },
    onContentInsideScroll (data) {
      this.$store.commit('AppLayout/updateLayoutHeaderElevated', data > 0)
    },
    confirmDialogAction (data) {
      if (this.confirmDialogData) {
        this.confirmDialogData.callback(data)
      } else {
        this.$store.commit('AppLayout/showConfirmDialog', {
          show: false
        })
      }
    },
    resize (val) {
      this.$store.commit('AppLayout/updateWindowSize', val)
      if (this.getLeftDrawerType === 'abrisham') {
        this.$store.commit('AppLayout/updateLayoutLeftDrawerWidth', 100)
        if (val.width < 1200) {
          this.$store.commit('AppLayout/updateLayoutLeftDrawerWidth', 80)
        } else if (val.width < 990) {
          this.$store.commit('AppLayout/updateLayoutLeftDrawerWidth', 60)
        }
      }
      // if (val.width > 1439) {
      //   this.$store.commit('AppLayout/updateLayoutLeftDrawerWidth', 314)
      //   this.$store.commit('AppLayout/updateLayoutLeftDrawerBehavior', 'mobile') && this.$store.commit('AppLayout/updateLayoutRightDrawerBehavior', 'mobile')
      // } else if (val.width > 599) {
      //   this.$store.commit('AppLayout/updateLayoutLeftDrawerWidth', 280)
      //   this.$store.commit('AppLayout/updateLayoutLeftDrawerBehavior', 'mobile') && this.$store.commit('AppLayout/updateLayoutRightDrawerBehavior', 'mobile')
      // } else {
      //   this.$store.commit('AppLayout/updateLayoutLeftDrawerWidth', 242)
      //   this.$store.commit('AppLayout/updateLayoutLeftDrawerBehavior', 'mobile') && this.$store.commit('AppLayout/updateLayoutRightDrawerBehavior', 'mobile')
      // }
    }
  }
}
</script>

<style lang="scss" scoped>
.main-layout {
  :deep(.main-layout-container) {
    background-color: #F2F2F2;
  }
  :deep(.q-layout__section--marginal) {
    background-color: transparent;
    color: inherit;
  }
  .content-inside {
    //padding-top: 20px;
  }
}
</style>
