<template>
    <div class="test">
    	<input style="width:75%;" type="text" v-model="title"><br />
    	<h1>{{title}}</h1>
    	<p v-if="showName">{{ user.firstName }}</p>
    	<p v-else>Nobody</p>

    	<ul>
    		<li v-for="item in items">{{item.title}}</li>
    	</ul>

    	<button v-on:click="greet('Hello World')">Say Greeting</button>
    	<br/>
    	<input type="text" v-on:keyup="pressKey" v-on:keyup.enter="enterHit">
    	<br/>
    	<label for="fname">First Name: </label><input type="text" name="fname" v-model="user.firstName">
    	<br/>
    	<label for="lname">Last Name: </label><input type="text" name="lname" v-model="user.lastName">
    	<h3>{{ fullName }}</h3>
    	<h2>{{ msg }}</h2>

    </div> 
</template>


<script>
	export default {
		name: 'test',
		props: {
			msg: {
				type: String,
				default: 'Foobar'
			}
		},
		data() {

			return {

				title: 'My First VueJS Component',

				user: {

					firstName: 'Apoorva',
					lastName: 'Chitre'
				},

				showName: true,

				items: [

					{title: 'Item One'},
					{title: 'Item Two'},
					{title: 'Item Three'},
				]
			}
		}, 

		methods: {

					greet: function(greeting) {

						alert(greeting);
					},

					pressKey: function(e) {

						console.log(e.target.value);
					},

					enterHit: function(){

						console.log('You hit enter!');
					}
				},

		computed: {

					fullName: function() {

						return this.user.firstName + ' ' + this.user.lastName;
					}

				}
			}
	
</script>


<style scoped>
	#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>