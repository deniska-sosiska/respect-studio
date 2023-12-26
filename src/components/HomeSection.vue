<template>
    <section class="home-section">
        <div class="logo">
            <img src="src/assets/main-logo.svg" />
        </div>
        <div class="agency-small-description">
            <p>Digital Marketing</p>
            <p>Agency</p>
        </div>
        <img
            class="agency-gallery"
            :src="currentImageSrc"
        />
    </section>
</template>

<script setup lang="ts">
    import { ref } from 'vue';

    import careersBg from '@/assets/careers_bg.webp?url';
    import topSlider from '@/assets/top_slider_1.webp?url';
    import linkedinTop from '@/assets/linkedin_top.webp?url';

    const imagesList = [topSlider, linkedinTop, careersBg];
    const currentImageSrc = ref(imagesList[0]);

    setInterval(() => {
        for (let index = 0; index < imagesList.length; index++) {
            if (currentImageSrc.value === imagesList[index]) {
                if (index + 1 < imagesList.length) {
                    currentImageSrc.value = imagesList[index + 1];
                    break;
                }
                return currentImageSrc.value = imagesList[0];
            }
        }
    }, 1200);

</script>
