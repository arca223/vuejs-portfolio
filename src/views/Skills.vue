<template>
    <div class="row">
        <div class="ui segment inverted black clearing">
            <button @click="transition" id="transition-switcher" class="ui inverted black button right floated">Try me !</button>
        </div>
        <div id="skills" class="content transition visible">
            <div class="row">
                Thanks to my different missions,
                I worked with a lot of different stacks and teams,
                allowing me to succeed in both versatility (different stacks and projects),
                and specialization (specialized PHP/JS).
            </div>
            <br />
            <Skills :key="skills.id" v-for="skills in mySkills" :skills="skills"></Skills>
        </div>

        <div id="hobbies" class="content transition hidden">
            <Hobby></Hobby>
        </div>
    </div>
</template>


<script>
    import Skills from '../components/skills/Skills';
    import Hobby from '../components/skills/Hobby';

    export default {
        components: {
            Skills,
            Hobby,
        },
        computed: {
            route() {
                return this.$store.getters.getRoute;
            },
            mySkills() {
                return this.$store.getters.getSkills;
            }
        },
        methods: {
            transition() {
                const elem=document.querySelector('#transition-switcher');
                elem.addClass('disabled');

                let visibleComponent = document.querySelector('.transition.visible');
                let hiddenComponent = document.querySelector('.transition.hidden');
                visibleComponent.transition('browse left', function () {
                    hiddenComponent.transition('browse');
                    elem.removeClass('disabled');
                });
            }
        },
        created() {
            this.$store.commit("setRoute", "skills");

            // In case of a double click, it will clear the permanent disabled class without influencing the flow
            setInterval(() => {
                const transitionBtn = document.querySelector('#transition-switcher');
                if (transitionBtn.hasClass('disabled')) {
                    setTimeout(() => {
                        document.querySelector('#transition-switcher').removeClass('disabled');
                    }, 500);
                }
            }, 500);
        },
    }
</script>

<style scoped>
    .content {
        text-align: center;
        margin: 2em 3em 3em 2em;
    }
</style>