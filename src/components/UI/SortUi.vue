<template>
    <div class="sortby">
        <select v-model="modelValue" @change="changeOption">
            <option disabled value="">Choose option</option>
            <option 
                v-for="option in options" 
                :key="option.value" 
                :value="option.value">{{ option.name }}</option>
        </select>
    </div>
</template>

<script>
    export default {
        name: 'sort-ui',
        props: {
            modelValue: {
                type: String
            },
            options: {
                type: Array,
                default: () => []
            }
        },
        methods: {
            changeOption(event) {
                this.$emit('update:modelValue', event.target.value)
            }
        }
    }
</script>

<style lang="css" scoped>

</style>