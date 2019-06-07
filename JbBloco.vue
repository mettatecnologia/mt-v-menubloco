<template>
<div>

    <v-hover>
        <v-card tile :color="color" dark  :width="width || '300'" :min-height="height || '140'" class="caixa-notificacao ma-1" slot-scope="{ hover }" >
            <v-card-text class="headline font-weight-bold pa-0"  >
                <v-layout align-center justify-space-between row fill-height class="pt-3">


                    <div class="text-sm-left">
                        <div class=" pl-3">
                            <slot></slot>
                        </div>
                    </div>

                    <div v-if="icone" class="pr-2">
                        <v-icon v-if="icone" class="icon icon-mdi">{{icone}}</v-icon>
                    </div>

                    <v-expand-transition v-if="hoverText">
                        <div v-if="hover" :class="configuraHoverClasses()"  style="height: 100%;" >
                        {{hoverText}}
                        </div>
                    </v-expand-transition>


                </v-layout>
            </v-card-text>
            <v-card-actions class="pa-0 fixar">
                <v-btn depressed small block :href="action" @click=" v => (action?null:dialog.mostrarDialog = true) " class="pa-0" ><jb-icon class="mr-1">{{actionIcon || 'arrow_forward'}}</jb-icon> {{actionText || 'Entrar'}} </v-btn>
            </v-card-actions>
        </v-card>

    </v-hover>

    <v-dialog :fullscreen="dialogFullscreen" :persistent="dialogPersistent" v-model="dialog.mostrarDialog" :max-width="dialogMaxWidth || '750px'">
        <v-card>
            <v-card-title>
                <span class="headline">{{ dialogTitulo }}</span>
                <v-spacer></v-spacer>
                <jb-icon tt-text="Fechar" @click="v=>( this.dialog.mostrarDialog = false )">fas fa-times</jb-icon>
            </v-card-title>

            <v-card-text>

                <slot name="conteudo-extra"></slot>

            </v-card-text>

        </v-card>
    </v-dialog>

</div>
</template>

<script>
    export default {
      props:{
          width:String,height:String, color:{type:String, required:true},
          icone:String,
          action:String, actionText:String, actionIcon:String,
          hoverText:String, hoverColor:String,

        //---- Dialog
        dialogTitulo:String,
        dialogPersistent:Boolean,
        dialogMaxWidth:String,
        dialogFullscreen:Boolean,

      },
      data(){
          return {
            dialog:{
                mostrarDialog: false,
                form: {
                    formValid: false,
                    resetValidation: false,
                    mensagens_data: this.mensagens,
                    mensagensTipo_data: this.mensagensTipo,
                },
            },
          }
      },
      methods:{
            configuraHoverClasses(){
                let base = "d-flex transition-fast-in-fast-out darken-4 subheading v-card--reveal white--text "
                let backColor = this.hoverColor || this.color;
                let classes = base + backColor;
                return classes;
            },
      }
    }
</script>

<style media="screen">

.caixa-notificacao.v-card .icon {
    -webkit-transition: all .3s linear;
    -o-transition: all .3s linear;
    transition: all .3s linear;
    z-index: 0;
    opacity: 0.25;
  }

.caixa-notificacao.v-card .icon.icon-mdi { font-size: 70px; }
.caixa-notificacao.v-card:hover .icon.icon-mdi { font-size: 75px; }

.caixa-notificacao.v-card .icon.icon-fa { font-size: 75px; }
.caixa-notificacao.v-card:hover .icon.icon-fa { font-size: 80px; }

.caixa-notificacao .v-card__actions.fixar {
    position: absolute;
    bottom: 0;
    width: 100%;
}

.caixa-notificacao .v-card__actions.fixar button,
.caixa-notificacao .v-card__actions.fixar a { background-color: rgba(0, 0, 0, 0.25) !important }

.caixa-notificacao .v-card--reveal {
    align-items: center;
    top: 0;
    position: absolute;
    justify-content: center;
    opacity: .9;
    width: 100%;
}

</style>
