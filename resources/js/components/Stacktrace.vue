<style scoped>

</style>

<template>
    <div class="border-t border-grey-light cursor-pointer">
        <div @click="toggleDisplay" class="bg-grey-darker text-sm w-full p-2 text-white block">
            <span class="text-monospace">{{ code.file }} &mdash; {{ code.frame ||  '{main}'}}</span>
        </div>
        <div class="overflow-hidden">
            <pre class="language-php text-sm text-base line-numbers language-php" style="margin: -1.7em -1em;" :data-line="6" :data-start="code.line - 5" :data-end="code.line +  5"  v-show="display">
                <code class="w-full block" v-text="Object.values(code.code).join('')"></code>
                <div class="mb-2 absolute text-sm" style="bottom: 1.4rem;left:1rem;">{{ code.file}}</div>
            </pre>
        </div>
    </div>
</template>

<script>
    export default {
        props: ['code', 'first', 'showVendor'],
        data() {
            return {
                display: false,
                loaded: false
            }
        },
        methods: {
            toggleDisplay() {
                this.display = !this.display;
                if (!this.loaded) {
                    this.loaded = true;
                    this.showTrace();
                }
            },
            showTrace() {
                Prism.highlightAll();
                console.log(this.code)
            }
        },

        mounted() {
            if (this.first)
                this.display = this.first
        }
    }
</script>
