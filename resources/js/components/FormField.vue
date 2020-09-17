<template>
    <default-field :field="field" :full-width-content="field.fullWidth">
        <template slot="field">
            <excerpt class="trumbowyg-details w-full pt-2" :content="field.value" :should-show="field.shouldShow" 
              v-if="isReadonly" />
            <div v-else :class="[errorClasses, errorClasses.length ? 'border' : '']" @keydown.stop>
                <trumbowyg v-model="value" :config="field.options" :disabled="isReadonly"></trumbowyg>
            </div>
            <p v-if="hasError" class="my-2 text-danger">
                {{ firstError }}
            </p>
        </template>
    </default-field>
</template>

<script>
import { FormField, HandlesValidationErrors } from 'laravel-nova'
import trumbowyg from 'vue-trumbowyg';
import 'trumbowyg/dist/ui/trumbowyg.css';

export default {
    mixins: [FormField, HandlesValidationErrors],

    props: ['resourceName', 'resourceId', 'field'],

    methods: {
        /*
         * Set the initial, internal value for the field.
         */
        setInitialValue() {
          this.value = this.field.value || ''
        },

        /**
         * Fill the given FormData object with the field's internal value.
         */
        fill(formData) {
          formData.append(this.field.attribute, this.value || '')
        },

        /**
         * Update the field's internal value.
         */
        handleChange(value) {
          this.value = value
        }
    },

    components: {
        trumbowyg
    }
}
</script>
