<template>
    <label
        :class="rootClasses"
        ref="label"
        :disabled="disabled"
        @click="focus"
        @keydown.prevent.enter="$refs.label.click()">
        <input
            v-model="computedValue"
            type="radio"
            ref="input"
            @click.stop
            :disabled="disabled"
            :required="required"
            :name="name"
            :value="nativeValue">
        <span :class="checkClasses" />
        <span :class="labelClasses"><slot/></span>
    </label>
</template>

<script>
import CheckRadioMixin from '../../utils/CheckRadioMixin'
import BaseComponentMixin from '../../utils/BaseComponentMixin'

/**
 * Select an option from a set
 * @displayName Radio
 * @example ./examples/Radio.md
 * @style _radio.scss
 */
export default {
    name: 'ORadio',
    mixins: [BaseComponentMixin, CheckRadioMixin],
    configField: 'radio',
    props: {
        rootClass: String,
        disabledClass: String,
        checkClass: String,
        labelClass: String,
        sizeClass: String,
        variantClass: String
    },
    computed: {
        rootClasses() {
            return [
                this.computedClass('rootClass', 'o-radio'),
                { [this.computedClass('sizeClass', 'o-size-', this.size)]: this.size },
                { [this.computedClass('disabledClass', 'o-radio-disabled')]: this.disabled }
            ]
        },
        checkClasses() {
            return [
                this.computedClass('checkClass', 'o-radio-check'),
                { [this.computedClass('variantClass', 'o-color-', this.variant)]: this.variant }
            ]
        },
        labelClasses() {
            return [
                this.computedClass('labelClass', 'o-radio-label')
            ]
        }
    }
}
</script>
