<template>
  <div id="app">
    <v-app id="inspire">
      <v-content>
        <v-container fluid fill-height>
          <v-layout align-center justify-center>
            <v-flex xs12 sm8 md4>
              <v-card class="elevation-12">
                <v-toolbar dark color="amber darken-4">
                  <v-toolbar-title>Consulta de CNPJ</v-toolbar-title>
                    <v-spacer></v-spacer>
                    
                    <v-btn color="amber darken-2" v-on:click="pesquisar()">Pesquisar</v-btn>
                  </v-toolbar>
               <v-card-text>
                  <v-form>
                  <v-text-field name="cnpj" v-model="cnpj" label="CNPJ" type="text" clearable></v-text-field>

                  <v-list v-if="this.infoCnpj.hasOwnProperty('status')" two-line subheader>
                    <v-subheader>Informações: </v-subheader>

                    <div v-if="this.infoCnpj.status == 'ERROR'">
                      <v-list-tile avatar>
                        <v-list-tile-content>
                           <v-list-tile-sub-title>Erro :/</v-list-tile-sub-title>
                           <v-list-tile-title>{{this.infoCnpj.message}}</v-list-tile-title>
                          </v-list-tile-content>
                      </v-list-tile>
                    </div>

                    <div v-else-if="this.infoCnpj.status == 'OK'">
                      <v-list-tile avatar v-if="this.infoCnpj.atividade_principal[0].text != ''">
                        <v-list-tile-content>
                           <v-list-tile-sub-title>Atividade principal</v-list-tile-sub-title>
                           <v-list-tile-title>{{this.infoCnpj.atividade_principal[0].text}}</v-list-tile-title>
                          </v-list-tile-content>
                      </v-list-tile>

                      <v-list-tile avatar v-if="this.infoCnpj.atividades_secundarias[0].text != ''">
                        <v-list-tile-content>
                           <v-list-tile-sub-title>Atividades secundarias</v-list-tile-sub-title>
                           <v-list-tile-title>{{this.infoCnpj.atividades_secundarias[0].text}}</v-list-tile-title>
                          </v-list-tile-content>
                      </v-list-tile>

                      <v-list-tile avatar v-if="this.infoCnpj.capital_social != ''">
                        <v-list-tile-content>
                           <v-list-tile-sub-title>Capital social</v-list-tile-sub-title>
                           <v-list-tile-title>{{this.infoCnpj.capital_social}}</v-list-tile-title>
                          </v-list-tile-content>
                      </v-list-tile>

                      <v-list-tile avatar v-if="this.infoCnpj.nome != ''">
                        <v-list-tile-content>
                           <v-list-tile-sub-title>Nome</v-list-tile-sub-title>
                           <v-list-tile-title>{{this.infoCnpj.nome}}</v-list-tile-title>
                          </v-list-tile-content>
                      </v-list-tile>

                      <v-list-tile avatar v-if="this.infoCnpj.uf != ''">
                        <v-list-tile-content>
                           <v-list-tile-sub-title>UF</v-list-tile-sub-title>
                           <v-list-tile-title>{{this.infoCnpj.uf}}</v-list-tile-title>
                          </v-list-tile-content>
                      </v-list-tile>

                      <v-list-tile avatar v-if="this.infoCnpj.municipio != ''">
                        <v-list-tile-content>
                           <v-list-tile-sub-title>Municipio</v-list-tile-sub-title>
                           <v-list-tile-title>{{this.infoCnpj.municipio}}</v-list-tile-title>
                          </v-list-tile-content>
                      </v-list-tile>

                      <v-list-tile avatar v-if="this.infoCnpj.bairro != ''">
                        <v-list-tile-content>
                           <v-list-tile-sub-title>Bairro</v-list-tile-sub-title>
                           <v-list-tile-title>{{this.infoCnpj.bairro}}</v-list-tile-title>
                          </v-list-tile-content>
                      </v-list-tile>

                      <v-list-tile avatar v-if="this.infoCnpj.cep != ''">
                        <v-list-tile-content>
                           <v-list-tile-sub-title>CEP</v-list-tile-sub-title>
                           <v-list-tile-title>{{this.infoCnpj.cep}}</v-list-tile-title>
                          </v-list-tile-content>
                      </v-list-tile>

                      <v-list-tile avatar v-if="this.infoCnpj.logradouro != ''">
                        <v-list-tile-content>
                           <v-list-tile-sub-title>Logradouro</v-list-tile-sub-title>
                           <v-list-tile-title>{{this.infoCnpj.logradouro}}</v-list-tile-title>
                          </v-list-tile-content>
                      </v-list-tile>

                      <v-list-tile avatar v-if="this.infoCnpj.complemento != ''">
                        <v-list-tile-content>
                           <v-list-tile-sub-title>Complemento</v-list-tile-sub-title>
                           <v-list-tile-title>{{this.infoCnpj.complemento}}</v-list-tile-title>
                          </v-list-tile-content>
                      </v-list-tile>

                      <v-list-tile avatar v-if="this.infoCnpj.numero != ''">
                        <v-list-tile-content>
                           <v-list-tile-sub-title>Número</v-list-tile-sub-title>
                           <v-list-tile-title>{{this.infoCnpj.numero}}</v-list-tile-title>
                          </v-list-tile-content>
                      </v-list-tile>

                      <v-list-tile avatar v-if="this.infoCnpj.telefone != ''">
                        <v-list-tile-content>
                           <v-list-tile-sub-title>Telefone</v-list-tile-sub-title>
                           <v-list-tile-title>{{this.infoCnpj.telefone}}</v-list-tile-title>
                          </v-list-tile-content>
                      </v-list-tile>

                      <v-list-tile avatar v-if="this.infoCnpj.abertura != ''">
                        <v-list-tile-content>
                           <v-list-tile-sub-title>Abertura</v-list-tile-sub-title>
                           <v-list-tile-title>{{this.infoCnpj.abertura}}</v-list-tile-title>
                          </v-list-tile-content>
                      </v-list-tile>

                      <v-list-tile avatar v-if="this.infoCnpj.natureza_juridica != ''">
                        <v-list-tile-content>
                           <v-list-tile-sub-title>Natureza juridica</v-list-tile-sub-title>
                           <v-list-tile-title>{{this.infoCnpj.natureza_juridica}}</v-list-tile-title>
                          </v-list-tile-content>
                      </v-list-tile>

                      <v-list-tile avatar v-if="this.infoCnpj.cnpj != ''">
                        <v-list-tile-content>
                           <v-list-tile-sub-title>CNPJ</v-list-tile-sub-title>
                           <v-list-tile-title>{{this.infoCnpj.cnpj}}</v-list-tile-title>
                          </v-list-tile-content>
                      </v-list-tile>

                      <v-list-tile avatar v-if="this.infoCnpj.ultima_atualizacao != ''">
                        <v-list-tile-content>
                           <v-list-tile-sub-title>Ultima atualização</v-list-tile-sub-title>
                           <v-list-tile-title>{{this.infoCnpj.ultima_atualizacao}}</v-list-tile-title>
                          </v-list-tile-content>
                      </v-list-tile>

                      <v-list-tile avatar v-if="this.infoCnpj.status != ''">
                        <v-list-tile-content>
                           <v-list-tile-sub-title>Status</v-list-tile-sub-title>
                           <v-list-tile-title>{{this.infoCnpj.status}}</v-list-tile-title>
                          </v-list-tile-content>
                      </v-list-tile>

                      <v-list-tile avatar v-if="this.infoCnpj.tipo != ''">
                        <v-list-tile-content>
                           <v-list-tile-sub-title>Tipo</v-list-tile-sub-title>
                           <v-list-tile-title>{{this.infoCnpj.tipo}}</v-list-tile-title>
                          </v-list-tile-content>
                      </v-list-tile>

                      <v-list-tile avatar v-if="this.infoCnpj.fantasia != ''">
                        <v-list-tile-content>
                           <v-list-tile-sub-title>Fantasia</v-list-tile-sub-title>
                           <v-list-tile-title>{{this.infoCnpj.fantasia}}</v-list-tile-title>
                          </v-list-tile-content>
                      </v-list-tile>

                      <v-list-tile avatar v-if="this.infoCnpj.email != ''">
                        <v-list-tile-content>
                           <v-list-tile-sub-title>E-mail</v-list-tile-sub-title>
                           <v-list-tile-title>{{this.infoCnpj.email}}</v-list-tile-title>
                          </v-list-tile-content>
                      </v-list-tile>

                      <v-list-tile avatar v-if="this.infoCnpj.efr != ''">
                        <v-list-tile-content>
                           <v-list-tile-sub-title>Ente federativo responsável</v-list-tile-sub-title>
                           <v-list-tile-title>{{this.infoCnpj.efr}}</v-list-tile-title>
                          </v-list-tile-content>
                      </v-list-tile>

                      <v-list-tile avatar v-if="this.infoCnpj.motivo_situacao != ''">
                        <v-list-tile-content>
                           <v-list-tile-sub-title>Motivo da situação</v-list-tile-sub-title>
                           <v-list-tile-title>{{this.infoCnpj.motivo_situacao}}</v-list-tile-title>
                          </v-list-tile-content>
                      </v-list-tile>

                      <v-list-tile avatar v-if="this.infoCnpj.situacao_especial != ''">
                        <v-list-tile-content>
                           <v-list-tile-sub-title>Situação especial</v-list-tile-sub-title>
                           <v-list-tile-title>{{this.infoCnpj.situacao_especial}}</v-list-tile-title>
                          </v-list-tile-content>
                      </v-list-tile>

                      <v-list-tile avatar v-if="this.infoCnpj.data_situacao_especial != ''">
                        <v-list-tile-content>
                           <v-list-tile-sub-title>Data da situação especiaç</v-list-tile-sub-title>
                           <v-list-tile-title>{{this.infoCnpj.data_situacao_especial}}</v-list-tile-title>
                          </v-list-tile-content>
                      </v-list-tile>
                    </div>

                     

                      

                    </v-list>


                  <v-list v-else two-line subheader>
                    <v-subheader>Informações: </v-subheader>

                      <v-list-tile avatar>
                        <v-list-tile-content>
                           <v-list-tile-sub-title>Atenção:</v-list-tile-sub-title>
                           <v-list-tile-title>Aguardando Informações</v-list-tile-title>
                          </v-list-tile-content>
                      </v-list-tile>
                  </v-list>

                </v-form>
              </v-card-text>
            </v-card>
          </v-flex>
        </v-layout>
      </v-container>
    </v-content>
  </v-app>
</div>
</template>


<script>
export default {
  data() {
    return {
      cnpj: "",
      infoCnpj: {}
    };
  },
  methods: {
    pesquisar: function() {
      let link = "https://cors.io/?https://www.receitaws.com.br/v1/cnpj/" + this.cnpj;

      this.infoCnpj = {};

      let varVue = this;

      var myHeaders = new Headers();

      var myInit = {
        method: "GET",
        headers: myHeaders,
        mode: "cors",
        cache: "default"
      };

      fetch(link, myInit).then(function(res){
            return res.text();
        })
        .then(function(data){
            varVue.pegar(JSON.parse(data));
        })


    },
    pegar: function(infoRecebida){
      this.infoCnpj = infoRecebida;
    }
  }
};
</script>