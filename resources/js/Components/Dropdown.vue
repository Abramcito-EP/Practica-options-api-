<template>
    <div class="relative">
        <div @click="toggleOpen">
            <slot name="trigger" />
        </div>

        <!-- Full Screen Dropdown Overlay -->
        <div
            v-show="open"
            class="fixed inset-0 z-40"
            @click="close"
        ></div>

        <Transition
            enter-active-class="transition ease-out duration-200"
            enter-from-class="opacity-0 scale-95"
            enter-to-class="opacity-100 scale-100"
            leave-active-class="transition ease-in duration-75"
            leave-from-class="opacity-100 scale-100"
            leave-to-class="opacity-0 scale-95"
        >
            <div
                v-show="open"
                class="absolute z-50 mt-2 rounded-md shadow-lg"
                :class="[widthClass, alignmentClasses]"
                style="display: none"
                @click="close"
            >
                <div
                    class="rounded-md ring-1 ring-black ring-opacity-5"
                    :class="contentClasses"
                >
                    <slot name="content" />
                </div>
            </div>
        </Transition>
    </div>
</template>

<script>
export default {
    name: 'Dropdown',
    props: {
        align: {
            type: String,
            default: 'right',
        },
        width: {
            type: String,
            default: '48',
        },
        contentClasses: {
            type: String,
            default: 'py-1 bg-white',
        },
    },
    data() {
        return {
            open: false,
        };
    },
    computed: {
        widthClass() {
            return {
                48: 'w-48',
            }[this.width.toString()];
        },
        alignmentClasses() {
            if (this.align === 'left') {
                return 'ltr:origin-top-left rtl:origin-top-right start-0';
            } else if (this.align === 'right') {
                return 'ltr:origin-top-right rtl:origin-top-left end-0';
            } else {
                return 'origin-top';
            }
        },
    },
    methods: {
        toggleOpen() {
            this.open = !this.open;
        },
        close() {
            this.open = false;
        },
        closeOnEscape(e) {
            if (this.open && e.key === 'Escape') {
                this.open = false;
            }
        },
    },
    mounted() {
        document.addEventListener('keydown', this.closeOnEscape);
    },
    unmounted() {
        document.removeEventListener('keydown', this.closeOnEscape);
    },
};
</script>