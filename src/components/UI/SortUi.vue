<template>
    <div class="sortby">
        <select v-model="modelValue" @change="changeOption" class="select_sort">
            <option disabled value="">Choose option</option>
            <option 
                v-for="option in options" 
                :key="option.value" 
                :value="option.value"
                class="option_sort" >{{ option.name }}</option>
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
.select_sort{
    margin-bottom: 10px;
    padding: 3px 10px;
    border: 2px solid rgb(93, 115, 216);
    border-radius: 5px;
}
</style>