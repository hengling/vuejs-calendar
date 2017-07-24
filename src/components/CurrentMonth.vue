<template>
    <div>
        <div>{{ formattedDate }}</div>
        <button @click="dec">-</button>
        <button @click="inc">+</button>
    </div>
</template>
<script>
    let JANUARY = 1;
    let DECEMBER = 12;
    export default {
        computed: {
            month() {
                return this.$store.state.currentMonth;
            },
            year() {
                return this.$store.state.currentYear;
            },
            formattedDate() {
                return this.$moment(`${this.year}-${this.month}-1`, 'YYYY-M-D').format('MMMM YYYY');
            }
        },
        methods: {
            dec() {
                if (this.month === JANUARY) {
                    this.$store.commit('setCurrentMonth', DECEMBER);
                    this.$store.commit('setCurrentYear', this.year - 1);
                } else {
                    this.$store.commit('setCurrentMonth', this.month - 1);
                }
                this.$store.commit('eventFormActive', false);
            },
            inc() {
                if (this.month === DECEMBER) {
                    this.$store.commit('setCurrentMonth', JANUARY);
                    this.$store.commit('setCurrentYear', this.year + 1);
                } else {
                    this.$store.commit('setCurrentMonth', this.month + 1);
                }
                this.$store.commit('eventFormActive', false);
            }
        }
    };
</script>