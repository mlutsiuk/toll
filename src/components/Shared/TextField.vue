<template>
    <div class="form-group">
        <label v-if="label" :for="id">{{ label }}</label>
        <input v-model="value" :id="id" :placeholder="placeholder" type="text" class="form-control">
        <small v-if="hint" class="form-text text-muted">{{ hint }}</small>
    </div>
</template>

<script>
export default {
    name: 'TextField',
    emits: ['update:modelValue'],
    props: {
        modelValue: {
            type: String,
            required: true
        },

        id: {
            type: String,
            required: true
        },
        label: {
            type: String,
            default: ''
        },
        hint: {
            type: String,
            default: ''
        },
        placeholder: {
            type: String,
            default: ''
        }
    },
    computed: {
        value: {
            get() {
                return this.modelValue;
            },
            set(val) {
                this.$emit('update:modelValue', val);
            }
        }
    }
};
</script>

<style scoped>

</style>
