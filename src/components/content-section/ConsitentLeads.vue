<template>
    <section class="consitent-leads">
        <div class="main-text">
            <p>Consitent leads flow to streamline</p>
            <p>Your business growth.</p>
        </div>
        <div class="grow-demonstration">
            <div class="second-text">
                <p>We combine disruptive marketing techniques with proven</p>
                <p>tech solutions to provide maximum business value.</p>
            </div>
            <div class="grow-demonstration-chart">
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
            <div class="statistic-demonstration-chart">
                <div
                    v-for="(item, index) of statisticValues"
                    :key="index"
                    class="row"
                    :style="`width: ${item.width}%`"
                >
                    <div class="info">
                        <p>{{ item.l1 }}</p>
                        <p>{{ item.l2 }}</p>
                    </div>
                    <span class="value">
                        {{ item.resultDigit }}
                    </span>
                </div>
            </div>
        </div>
    </section>
</template>

<script setup lang="ts">
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

</script>
