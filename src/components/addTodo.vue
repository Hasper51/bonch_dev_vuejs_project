<template>
  <v-row justify="center">
      
    <v-dialog
      v-model="dialog"
      persistent
      max-width="600px"
    >
      <template v-slot:activator="{ on, attrs }">
        <v-btn
          color="primary"
          dark
          v-bind="attrs"
          v-on="on"
        >
          Добавить Запись
        </v-btn>
      </template>
      <v-card>
        <v-card-title>
          <span class="headline">Новая запись</span>
        </v-card-title>
        <v-card-text>
          <v-container>
            <v-row>
              <v-col
                cols="12"
              >
                <v-text-field
                  v-model="title"
                  :error-messages="titleErrors"
                  label="Title*"
                  required
                  @input="$v.title.$touch()"
                  @blur="$v.title.$touch()"
                ></v-text-field>
              </v-col>
              <v-col cols="12">
                <v-text-field
                  type='number'
                  v-model="sum"
                  :error-messages="sumErrors"
                  label="Sum*"
                  required
                  @input="$v.sum.$touch()"
                  @blur="$v.sum.$touch()"
                ></v-text-field>
              </v-col>
              <v-col cols="12">
                <v-text-field
                  v-model="description"
                  :error-messages="descriptionErrors"
                  label="Description*"
                  required
                  @input="$v.description.$touch()"
                  @blur="$v.description.$touch()"
                ></v-text-field>
              </v-col>
              <v-col
                cols="12"
              >
                <v-select
                  required
                  label="Type"
                  :items="items"
                  v-model="type"
                  :error-messages="typeErrors"
                  @change="$v.type.$touch()"
                  @blur="$v.type.$touch()"
                ></v-select>
                
              </v-col>
              
            </v-row>
          </v-container>
          <small>*indicates required field</small>
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn
            color="blue darken-1"
            text
            @click="clear"
          >
            Close
          </v-btn>
          <v-btn
            color="blue darken-1"
            text
            @click="onSubmit"
            
          >
            Add
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-row>
</template>

<script>
import { validationMixin } from 'vuelidate'
import { required } from 'vuelidate/lib/validators'
export default {
    mixins: [validationMixin],
    validations: {
      title: { required },
      sum: { required },
      description: { required },
      type: { required },
      },
    
    props: ['todos'],
    data: () => ({
      dialog: false,
      
        title: '',
        sum: '', 
        date: new Date().toLocaleString(),
        description: '',
        type: null,
        items: ['Доход', 'Расход'],
      
    }),
    computed: {
      typeErrors () {
        const errors = []
        if (!this.$v.type.$dirty) return errors
        !this.$v.type.required && errors.push('Item is required')
        return errors
      },
      titleErrors () {
        const errors = []
        if (!this.$v.title.$dirty) return errors
        !this.$v.title.required && errors.push('Title is required.')
        return errors
      },
      descriptionErrors () {
        const errors = []
        if (!this.$v.description.$dirty) return errors
        !this.$v.description.required && errors.push('Description is required.')
        return errors
      },
      sumErrors () {
        const errors = []
        if (!this.$v.sum.$dirty) return errors
        !this.$v.sum.required && errors.push('Sum is required')
        return errors
      },
    },
    methods: {
        clear() {
            this.$v.$reset()
            this.title = ''
            this.sum = ''
            this.description = ''
            this.type = null
            this.dialog = false
            
        },
        onSubmit(){
            this.$v.$touch()
            if (this.title.trim() && this.sum.trim() && this.description.trim() && this.type.trim()){
                this.$emit('add-todo', {
                    title: this.title,
                    sum: this.sum,
                    date: this.date,
                    description: this.description,
                    type: this.type,
                })
                this.clear()
            }
            
            
            
        },
        
    }
}
</script>

<style scoped>
.row {
    flex: 0 0 auto;
}    
</style>