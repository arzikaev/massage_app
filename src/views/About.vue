<template>
  <v-container>
    <template>
      <v-text-field
      v-model="search"
      label="Поиск клиента"
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
                    <v-btn>
                      <v-icon>
                        mdi-account-edit
                      </v-icon>
                    </v-btn>
                    <v-btn color="red">
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
    <template v-if="clientsadd === true">
      <v-row justify="center">
        <v-dialog
            v-model="clientsadd"
            persistent
            max-width="600px"
        >
          <v-card>
            <v-card-title>
              <span class="text-h5">Карточка клиента</span>
            </v-card-title>
            <v-card-text>
              <v-container>
                <v-row>
                  <v-col cols="12">
                    <v-text-field
                        label="ФИО"
                        required
                    ></v-text-field>
                  </v-col>
                  <v-col cols="12">
                    <v-text-field
                        label="Телефон"
                        type="number"
                        required
                    ></v-text-field>
                  </v-col>
                  <v-col
                      cols="12"
                  >
                    <v-menu
                        ref="menu"
                        v-model="menu"
                        :close-on-content-click="false"
                        :return-value.sync="date"
                        transition="scale-transition"
                        offset-y
                        min-width="auto"
                    >
                      <template v-slot:activator="{ on, attrs }">
                        <v-text-field
                            v-model="dates"
                            label="Дата рождения"
                            prepend-icon="mdi-calendar"
                            readonly
                            v-bind="attrs"
                            v-on="on"
                        ></v-text-field>
                      </template>
                      <v-date-picker
                          v-model="dates"
                      >
                        <v-spacer></v-spacer>
                        <v-btn
                            text
                            color="primary"
                            @click="menu = false"
                        >
                          Cancel
                        </v-btn>
                        <v-btn
                            text
                            color="primary"
                            @click="$refs.menu.save(dates)"
                        >
                          OK
                        </v-btn>
                      </v-date-picker>
                    </v-menu>
                  </v-col>
                </v-row>
              </v-container>
            </v-card-text>
            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn
                  color="blue darken-1"
                  text
                  @click="clientsadd = false"
              >
                Закрыть
              </v-btn>
              <v-btn
                  color="blue darken-1"
                  text
                  @click="clientsadd = false"
              >
                Сохранить
              </v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
      </v-row>
    </template>
    <template v-if="abonents === true">
      <v-row justify="center">
        <v-dialog
            v-model="abonents"
            persistent
            max-width="600px"
        >
          <v-card>
            <v-card-title>
              <span class="text-h5">Карточка клиента</span>
            </v-card-title>
            <v-card-text>
              <v-container>
                <v-row>
                  <v-col cols="12">
                    <v-text-field
                        label="ФИО"
                        required
                    ></v-text-field>
                  </v-col>
                  <v-col cols="12">
                    <v-text-field
                        label="Телефон"
                        type="number"
                        required
                    ></v-text-field>
                  </v-col>
                  <v-col
                      cols="12"
                  >
                    <v-menu
                        ref="menu"
                        v-model="menu"
                        :close-on-content-click="false"
                        :return-value.sync="date"
                        transition="scale-transition"
                        offset-y
                        min-width="auto"
                    >
                      <template v-slot:activator="{ on, attrs }">
                        <v-text-field
                            v-model="dates"
                            label="Дата рождения"
                            prepend-icon="mdi-calendar"
                            readonly
                            v-bind="attrs"
                            v-on="on"
                        ></v-text-field>
                      </template>
                      <v-date-picker
                          v-model="dates"
                      >
                        <v-spacer></v-spacer>
                        <v-btn
                            text
                            color="primary"
                            @click="menu = false"
                        >
                          Cancel
                        </v-btn>
                        <v-btn
                            text
                            color="primary"
                            @click="$refs.menu.save(dates)"
                        >
                          OK
                        </v-btn>
                      </v-date-picker>
                    </v-menu>
                  </v-col>
                </v-row>
              </v-container>
            </v-card-text>
            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn
                  color="blue darken-1"
                  text
                  @click="abonents = false"
              >
                Закрыть
              </v-btn>
              <v-btn
                  color="blue darken-1"
                  text
                  @click="abonents = false"
              >
                Сохранить
              </v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
      </v-row>
    </template>

  </v-container>

</template>

<script>

export default {
  name: 'About',

  data() {
    return {
      card: {},
      clientsadd: false,
      abonents: false,
      menu: false,
      dates: '',
      search:'',
      items: [
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
        },
        {
          name: 'Оксана Иванова',
          id: '2',
          status: 'Завершен(а)',
        },
        {
          name: 'Оксана Иванова',
          id: '2',
          status: 'Завершен(а)',
        },
        {
          name: 'Оксана Иванова',
          id: '2',
          status: 'Завершен(а)',
        },
      ],
    }
  },
};
</script>