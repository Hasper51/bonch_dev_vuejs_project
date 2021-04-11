
<template>
    <v-card
        class="mx-auto mt-5 lighten-1"
        :class="{red: todo.type == 'Расход', green: todo.type == 'Доход'}"
        max-width="344px"
        elevation="10"
        tile
        
        
    >     
        <v-card-text
            class="grey--text text--lighten-4 font-weight-medium"
        >
            <p>ID: {{id + 1}}</p>
            <p>Title: {{todo.title}}</p>
            <p>Sum: {{todo.sum}}</p>
            <p>Type: {{todo.type}}</p>
            <p>Description: {{todo.description}}</p> 
            <p>Date: {{todo.date}}</p>
        </v-card-text>
        <v-card-actions>
            <v-btn
                color="black"
                text
                @click="$emit('remove-todo', id)"
            >
                Delete
            </v-btn>

            <v-btn
                color="white"
                text
                @click="$emit('edit-todo', id)"
            >
                Edit
            </v-btn>
        </v-card-actions>
    </v-card>
</template>
<script>
export default {
    props: {
        todo: {
            type: Object,
            required: true
        },
        id: Number
    }, 
    data: () => ({
      
    }),
}
</script>

<style scoped>

</style>