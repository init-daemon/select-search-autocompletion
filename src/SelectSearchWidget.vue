<template>
    <div class="select-search-container">
        <div class="dropdown-closer" @click="showDropdown = false" v-if="showDropdown"></div>
        <div class="select-search">
            <div class="input-container" :class="inputContainerClass">
                <input type="search" @focus="showDropdown = true" name="" v-model="inputValue" :class="inputClass"
                    :placeholder="placeholder" @input="value => $emit('search-change', value.currentTarget.value)"
                    :disabled="disabled">
                <div class="loader-container" v-if="loading">
                    <slot name="loader"></slot>
                </div>
            </div>
            <ul class="result-search" v-if="showDropdown">
                <li class="result-search-item" v-for="(option, i) in options" :key="i" @click="selection(option)">{{
                    option[optionName] }}</li>
            </ul>
        </div>
    </div>
</template>
<script setup>
import { ref, defineEmits } from 'vue';

const emit = defineEmits();

const props = defineProps({
    placeholder: { type: String, default: "Find" },
    inputClass: { type: String, default: "form-control" },
    inputContainerClass: { type: String, default: "form-group" },
    options: { type: Object, required: true },
    optionName: { type: String, required: true },
    optionValue: { type: String, required: false },
    loading: { type: Boolean, default: false },
    disabled: { type: Boolean, default: false }
});

const inputValue = ref('');

const showDropdown = ref(false);


const selection = (option) => {
    if (props.optionValue) {
        emit("select", option[props.optionValue])
    } else {
        emit("select", option)
    }
}

</script>
<style src="./main.css"></style>