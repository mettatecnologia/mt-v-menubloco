/** Modelo de array aceito
$array = [
    'operacoes'=>[
        ['action'=>'pessoas','color'=>'orange darken-4','icone'=>'fas fa-users','qtd'=>$pessoas_qtd,'titulo'=>'Pessoas','action-text'=>null,'action-icon'=>null]
    ],
    'config'=>[
        ['action'=>'pessoas','color'=>'orange darken-4','icone'=>'fas fa-users','qtd'=>$pessoas_qtd,'titulo'=>'Pessoas','action-text'=>null,'action-icon'=>null]
    ]
];
*/
<template>
<v-layout align-start row wrap>

     <v-flex xs12 v-for="(blocos, tipo) in array_itens" :key="tipo">
         <v-layout align-start row wrap>

                <v-flex v-if="tipo && blocos.length" xs12 :key="i" >
                    <v-divider></v-divider>
                    <v-layout justify-end  > <span class="title font-italic grey--text">{{tipo}}</span>  </v-layout>
                </v-flex>

                <template v-for="(bloco, i) in blocos">

                    <v-flex xs3 :key="i">
                        <jb-bloco :action="bloco.action" :action-text="bloco['action-text']" :action-icon="bloco['action-icon']" :color="bloco.color" :icone="bloco.icone">
                            <div :class="bloco.qtd !== null ? 'display-1 font-weight-bold':'display-1 font-weight-bold mt-4 pt-3' ">{{bloco.qtd}}</div>
                            <div class="subheading">{{bloco.titulo}}</div>
                        </jb-bloco>
                    </v-flex>

                </template>

         </v-layout>
     </v-flex>

</v-layout>
</template>

<script>
    export default {
      props:{
          itens: String
      },
      data(){
          return {
              array_itens: [],
          }
      },
      created(){
          this.array_itens = JSON.parse(this.itens)
      }
    }
</script>
