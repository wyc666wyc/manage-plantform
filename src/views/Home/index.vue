<template>
    <div>123</div>
</template>
<script setup lang="ts">
import { WebContainer } from '@webcontainer/api'
import { onMounted } from 'vue';

let wci
onMounted(async () => {
    wci = await WebContainer.boot();
    const process = await wci.spawn('node', ['-v'])

    process.output.pipeTo(new WritableStream({
        write: (chunk) => {
            console.log(chunk)
        }
    }))
    if (await process.exit) {
        console.log('123')
    }
})
</script>