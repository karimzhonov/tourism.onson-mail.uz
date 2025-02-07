<template>
  <div class="overflow-hidden relative h-full w-full">
<!--    <Globus v-if="globusif" :class="{'opacity-0 transition-opacity': !globusShow}"/>-->
<!--    <LeafletMap v-else :class="{'opacity-0 transition-opacity': !mapShow}"/>-->

    <LeafletMap style="z-index: 1" class="w-full h-full"/>
    <div class="absolute top-0 left-0 w-full h-full" v-if="globusif">
      <Globus style="z-index: 2" :class="{'opacity-0 transition-opacity': !globusShow, 'opacity-100 transition-opacity': globusShow}"/>
    </div>

  </div>
</template>

<script>
useHead({
  title: 'Onson Mail Tourism',
  meta: [
    {name: 'description', content: 'Cargo, turism and consalting'},
  ],
  link: [
    {rel: 'icon', type: 'image/png', href: '/logo.png'}
  ],
})
export default {
  data() {
    return {
      globusShow: true,
      globusif: true,
      mapShow: false,
    };
  },
  mounted() {
    setTimeout(this.switchToMap, 5000)
  },
  methods: {
    switchToMap() {
      // Переключаем вид на карту (Leaflet)
      // this.currentView = 'LeafletMap';
      // this.currentViewKey = 'LeafletMap'; // Обновляем ключ для анимации
      this.globusShow = false
      console.log(this.globusShow)
      setTimeout(() => {
        this.globusif = false
      }, 500)
    }
  }
}
;
</script>

<style scoped>
.fade-enter-active, .fade-leave-active {
  transition: opacity 0.5s ease;
}

.fade-enter, .fade-leave-to {
  opacity: 0;
}
</style>
