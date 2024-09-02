<template>
  <v-app>
    <v-app-bar>
      <v-app-bar-title>BOT TRADING SIMULATION</v-app-bar-title>
    </v-app-bar>
    <v-main>
      <v-container fluid="">

        <v-row>

          <!-- Início de seção -->
          <v-col>

            <v-card-title class="pb-0">PullBack 
              <span v-if="media_acc1 < 100" class="text-red">({{ media_acc1 }}%)</span>
              <span v-if="media_acc1 >= 100" class="text-green">({{ media_acc1 }}%)</span>
              <div style="float: right;">{{ lastItem1.ult_atualizacao }}</div>
            </v-card-title>
            
            <v-card-subtitle class="pb-2">↓3% ↑2% ↓3%</v-card-subtitle>
            
            <v-container fluid="">

              <v-row v-if="jsonData1 && jsonData1.items">

                <!-- Início de card -->
                <v-col
                  v-for="(item, index) in jsonData1.items" :key="index"
                  cols="12" md="6" lg="6" xxl="4" class="pt-0">

                  <v-card :style="item.acumulado < 100 ? 'border-bottom: 4px solid lightcoral;' : (item.acumulado > 150 ? 'border-bottom: 10px solid black;' : 'border-bottom: 4px solid lightgreen;')" :color="item.status === 'comprado' ? (item.variacao < 0 ? 'orange-lighten-5' : 'green-lighten-5') : 'blue-grey-lighten-5'">
                    <v-card-title class="pb-0">
                      <div v-if="item.variacao < 2 && item.variacao > -3" style="float: right;"><a class="text-primary text-decoration-none" target="_blank" :href="`https://www.binance.com/en/trade/${item.ticker.slice(0, -4)}_USDT?_from=markets&type=spot`">{{ index+1 }}</a></div>
                      <div v-if="item.variacao >= 2" style="float: right;">
                        <v-progress-circular
                          color="green"
                          indeterminate
                        ></v-progress-circular>
                      </div>
                      <div v-if="item.variacao <= -3" style="float: right;">
                        <v-progress-circular
                          color="red"
                          indeterminate
                        ></v-progress-circular>
                      </div>
                      {{ item.ticker }}
                      <span v-if="item.variacao < 0 && item.status === 'comprado'" class="text-red">({{ item.variacao.toFixed(1) }}%)</span>
                      <span v-if="item.variacao >= 0 && item.status === 'comprado'" class="text-green">({{ item.variacao.toFixed(1) }}%)</span>
                    </v-card-title>
                    <v-card-text>
                      <div v-if="item.status === 'comprado'">
                        <v-icon color="green" icon="mdi-cash" size="small"></v-icon> {{ item.compra }} 
                        <v-icon color="orange-darken-2" icon="mdi-cash" size="small"></v-icon> {{ item.atual }} 
                      </div>
                      <div>
                        <v-icon :color="item.acumulado >= 100 ? 'green' : 'red'" icon="mdi-cash-multiple" size="small"></v-icon> {{ item.acumulado.toFixed(2) }} ({{ item.num_operacoes }})
                        <div style="float: right;">{{ item.ts_operacao }}</div>
                      </div>
                    </v-card-text>
                  </v-card>
                </v-col>
                <!-- Fim de card -->
                
              </v-row>

            </v-container>

          </v-col>
          <!-- Fim de seção -->
          
          <!-- Início de seção -->
          <v-col>

            <v-card-title class="pb-0">PullBack 
              <span v-if="media_acc2 < 100" class="text-red">({{ media_acc2 }}%)</span>
              <span v-if="media_acc2 >= 100" class="text-green">({{ media_acc2 }}%)</span>
              <div style="float: right;">{{ lastItem2.ult_atualizacao }}</div>
            </v-card-title>
            <v-card-subtitle class="pb-2">↓2% ↑1.5% ↓3%</v-card-subtitle>

            <v-container fluid="">

              <v-row v-if="jsonData2 && jsonData2.items">

                <!-- Início de card -->
                <v-col
                  v-for="(item, index) in jsonData2.items" :key="index"
                  cols="12" md="6" lg="6" xxl="4" class="pt-0">

                  <v-card :style="item.acumulado < 100 ? 'border-bottom: 4px solid lightcoral;' : (item.acumulado > 150 ? 'border-bottom: 10px solid black;' : 'border-bottom: 4px solid lightgreen;')" :color="item.status === 'comprado' ? (item.variacao < 0 ? 'orange-lighten-5' : 'green-lighten-5') : 'blue-grey-lighten-5'">
                    <v-card-title class="pb-0">
                      <div v-if="item.variacao < 1.5 && item.variacao > -3" style="float: right;"><a class="text-primary text-decoration-none" target="_blank" :href="`https://www.binance.com/en/trade/${item.ticker.slice(0, -4)}_USDT?_from=markets&type=spot`">{{ index+1 }}</a></div>
                      <div v-if="item.variacao >= 1.5" style="float: right;">
                        <v-progress-circular
                          color="green"
                          indeterminate
                        ></v-progress-circular>
                      </div>
                      <div v-if="item.variacao <= -3" style="float: right;">
                        <v-progress-circular
                          color="red"
                          indeterminate
                        ></v-progress-circular>
                      </div>
                      {{ item.ticker }}
                      <span v-if="item.variacao < 0 && item.status === 'comprado'" class="text-red">({{ item.variacao.toFixed(1) }}%)</span>
                      <span v-if="item.variacao >= 0 && item.status === 'comprado'" class="text-green">({{ item.variacao.toFixed(1) }}%)</span>
                    </v-card-title>
                    <v-card-text>
                      <div v-if="item.status === 'comprado'">
                        <v-icon color="green" icon="mdi-cash" size="small"></v-icon> {{ item.compra }}
                        <v-icon color="orange-darken-2" icon="mdi-cash" size="small"></v-icon> {{ item.atual }}
                      </div>
                      <div>
                        <v-icon :color="item.acumulado >= 100 ? 'green' : 'red'" icon="mdi-cash-multiple" size="small"></v-icon> {{ item.acumulado.toFixed(2) }} ({{ item.num_operacoes }})
                        <div style="float: right;">{{ item.ts_operacao }}</div>
                      </div>
                    </v-card-text>
                  </v-card>

                </v-col>
                <!-- Fim de card -->

              </v-row>

            </v-container>

          </v-col>
          <!-- Fim de seção -->

          <!-- Início de seção -->
          <v-col>

            <v-card-title class="pb-0">PullBack 
              <span v-if="media_acc3 < 100" class="text-red">({{ media_acc3 }}%)</span>
              <span v-if="media_acc3 >= 100" class="text-green">({{ media_acc3 }}%)</span>
              <div style="float: right;">{{ lastItem2.ult_atualizacao }}</div>
            </v-card-title>
            <v-card-subtitle class="pb-2">↓1.5% ↑1.2% ↓1.1%</v-card-subtitle>

            <v-container fluid="">

              <v-row v-if="jsonData3 && jsonData3.items">

                <!-- Início de card -->
                <v-col
                  v-for="(item, index) in jsonData3.items" :key="index"
                  cols="12" md="6" lg="6" xxl="4" class="pt-0">

                  <v-card :style="item.acumulado < 100 ? 'border-bottom: 4px solid lightcoral;' : (item.acumulado > 150 ? 'border-bottom: 10px solid black;' : 'border-bottom: 4px solid lightgreen;')" :color="item.status === 'comprado' ? (item.variacao < 0 ? 'orange-lighten-5' : 'green-lighten-5') : 'blue-grey-lighten-5'">
                    <v-card-title class="pb-0">
                      <div v-if="item.variacao < 1.5 && item.variacao > -3" style="float: right;"><a class="text-primary text-decoration-none" target="_blank" :href="`https://www.binance.com/en/trade/${item.ticker.slice(0, -4)}_USDT?_from=markets&type=spot`">{{ index+1 }}</a></div>
                      <div v-if="item.variacao >= 1.5" style="float: right;">
                        <v-progress-circular
                          color="green"
                          indeterminate
                        ></v-progress-circular>
                      </div>
                      <div v-if="item.variacao <= -3" style="float: right;">
                        <v-progress-circular
                          color="red"
                          indeterminate
                        ></v-progress-circular>
                      </div>
                      {{ item.ticker }}
                      <span v-if="item.variacao < 0 && item.status === 'comprado'" class="text-red">({{ item.variacao.toFixed(1) }}%)</span>
                      <span v-if="item.variacao >= 0 && item.status === 'comprado'" class="text-green">({{ item.variacao.toFixed(1) }}%)</span>
                    </v-card-title>
                    <v-card-text>
                      <div v-if="item.status === 'comprado'">
                        <v-icon color="green" icon="mdi-cash" size="small"></v-icon> {{ item.compra }}
                        <v-icon color="orange-darken-2" icon="mdi-cash" size="small"></v-icon> {{ item.atual }}
                      </div>
                      <div>
                        <v-icon :color="item.acumulado >= 100 ? 'green' : 'red'" icon="mdi-cash-multiple" size="small"></v-icon> {{ item.acumulado.toFixed(2) }} ({{ item.num_operacoes }})
                        <div style="float: right;">{{ item.ts_operacao }}</div>
                      </div>
                    </v-card-text>
                  </v-card>

                </v-col>
                <!-- Fim de card -->

              </v-row>

            </v-container>

          </v-col>
          <!-- Fim de seção -->

        </v-row>

      </v-container>

    </v-main>
    
    <!--<AppFooter />-->
  </v-app>
</template>

<script setup="">
  //
</script>

<script>
  export default {
    data() {
      return {
        tab: null,
        jsonData1: null, // Armazena os dados do primeiro JSON
        jsonData2: null, // Armazena os dados do segundo JSON
        jsonData3: null, // Armazena os dados do segundo JSON
        intervalId: null, // Armazena o ID do intervalo para poder limpar mais tarde
      };
    },
    mounted() {
      this.loadJsonData();
      // Atualiza os dados a cada 10 segundos
      this.intervalId = setInterval(() => {
        this.loadJsonData();
      }, 10000);
    },
    beforeUnmount() {
      // Limpa o intervalo quando o componente é desmontado
      clearInterval(this.intervalId);
    },
    methods: {

      async loadJsonData() {
        try {
          // const response1 = await fetch('dados_estrategia_01.json');
          // const data1 = await response1.json();
          // this.jsonData1 = data1;

          const response1 = await fetch('dados_estrategia_01.json');
          const data1 = await response1.json();
          // const filteredData1 = '';
          const arrayData1 = data1.items;
          // const tickersToFilter1 = ['SOLUSDT', 'ZECUSDT', 'AAVEUSDT', 'ICPUSDT', 'SUIUUSDT', 'ALPINEUSDT', 'STORJUSDT', 'UNIUSDT', 'SKLUSDT', 'REEFUSDT', 'SPELLUSDT', 'POLYXUSDT', 'GLMUSDT', 'ROSEUSDT']; // Files3
          const tickersToFilter1 = ['VITEUSDT', 'SLPUSDT', 'SANTOSUSDT', 'LOKAUSDT', 'PORTOUSDT', 'VTHOUSDT', 'DIAUSDT', 'MASKUSDT', 'RADUSDT'];
          const filteredItems1 = arrayData1.filter(item => tickersToFilter1.includes(item.ticker));
          // Criar um novo objeto com a estrutura original e o array filtrado
          const filteredData1 = {
            ...arrayData1,
            items: filteredItems1
          };
          this.jsonData1 = filteredData1 || data1;

          const response2 = await fetch('dados_estrategia_02.json');
          const data2 = await response2.json();
          // const filteredData2 = '';
          const arrayData2 = data2.items;
          // const tickersToFilter2 = ['ADAUSDT', 'ZECUSDT', 'LRCUSDT', 'IOTAUSDT', 'LOKAUSDT', 'ALPINEUSDT', 'LOOMUSDT', 'ALGOUSDT', 'OXTUSDT', 'COMPUSDT', 'GLMUSDT', 'RADUSDT', 'PORTOUSDT', 'FLOWUSDT', 'IOSTUSDT', 'UNIUSDT']; // Files3
          const tickersToFilter2 = ['VITEUSDT', 'LOKAUSDT', 'MASKUSDT', 'NEARUSDT', 'OGNUSDT', 'LTCUSDT', 'EOSUSDT']; 

          const filteredItems2 = arrayData2.filter(item => tickersToFilter2.includes(item.ticker));
          // Criar um novo objeto com a estrutura original e o array filtrado
          const filteredData2 = {
            ...arrayData2,
            items: filteredItems2
          };
          this.jsonData2 = filteredData2 || data2;

          const response3 = await fetch('dados_estrategia_03.json');
          const data3 = await response3.json();
          // const filteredData3 = '';
          const arrayData3 = data3.items;
          
          // const tickersToFilter3 = ['ZECUSDT','LAZIOUSDT', 'YFIN', 'REEFUSDT', 'COMPUSDT', 'IOSTUSDT', 'ADAUSDT', 'ICXUSDT', 'STMXUSDT','AUDIOUSDT', 'ALPINEUSDT', 'CRVUSDT', 'FETUSDT', 'SLPUSDT', 'REQUSDT', 'DGBUSDT', 'ENJUSDT']; // Files3
          const tickersToFilter3 = ['VITEUSDT', 'LOKAUSDT', 'KDAUSDT', 'APEUSDT', 'EOSUSDT', 'GLMUSDT', 'CLVUSDT', 'VOXELUSDT', 'PORTOUSDT', 'GTCUSDT']; 
          const filteredItems3 = arrayData3.filter(item => tickersToFilter3.includes(item.ticker));
          // Criar um novo objeto com a estrutura original e o array filtrado
          const filteredData3 = {
            ...arrayData3,
            items: filteredItems3
          };
          this.jsonData3 = filteredData3 || data3;
          //console.log(filteredData);

          // Supondo que jsonData3 seja um array de objetos e cada objeto tenha um campo 'ticker'
          
          // Filtra os dados pelos tickers e atualiza jsonData1 com os dados filtrados
          //this.jsonData3 = this.jsonData3.filter(item => tickersToFilter.includes(item.ticker));
        } catch (error) {
            console.error("Erro ao carregar os arquivos JSON:", error);
        }
      },

      calcularMedia(jsonData) {
        if (!jsonData || !jsonData.items.length) {
          return 0; // Retorna 0 se jsonData não estiver definido ou estiver vazio
        }
        const total = jsonData.items.reduce((acc, item) => acc + item.acumulado, 0);
        return (total / jsonData.items.length).toFixed(2);
      },

      lastItem(jsonData) {
        if (!jsonData || !jsonData.items.length) {
          return 0; // Retorna 0 se jsonData1 não estiver definido ou estiver vazio
        }
        const items = jsonData.items;
        // Verifica se a lista não está vazia antes de acessar o último item
        return items.length ? items[items.length - 1] : null;
      },

    },
    computed: {
      media_acc1() {
        return this.calcularMedia(this.jsonData1);
      },
      media_acc2() {
        return this.calcularMedia(this.jsonData2);
      },
      media_acc3() {
        return this.calcularMedia(this.jsonData3);
      },
      lastItem1() {
        return this.lastItem(this.jsonData1);
      },
      lastItem2() {
        return this.lastItem(this.jsonData2);
      },
      lastItem3() {
        return this.lastItem(this.jsonData3);
      },

    }
  };


</script>
