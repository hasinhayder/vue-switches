<template>
    <label :class="classObject">
        <span class="vue-switcher__label" v-if="shouldShowLabel">
            <span v-if="label" v-text="label"></span>
            <span v-if="!label && value" v-text="textEnabled"></span>
            <span v-if="!label && !value" v-text="textDisabled"></span>
        </span>

        <input type="checkbox" :disabled="disabled" @change="trigger" :checked="modelValue" v-bind="$attrs" >

        <div></div>
    </label>
</template>

<script>

export default {
    name: 'switches',
    inheritAttrs: false,
    props: {
        typeBold: {
            default: false
        },

        modelValue:{
            default: false
        },

        disabled: {
            default: false
        },

        label: {
            default: ''
        },

        textEnabled: {
            default: ''
        },

        textDisabled: {
            default: ''
        },

        color: {
            default: 'default'
        },

        theme: {
            default: 'default'
        },

        emitOnMount: {
            default: true
        }
    },

    mounted () {
        if(this.emitOnMount) {
            this.$emit('update:modelValue', this.modelValue)
        }
    },

    methods: {
        trigger (e) {
            this.$emit('update:modelValue', e.target.checked)
        }
    },

    computed: {
        classObject () {

            const { color, modelValue, theme, typeBold, disabled } = this;

            return {
                'vue-switcher' : true,
                ['vue-switcher--unchecked'] : !modelValue,
                ['vue-switcher--disabled'] : disabled,
                ['vue-switcher--bold']: typeBold,
                ['vue-switcher--bold--unchecked']: typeBold && !modelValue,
                [`vue-switcher-theme--${theme}`] : color,
                [`vue-switcher-color--${color}`] : color,
            };

        },

        shouldShowLabel () {
            return this.label !== '' || this.textEnabled !== '' || this.textDisabled !== '';
        }
    }
}

</script>

<style src="./../dist/switches.css"></style>
