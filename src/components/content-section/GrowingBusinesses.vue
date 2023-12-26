<template>
    <section class="growing-businesses">
        <div
            ref="mainTextBlock"
            class="main-text"
        >
            Growing <br />
            businesses by <br />
            building <br />
            relationships
        </div>
        <div
            ref="secondText"
            class="second-text"
        >
            <p>B2B Marketing & LinkedIn Lead</p>
            <p>Generation agency </p>
        </div>
    </section>
</template>

<script setup lang="ts">
    import { gsap } from 'gsap-trial';
    import { SplitText } from 'gsap-trial/SplitText';
    import { ScrollTrigger } from 'gsap-trial/ScrollTrigger';
    import { onMounted, Ref, ref } from 'vue';

    gsap.registerPlugin(ScrollTrigger, SplitText);

    const classNameTemplate = 'line-';
    const mainTextBlock: Ref<HTMLElement | null> = ref(null);
    const secondText: Ref<HTMLElement | null> = ref(null);

    const mainTextAnimation = () => {
        if (mainTextBlock.value === null) {
            return;
        }

        const splitLines = new SplitText(mainTextBlock.value, { type: 'lines', linesClass: `${classNameTemplate}++` });

        splitLines.lines.forEach((line, index) => {
            const split = new SplitText(line, { type: 'chars,words' });
            gsap.set(split.chars, { autoAlpha: 0 });
            const tween = gsap.to(split.chars, { duration: 0.25, autoAlpha: 1, stagger: 0.08 });

            ScrollTrigger.create({
                animation: tween,
                once: true,
                trigger: mainTextBlock.value?.querySelector(`.${classNameTemplate}${(index + 1)}`),
                start: 'bottom bottom',
            });
        });
    };

    const secondTextAnimation = () => {
        if (secondText.value === null) {
            return;
        }

        const tween = gsap.from(secondText.value, { duration: 0.5, opacity: 0, y: 30 });

        ScrollTrigger.create({
            animation: tween,
            once: true,
            trigger: secondText.value,
            start: 'top 95%',
        });
    };


    onMounted(() => {
        mainTextAnimation();
        secondTextAnimation();
    });

</script>
