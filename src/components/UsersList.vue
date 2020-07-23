<template>
  <v-list>
    <UserListItem
      v-for="(user, index) in users"
      :key="user.name"
      :user="user"
      @update-user-status="$emit('update-user-status', { index, active: $event })"
    />

    <v-list-item
      v-if="newUserInputVisible"
    >
      <v-list-item-content>
        <v-text-field
          label="New User"
          v-model="newUserName"
          ref="newUserInput"
          @keyup.enter="addUser"
        />
      </v-list-item-content>
    </v-list-item>
  </v-list>
</template>

<script>
import UserListItem from '@/components/UserListItem.vue';

export default {
  name: 'UsersList',

  components: {
    UserListItem,
  },

  props: {
    newUserInputVisible: {
      type: Boolean,
      required: false,
      default: false,
    },

    users: {
      type: Array,
      required: false,
      default: () => [],
    },
  },

  data: () => ({
    newUserName: null,
  }),

  methods: {
    addUser() {
      this.$emit('add-user', this.newUserName);
      this.newUserName = null;
    },
  },

  watch: {
    async newUserInputVisible() {
      if (this.newUserInputVisible) {
        await this.$nextTick();
        this.$refs.newUserInput.focus();
      }
    },
  },
};
</script>
