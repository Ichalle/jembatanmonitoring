<template>
  <v-toolbar
    color="primary"
    fixed
    dark
    app
  >
    <v-toolbar-title class="ml-0 pl-3">
      <v-toolbar-side-icon @click.stop="toggleDrawer()"></v-toolbar-side-icon>
    </v-toolbar-title>
    <v-breadcrumbs divider="-" :items="breadcrumbs">

    </v-breadcrumbs>
    <v-spacer></v-spacer>
    <v-btn icon @click="handleFullScreen()">
      <v-icon>fullscreen</v-icon>
    </v-btn>
    <v-btn-toggle v-model="view">
      <v-btn flat value="list">
        <v-icon color="primary">view_headline</v-icon>
      </v-btn>
      <v-btn flat value="grid">
        <v-icon color="primary">view_list</v-icon>
      </v-btn>
    </v-btn-toggle>
  </v-toolbar>
</template>
<script>
  import NotificationList from '@/components/widgets/list/NotificationList';
  import menu from '@/api/menu';
  import Util from '@/util';

  export default {
    name: 'app-toolbar',
    components: {
      NotificationList
    },
    data:  function () {
      return {
        title:'',
        view: 'grid',
      }
    },
    computed: {
      toolbarColor() {
        return this.$vuetify.options.extra.mainNav;
      },
      breadcrumbs: function () {
        let breadcrumbs = [];
        menu.forEach(item => {
          if (item.items) {
            let child =  item.items.find(i => {
              return i.href === this.$route.path;
            });
            if (child) {
              breadcrumbs.push({text: item.title});
              breadcrumbs.push({text: child.title, disabled: true});
              this.title = child.title;
            }
          } else {
            if (item.href === this.$route.path) {
              this.title = item.title;
              breadcrumbs.push({text: item.title});
            }
          }
        });
        return breadcrumbs;
      },    
    },
    methods: {
      toggleDrawer() {
        this.$store.commit('toggleDrawer')
      },
      handleFullScreen() {
        Util.toggleFullScreen();
      },
      handleLogout() {
        this.$router.push('/login');
      }
    }
  };
</script>
