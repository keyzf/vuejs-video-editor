<template>
    <div class="split-view" :style="{ 'flex-direction': splitViewDirection }">
        <template v-for="(slotItem, slotKey, n) in slots" :key="slotKey">
            <div class="split-view__pane">
                <slot :name="slotKey"></slot>
            </div>
            <div v-if="n < numSlot - 1" class="split-view__gripper">|</div>
        </template>
    </div>
</template>

<script setup>
import { useSlots } from "vue"

const slots = useSlots()
const numSlot = Object.keys(slots).length
const props = defineProps({
    direction: {
        type: String,
        default: 'horizontal' // vertical
    },
})
const splitViewDirection = props.direction === 'horizontal' ? 'row' : 'column'

</script>

<style scoped>
.split-view {
    display: flex;
}
</style>