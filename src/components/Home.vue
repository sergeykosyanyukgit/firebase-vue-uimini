<template lang="pug">
  .content-wrapper
    section
      .container
        h1.ui-title-1 Home
        input(
          type="text"
          placeholder="What we will watch?"
          v-model="taskTitle"
          @keyup.enter="newTask"
        )
        textarea(
          type="text"
          v-model="taskDescription"
          @keyup.enter="newTask"
        )
        .option-list
          input.what-watch--radio(
            type="radio"
            id="radioFilm"
            value="Film"
            v-model="whatWatch"
          )
          label(
            for="radioFilm"
          ) Film
          input.what-watch--radio(
            type="radio"
            id="radioSerial"
            value="Serial"
            v-model="whatWatch"
          )
          label(
            for="radioSerial"
          ) Serial
        .total-Time
          //Film Time
          .total-time__film(
            v-if="whatWatch === 'Film'"
          )
            span.time-title Hours
            input.time-input(
              type="number"
              v-model="filmHours"
            )
            span.time-title Minutes
            input.time-input(
              type="number"
              v-model="filmMinutes"
            )
          //Serial Time
          .total-time__serial(
            v-if="whatWatch === 'Serial'"
          )
            span.time-title How many season?
            input.time-input(
              type="number"
              v-model="serialSeason"
            )
            span.time-title How many series?
            input.time-input(
              type="number"
              v-model="serialSeries"
            )
            span.time-title How long is one series? (minutes)
            input.time-input(
              type="number"
              v-model="serialSeriesMinutes"
            )

        .tag-list
        .ui-tag__wrapper
          .ui-tag
            span.tag-title Dogs
            span.button-close

</template>

<script>
export default {
  data () {
    return {
      taskTitle: '',
      taskId: 3,
      taskDescription: '',
      whatWatch: 'Film',
      filmHours: 1,
      filmMinutes: 30,
      serialSeason: 1,
      serialSeries: 11,
      serialSeriesMinutes: 40
    }
  },
  methods: {
    newTask () {
      if (this.taskTitle === '') {
        return
      }
      const task = {
        id: this.taskId,
        title: this.taskTitle,
        description: this.taskDescription,
        whatWatch: this.whatWatch,
        completed: false,
        editing: false
      }
      console.log(task)

      this.taskId++
      this.taskTitle = ''
      this.taskDescription = ''
    },
    getHoursAndMinutes (minutes) {
      let hours = Math.trunc(minutes / 60)
      let min = minutes % 60
      return hours + ' Hours ' + min + ' Minutes '
    }
  },
  computed: {
    filmTime () {
      let min = this.filmHours * 60 + this.filmMinutes
      return this.getHoursAndMinutes(min)
    },
    serialTime () {
      let min = this.serialSeason * this.serialSeries * this.serialSeriesMinutes
      return this.getHoursAndMinutes(min)
    }
  }
}
</script>

<style lang="stylus" scoped>
.option-list
  display flex
  .what-watch--radio
    margin-right 12px
  label
    margin-right 20px
    &:last-child
      margin-bottom 0

// Total time
.total-time
  margin-bottom 20px
.time-title
  display block
  margin-bottom 6px
.time-input
  max-width 80px
  margin-right 10px
</style>
