<template>
    <section id="services" class="pt-20 md:pt-24 relative">
        <AtomsContainer>
            <div class="flex justify-between items-center pb-6">
                <div class="">
                    <AtomsTitle :texte="$t('Наши услуги')" />
                </div>
            </div>
            <div class="relative">
                <!--  -->
                <div 
                    class="flex absolute top-1/2 -left-5 -translate-y-1/2 z-10 transition duration-300 ease-linear" 
                    :class="prevIsVisible?'visible opacity-100':'insisible opacity-0'" 
                    
                    >
                    <AtomsSwiperNavButton @click="scrollToLeft()">
                        <IconsPrevIco />
                    </AtomsSwiperNavButton>
                </div><!--  -->
                <div  
                    class="flex absolute top-1/2 -right-5 -translate-y-1/2 z-10 transition duration-300 ease-linear" 
                    :class="nextIsVisible ? 'visible opacity-100':'insisible opacity-0'">
                    <AtomsSwiperNavButton @click="scrollToRight()">
                        <IconsNextIco />
                    </AtomsSwiperNavButton>
                </div>

                <div data-slide-recent @scroll="initScroll()"
                    class="flex items-stretch gap-5 overflow-hidden overflow-x-auto invisible-scroll">
                    <div
                        class=" w-11/12 min-w-[91.666667%] xs:w-80 xs:min-w-[20rem] md:w-1/3 md:min-w-[33.333333%] lg:w-1/4 lg:min-w-[25%]">
                        <CardsRecentPod :title="$t('Грузоперевозки')" duration="23min" href="#" :desc="$t('Надежные и оперативные грузоперевозка')"
                            cover-image="/images/plane.jpeg" />
                    </div>

                    <div
                        class=" w-11/12 min-w-[91.666667%] xs:w-80 xs:min-w-[20rem] md:w-1/3 md:min-w-[33.333333%] lg:w-1/4 lg:min-w-[25%]">
                        <CardsRecentPod :title="$t('Туризм')" duration="1h:22min" href="#" :desc="$t('Индивидуальные и корпоративные туры')"
                            cover-image="/images/turizm.webp" />
                    </div>

                    <div
                        class=" w-11/12 min-w-[91.666667%] xs:w-80 xs:min-w-[20rem] md:w-1/3 md:min-w-[33.333333%] lg:w-1/4 lg:min-w-[25%]">
                        <CardsRecentPod :title="$t('Консалтинг')" duration="12min" href="#" :desc="$t('Профессиональные услуги консалтинга')"
                            cover-image="/images/consalting.jpg" />
                    </div>

                    <div
                        class=" w-11/12 min-w-[91.666667%] xs:w-80 xs:min-w-[20rem] md:w-1/3 md:min-w-[33.333333%] lg:w-1/4 lg:min-w-[25%]">
                        <CardsRecentPod :title="$t('Таможенное оформление')" duration="50min" href="#" :desc="$t('Быстрое и эффективное таможенное оформление')"
                            cover-image="/images/custom.webp" />
                    </div>
                </div>
            </div>
        </AtomsContainer>
    </section>
</template>

<script lang="ts" setup>


// const scrollLeft = useState('scrollLeft', ()=> 0)
const nextIsVisible = useState('nextIsVisible', () => false)
const prevIsVisible = useState('prevIsVisible', () => false)

let element:HTMLDivElement
if (typeof document !== "undefined") {
    element = document.querySelector("[data-slide-recent]") as HTMLDivElement
}
function initScroll(): void {
    if (typeof element === "undefined" || element === null) {
        return
    }
    prevIsVisible.value = element.scrollLeft > 0
    nextIsVisible.value = element.scrollLeft < element.scrollWidth - element.offsetWidth - 1
}

function scrollToLeft():void{
    if (typeof element === "undefined" || element === null) {
        return
    }
    element.scrollLeft -= element.clientWidth
}

function scrollToRight():void{
    if (typeof element === "undefined" || element === null) {
        return
    }
    element.scrollLeft += element.clientWidth
}

onMounted(() => {
    if (window !== null) {
        initScroll()
    }
})
</script>