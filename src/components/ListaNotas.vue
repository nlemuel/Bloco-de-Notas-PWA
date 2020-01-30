<template>
    <v-container fluid>
      <v-row dense>
        <v-col v-for="(nota, index) in notas" :key="index" cols="12" md = "4" xs = "12">
            <CardNota :nota="nota" :id="index"
            @clickEditaNota="editarNota"
            @clickRemoveNota="removerNota"></CardNota>
        </v-col>
      </v-row>
      <v-btn
          fixed
          dark
          fab
          bottom
          right
          color = "pink"
          @click="dialog = true"
          >
          <v-icon>mdi-plus</v-icon>
      </v-btn>
      <v-dialog v-model="dialog" fullscreen hide-overlay transition="dialog-bottom-transition">
        <v-card>
        <v-toolbar dark color="primary">
        <v-btn icon dark @click="dialog = false">
            <v-icon>mdi-close</v-icon>
        </v-btn>
        <v-toolbar-title>Nova nota</v-toolbar-title>
        <v-spacer></v-spacer>
        <v-toolbar-items>
            <v-btn dark text @click="Salvarnota" >Save</v-btn>
        </v-toolbar-items>
        </v-toolbar>
            <v-form>
                <v-container>
                    <v-row>
                        <v-col cols="12">
                            <v-text-field label="Titulo" v-model="nota.titulo">
                            </v-text-field>
                        </v-col>
                        <v-col cols="12">
                            <v-textarea label="Descrição" v-model="nota.descricao">
                                aria-placeholder='a'
                            </v-textarea>
                        </v-col>
                        
                    </v-row>
                </v-container>
            </v-form>
        </v-card>
      </v-dialog>
    </v-container>
</template>
<script>
import CardNota from './CardNota.vue'
export default {
    name: 'ListaNotas',
    components: {
        CardNota
    },
    data () {
      return {
        dialog: false,
        nota:{
            titulo:null,
            descricao:null
        },
        notas:[]
      }

    },
    methods:{
        Salvarnota(){
            let nota={}
            nota = Object.assign(nota, this.nota)
            if(nota.id !==null && nota.id >= 0) {
                this.notas[nota.id]=nota
            } else{
                this.notas.push(nota)
            }
            this.dialog=false
            this.limpanota()
        },
        limpanota() {
            for(let k in this.nota) {
                this.nota[k] = null
            }
        },
        editarNota(id) {
            this.nota = this.notas[id]
            this.nota.id = id;
            this.dialog = true;
        },
        removerNota (id) {
            this.notas.splice(id, 1)
        }
    }
}
</script>