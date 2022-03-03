<template>
  <div>
    <div class="number" :id="'number-'+number" v-for="number in n()" :key="number" @mouseover="hov(number)" @mouseout="reset">
      {{number}}
    </div>
  </div>
</template>

<script>
export default {
  data()
  {
    return {
      limit: this.$parent.limit,
      numbers: []
    }
  },
  watch: {
    ['$parent.limit'](newLimit)
    {
      this.limit = newLimit;
    }
  },
  methods: {
    n()
    {
      let numbers = [];
      for(var i = 0; i < this.limit; i++)
      {
        numbers = [...numbers, i];
      }
        console.log(numbers);
      return numbers.sort(() => Math.random() - 0.5);
    },
    hov(number)
    {

      // The below functionality was redundent and it was going through every 
      // number even if the number was nog used or heigher then the hov:number.
      // I have updated the functionality to be more functional. 
      // I do not have alot of experience on vue and interested in 
      // learning and developing this skill as I do enjoy javascript and js frameworks.

      document.getElementById('number-' + number).classList.add('active');
      
      // const nums = document.querySelectorAll('.number');
      
      for(let i = 0; i < number; i++)
      {
        if(number % i === 0)
        {
          document.getElementById('number-' + i).classList.add('active');
        }
      }
    },
    reset()
    {
      const nums = document.querySelectorAll('.number');
      nums.forEach(num => num.classList.remove('active'))
    }
  }
}
</script>

<style scoped>
	.number {
		display: inline-block;
		padding: 5px;
		background-color: lightgrey;
		margin: 5px;
	}

	.active {
		background-color: red;
	}

</style>
