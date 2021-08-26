<template>
  <v-app>
    <v-main>
      <template>
        <v-card class="ma-1 pa-1" height="800">
          <v-row>
            <v-col cols="2">
              <v-navigation-drawer
                  permanent
              >
                <v-list-item class="px-2">
                  <v-list-item-avatar>
                    <v-img src="https://randomuser.me/api/portraits/women/85.jpg"></v-img>
                  </v-list-item-avatar>
                  <v-list-item-content>
                    <v-list-item-title>{{ user.name }}</v-list-item-title>
                    <v-list-item-subtitle>{{ user.email }}</v-list-item-subtitle>
                  </v-list-item-content>
                </v-list-item>

                <v-divider></v-divider>

                <v-list dense>
                  <v-list-item
                      v-for="item in items"
                      :key="item.title"
                      router :to="item.link"
                  >
                    <v-list-item-icon>
                      <v-icon>{{ item.icon }}</v-icon>
                    </v-list-item-icon>

                    <v-list-item-content>
                      <v-list-item-title>{{ item.title }}</v-list-item-title>
                    </v-list-item-content>
                  </v-list-item>
                </v-list>
              </v-navigation-drawer>
            </v-col>
            <v-col>
                <router-view/>
            </v-col>
          </v-row>
        </v-card>
      </template>
    </v-main>
  </v-app>
</template>
<script>

export default {
  name: 'App',

  data() {
    return {
      user: {
        name: 'Арзыкаева Оксана',
        email: 'oa.arzikaeva@ya.ru',
        foto: 'https://randomuser.me/api/portraits/women/85.jpg'
      },
      items: [
        {title: 'Календарь', icon: 'mdi-calendar', link: '/calendar'},
        {title: 'Клиенты', icon: 'mdi-account-box-multiple', link: '/clients'},
      ],
    }
  },
}
;
</script>
