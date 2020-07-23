<template>
  <v-list-item>
    <v-list-item-action>
      <v-checkbox
        :input-value="user.active"
        color="primary"
        @click.stop="updateUserStatus"
      />
    </v-list-item-action>

    <v-list-item-content>
      <v-list-item-title>
        {{ user.name }}
      </v-list-item-title>
    </v-list-item-content>
  </v-list-item>
</template>

<script>
export default {
  name: 'UserListItem',

  props: {
    user: {
      type: Object,
      required: true,
    },
  },

  methods: {
    updateUserStatus() {
      const { active } = this.user;
      this.$emit('update-user-status', !active);
    },
  },
};
</script>
