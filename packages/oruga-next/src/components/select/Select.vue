<template>
    <div :class="rootClasses">
        <select
            :class="selectClasses"
            v-model="computedValue"
            ref="select"
            :multiple="multiple"
            :size="nativeSize"
            v-bind="$attrs"
            @blur="$emit('blur', $event) && checkHtml5Validity()"
            @focus="$emit('focus', $event)">

            <template v-if="placeholder">
                <option
                    v-if="computedValue == null"
                    :value="null"
                    disabled
                    hidden>
                    {{ placeholder }}
                </option>
            </template>

            <slot/>

        </select>

        <o-icon
            v-if="icon"
            :class="iconLeftClasses"
            :icon="icon"
            :pack="iconPack"
            :size="size"/>

         <o-icon
            v-if="iconRight"
            :class="iconRightClasses"
            :icon="iconRight"
            :pack="iconPack"
            :size="size"
            both />
    </div>
</template>

<script lang="ts">
import Icon from '../icon/Icon.vue'

import FormElementMixin from '../../utils/FormElementMixin'
import BaseComponentMixin from '../../utils/BaseComponentMixin'
import config from '../../utils/config'
import { getValueByPath } from '../../utils/helpers'
import { defineComponent } from 'vue'

/**
 * Select an item in a dropdown list. Use with Field to access all functionalities
 * @displayName Select
 * @example ./examples/Select.md
 * @style _select.scss
 */
export default defineComponent({
    name: 'OSelect',
    components: {
        [Icon.name]: Icon
    },
    mixins: [BaseComponentMixin, FormElementMixin],
    inheritAttrs: false,
    provide() {
        return {
            $elementRef: 'select'
        }
    },
    emits: ['update:modelValue', 'focus', 'blur'],
    props: {
        /** @model */
        modelValue: {
            type: [String, Number, Boolean, Object, Array],
            default: null
        },
        /**
         * Vertical size of input, optional
         * @values small, medium, large
         */
        size: String,
        /**
         * 	Icon name to be added on the right side
         */
        iconRight: {
            type: String,
            default: () => {
                return getValueByPath(config, 'select.iconRight', 'caret-down')
            }
        },
        /** Text when nothing is selected */
        placeholder: String,
        multiple: Boolean,
        /** Same as native size */
        nativeSize: [String, Number],
        rootClass: String,
        controlExpandedClass: String,
        controlIconLeftClass: String,
        controlIconRightClass: String,
        roundedClass: String,
        multipleClass: String,
        emptyClass: String,
        expandedClass: String,
        iconLeftClass: String,
        iconRightClass: String,
        sizeClass: String,
        variantClass: String
    },
    data() {
        return {
            selected: this.modelValue
        }
    },
    computed: {
        rootClasses() {
            return [
                this.computedClass('select', 'rootClass', 'o-control-select'),
                { [this.computedClass('select', 'controlExpandedClass', 'o-control-select-expanded')]: this.expanded },
                { [this.computedClass('select', 'controlIconLeftClass', 'o-control-select-icons-left')]: this.icon },
                { [this.computedClass('select', 'controlIconRightClass', 'o-control-select-icons-right')]: this.iconRight }
            ]
        },
        selectClasses() {
            return [
                this.computedClass('select', 'selectClass', 'o-select'),
                { [this.computedClass('select', 'roundedClass', 'o-select-rounded')]: this.rounded },
                { [this.computedClass('select', 'emtpyClass', 'o-select-empty')]: this.selected === null },
                { [this.computedClass('select', 'multipleClass', 'o-select-multiple')]: this.multiple },
                { [this.computedClass('select', 'expandedClass', 'o-select-expanded')]: this.expanded },
                { [`${this.computedClass('select', 'sizeClass', 'o-size-', true)}${this.size}`]: this.size },
                { [`${this.computedClass('select', 'variantClass', 'o-color-', true)}${this.statusVariant}`]: this.statusVariant }
            ]
        },
        iconLeftClasses() {
            return [
                this.computedClass('select', 'iconLeftClass', 'o-icon-left')
            ]
        },
        iconRightClasses() {
            return [
                this.computedClass('select', 'iconRightClass', 'o-icon-right')
            ]
        },
        computedValue: {
            get() {
                return this.selected
            },
            set(value: any) {
                this.selected = value
                this.$emit('update:modelValue', value)
                !this.isValid && this.checkHtml5Validity()
            }
        }
    },
    watch: {
        /**
        * When v-model is changed:
        *   1. Set the selected option.
        *   2. If it's invalid, validate again.
        */
        modelValue(value: any) {
            this.selected = value
            !this.isValid && this.checkHtml5Validity()
        }
    }
})
</script>
