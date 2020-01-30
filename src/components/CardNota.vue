<template>
    
<v-card
            color="#385F73"
            dark
          >
            <v-card-title class="headline">{{nota.titulo}}</v-card-title>
            <v-card-text> {{nota.descricao}} </v-card-text>
            <v-card-actions class = "justify-end">
                <v-tooltip bottom>
                    <template v-slot:activator = "{on}">
                        <v-btn icon v-on="on" @click="$emit('clickEditaNota',id)">
                            <v-icon>mdi-pencil</v-icon>
                        </v-btn>
                    </template>
                    <span> Editar </span>
                </v-tooltip>
                <v-tooltip bottom>
                    <template v-slot:activator = "{on}">
                        <v-btn icon v-on="on" @click="$emit('clickRemoveNota',id)">
                            <v-icon>mdi-delete</v-icon>
                        </v-btn>
                    </template>
                    <span> Deletar </span>
                </v-tooltip>
            </v-card-actions>
          </v-card>
</template>
<script>
export default {
    name:"CardNota",
    props:{
        nota:Object,
        id:Number
    }
}
</script>