<template>
  <div class="container">
    <h1>
      {{ $t("page.questlines") }}
      <span v-if="this.$store.getters.hasCharacter" class="fs-3 fw-lighter">
        {{
          $t("message.clearedByCharacter", 2, { characterName: this.$store.getters.character.Name })
        }}
        <div v-if="this.$store.getters.activeCharacterOutOfDate" class="text-info fs-6">
          <div class="spinner-border spinner-border-sm" role="status"></div>
          Updating character data, this may take a minute...
        </div>
        <div v-else-if="!this.$store.getters.achievementsPublic" class="text-warning fs-6">
          The achievements for this characters are not set to public in Lodestone.
        </div>
      </span>
    </h1>
    <AlertMsg
      v-if="!this.$store.getters.userData"
      type="normal"
      :msg="
        'No characters found. You can <a href=\'' +
        this.$store.state.env.VUE_APP_DISCORD_AUTH_URI +
        '\' class=\'alert-link\'>sign in with Discord</a> to add them.'
      "
    />
    <AlertMsg
      v-else-if="!this.$store.getters.hasCharacter"
      type="normal"
      msg="No characters found. You can add your characters from the <a href='/settings' class='alert-link'>Settings</a>."
    />
    <hr />
    <div class="row">
      <h2>Stories</h2>

      <div class="col-12 col-lg-4">
        <DutyList title="Main Story Quest" :duties="db.mainStoryQuest" />
      </div>

      <div class="col-12 col-lg-4">
        <DutyList title="Side Story Quests" :duties="db.sideStoryQuests" />
        <DutyList title="Encounter Quests" :duties="db.dutiesQuests" />
      </div>

      <div class="col-12 col-lg-4">
        <DutyList title="Tribal Quests" :duties="db.beastTribeQuests" />
        <DutyList title="Allied Tribal Quests" :duties="db.alliedBeastTribeQuests" />
        <DutyList title="Custom Delivery Quests" :duties="db.customDeliveryQuests" />
      </div>
    </div>
    <hr />
    <div class="row">
      <h2>Jobs, Roles, &amp; Relics</h2>

      <div class="col-12 col-lg-4">
        <DutyList title="Combat Job Quests" :duties="db.combatJobQuests" />
        <DutyList title="Gatherer Job Quests" :duties="db.gathererJobQuests" />
        <DutyList title="Crafter Job Quests" :duties="db.crafterJobQuests" />
      </div>
      <div class="col-12 col-lg-4">
        <DutyList title="Role Quests - Shadowbringers" :duties="db.shbRoleQuests" />
        <DutyList title="Role Quests - Endwalker" :duties="db.ewRoleQuests" />
        <DutyList title="Relic Quests" :duties="db.relicQuests" />
      </div>
      <div class="col-12 col-lg-4">
        <DutyList title="Crystalline Mean Quests" :duties="db.crystallineMeanQuests" />
        <DutyList title="Studium Delivery Quests" :duties="db.studiumDeliveryQuests" />
      </div>
    </div>
  </div>
</template>

<script>
import AlertMsg from "@/components/AlertMsg.vue";
import DutyList from "@/components/DutyList.vue";

import dbJson from "@/assets/db.json";

export default {
  name: "QuestlinesView",
  data() {
    return {
      db: dbJson,
    };
  },
  components: {
    AlertMsg,
    DutyList,
  },
};
</script>
