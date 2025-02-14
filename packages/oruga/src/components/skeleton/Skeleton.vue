<script>
import BaseComponentMixin from '../../utils/BaseComponentMixin'
import { toCssDimension } from '../../utils/helpers'

/**
 * A placeholder for content to load
 * @displayName Skeleton
 * @example ./examples/Skeleton.md
 * @style _skeleton.scss
 */
export default {
    name: 'OSkeleton',
    mixins: [BaseComponentMixin],
    configField: 'skeleton',
    props: {
        /** Show or hide loader	 */
        active: {
            type: Boolean,
            default: true
        },
        /** Show a loading animation */
        animated: {
            type: Boolean,
            default: true
        },
        /** Custom width */
        width: [Number, String],
        /** Custom height */
        height: [Number, String],
        /** Show a circle shape */
        circle: Boolean,
        /** Rounded style */
        rounded: {
            type: Boolean,
            default: true
        },
        /** Number of shapes to display */
        count: {
            type: Number,
            default: 1
        },
        /**
         * Skeleton position in relation to the element
         * @values left, centered, right
         */
        position: {
            type: String,
            default: '',
            validator(value) {
                return [
                    '',
                    'centered',
                    'right'
                ].indexOf(value) > -1
            }
        },
        /**
         * Size of skeleton
         * @values small, medium, large
         */
        size: String,
        rootClass: String,
        animationClass: String,
        positionClass: String,
        itemClass: String,
        itemRoundedClass: String,
        sizeClass: String
    },
    render(h) {
        if (!this.active) return
        const items = []
        const width = this.width
        const height = this.height
        for (let i = 0; i < this.count; i++) {
            items.push(h('div',
                {
                    staticClass: this.computedClass('itemClass', 'o-sklt__item'),
                    class: [
                      { [this.computedClass('itemRoundedClass', 'o-sklt__item--rounded')]: this.rounded },
                      { [this.computedClass('animationClass', 'o-sklt__item--animated')]: this.animated },
                      { [this.computedClass('sizeClass', 'o-sklt__item--', this.size)]: this.size },
                    ],
                    key: i,
                    style: {
                        height: toCssDimension(height),
                        width: toCssDimension(width),
                        borderRadius: this.circle ? '50%' : null
                    }
                }
            ))
        }
        return h('div',
            {
                staticClass: this.computedClass('rootClass', 'o-sklt'),
                class: [
                    { [this.computedClass('positionClass', 'o-sklt--', this.position)]: this.position }
                ]
            },
            items
        )
    }
}
</script>
