<script setup>
import { useDark, useToggle } from "@vueuse/core"

const isDark = useDark({
    selector: "body",
    attribute: "color-scheme",
    valueDark: "dark",
    valueLight: "light",
})

const toggleDark = useToggle(isDark)
</script>

<template>
    <label class="switch">
        <input type="checkbox" @click="toggleDark()" v-model="isDark">
        <span class="slider round"></span>
    </label>
</template>
  
<style>
.switch {
    position: relative;
    display: inline-block;
    width: 60px;
    height: 34px;
}

.switch input {
    opacity: 0;
    width: 0;
    height: 0;
}

.slider {
    position: absolute;
    cursor: pointer;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background-color: #a49df9;
    -webkit-transition: .4s;
    transition: .4s;
    /* border: 2px solid #1b2a4a; */
}

.slider:before {
    position: absolute;
    content: "";
    height: 26px;
    width: 26px;
    left: 4px;
    bottom: 4px;
    background-color: white;
    -webkit-transition: .4s;
    transition: .4s;
}

input:checked+.slider {
    background-color: #1b2a4a;
    border: 2px solid #a49df9;
}

input:focus+.slider {
    box-shadow: 0 0 1px #2196F3;
}

input:checked+.slider:before {
    -webkit-transform: translateX(26px);
    -ms-transform: translateX(26px);
    transform: translateX(26px);
}

.slider.round {
    border-radius: 34px;
}

.slider.round:before {
    border-radius: 50%;
}

[color-scheme= 'dark'] {
  background-color: #1e1e1e;
}

[color-scheme= 'light'] {
  background-color: #ebebeb;
}
</style>
  