<template>
    <label
        :class="rootClasses"
        ref="label"
        :disabled="disabled"
        @click="focus"
        @keydown.prevent.enter="$refs.label.click()"
        @mousedown="isMouseDown = true"
        @mouseup="isMouseDown = false"
        @mouseout="isMouseDown = false"
        @blur="isMouseDown = false">
        <input
            v-model="computedValue"
            type="checkbox"
            ref="input"
            @click.stop
            :disabled="disabled"
            :name="name"
            :required="required"
            :value="nativeValue"
            :true-value="trueValue"
            :false-value="falseValue">
        <span :class="checkClasses"/>
        <span :class="labelClasses"><slot/></span>
    </label>
</template>

<script>
import { defineComponent } from 'vue'

import BaseComponentMixin from '../../utils/BaseComponentMixin'

/**
 * Switch between two opposing states
 * @displayName Switch
 * @example ./examples/Switch.md
 * @style _switch.scss
 */
export default defineComponent({
    name: 'OSwitch',
    mixins: [BaseComponentMixin],
    emits: ['update:modelValue'],
    props: {
        /** @model */
        modelValue: [String, Number, Boolean],
        /**
         * Same as native value
         */
        nativeValue: [String, Number, Boolean],
        disabled: Boolean,
        /**
         * Color of the switch, optional
         * @values primary, info, success, warning, danger, and any other custom color
         */
        variant: String,
         /**
         * Color of the switch when is passive, optional
         * @values primary, info, success, warning, danger, and any other custom color
         */
        passiveVariant: String,
        /** Name attribute on native checkbox */
        name: String,
        required: Boolean,
        /**
         * Vertical size of switch, optional
         * @values small, medium, large
         */
        size: String,
        /**
         * Overrides the returned value when it's checked
         */
        trueValue: {
            type: [String, Number, Boolean],
            default: true
        },
        /**
         * Overrides the returned value when it's not checked
         */
        falseValue: {
            type: [String, Number, Boolean],
            default: false
        },
        /** Rounded style */
        rounded: {
            type: Boolean,
            default: true
        },
        /** Outlined style */
        outlined: {
            type: Boolean,
            default: false
        },
        /** Show label on left */
        leftLabel: {
            type: Boolean,
            default: false
        },
        rootClass: String,
        disabledClass: String,
        checkClass: String,
        roundedClass: String,
        outlinedClass: String,
        labelClass: String,
        sizeClass: String,
        variantClass: String,
        passiveVariantClass: String,
        animationClass: String,
        leftLabelClass: String
    },
    data() {
        return {
            newValue: this.modelValue,
            isMouseDown: false
        }
    },
    computed: {
        rootClasses() {
            return [
                this.computedClass('switch', 'rootClass', 'o-switch'),
                { [`${this.computedClass('switch', 'sizeClass', 'o-size-', true)}${this.size}`]: this.size },
                { [this.computedClass('switch', 'disabledClass', 'o-switch-disabled')]: this.disabled },
                { [this.computedClass('switch', 'roundedClass', 'o-switch-rounded')]: this.rounded },
                { [this.computedClass('switch', 'outlinedClass', 'o-switch-outlined')]: this.outlined },
                { [this.computedClass('switch', 'leftLabelClass', 'o-switch-left')]: this.leftLabel }
            ]
        },
        checkClasses() {
            return [
                this.computedClass('switch', 'checkClass', 'o-switch-check'),
                { [this.computedClass('switch', 'animationClass', 'o-switch-elastic')]: (this.isMouseDown && !this.disabled)},
                { [`${this.computedClass('switch', 'variantClass', 'o-color-', true)}${this.variant}`]: this.variant },
                { [`${this.computedClass('switch', 'passiveVariantClass', 'o-color-', true)}${this.passiveVariant}-passive`]: this.passiveVariant }
            ]
        },
        labelClasses() {
            return [
                this.computedClass('switch', 'labelClass', 'o-switch-label')
            ]
        },
        computedValue: {
            get() {
                return this.newValue
            },
            set(value) {
                this.newValue = value
                this.$emit('update:modelValue', this.newValue)
            }
        }
    },
    watch: {
        /**
        * When v-model change, set internal value.
        */
        modelValue(value) {
            this.newValue = value
        }
    },
    methods: {
        focus() {
            // MacOS FireFox and Safari do not focus when clicked
            this.$refs.input.focus()
        }
    }
})
</script>
