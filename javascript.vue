new Vue({
  el: "#app",

  data: {
    start: false,
    you: 100,
    monster: 100,
    logs: []
  },
  methods: {
    attack: function() {
      var damageToYou = Math.floor(Math.random() * 17)
      var damageToMonster = Math.floor(Math.random() * 20)
      this.monster -= damageToMonster
      this.you -= damageToYou
      this.updatePlayer(damageToYou)
      this.updateMonster(damageToMonster)
    },
    super_attack: function() {
      var damageToYou = Math.floor(Math.random() * 25)
      var damageToMonster = Math.floor(Math.random() * 30)
      this.monster -= damageToMonster
      this.you -= damageToYou
      this.updatePlayer(damageToYou)
      this.updateMonster(damageToMonster)
    },
    heal: function() {
      var damageToYou = Math.floor(Math.random() * 10) + 1
      var damageToMonster = Math.floor(Math.random() * 7)
      this.you += damageToYou
      this.you -= damageToMonster
      this.updateMonster(damageToMonster)
      this.updatePlayer(-damageToYou)
    },
    giveUp: function() {
      this.newGame()
    },
    updatePlayer: function(value) {
      this.logs.unshift(value)
    },
    updateMonster: function(value) {
      this.logs.unshift(value)
    },
    newGame: function() {
      this.start = false
      this.you = 100
      this.monster = 100
      this.logs = []
    }
  },
  watch: {
    you: function() {
      if (this.you < 1) {
        var vm = this
        setTimeout(function() {
          alert("Monster won! Game over")
          vm.newGame()
        }, 50)
      }
      else if (this.you >= 100) {
        this.you = 100
      }
    },
    monster: function() {
      if (this.monster < 1) {
        var vm = this
        setTimeout(function() {
          alert("You won! Congratulations!!")
          vm.newGame()
        }, 50)
      }
    }
  }
})
