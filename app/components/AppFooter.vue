<template>
    <footer class="pt-5 bg-gray-100 dark:bg-body border-t border-gray-200 dark:border-gray-100/20">
        <AtomsContainer class-name="pb-5">
            <div class="flex justify-between">
                <div class="col-span-2 md:col-span-4 lg:col-span-2">
                    <NuxtLink :to="localPath('/')" class=" flex items-center gap-2">
                        <span class="flex">
                            <img src="/logo.png" width="50" height="50" alt="logo"/>
                        </span>
                        <span class="text-lg text-gray-700 dark:text-white">
                            <p class="mb-0 font-bold" style="line-height: 16px;">ONSON</p>
                            <p class="mb=0 font-bold" style="font-size: 12px; line-height: 12px;">MAIL GROUP</p>
                        </span>
                    </NuxtLink>

                    <!-- <p class="text-gray-600 dark:text-gray-300 pt-6">
                        Верьте и воплощайте свои мечты
                    </p> -->
                </div>

                <div class="flex items-center gap-x-3 text-gray-600 dark:text-gray-300">
                    <NuxtLink target="_blank" to="#" class="transition hover:!text-primary">
                        <img src="/Telegram.svg" height="35" width="35"/>
                    </NuxtLink>

                    <NuxtLink target="_blank" to="#" class="transition hover:!text-primary">
                        <img src="/Instagram.svg" height="35" width="35"/>
                    </NuxtLink>
                </div>
            </div>
        </AtomsContainer>
    </footer>
</template>

<script lang="ts" setup>
const localPath = useLocalePath()
</script>