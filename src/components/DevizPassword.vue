<template>
    <div>
        <v-progress-linear
            :value="power"
            :color="color"
            height="10"
        ></v-progress-linear>

        <small>Password check: <strong :class="color + '--text'">{{ text }}</strong></small>
    </div>
</template>

<script scoped>
  export default {
    props: {
      password: String
    },
    data: () => ({
      power: 0,
      color: 'red',
      label: 'Weak',

      rules: [
        {
          score: 1,
          match: (v) => {
            return /[a-z]/.test(v)
          }
        },
        {
          score: 2,
          match: (v) => {
            return /[A-Z]/.test(v)
          }
        },
        {
          score: 3,
          match: (v) => {
            return /[0-9]/.test(v)
          }
        },
        {
          score: 5,
          match: (v) => {
            return /[^A-z0-9]/.test(v)
          }
        },
        {
          score: 3,
          match: (v) => {
            return v.length > 14
          }
        }
      ],

      status: [
        { percentMin: 0,  percentMax: 30, text: 'Weak', color: 'red'},
        { percentMin: 30, percentMax: 70, text: 'Good', color: 'amber'},
        { percentMin: 70, percentMax: 90, text: 'Strong', color: 'yellow'},
        { percentMin: 90, percentMax: 100, text: 'Very Strong', color: 'green'}
      ]
    }),

    watch: {
      password: {
        handler (value) {
          let matches = this.getMatches(value)
          let score = this.countScore(matches)
          
          this.update(score);
        },
        // force eager callback execution
        immediate: true
      }
    },

    methods: {
      getMatches (value) {
        return this.rules.filter( el => el.match(value) );
      },

      countScore (rules) {
        let total = 0
        rules.forEach((rule) => { total += rule.score })
        return total
      },

      getStatus(percent) {
        return this.status.find( el => percent >= el.percentMin && percent <= el.percentMax );
      },

      update (score) {
        let percent = (score / this.countScore(this.rules)) * 100
        let status = this.getStatus(percent)

        this.power = percent
        this.color = status.color
        this.text = status.text
      }
    }
  }
</script>