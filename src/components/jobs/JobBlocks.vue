<template>
    <div class="row wide">
        <SectionTitle :title="sectionTitle"></SectionTitle>
        <ViewSwitcher></ViewSwitcher>
        <div class="jobs">
            <div class="row job-tile"
                 :class='index%2 ? "odd" : "even"'
                 :key="experience.id"
                 v-for='(experience, index) in experiences'>
                <JobTile :experience="experience"></JobTile>
            </div>
        </div>
    </div>
</template>

<script>
    import ViewSwitcher from "../ViewSwitcher.vue";
    import JobTile from "./JobTile.vue";
    import SectionTitle from "../SectionTitle.vue";

    export default {
        components: {
            ViewSwitcher,
            JobTile,
            SectionTitle,
        },
        computed: {
            sectionTitle() {
                return this.$store.getters.getExperienceSectionTitle;
            },
            experiences() {
                return this.$store.getters.getExperiences;
            }
        },
    }
</script>

<style scoped>
    .jobs {
        background-color: inherit;
        text-align: center;
        margin: 0 2em 0 2em;
    }

    .job-tile {
        margin: 1.5em 0 1.5em 0!important; /* necessary to overrides ui grid negative margin */
    }

    .odd {
        background-color: #373737;
    }
    .even {
        background-color: #535353;
    }
</style>
