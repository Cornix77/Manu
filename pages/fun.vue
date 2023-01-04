<template>
    <h1>Hello this is fun!</h1>
    <nuxt-link>Fun</nuxt-link>
    <button @click="increase">Click me {{ number }}</button>
    <h1>{{ activity }}</h1>
</template>

<script>
import { defineComponent, ref } from 'vue';

export default defineComponent({
    async setup() {
        const number = ref(0)
        const activity = ref()

        onBeforeMount(async () => {
            await fetch('https://www.boredapi.com/api/activity').then(async (response) => {
                const responseJson = await response.json()
                activity.value = responseJson.activity
            }).catch((error) => console.error(error))
            
            
        })

        const increase = () => {
            ++number.value
        }

        return {
            number,
            increase,
            activity
        }
    }
})

</script>