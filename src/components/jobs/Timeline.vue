<template>
    <div class="row wide">
        <SectionTitle :title="sectionTitle"></SectionTitle>
        <ViewSwitcher></ViewSwitcher>
        <div class="segment inverted module">
            <div class="timeline">
                <div :key="experience.id"
                     v-for="(experience, index) in experiences"
                     class="container"
                     :class='(index%2 === 0) ? "left" : "right"'>
                    <div class="content">
                        <img class="timeline-logo"
                             :src="experience.companyLogoSrc"/>
                        <div :class='(index%2 === 0) ? "text-left" : "text-right"'>
                            <h2 class="ui inverted header timeline-tile-header">
                                {{ experience.start.format('MMM, YYYY') }}
                            </h2>
                            <h3 class="ui inverted header timeline-tile-header">
                                {{ experience.name }}
                            </h3>
                        </div>
                        <TileDigestContent :experience="experience"></TileDigestContent>
                    </div>
                </div>

            </div>
        </div>
    </div>
</template>


<script>
    import ViewSwitcher from "../ViewSwitcher";
    import SectionTitle from "../SectionTitle";
    import TileDigestContent from "./TileDigestContent";

    export default {
        components: {
            ViewSwitcher,
            SectionTitle,
            TileDigestContent,
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
    .module {
        margin-bottom: 3em;
    }

    /* W3SCHOOL timeline reworked */

    /* The actual timeline (the vertical ruler) */
    .timeline {
        position: relative;
        margin: 0 auto;
    }

    /* The actual timeline (the vertical ruler) */
    .timeline::after {
        content: '';
        position: absolute;
        width: 6px;
        background-color: white;
        top: 0;
        bottom: 0;
        left: 50%;
        margin-left: -3px;
    }

    /* Container around content */
    .container {
        padding: 10px 40px;
        position: relative;
        background-color: inherit;
        width: 50%;
    }

    /* The circles on the timeline */
    .container::after {
        content: '';
        position: absolute;
        width: 25px;
        height: 25px;
        right: -0.90em;
        background-color: #919191;
        border: 4px solid white;
        top: 2.3em;
        border-radius: 50%;
        z-index: 1;
    }

    /* Place the container to the left */
    .left {
        left: 0;
    }

    /* Place the container to the right */
    .right {
        left: 50%;
    }

    /* Add arrows to the left container (pointing right) */
    .left::before {
        content: " ";
        height: 0;
        position: absolute;
        top: 2.5em;
        width: 0;
        z-index: 1;
        right: 30px;
        border: medium solid #4b4b4b;
        border-width: 10px 0 10px 10px;
        border-color: transparent transparent transparent #4b4b4b;
    }

    /* Add arrows to the right container (pointing left) */
    .right::before {
        content: " ";
        height: 0;
        position: absolute;
        top: 2.5em;
        width: 0;
        z-index: 1;
        left: 30px;
        border: medium solid #4b4b4b;
        border-width: 10px 10px 10px 0;
        border-color: transparent #4b4b4b transparent transparent;
    }

    /* Fix the circle for containers on the right side */
    .right::after {
        left: -0.90em;
    }

    /* The actual content */
    .content {
        padding: 20px 30px;
        background-color: #4b4b4b;
        position: relative;
        border-radius: 2em;
    }

    .content .timeline-tile-header {
        margin: 0 0 0.5em 0;
    }

    .content .timeline-tile-content {
        margin-top: 0.5em;
    }

    .content h2 {
        margin-top: 0;
    }

    /* aligning next to the timeline */
    .text-right {
        text-align: left;
    }

    .text-left {
        text-align: right;
    }

    .timeline-logo {
        position: absolute;
        top: 1em;
        max-height: 48px;
        max-width: 64px;
    }

    .left .timeline-logo {
        left: 1em;
        float: left;
    }
    .right .timeline-logo {
        right: 1em;
        float: right;
    }

    /* Media queries - Mobile - Responsive timeline on screens less than 600px wide */
    @media screen and (max-width: 600px) {
        /* Place the timelime to the left */
        .timeline::after {
            left: 31px;
        }
        /* Full-width containers */
        .container {
            width: 100%;
            padding-left: 70px;
            padding-right: 25px;
        }
        /* Make sure that all arrows are pointing leftwards */
        .container::before {
            left: 60px;
            border: medium solid #4b4b4b;
            border-width: 10px 10px 10px 0;
            border-color: transparent #4b4b4b transparent transparent;
        }

        /* Rework all left/right styles to match mobile display, all tiles on right */
        /* Make sure all circles are at the same spot */
        .left::after, .right::after {
            left: 15px;
        }
        /* Make all right containers behave like the left ones */
        .right {
            left: 0%;
        }
        .text-left,.text-right {
            text-align: left;
        }
        /* unset left set for desktop and set all pictures to right floating*/
        .timeline-logo {
            left: unset!important;
            right: 1em!important;
            float: right!important;
        }
    }

</style>
