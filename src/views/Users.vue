<template>
  <v-sheet
    max-width="400"
    class="mx-auto"
  >
    <v-switch
      inset
      v-model="showActiveOnly"
      label="Active Only"
    />

    <v-card>
      <v-toolbar
        color="blue-grey darken-4"
        dark
      >
        <v-toolbar-title>Users</v-toolbar-title>
        <v-spacer></v-spacer>
        <v-btn
          icon
          @click="showNewUserInput"
        >
          <v-icon>mdi-plus</v-icon>
        </v-btn>
      </v-toolbar>
      <UsersList
        :users="visibleUsers"
        :new-user-input-visible="newUserInputVisible"
        @update-user-status="updateUserStatus"
        @add-user="addUser"
      />
    </v-card>
  </v-sheet>
</template>

<script>
import UsersList from '@/components/UsersList.vue';

export default {
  name: 'Users',

  components: {
    UsersList,
  },

  data: () => ({
    newUserInputVisible: false,
    showActiveOnly: false,
    users: [
      { name: 'User 1', active: true },
      { name: 'User 2', active: false },
      { name: 'User 3', active: true },
      { name: 'User 4', active: false },
      { name: 'User 5', active: true },
    ],
  }),

  computed: {
    activeUsers() {
      const { users } = this;
      return users.filter(({ active }) => active);
    },
    visibleUsers() {
      const { activeUsers, showActiveOnly, users } = this;
      return showActiveOnly ? activeUsers : users;
    },
  },

  methods: {
    addUser(user) {
      if (user) {
        this.users.push({ name: user, active: true });
      }
      this.newUserInputVisible = false;
    },
    showNewUserInput() {
      this.newUserInputVisible = true;
    },
    updateUserStatus({ index, active }) {
      const { [index]: user } = this.visibleUsers;
      if (user) {
        user.active = active;
      }
    },
  },
};
</script>
