<template>
    <button
        class="btn-content"
        type="button"
        @click="func"
    >
        <svg
            xmlns="http://www.w3.org/2000/svg"
            width="21.214"
            height="21.215"
            viewBox="0 0 21.214 21.215"
        >
            <path
                id="Контур_8510"
                data-name="Контур 8510"
                d="M15,0H6.92L4.9,2.02H11.56L0,13.569,1.433,15,12.994,3.44,12.98,10.1,15,8.081Z"
                transform="translate(10.608) rotate(45)"
                fill="#e63e3a"
            />
        </svg>
        <span>{{ text }}</span>
    </button>
</template>

<script setup lang="ts">
    import { PropType } from 'vue';

    defineProps({
        text: {
            type: String,
            required: true,
        },
        func: {
            type: Function as PropType<() => void>,
            default: () => {},
        },
    });
</script>

<style lang="scss">
    @import "src/styles/variables";

    .btn-content {
        width: min(330px, 100%);
        height: 51px;
        font-size: 22px;
        padding: $base-spacing - 2px;
        gap: 15px;
        border: none;
        color: $red;
        background-color: $black;
        display: flex;
        align-items: center;
        justify-content: space-between;
        transition: 0.4s;

        figure {
            line-height: 0;
        }

        &:hover {
            background-color: $hover-gray;
        }
    }
</style>
