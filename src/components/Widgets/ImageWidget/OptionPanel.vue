<template>
  <option-panel-tabs v-model:options="localOptions">
    <template #main-tab>
      <div class="option-panel-container">
        <div class="row q-col-gutter-md">
          <div class="input-container col-12 q-mt-md">
            <div class="outsideLabel">آدرس عکس</div>
            <image-uploader v-model:file="localOptions.imageSource" />
          </div>
          <!--          <div class="input-container q-py-md">-->
          <!--            <div class="outsideLabel">height</div>-->
          <!--            <q-input v-model="localOptions.height"-->
          <!--                     label="image" />-->
          <!--          </div>-->
          <div class="input-container col-4">
            <div class="outsideLabel">size</div>
            <q-select v-model="size"
                      :options="sizeOptions"
                      label="page size" />
          </div>
          <div class="input-container col-4">

            <div class="outsideLabel">عرض در سایز {{size}}</div>
            <q-input v-model="localOptions[size].width"
                     label="width" />
          </div>
          <div class="input-container col-4">

            <div class="outsideLabel">ارتفاع در سایز {{size}}</div>
            <q-input v-model="localOptions[size].height"
                     label="height" />
          </div>
          <div class="input-container col-12">
            <div class="outsideLabel">لینک عکس در سایز {{size}}</div>
            <q-input v-model="localOptions[size].src"
                     label="image link" />
          </div>
          <div class="action col-md-12">
            <div class="cehckBox">
              <q-checkbox v-model="localOptions.hasAction"
                          label="hasAction"
                          right-label />
            </div>
            <div v-if="localOptions.hasAction"
                 class="action-container">
              <div class="col-3">
                <q-select v-model="localOptions.action.type"
                          :options="actionTypes" />
              </div>
              <div v-if="localOptions.action.type === 'link'"
                   class="col-9">
                <q-input v-model="localOptions.action.route"
                         label="route" />
              </div>
              <div v-if="localOptions.action.type === 'event'"
                   class="col-6">
                <q-input v-model="localOptions.action.eventName"
                         label="event name" />
              </div>
              <div v-if="localOptions.action.type === 'event'"
                   class="col-6">
                <q-input v-model="localOptions.action.eventArgs"
                         label="event args" />
              </div>
            </div>
          </div>
        </div>
      </div>
    </template>
  </option-panel-tabs>
</template>

<script>
import { defineComponent } from 'vue'
import { mixinOptionPanel } from 'quasar-ui-q-page-builder'
import ImageUploader from 'src/components/ImageUploader.vue'
import OptionPanelTabs from 'quasar-ui-q-page-builder/src/components/OptionPanelComponents/OptionPanelTabs.vue'

export default defineComponent({
  name: 'OptionPanel',
  components: { ImageUploader, OptionPanelTabs },
  mixins: [mixinOptionPanel],
  data() {
    return {
      size: 'xs',
      sizeOptions: ['xs', 'sm', 'md', 'lg', 'xl'],
      actionTypes: ['event', 'link', 'full-view'],
      defaultOptions: {
        imageSource: null,
        ratio: null,
        hasAction: false,
        action: {
          name: null,
          route: null,
          scrollTo: null,
          eventName: null,
          eventArgs: null
        },
        xs: {
          height: null,
          width: null,
          src: null
        },
        sm: {
          height: null,
          width: null,
          src: null
        },
        md: {
          height: null,
          width: null,
          src: null
        },
        lg: {
          height: null,
          width: null,
          src: null
        },
        xl: {
          height: null,
          width: null,
          src: null
        }
      }
    }
  }
})
</script>
