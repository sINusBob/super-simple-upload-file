<template>
    <v-card :height="getHeight" tile flat :color="getColor">

        <!--FLEX CENTER HORIZON CENTER VERTICAL CENTER-->
        <v-layout class="uploadbox-layout fill-height align-center text-center">
            <v-flex>

                <label :for="nameid" class="uploadbox-file-upload">
                    <v-icon v-show="!url" large color="gray darken-2">{{icon}}</v-icon>
                    <img alt="" v-show="url" :src="url" />
                </label>

                <input :id="nameid" :name="nameid" type="file" accept="image/*" @change="onChange" />

            </v-flex>
        </v-layout>

    </v-card>
</template>


<script>
    const _filename = 'UploadBox';


    export default {
        name: _filename,


        /**
         * DATA
         */
        data() {
            return {
            }
        },


        /**
         * PROPS
         */
        props: {

            url: {
                default: null
            },

            nameid: {
                default: 'file_upload'
            },

            /**
             * mdi-account | mdi-cloud-upload
             */
            icon: {
                default: 'mdi-cloud-upload'
            },

            /**
             * height precisa ser '57'
             */
            height: {
                default: '57'
            },

            color: {
                default: 'white'
            },

            label: {
                default: 'label...'
            },

            error: {
                default: false
            },

            value: {
                default: false
            },

            checked: {
                default: false
            },

            multiple: {
                default: true
            },

            selected: {
                default: []
            },

            items: {
                default: []
            },
        },


        /**
         * CREATED
         */
        created() {
            // Mutating the prop
            // this.value = this.list.reverse();
            // this.value = false;
        },


        /**
         * MOUNTED
         */
        mounted() {
        },


        /**
         * COMPUTED
         */
        computed: {

            getColor() {
                return this.color;
            },


            getHeight() {
                return this.height;
            },

            isChecked() {

                const str = String(this.checked).toUpperCase();

                this.value = (str === 'S' || str === 'TRUE');
            },
        },


        /**
         * METHODS
         */
        methods: {

            onChange(e) {

                const file = e.target.files[0];

                this.url = URL.createObjectURL(file);

                /**
                 * Emitir arquivo ou blob (this.url) ???
                 */
                this.$emit('onChange', file);
            },
        },


        /**
         * WATCH
         */
        watch: {
            // value() {
            //     console.error('valuevaluevaluevalue');
            //     console.log(this.value);
            // }
        },
    }
</script>

<style>

    input[type="file"] {
        display: none;
    }

    .uploadbox-file-upload {
        cursor: pointer;
        display: inline-block;
    }

    .uploadbox-layout {
        border-bottom: 1px rgba(148, 148, 148, 1) solid;
        background-color: rgba(0, 0, 0, 0.06);
    }

    img {
        margin-top: 6px;
        max-width: 100%;
        max-height: 56px;
    }
</style>