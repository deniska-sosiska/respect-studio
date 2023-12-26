<template>
    <section ref="preloaderSection" class="preloader-section">
        <MainLogoSVG />

        <div class="timer">
            <span ref="timerRef">{{ timerValue }}</span>
        </div>
    </section>
</template>

<script setup lang="ts">
    import { onMounted, ref, Ref } from 'vue';
    import MainLogoSVG from '@/components/base-components/MainLogoSVG.vue';

    import { gsap } from 'gsap-trial';
    import { ScrollTrigger } from 'gsap-trial/ScrollTrigger';
    import { TextPlugin } from 'gsap-trial/TextPlugin';

    gsap.registerPlugin(ScrollTrigger, TextPlugin);
    const timeline = gsap.timeline();

    const timerValue = ref(0);
    const timerRef: Ref<HTMLElement | null> = ref(null);
    const preloaderSection: Ref<HTMLElement | null> = ref(null);

    function getRandomNumber(min: number, max: number) {
        return Math.round(Math.random() * (max - min) + min);
    }

    function getCorrectRandom(min: number, max: number) {
        const randomNumber = getRandomNumber(min, max);
        if (randomNumber > 0 && randomNumber < 100) {
            return randomNumber;
        }

        return getCorrectRandom(min, max);
    }

    const timerAnimation = () => {
        const length = getRandomNumber(4, 5);
        const range = new Array(length).fill(null).map((_, index) => {
            const part = 100 / length;
            if (!index) {
                return getCorrectRandom(part / 2, part * (index + 1));
            }
            const prev = part * index + part / 2;
            const current = part * index + 1;

            return getCorrectRandom(prev, current);
        });

        timerValue.value = range[0];
        range.push(99);

        timeline.from(timerRef.value, { autoAlpha: 0, delay: 0.2 });
        range.slice(1).forEach((timerValue) => {
            timeline.to(timerRef.value, { text: `${timerValue}`, duration: 0.35 });
        });

        timeline.to(timerRef.value, { autoAlpha: 0, duration: 0.1 });
    };

    const logoAnimation = () => {
        const lettersSelector = ' > path:not(:first-child)';
        const svgElement = preloaderSection.value?.querySelector('svg')!;
        const respectLetters = svgElement?.querySelectorAll('#respect' + lettersSelector)!;
        const studioLetters = svgElement?.querySelectorAll('#studio' + lettersSelector)!;

        gsap.set([respectLetters,   studioLetters], { autoAlpha: 0 });

        timeline.from(svgElement, { autoAlpha: 0, delay: 0.35, duration: 0.3 });
        for (let index = 0; index < Math.max(respectLetters.length, studioLetters.length); index++) {
            timeline.to([respectLetters[index], studioLetters[index]], { autoAlpha: 1, duration: 0.15 });
        }
    };

    onMounted(() => {
        timerAnimation();
        logoAnimation();

        timeline.to(preloaderSection.value, { y: '-100%', delay: 0.5, duration: '0.8' });
    });

</script>
