<template>
  <q-page-builder v-model:sections="currenSections"
                  v-model:options="pageConfig"
                  :editable="pageBuilderEditable"
                  :loading="pageBuilderLoading" />
</template>

<script>
import { mixinPageOptions, mixinPrefetchServerData, mixinSEO } from 'src/mixin/Mixins.js'

export default {
  name: 'Public.FabFamily',
  mixins: [mixinPrefetchServerData, mixinPageOptions, mixinSEO]
  // data: () => {
  //   return {
  //     sections: [{ data: { rows: [{ cols: [{ widgets: [{ name: 'TextWidget', options: { fontFamily: null, color: null, fontSize: null, fontWeight: null, fontStyle: null, xs: { fontSize: null, fontWeight: null, fontStyle: null }, sm: { fontSize: null, fontWeight: null, fontStyle: null }, md: { fontSize: null, fontWeight: null, fontStyle: null }, lg: { fontSize: null, fontWeight: null, fontStyle: null }, xl: { fontSize: null, fontWeight: null, fontStyle: null }, style: { marginTop: '100px', marginBottom: '4px' }, text: '<div style="text-align: center;"><font size="5" color="#a4a4a4">خانواده فب</font></div>' } }, { name: 'TextWidget', options: { fontFamily: null, color: null, fontSize: null, fontWeight: null, fontStyle: null, xs: { fontSize: null, fontWeight: null, fontStyle: null }, sm: { fontSize: null, fontWeight: null, fontStyle: null }, md: { fontSize: null, fontWeight: null, fontStyle: null }, lg: { fontSize: null, fontWeight: null, fontStyle: null }, xl: { fontSize: null, fontWeight: null, fontStyle: null }, style: { marginBottom: '', paddingBottom: '100px' }, text: '<div style="text-align: center;"><b><font size="6">با دیگر اعضای کارخانه آشنا شوید</font></b></div>' } }], options: {} }], options: {} }, { cols: [{ widgets: [{ name: 'ImageWidget', options: { imageSource: '/img/custom/Logos_111.png', ratio: null, hasAction: false, action: { name: null, route: null, scrollTo: null, eventName: null, eventArgs: null }, xs: { height: null, width: '150px', src: null }, sm: { height: null, width: null, src: null }, md: { height: null, width: null, src: null }, lg: { height: null, width: null, src: null }, xl: { height: null, width: null, src: null }, style: {} } }], options: { style: {}, colNumber: 'col-xs-12 col-sm-12 col-md-4 col-lg-4 col-xl-4', className: 'text-center' } }, { widgets: [{ name: 'ImageWidget', options: { imageSource: '/img/custom/Frame_3409.png', ratio: null, hasAction: false, action: { name: null, route: null, scrollTo: null, eventName: null, eventArgs: null }, xs: { height: null, width: '150px', src: null }, sm: { height: null, width: null, src: null }, md: { height: null, width: null, src: null }, lg: { height: null, width: null, src: null }, xl: { height: null, width: null, src: null }, style: {} } }], options: { style: {}, colNumber: 'col-xs-12 col-sm-12 col-md-4 col-lg-4 col-xl-4', className: 'text-center' } }, { widgets: [{ name: 'ImageWidget', options: { imageSource: '/img/custom/Logos_23131.png', ratio: null, hasAction: false, action: { name: null, route: null, scrollTo: null, eventName: null, eventArgs: null }, xs: { height: null, width: '150px', src: null }, sm: { height: null, width: null, src: null }, md: { height: null, width: null, src: null }, lg: { height: null, width: null, src: null }, xl: { height: null, width: null, src: null }, style: {} } }], options: { style: {}, colNumber: 'col-xs-12 col-sm-12 col-md-4 col-lg-4 col-xl-4', className: 'text-center' } }], options: { className: '', height: 'auto', boxed: true, boxedWidth: 1200, gutterXSize: 'xl', gutterYSize: 'md', absolute: 'none', paddingOfBoxedInFullWidth: '30px', style: { maxWidth: '1200px', width: '1200px' } } }] }, options: { fullHeight: false, backgrounds: { xs: { size: null, color: null, image: null, repeat: null, position: null, attachment: null }, sm: { size: null, color: null, image: null, repeat: null, position: null, attachment: null }, md: { size: null, color: null, image: null, repeat: null, position: null, attachment: null }, lg: { size: null, color: null, image: null, repeat: null, position: null, attachment: null }, xl: { size: null, color: null, image: null, repeat: null, position: null, attachment: null } }, verticalAlign: null, style: { paddingBottom: '100px', minHeight: 'auto' } } }]
  //   }
  // },
  // mounted() {
  //   this.currenSections = this.sections
  // }
}
</script>
