<template>
    <div>
        <ul class="nav nav-tabs">
            <li
                @click="activeTab = tab.id"
                v-for="tab in headers"
                :key="'tab-header-' + tab.title"
                class="nav-item"
                :class="{ 'active': tab.id === this.activeTab }"
            >
                <a
                    class="nav-link"
                >
                    {{ tab.title }}
                </a>
            </li>
        </ul>
        <div>
            <div
                v-show="tab.id === this.activeTab"
                v-for="tab in headers"
                :key="'tab-content-' + tab.title"
            >
                <slot :name="'tab-' + tab.id">
                    <h4>{{ tab.title }}</h4>
                </slot>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'BrandTabs',
    props: {
        headers: {
            type: Array,
            required: true
        }
    },
    data: () => ({
        activeTab: null
    }),
    created() {
        this.activeTab = this.headers[0].id ?? '';
    }
};
</script>

<style scoped>
li.nav-item {
    cursor: pointer;
}

li.nav-item > a {
    border-radius: 0;
}
</style>
