<template>
  <v-navigation-drawer
    clipped
    v-model="drawer"
    permanent
    fixed
    app
  >
    <v-list>
      <template v-for="item in items">
        <v-list-group
          v-if="item.children"
          v-model="item.model"
          :key="item.text"
          :prepend-icon="item.icon"
        >
          <v-list-tile slot="activator">
            <v-list-tile-content>
              <v-list-tile-title>
                {{ item.text }}
              </v-list-tile-title>
            </v-list-tile-content>
          </v-list-tile>
          <v-list-tile
            v-for="(child, i) in item.children"
            :key="i"
            :to="{name: child.link}"
          >
            <v-list-tile-action v-if="child.icon">
              <v-icon class="pl-3">{{ child.icon }}</v-icon>
            </v-list-tile-action>
            <v-list-tile-content>
              <v-list-tile-title>
                {{ child.text }}
              </v-list-tile-title>
            </v-list-tile-content>
          </v-list-tile>
        </v-list-group>
        <v-list-tile v-else :key="item.text" :to="{name: item.link}">
          <v-list-tile-action>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-tile-action>
          <v-list-tile-content>
            <v-list-tile-title>
              {{ item.text }}
            </v-list-tile-title>
          </v-list-tile-content>
        </v-list-tile>
      </template>
    </v-list>
  </v-navigation-drawer>
</template>

<script>
export default {
  name: 'Navigation',
  data: () => ({
    drawer: null,
    items: [
      {
        icon: 'people',
        text: 'Manage People',
        model: true,
        children: [
          { icon: 'supervised_user_circle', text: 'Learners', link: 'learners' }
        ]
      },
      { icon: 'attach_money', text: 'Manage Money', link: 'manage-money' },
      { icon: 'location_on', text: 'Manage Locations', link: 'manage-locations' },
      {
        icon: 'inbox',
        text: 'Manage Content',
        model: false,
        children: [
          { icon: 'assignment', text: 'Catalogue', link: 'catalogue' }
        ]
      }
    ]
  })
}
</script>

<style scoped>

</style>
