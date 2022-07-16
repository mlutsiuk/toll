<template>
    <toll-calculator/>
</template>

<script>

import TollCalculator from '@/components/TollCalculator/TollCalculator';

export default {
    name: 'App',
    components: {
        TollCalculator
    }
};
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Open+Sans&display=swap');

#app {
    font-family: 'OpenSans-Regular', sans-serif;
}
</style>
