<template>
    <div class="calendar dark-box">
      <div class="header">
        <button @click="prevMonth"><Arrow style="transform: rotateZ(180deg);"/></button>
        <h2>{{ currentMonth }}</h2>
        <button @click="nextMonth"><Arrow/></button>
      </div>
      <table>
        <thead>
          <tr>
            <th v-for="day in daysOfWeek" :key="day">{{ day }}</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(week, index) in calendar" :key="index">
            <td v-for="(day, index) in week" :key="index" :class="{ 'prev-month': day.prevMonth, 'next-month': day.nextMonth, 'selected': isToday(day.date) }">
              {{ day.date.getDate() }}
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        currentDate: new Date(),
        currentMonth: '',
        daysOfWeek: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun'],
        calendar: []
      };
    },
    mounted() {
      this.updateCalendar();
    },
    methods: {
      updateCalendar() {
        this.currentMonth = this.currentDate.toLocaleString('default', { month: 'long', year: 'numeric' });
        const firstDayOfMonth = new Date(this.currentDate.getFullYear(), this.currentDate.getMonth(), 0);
        const lastDayOfMonth = new Date(this.currentDate.getFullYear(), this.currentDate.getMonth() + 1, 0);
        const startDay = firstDayOfMonth.getDay();
        const endDay = lastDayOfMonth.getDate();
        
        const calendar = [];
        let week = [];
        
        for (let i = 0; i < startDay; i++) {
          const prevDate = new Date(firstDayOfMonth);
          prevDate.setDate(prevDate.getDate() - (startDay - i));
          week.push({ date: prevDate, prevMonth: true });
        }
        
        for (let i = 1; i <= endDay; i++) {
          const currentDate = new Date(this.currentDate.getFullYear(), this.currentDate.getMonth(), i);
          week.push({ date: currentDate, prevMonth: false, nextMonth: false });
          if (week.length === 7) {
            calendar.push(week);
            week = [];
          }
        }
        
        const remainingDays = 7 - week.length;
        for (let i = 1; i <= remainingDays; i++) {
          const nextDate = new Date(lastDayOfMonth);
          nextDate.setDate(nextDate.getDate() + i);
          week.push({ date: nextDate, nextMonth: true });
        }
        
        calendar.push(week);
        this.calendar = calendar;
      },
      prevMonth() {
        this.currentDate.setMonth(this.currentDate.getMonth() - 1);
        this.updateCalendar();
      },
      nextMonth() {
        this.currentDate.setMonth(this.currentDate.getMonth() + 1);
        this.updateCalendar();
      },
      isToday(date) {
        const today = new Date();
        return date.getDate() === today.getDate() && date.getMonth() === today.getMonth() && date.getFullYear() === today.getFullYear();
      }
    }
  };
  </script>
  
  <style lang="scss" scoped>
  .calendar {
  
    font-size: inherit;
    font-family: Arial, sans-serif;
    padding: 1.2rem;
    padding-bottom: 3vh;
    background-color: rgb(40, 40, 40, 0.98);
    width: 40%;

    @media (max-width: 768px) {
      width: 100%;
      font-size: 0.5rem;
    }
  
    @media (max-width: 467px) {
      font-size: 0.5rem;
      width: 100%;
    }
  

  }
  
  .header {
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-bottom: 10px;
  }
  
  .header button {
    background: none;
    border: none;
    cursor: pointer;
  }
  
  table {
    width: 100%;
    border-collapse: collapse;
}
  
  th,
  td {
    border: 1px solid #cccccc9a;
    padding: 5px;
    /* width: 5em;
    height: 5em; */
    text-align: center;
  }
  td {
    cursor: pointer;
  }
  
  .prev-month,
  .next-month {
    color: #999;
  }
  
  .selected {
    background-color: #f0f0f0;
    color: black;
    font-weight: 600;
    border-radius: 2px;
  }
  
  .selected:hover {
    background-color: #e0e0e0;
  }
  </style>
  