<template>
    <v-form model="valid">
        <div v-for="(schemaItem, schemaItemIndex) in schema" :key='schemaItemIndex'>
            <div v-if="schemaItemIndex == 'groups'">
                <v-tabs>
                    <v-tabs-bar class="cyan" dark>
                        <v-tabs-item
                            v-for="group in schemaItem"
                            :key="group.key"
                            :href="'#' + group.key"
                            ripple>
                            {{group.legend}}
                        </v-tabs-item>
                        <v-tabs-slider color="yellow"></v-tabs-slider>
                    </v-tabs-bar>
                    <v-tabs-items>
                        <v-tabs-content
                          v-for="group in schemaItem"
                          :key="group.key"
                          :id="group.key">
                            <div class="ma-3">
                              <div v-for="(index, field) in group.fields" :key='index'>
                                <v-form-generator-field 
                                    :field="field" 
                                    :value="model[field.model]"
                                    @blur="onBlur"
                                    @change="onChange"
                                    @focus="onFocus"
                                    @input="onInput"
                                    />
                              </div>
                            </div>
                        </v-tabs-content>
                    </v-tabs-items>
                </v-tabs>

            </div>
            <div v-if="schemaItemIndex == 'fields'">
                <div v-for="(index,field) in schemaItem" :key='index'>
                    <v-form-generator-field :field="field" :value="model[field.model]" @change="onChange"></v-form-generator-field>
                </div>
            </div>
        </div>
    </v-form>
</template>

<script>
    export default{
        name: 'v-form-generator',
        props: {
            'model': Object,
            'schema': Object,
            'options': Object,
            'valid': Boolean
        },
        components: {
            'v-form-generator-field': require('./form-field.vue').default
        },
        data(){
            return {
                
            }
        },
        created: function () {
            // On load
        },
        methods: {
            onBlur(){
                console.info('blur')
            },
            onChange(payload){
                this.model[payload.field.model] = payload.value
            },
            onFocus(){
                console.info('focus')
            },
            onInput(){
                console.info('input')
            },
        }
    }
</script>