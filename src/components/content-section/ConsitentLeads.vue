<template>
    <section class="consitent-leads">
        <div
            ref="mainTextBlock"
            class="main-text"
        >
            <p>Consitent leads flow to streamline</p>
            <p>Your business growth.</p>
        </div>

        <div class="grow-demonstration">
            <div
                ref="secondTextBlock"
                class="second-text"
            >
                <p>We combine disruptive marketing techniques with proven</p>
                <p>tech solutions to provide maximum business value.</p>
            </div>

            <div
                ref="growDemonstrationChart"
                class="grow-demonstration-chart"
            >
                <div
                    v-for="(item, index) of growthValues"
                    :key="index"
                    class="column"
                    :style="`height: ${item.h}%`"
                >
                    <span class="value">{{ item.v }}</span>
                </div>
            </div>
        </div>
        <div class="statistic-demonstration">
            <div
                ref="statisticDemonstrationChart"
                class="statistic-demonstration-chart"
            >
                <div
                    v-for="(item, index) of statisticValues"
                    :key="index"
                    class="row"
                    :style="`width: ${item.width}%`"
                >
                    <div class="info-block">
                        <div class="text">
                            <p>{{ item.l1 }}</p>
                            <p>{{ item.l2 }}</p>
                        </div>
                        <span class="value">
                            {{ item.resultDigit }}
                        </span>
                    </div>
                </div>
            </div>
        </div>
    </section>
</template>

<script setup lang="ts">
    import { onMounted, ref, Ref } from 'vue';
    import { gsap } from 'gsap-trial';
    import { SplitText } from 'gsap-trial/SplitText';
    import { ScrollTrigger } from 'gsap-trial/ScrollTrigger';

    interface IGrowthValues {
        v: number,
        h: number
    }

    interface IStatisticValues {
        resultDigit: number,
        l1: string;
        l2: string;
        width: number;
    }

    const gValues = [27, 53, 61, 58, 30, 63, 55, 63, 71, 76, 67, 88, 78, 90];
    const gHeights = [25, 39, 50, 44.7, 28.5, 39, 50, 62, 44.7, 59.7, 74.6, 87.5, 65.25, 100];

    const growthValues: IGrowthValues[] = gValues.map((value, index) => ({
        v: value,
        h: gHeights[index],
    }));

    const statisticValues: IStatisticValues[] = [
        {
            resultDigit: 1570,
            l1: 'Revenue generated',
            l2: 'for clients',
            width: 100,
        },
        {
            resultDigit: 1200,
            l1: 'Conversationd',
            l2: 'opened',
            width: 59.3,
        },
        {
            resultDigit: 378,
            l1: 'Leads generated',
            l2: 'via targeted',
            width: 100,
        },
        {
            resultDigit: 197,
            l1: 'Calls scheduled',
            l2: 'for clients',
            width: 43.8
        },
    ];


    gsap.registerPlugin(ScrollTrigger, SplitText);

    const mainTextBlock: Ref<HTMLElement | null> = ref(null);
    const secondTextBlock: Ref<HTMLElement | null> = ref(null);
    const growDemonstrationChart: Ref<HTMLElement | null> = ref(null);
    const statisticDemonstrationChart: Ref<HTMLElement | null> = ref(null);

    const mainTextAnimation = () => {
        const split = new SplitText(mainTextBlock.value, { type: 'words,chars' });
        gsap.set(split.chars, { autoAlpha: 0 });
        gsap.to(split.chars, {
            duration: 0.15,
            autoAlpha: 1,
            stagger: 0.03,
            scrollTrigger: {
                once: true,
                trigger: mainTextBlock.value,
                start: 'top 75%',
            },
        });
    };

    const secondTextAnimation = () => {
        gsap.set(secondTextBlock.value, { autoAlpha: 0 });
        gsap.to(secondTextBlock.value, {
            duration: 0.8,
            y: -30,
            autoAlpha: 1,
            scrollTrigger: {
                once: true,
                trigger: secondTextBlock.value,
                start: 'top 80%',
            },
        });
    };

    const growAnimation = () => {
        const timeline = gsap.timeline();

        growDemonstrationChart.value?.querySelectorAll('.column').forEach((column) => {
            timeline.from(column, { height: 0, duration: 0.24 }, '-=0.12');
        });


        ScrollTrigger.create({
            animation: timeline,
            once: true,
            trigger: growDemonstrationChart.value,
            start: 'top 75%',
        });
    };

    const statisticAnimation = () => {
        const timeline = gsap.timeline();
        const rows = statisticDemonstrationChart.value?.querySelectorAll('.row')!;

        rows?.forEach((row) => {
            const rowWidth = row.clientWidth;
            const infoBlock = row.querySelectorAll('.info-block');

            gsap.set(row, { width: 0 });
            gsap.set(infoBlock, { autoAlpha: 0 });
            timeline.to(row, { width: rowWidth, duration: 0.2 }, '-=0.12');
            timeline.to(infoBlock, { autoAlpha: 1, duration: 0.2 }, '-=0.06');
        });


        ScrollTrigger.create({
            animation: timeline,
            once: true,
            trigger: statisticDemonstrationChart.value,
            start: 'top 80%',
        });
    };

    onMounted(() => {
        mainTextAnimation();
        secondTextAnimation();
        growAnimation();
        statisticAnimation();
    });
</script>
