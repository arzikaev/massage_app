<template>
  <v-container>
    <template>
      <v-text-field
      v-model="search"
      label="Поиск клиента"
      @input="viewItem(search)"
      ></v-text-field>
    </template>
    <v-card
        outlined
        shaped
    >
      <v-row>
        <v-col>
          <template>
            <v-simple-table>
              <template v-slot:default>
                <thead>
                <tr>
                  <th class="text-center">
                    Абонементы
                  </th>
                  <th class="text-center">
                    Замеры
                  </th>
                  <th class="text-center">
                    Имя
                  </th>
                  <th class="text-center">
                    Телефон
                  </th>
                  <th class="text-center">
                    Дата рождения
                  </th>
                  <th class="text-center">
                    Статус
                  </th>
                  <th class="text-center">
                    Последняя дата посещения
                  </th>
                  <th class="text-center">
                    Действия
                  </th>
                </tr>
                </thead>
                <tbody>
                <tr
                    v-for="item in items"
                    :key="item.name"
                >
                  <td class="text-center">
                    <v-btn @click="abonents = true">
                      <v-icon>
                        mdi-card-account-details-outline
                      </v-icon>
                    </v-btn>
                  </td>
                  <td class="text-center">
                    <v-btn>
                      <v-icon>
                        mdi-human-handsdown
                      </v-icon>
                    </v-btn>
                  </td>
                  <td class="text-center">{{ item.name }}</td>
                  <td class="text-center">{{ item.phone }}</td>
                  <td class="text-center">{{ item.birthday }}</td>
                  <td class="text-center">{{ item.status }}</td>
                  <td class="text-center">30.01.2021</td>
                  <td class="text-center">
                    <v-btn @click="clientsadd = true">
                      <v-icon>
                        mdi-account-edit
                      </v-icon>
                    </v-btn>
                    <v-btn color="red" @click="deleteItem(item)">
                      <v-icon>
                        mdi-account-remove
                      </v-icon>
                    </v-btn>
                  </td>
                </tr>
                </tbody>
              </template>
            </v-simple-table>
          </template>
        </v-col>
      </v-row>
    </v-card>
    <router-view></router-view>
    <v-row class="ma-1 pa-1">
      <v-spacer></v-spacer>
      <v-col cols="1">
        <v-btn color="success" @click="clientsadd = true">+</v-btn>
      </v-col>
    </v-row>
    <ClientAdd
        v-if="clientsadd === true"
        v-bind:cliensadd="clientsadd"
    />
    <Abonents
        v-if="abonents === true"
        v-bind:abonents="abonents"
    />

  </v-container>

</template>

<script>
import ClientAdd from "@/components/ClientAdd";
import Abonents from "@/components/Abonents";
export default {
  name: 'About',
  components:{ClientAdd, Abonents},
  data() {
    return {
      card: {},
      clientsadd: false,
      abonents: false,
      menu: false,
      dates: '',
      search:'',
      itemsData: [
        {
          name: 'Иван Иванов',
          id: '1',
          status: 'В работе',
          birthday: '15.02.90',
          phone: 8193241432
        },
        {
          name: 'Оксана Иванова',
          id: '2',
          status: 'Завершен(а)',
          birthday: '12.12.88',
          phone: 8193241432
        },
        {
          name: 'Оксана Иванова',
          id: '2',
          status: 'Завершен(а)',
          birthday: '12.12.88',
          phone: ''
        },
        {
          name: 'Оксана Иванова',
          id: '2',
          status: 'Завершен(а)',
          birthday: '12.12.88',
          phone: ''
        },
        {
          name: 'Оксана Иванова',
          id: '2',
          status: 'Завершен(а)',
          birthday: '12.12.88',
          phone: ''
        },
        {
          name: 'Оксана Иванова',
          id: '2',
          status: 'Завершен(а)',
          birthday: '12.12.88',
          phone: ''
        },
      ],
      items: []
    }
  },
  methods:{
    deleteItem(item){
    const deleteItem = this.items.indexOf(item)
      if (deleteItem > -1) {
        this.items.splice(deleteItem, 1);
      }
    },
    viewItem(search = ''){
      if(search.length > 0){
        const searchItem = this.itemsData.filter((e) => {
          console.log({e})
          console.log({search})
          return e.phone == search
        })
        console.log({searchItem})
        this.items = []
        this.items = searchItem
      }else{
        this.items = this.itemsData
      }
    }
  },
  mounted() {
    this.items = []
    this.viewItem()
  }
};
</script>