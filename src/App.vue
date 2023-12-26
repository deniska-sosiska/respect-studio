<template>
    <PreloaderView />
    <HomeSection />
    <AppHeader />
    <AppContent />
</template>

<script setup lang="ts">
    import AppHeader from '@/components/AppHeader.vue';
    import AppContent from '@/components/AppContent.vue';
    import HomeSection from '@/components/HomeSection.vue';
    import PreloaderView from '@/components/PreloaderView.vue';

    // import { gsap } from 'gsap-trial';
    // import { ScrollTrigger } from 'gsap-trial/ScrollTrigger';
    // import { ScrollSmoother } from 'gsap-trial/ScrollSmoother';
    //
    // gsap.registerPlugin(ScrollTrigger, ScrollSmoother);
    //
    // ScrollSmoother.create({
    //     smooth: 1.8,
    //     effects: true,
    //     content: '#app'
    // });

</script>
