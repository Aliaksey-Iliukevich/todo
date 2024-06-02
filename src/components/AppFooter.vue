<template>
    <footer class="app-footer">{{ stats.active }} to do, {{ stats.done }} done</footer>
</template>

<script lang="ts">
import { defineComponent, PropType } from 'vue';

export interface Stats {
    active: number,
    done: number
}

export default defineComponent({
    props: {
        stats: {
            type: Object as PropType<Stats>,
                required: true
        }
    }
})
</script>