<template>
    <header>
        <nav>
            <figure class="small-logo">
                <img src="@/assets/small-logo.svg" alt="" />
            </figure>

            <div class="nav_row nr_1">
                <a href="#">Services</a>
                <a href="#">Case Studies</a>
                <a href="#">Blog</a>
                <a href="#">About us</a>
            </div>

            <div class="nav_row nr_2">
                <a href="#">We're hiring</a>
                <a href="#">Contacts</a>
                <VButton text="Book a call" />
            </div>
        </nav>
    </header>
</template>

<script setup lang="ts">
    import VButton from '@/components/base-components/VButton.vue';
</script>
