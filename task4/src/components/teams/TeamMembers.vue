<template>
  <section>
    <h2>{{ teamName }}</h2>
    <ul>
      <user-item
        v-for="member in members"
        :key="member.id"
        :name="member.fullName"
        :role="member.role"
      ></user-item>
    </ul>
  </section>
</template>

<script>
import UserItem from "../users/UserItem.vue";

export default {
  props: ["teamId"],
  components: {
    UserItem
  },
  inject: ["users", "teams"],
  data() {
    return {
      members: [],
      teamName: ""
    };
  },
  methods: {
    setTeam(teamId) {
      const team = this.teams.find(el => el.id === teamId);
      this.teamName = team.name;
      this.members = team.members.map(userId =>
        this.users.find(user => user.id === userId)
      );
    }
  },
  created() {
    this.setTeam(this.teamId);
  },
  watch: {
    teamId(teamId) {
      this.setTeam(teamId);
    }
  }
};
</script>

<style scoped>
section {
  margin: 2rem auto;
  max-width: 40rem;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  padding: 1rem;
  border-radius: 12px;
}

h2 {
  margin: 0.5rem 0;
}

ul {
  list-style: none;
  margin: 0;
  padding: 0;
}
</style>
