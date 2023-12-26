<template>
    <section class="trusted-long-term-partner">
        <div class="wrapper-block">
            <h2 ref="h2">Trusted long-term partner</h2>
            <h3 ref="h3">
                For leading B2B tech and<br />
                service companies
            </h3>
        </div>
    </section>
</template>

<script setup lang="ts">
    import { gsap } from 'gsap-trial';
    import { SplitText } from 'gsap-trial/SplitText';
    import { ScrollTrigger } from 'gsap-trial/ScrollTrigger';
    import { onMounted, ref, Ref } from 'vue';

    gsap.registerPlugin(ScrollTrigger, SplitText);

    const h2: Ref<HTMLElement | null> = ref(null);
    const h3: Ref<HTMLElement | null> = ref(null);

    onMounted(() => {
        const split = new SplitText(h2.value, { type: 'words,chars' });

        gsap.set([h3.value, split.chars], { autoAlpha: 0 });

        gsap.to(split.chars, {
            duration: 0.25,
            autoAlpha: 1,
            stagger: 0.08,
            scrollTrigger: {
                once: true,
                trigger: h2.value,
                start: 'top 85%',
            },
        });

        gsap.to(h3.value, {
            duration: 0.8,
            autoAlpha: 1,
            scrollTrigger: {
                once: true,
                trigger: h3.value,
                start: 'top 85%',
            },
        });
    });

</script>
