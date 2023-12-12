<template>
  <div class="app">
    <h1>{{ newdate }}</h1>

    <div>
      <p>
        Day: {{ newDay }}
        <span v-if="addedDay !== 0">
          {{
            addedDay === 1 ? ` (+ ${addedDay} day)` : ` (+ ${addedDay} days)`
          }}
        </span>
      </p>
      <button @click="handleAddedDay">Add Days</button>
    </div>

    <div>
      <p>
        Month: {{ newMonth }}
        <span v-if="addedMonth !== 0">
          {{
            addedMonth === 1
              ? ` (+ ${addedMonth} month)`
              : ` (+ ${addedMonth} months)`
          }}
        </span>
      </p>
      <button @click="handleAddedMonth">Add Months</button>
    </div>

    <div class="action-btn">
      <button @click="handleAddedDaysAndMonths" class="change-btn" title="Click to set a new date">
        Change The World!
      </button>
      <button @click="handleReset" class="reset-btn">Reset</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      date: new Date(),
      addedDay: 0,
      addedMonth: 0,
      newdate: new Date().toString(),
    };
  },

  computed: {
    newDay() {
      return this.addDay(this.addedDay).getDate();
    },
    newMonth() {
      return this.addMonth(this.addedMonth).getMonth() + 1;
    },
  },

  methods: {
    addDay(numberOfDays, baseDate = this.date) {
      const newDate = new Date(baseDate);
      newDate.setDate(newDate.getDate() + numberOfDays);
      return newDate;
    },
    addMonth(numberOfMonths, baseDate = this.date) {
      const newDate = new Date(baseDate);
      newDate.setMonth(newDate.getMonth() + numberOfMonths);
      return newDate;
    },
    handleAddedDay() {
      this.addedDay += 1;
    },
    handleAddedMonth() {
      this.addedMonth += 1;
    },
    handleAddedDaysAndMonths() {
      this.newdate = this.addMonth(
        this.addedMonth,
        this.addDay(this.addedDay)
      ).toString();
    },
    handleReset() {
      this.newdate = this.date.toString();
      this.addedDay = 0;
      this.addedMonth = 0;
    },
  },
};
</script>
